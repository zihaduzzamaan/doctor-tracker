# Engineering Skill Sources & Supply-Chain Inventory

This document tracks all agent skills, external reference repositories, and operational frameworks active in the Doctor Tracker workspace.

---

# 1. Active Workspace Skills Inventory

| Skill Name | Location | Origin & Source URL | License | Purpose | Status |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **`environment-setup`** | `.agents/skills/environment-setup/` | Antigravity Customization Framework | MIT | Workspace prerequisites, documentation initialization, and quality gates | **Verified & Active** |
| **`spec-kit`** | `.agents/skills/spec-kit/` | `https://github.com/github/spec-kit` | MIT | Feature specifications, user story matrices, and acceptance criteria | **Verified & Active** |
| **`impeccable`** | `.agents/skills/impeccable/` | `https://github.com/pbakaus/impeccable` | Apache 2.0 | Design tokens, 5-state UI coverage, and WCAG 2.2 AA accessibility audits | **Verified & Active** |
| **`architecture`** | `.agents/skills/architecture/` | `https://github.com/anthropics/knowledge-work-plugins` | MIT | Clean architecture, decoupled REST boundaries, facet pipelines, code reviews | **Verified & Active** |
| **`owasp-security`** | `.agents/skills/owasp-security/` | `https://owasp.org/` | CC BY-SA 4.0 | ASVS compliance, JWT lifecycle, NoSQL injection defenses, zero secrets policy | **Verified & Active** |
| **`git-workflow`** | `.agents/skills/git-workflow/` | `https://github.com/netresearch/git-workflow-skill` | MIT | Conventional commits, multi-repo synchronization, and branch safety | **Verified & Active** |

---

# 2. Supply-Chain Security Rules

| Priority | Rule Name | Mandatory Guideline |
| :--- | :--- | :--- |
| **1** | **Code Inspection First** | Never execute third-party install scripts or binaries without reviewing their full contents first. |
| **2** | **Valid Skill Frontmatter** | Skill frontmatter must contain valid YAML `name` and `description` attributes. |
| **3** | **Traceable Provenance** | Every installed skill must have its source repository, license, and purpose logged in this inventory. |
| **4** | **Code-Free Documentation** | Documentation records must remain code-free and structured in pure markdown tables and diagrams. |
