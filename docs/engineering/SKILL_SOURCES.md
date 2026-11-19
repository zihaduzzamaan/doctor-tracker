# Engineering Skill Sources & Supply-Chain Inventory

This document tracks all external agent skills, reference repositories, and tooling frameworks referenced in the Doctor Tracker workspace.

---

# 1. Active Workspace Skills

| Attribute | Details |
| :--- | :--- |
| **Skill Name** | `environment-setup` |
| **Workspace Location** | `.agents/skills/environment-setup/SKILL.md` |
| **Origin & Source** | Synthesized from `master_structural_prompt.md` and Antigravity Customization System |
| **License** | MIT / Workspace Configuration |
| **Operational Purpose** | Runbook for inspecting prerequisites, installing open-source engineering skills, initializing documentation, and checking quality gates. |
| **Verification Status** | **Verified & Active** |

---

# 2. Curated Reference Catalog

| Resource Name | Source URL | Purpose | Integration Status |
| :--- | :--- | :--- | :--- |
| **GitHub Spec Kit** | `https://github.com/github/spec-kit` | Structured product specs and feature breakdowns | Evaluated; available via `specify init --here --integration agy` |
| **Impeccable** | `https://github.com/pbakaus/impeccable` | UI/UX design tokens and accessibility audits | Evaluated; available via `npx impeccable install` |
| **Anthropic Engineering** | `https://github.com/anthropics/knowledge-work-plugins/tree/main/engineering` | System design, code reviews, and testing patterns | Referenced in architecture guidelines |
| **OWASP ASVS & Top 10** | `https://owasp.org/www-project-application-security-verification-standard/` | Application security guidelines | Incorporated into `AGENTS.md` and `DEFINITION_OF_DONE.md` |
| **Git Workflow** | `https://github.com/netresearch/git-workflow-skill` | Conventional commits and pull request standards | Incorporated into `.github/` and `AGENTS.md` |

---

# 3. Supply-Chain Rules

| Priority | Rule Name | Mandatory Guideline |
| :--- | :--- | :--- |
| **1** | **Code Inspection First** | Never run third-party install scripts or binaries without reviewing the source code first. |
| **2** | **Valid Skill Frontmatter** | Skill frontmatter must use valid `name` and `description` fields. |
| **3** | **Traceable Provenance** | When external skills are imported, log their repository URL, commit hash, and license in this inventory. |
