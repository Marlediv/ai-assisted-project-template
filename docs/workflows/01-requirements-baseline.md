# Step 1: Requirements & Baseline

**Workflow version:** 1.1-draft  
**Status:** Draft  
**Process owner:** Product Owner  
**Scope:** Reusable across projects

## 1. Purpose

Turn a project idea, business need, or change request into a structured, testable, versioned, and explicitly approved requirements baseline. This workflow defines **what must be established and approved**, not a mandatory implementation architecture.

A draft specification is not an implementation authorization. Approval is a recorded Product Owner decision tied to an exact revision.

## 2. Applicability and prerequisites

This workflow applies to new and existing projects, including projects without GitHub or pre-existing AI agent configuration.

Before starting, identify:

- The Product Owner and relevant stakeholders.
- The problem, desired outcomes, constraints, and known risks.
- The project's versioning or document-control mechanism.
- The authoritative location of requirements and the applicable approval rules.
- Which assistants or review tools, if any, are available and authorized.

**Repository examples in this document are illustrative.** Paths, filenames, and agent adapters must follow the project's conventions. GitHub is not required. Where a project uses Git, record the exact commit; otherwise use an immutable document revision or equivalent identifier.

## 3. Workflow

### 1.1 Discover and clarify requirements

**Accountable:** Product Owner  
**Support:** Requirements engineer or authorized assistant

Capture objectives, non-goals, users, stakeholders, constraints, functional and non-functional requirements, dependencies, risks, and measurable acceptance criteria. Explicitly label statements as **confirmed**, **proposed**, or **open**. Do not infer approval from discussion alone.

**Evidence:** Requirements notes and decision log.

### 1.2 Draft the requirements specification

**Accountable:** Product Owner  
**Support:** Requirements engineer or authorized assistant

Consolidate findings into a versioned specification. Include, as applicable, background, scope, non-goals, roles, requirements with stable identifiers, acceptance criteria, security and quality expectations, risks, assumptions, proposed delivery stages, open decisions, approval status, and change history.

Use the terminology and language appropriate to the project's stakeholders. Do not introduce implementation choices as approved requirements without an explicit decision.

**Evidence:** Requirements specification marked **Draft**.

### 1.3 Publish and reference the authoritative draft

**Accountable:** Authorized project maintainer

Store the specification in the project's designated authoritative location. Example:

`docs/requirements/requirements.md`

Where the project uses `AGENTS.md` and/or `CLAUDE.md`, add a concise reference and approval rule to the existing **Sources of truth**, **Project context**, or equivalent section. If the files do not exist, do not create them solely for this step unless those agents will be used and their configuration is authorized.

**Do not copy the full specification into agent instruction files.** Keep one authoritative source and link to it. If a separate chat or workspace needs a copy, label its revision and avoid treating it as independently authoritative.

#### Suggested wording for `AGENTS.md` and `CLAUDE.md`

Adapt the path, terminology, and approval process to the project. The following block can be used in either file:

```markdown
## Sources of truth

- Product requirements: `docs/requirements/requirements.md`

Read the relevant requirements and their approval status before planning,
implementing, or reviewing work.

Draft or proposed requirements may be analyzed and reviewed, but do not
constitute approval to implement. Use only the explicitly approved scope
and acceptance criteria for authorized implementation work.

Do not independently approve requirements, expand scope, or bypass quality
and security gates. Report contradictions and missing approvals to the
Product Owner or designated approval authority.
```

If the file already has a **Sources of truth** section, **merge** these lines into it rather than adding a duplicate heading. Preserve stricter existing policies. Referencing a document does not itself grant file, shell, network, or merge permissions.

**Evidence:** Authoritative document reference and, where applicable, updated agent instructions.

### 1.4 Conduct an independent requirements review

**Accountable:** Independent reviewer  
**Preferred tool where configured:** Codex CLI

Review the exact draft revision for completeness, internal consistency, clarity, testability, traceability, scope/MVP boundaries, risks, and unresolved decisions. Cross-check relevant project decisions and conventions where available.

The reviewer must not modify source files during the review. Record each finding with an ID, severity, source reference, impact, and recommended resolution. Distinguish confirmed issues from assumptions and questions. Do not claim to have checked material that was unavailable.

#### Short Codex CLI prompt

Replace `<REQUIREMENTS_PATH>` with the project's actual path:

```text
Review <REQUIREMENTS_PATH> independently as a requirements specification.
Read relevant project decisions and agent instructions. Check completeness,
consistency, ambiguity, testability, traceability, scope/MVP boundaries,
risks, and unresolved decisions. Do not edit files or implement anything.
Return findings ordered by severity, each with ID, exact reference, impact,
and proposed resolution. Separate blocking findings, non-blocking findings,
and questions for the Product Owner. Identify the reviewed Git commit or
revision and explicitly state what you could not verify.
```

**Evidence:** Review report tied to the reviewed revision.

### 1.5 Resolve findings and revalidate

**Accountable:** Product Owner

Classify each finding as **accepted**, **rejected with rationale**, **deferred under an explicit rule**, or **requiring clarification**. Resolve blocking issues before baseline approval. Apply authorized edits through the project's normal change process. Re-review materially changed or previously unreviewed requirements; record the new revision.

Retries and review rounds must remain bounded by project policy. Do not assume an arbitrary fixed number of rounds.

**Evidence:** Findings register, decisions, revised specification, and any follow-up reviews.

### 1.6 Approve the baseline

**Accountable:** Product Owner

Approve or reject the exact consolidated revision. Record approver, decision, date, immutable revision identifier, and any explicitly accepted residual issues. Do not silently change an approved baseline; use change control for subsequent modifications.

**Evidence:** Approval record and identified requirements baseline.

## 4. Exit gate: Requirements Baseline

| ID | Criterion | Evidence |
|---|---|---|
| RG-01 | Specification is identifiable and versioned | Document and revision |
| RG-02 | Confirmed, proposed, and open items are distinguishable | Specification and decision log |
| RG-03 | Applicable requirements have verifiable acceptance criteria | Requirements-to-criteria references |
| RG-04 | Independent review of the identified revision is complete | Review report |
| RG-05 | Blocking findings are resolved; other findings have documented dispositions | Findings register |
| RG-06 | Scope, exclusions, and relevant delivery boundaries are sufficiently defined | PO scope decision |
| RG-07 | Remaining open issues do not block the next phase | Explicit PO disposition |
| RG-08 | PO explicitly approves the exact baseline revision | Approval record |

**Gate not passed:** No binding technical design or implementation may be authorized against this draft. Separately approved feasibility work may proceed within its own scope.

## 5. Deliverables and storage

- Versioned requirements specification.
- Requirements decisions and open-questions log.
- Independent review report and findings register.
- Approved or rejected baseline decision tied to an exact revision.

Store these artifacts in the project's designated documentation system. For repository-based projects, a possible layout is:

```text
docs/
  requirements/
    requirements.md
    decisions.md
    reviews/
      review-<revision>.md
    approvals/
      baseline-<revision>.md
  workflows/
    01-requirements-baseline.md
```

The layout is an example, not a required directory contract. Avoid redundant copies of authoritative content.

## 6. Roles and boundaries

| Role | Responsibility | May approve baseline? |
|---|---|---|
| Product Owner | Scope, requirements decisions, acceptance, approval | Yes |
| Requirements engineer / assistant | Elicitation, drafting, clarification | No |
| Independent reviewer / Codex CLI | Evidence-based review, findings | No |
| Implementation agent / Claude Code | Authorized corrections or later implementation | No |
| Orchestrator, where present | Tracking, handoffs, gates, approval enforcement | No |

A reviewer must be independent of the work being assessed. An automated tool cannot grant its own permissions or substitute its assessment for PO approval.

## 7. Transition

Once the gate passes, proceed to **Step 2: Technical Concept & Architecture** or the equivalent next phase in the project's workflow. Technical decisions must remain traceable to the approved requirements baseline.

## 8. Workflow adoption checklist

- [ ] Replace example document paths with the project's actual authoritative path.
- [ ] Confirm which agent instruction files are used; update only those applicable.
- [ ] Assign the PO and independent reviewer.
- [ ] Confirm review report and approval record locations.
- [ ] Apply the project's security, tool access, and change-control rules.

**Workflow status:** Draft. This workflow itself requires normal project review and approval before being treated as a mandatory organizational policy.
