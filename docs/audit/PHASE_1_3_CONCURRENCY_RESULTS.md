# Phase 1.3: Concurrency Stress Test Results & Race Condition Validation

**Execution Date**: 2026-11-20T07:29:08.540Z  
**Audit Role**: Senior Concurrency Architect & Database Reliability Engineer  
**Target Environment**: Isolated Test Doctors and Patients on Local API & MongoDB Atlas Cluster  

---

## 1. Concurrency Experiment Summary Table

| Experiment ID | Action Tested | Concurrency Level | Stored Doctor Counter | Actual Active DB Records | Count Mismatch | Verdict |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **EXP-4.1** | Simultaneous Admissions | 10 Parallel Requests | 10 | 10 | 0 | CONSISTENT (0 Drift) |
| **EXP-4.2** | Simultaneous Discharges | 5 Parallel Requests | 5 | 5 | 0 | CONSISTENT (0 Drift) |
| **EXP-4.3** | Mixed Interleaved Admissions & Discharges | 5 Parallel Requests | 6 | 6 | 0 | CONSISTENT (0 Drift) |
| **EXP-4.4** | Doctor Transfer Concurrent with Discharge | 2 Parallel Requests | Doc1: 4, Doc2: 1 | Doc1: 4, Doc2: 1 | 0 | CONSISTENT (0 Drift) |
| **EXP-4.5** | Patient Readmission (Discharged -> Admitted) | Sequential Transition | 5 | 5 | 0 | CONSISTENT (0 Drift) |
| **EXP-4.6** | Duplicate Retried Update (Idempotency) | 2 Identical Requests | 4 | 4 | 0 | CONSISTENT (Idempotent) |

---

## 2. TOCTOU (Time-of-Check to Time-of-Use) Deep Dive

### Why the Self-Healing Mechanism Did Not Drift in Empirical Tests
- In EXP-4.1, `Doctor.findByIdAndUpdate(docId, { $inc: { active_patient_count: 1 } })` is executed as an atomic MongoDB command. The database engine serializes atomic counter increments on the single document, preventing lost updates.
- In EXP-4.2 through EXP-4.6, `updatePatient` uses `Patient.countDocuments` and sets the exact calculated count. In single-process Express execution with connection pooling over Atlas, Mongoose connections process rapidly enough that interleaving did not produce a TOCTOU drift in 10-concurrency tests.

### The Theoretical Failure Window under Multi-Instance Scale
Despite passing at 10 concurrency, a race condition exists in distributed multi-process deployments:
1. Process A executes `countDocuments` for Doctor 1 (returns 5).
2. Process B concurrently inserts a new patient for Doctor 1 and executes `$inc: 1` (Doctor counter becomes 6).
3. Process A finishes and writes its previously read count of 5 via `findByIdAndUpdate`.
4. Result: Stored counter becomes 5 while true DB count is 6 (Silent Lost Increment).

### Transactional Boundary Design (withTransaction)
A transaction resolves this ONLY if both the patient write and doctor counter recalculation participate in the same session with Snapshot Read Concern:
- Session starts.
- Insert or update patient within session.
- Read `countDocuments` within session.
- Update doctor within session.
- Commit session.
Without passing `{ session }` to both operations, wrapping in `withTransaction` provides zero race protection.