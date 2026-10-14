# Step 1: Requirements & Baseline

**Workflow:** AI-Project-Toolkit / Project Rebirth  
**Version:** 1.0-draft  
**Status:** Draft  
**Process Owner:** Product Owner  
**Participants:** ChatGPT (Requirements Engineering), Codex CLI (Independent Review), Claude Code (Approved Changes)

## 1. Purpose

Transform an initial project idea, business need, or change request into a structured, verifiable, and formally approved requirements baseline.

The approved baseline establishes the authoritative functional scope for subsequent technical planning, architecture, and implementation.

This workflow separates requirements definition, independent quality assurance, and final approval.

**Core principle:** No implementation authorization is implied by the existence of a requirements document.

## 2. Prerequisites

Before starting this workflow:

- A project idea, business need, or change request has been identified.
- A Product Owner has been assigned.
- A version-controlled project workspace is available.
- Applicable project conventions and agent instructions are accessible.
- The intended scope and relevant stakeholders can be identified.

For the current Project Rebirth workflow, Git is used for version control. GitHub is optional and must not be treated as a mandatory dependency of the future product.

## 3. Workflow

### Step 1.1: Requirements Discovery

**Responsible:** Product Owner and ChatGPT

The Product Owner describes the problem, intended outcomes, constraints, and expectations.

ChatGPT supports structured requirements engineering by:

- Identifying business goals and non-goals.
- Clarifying functional and non-functional requirements.
- Identifying stakeholders, dependencies, assumptions, and risks.
- Proposing measurable acceptance criteria.
- Identifying contradictions, ambiguities, and missing information.
- Distinguishing confirmed decisions from proposals and unresolved questions.

The Product Owner remains responsible for all binding business decisions.

**Output:** Structured requirements and decision records.

### Step 1.2: Requirements Specification

**Responsible:** ChatGPT, with Product Owner validation

Consolidate the collected requirements into a formal requirements specification (*Lastenheft*).

The document should include, where applicable:

- Project background and objectives.
- Scope and explicit non-goals.
- Stakeholders, roles, and responsibilities.
- Functional and non-functional requirements.
- Business workflows and constraints.
- Security and quality requirements.
- Acceptance criteria and validation scenarios.
- Risks, assumptions, and dependencies.
- Proposed MVP scope and future development stages.
- Open questions and outstanding decisions.
- Document version, approval status, and change history.

Requirements must be identifiable and traceable.

Confirmed requirements, proposed solutions, and unresolved questions must remain clearly distinguishable.

**Output:** Draft requirements specification.

### Step 1.3: Versioning and Agent Accessibility

**Responsible:** Product Owner / Authorized Project Maintainer

Store the requirements specification in the repository under:

`docs/requirements/lastenheft-v1.0.md`

Ensure that the repository-level agent instructions reference the authoritative document:

- `AGENTS.md` for Codex CLI.
- `CLAUDE.md` for Claude Code.

Shared project knowledge must remain in `docs/` rather than being duplicated across agent-specific configuration directories.

Changes must be traceable through version control.

A document's presence in the repository does not establish its approval status.

**Output:** Versioned and accessible requirements draft.

### Step 1.4: Independent Requirements Review

**Responsible:** Codex CLI

Codex performs an independent review of the current requirements specification.

The review must evaluate:

1. **Completeness:** Missing requirements, constraints, stakeholders, or expected outcomes.
2. **Consistency:** Contradictions between requirements and documented decisions.
3. **Clarity:** Ambiguous, unverifiable, or conflicting statements.
4. **Testability:** Whether requirements can be objectively validated.
5. **Traceability:** Relationships between objectives, requirements, and acceptance criteria.
6. **MVP Scope:** Clear distinction between mandatory MVP capabilities and future extensions.
7. **Risks:** Security, operational, architectural, and process-related concerns.
8. **Open Decisions:** Questions that must be resolved before baseline approval.

Codex must distinguish verified findings from assumptions and recommendations.

Each finding should include:

- A unique identifier.
- Severity or priority.
- A reference to the affected requirement or document section.
- A description of the issue.
- Its potential impact.
- A recommended resolution.

**Review restriction:** Codex must not modify the requirements specification during this review.

The review must identify the exact document revision or Git commit being evaluated.

**Output:** Independent, traceable review report.

### Step 1.5: Findings Resolution

**Responsible:** Product Owner, supported by ChatGPT and authorized implementation agents

Review findings are evaluated and classified.

Possible outcomes include:

- Accepted: The finding requires a correction.
- Rejected: The finding is not applicable, with justification.
- Deferred: The finding is documented for later resolution.
- Clarification required: Additional Product Owner input is necessary.

Material scope, security, or acceptance changes require explicit Product Owner decisions.

Approved corrections are incorporated into the requirements specification.

Where changes materially affect previously reviewed requirements, another independent review must be performed.

Review and correction cycles must follow defined limits and escalation rules. No fixed maximum number of cycles is assumed unless explicitly approved.

**Output:** Consolidated requirements draft and documented finding dispositions.

### Step 1.6: Formal Baseline Approval

**Responsible:** Product Owner

The Product Owner evaluates the consolidated requirements specification and its supporting review evidence.

Approval must explicitly identify:

- The approved document version.
- The corresponding Git commit or immutable revision.
- The approval decision and date.
- Any accepted limitations or outstanding issues.

An approved baseline must not be silently changed.

Subsequent changes require documented change control and renewed approval where applicable.

**Output:** Formally approved requirements baseline.

## 4. Quality Gate: Requirements Baseline

Step 1 is complete only when all applicable exit criteria have been satisfied.

| ID | Exit criterion | Required evidence |
|---|---|---|
| RG-01 | Requirements are documented and versioned | Requirements specification and revision reference |
| RG-02 | Confirmed decisions, proposals, and open questions are distinguishable | Document review |
| RG-03 | Requirements have verifiable acceptance criteria where applicable | Requirements and acceptance mapping |
| RG-04 | Independent Codex review has been completed | Review report |
| RG-05 | Critical findings are resolved or explicitly dispositioned under approved rules | Findings register |
| RG-06 | MVP scope and relevant exclusions are sufficiently defined | Approved scope decision |
| RG-07 | Remaining open questions do not prevent the next phase | Documented PO decision |
| RG-08 | The Product Owner has explicitly approved the baseline | Approval record tied to an exact revision |

**Gate failure:** The workflow remains in the requirements phase. Binding technical design and implementation must not proceed against an unapproved baseline.

Exploratory analysis and feasibility investigation may be performed only within their separately authorized scope.

## 5. Deliverables

The workflow produces:

1. A version-controlled requirements specification.
2. A documented record of relevant Product Owner decisions.
3. An independent Codex review report.
4. A findings register with resolutions and outstanding issues.
5. A formal baseline approval record.
6. A stable reference for subsequent project phases.

Supporting review and decision artifacts should be stored in the repository or another explicitly designated authoritative location.

The exact artifact naming convention and storage structure beyond the requirements specification remain to be defined.

## 6. Responsibilities and Approval Boundaries

| Role | Responsibility | Approval authority |
|---|---|---|
| Product Owner | Requirements decisions, scope, prioritization, baseline approval | Final authority |
| ChatGPT | Requirements discovery, consolidation, clarification, decision support | None |
| Codex CLI | Independent requirements review and documented findings | None |
| Claude Code | Implementation of explicitly authorized changes when assigned | None |
| Orchestrator (future) | State tracking, task handoffs, quality gates, evidence, approval enforcement | Enforces decisions; does not replace the PO |

No agent may independently approve the requirements baseline, expand the authorized scope, or bypass required quality gates.

## 7. Transition to Step 2

After successful completion of the Requirements Baseline Quality Gate, the project may proceed to:

**Step 2: Technical Concept & Architecture**

Step 2 transforms the approved functional requirements into a technical solution proposal, architecture decisions, implementation constraints, and a verifiable development approach.

Technical design decisions must remain traceable to the approved requirements baseline.

## 8. Current Application: Project Rebirth

This workflow is being documented while Project Rebirth performs its initial requirements phase.

**Completed or prepared:**

- Requirements discovery and consolidation.
- Requirements specification v1.0 drafted.
- Requirements document stored in the repository.
- Requirements document made available in the ChatGPT project.
- References added to `AGENTS.md` and `CLAUDE.md`.

**Outstanding:**

- Independent Codex requirements review.
- Resolution of review findings and blocking open decisions.
- Final consistency verification.
- Explicit Product Owner baseline approval.

**Current gate status:** NOT PASSED.

Project Rebirth must not treat the current draft as an approved implementation baseline.

---

**Document status:** Draft  
**Approval:** Pending Product Owner review  
**Next action:** Prepare and execute the independent Codex requirements review.