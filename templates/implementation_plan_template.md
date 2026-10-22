# Implementation Plan

> **Purpose:** Translate the approved study design into small, manageable, independently verifiable programming tasks.
>
> **How to use:** Work through the numbered units in order. For each unit, ask AI to generate the implementation, run it locally, request independent verification, and commit the completed work to Git.
>
> This document specifies **what to implement and verify**, not the implementation code itself.

## 1. Project overview

**Project:** [Project name]

**Study design:** `study_design.md`

**Programming language:** [Python / R / Other]

**Development environment:** [e.g., VS Code, RStudio, Jupyter]

**Data location:** [Path or instructions for obtaining data]

**Final deliverable:** [e.g., reproducible analysis repository and report]

### General implementation principles

- Complete one unit at a time, in dependency order.
- Keep each unit as small as reasonably possible, ideally achievable in 5–15 minutes.
- Prefer one clearly defined objective and one small deliverable per unit.
- Generate only the code needed for the current unit.
- Keep code readable, beginner-friendly, and appropriately commented.
- Reuse previously completed code rather than duplicating it.
- Run and inspect code locally; do not assume AI-generated code is correct.
- Verify each unit against its requirements before marking it complete.
- Commit each completed and verified unit to Git.
- Do not silently modify the study design, implementation plan, or previously approved decisions.

## 2. Project structure

Describe the intended organization of the repository.

```text
project/
├── README.md
├── study_design.md
├── implementation_plan.md
├── data/
├── scripts/
└── results/
```

[Adapt this structure to the project. Add files and directories only when needed. Specify which data and generated files should not be committed to Git.]

## 3. Implementation overview

Organize related units into stages. Each stage should correspond to a meaningful part of the study design.

| Unit | Task | Expected deliverable | Dependencies |
|---|---|---|---|
| 1.1 | [Small task] | [File or output] | None |
| 1.2 | [Small task] | [File or output] | 1.1 |
| 2.1 | [Small task] | [File or output] | 1.2 |
| 2.2 | [Small task] | [File or output] | 2.1 |

The overview is a navigation aid. Detailed requirements are specified below.

## 4. Implementation units

Repeat the following structure for every unit.

### Stage 1 — [Stage name]

**Stage objective:** [What this stage accomplishes and how it contributes to the study design.]

#### Unit 1.1 — [Short, action-oriented title]

**Goal**

[Describe one specific objective and why it is necessary.]

**Dependencies**

[Previously completed units, or "None".]

**Inputs**

[Required datasets, variables, files, or outputs from previous units. Include filenames and relevant locations.]

**Implementation requirements**

[Specify exactly what the code must accomplish, using a short numbered list if necessary. Describe the required behavior, not the code itself.]

**Deliverable**

[Specify the file to create or modify, its intended purpose, and any expected outputs.]

**Verification requirements**

[Describe concrete checks that establish whether the implementation meets its requirements. Include expected values, invariants, or failure conditions where known. Prefer checks that can be performed independently of the implementation.]

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git.

---

#### Unit 1.2 — [Short, action-oriented title]

[Repeat the same structure.]

### Stage 2 — [Stage name]

**Stage objective:** [Description]

#### Unit 2.1 — [Short, action-oriented title]

[Repeat the same structure.]

[Continue until all approved study-design requirements are covered.]

## 5. Integration and final verification

After completing the individual units, verify that the project works as a whole.

**End-to-end execution**

[How should the complete analysis be run from the beginning?]

**Expected outputs**

[Which files, tables, figures, or reports should be produced?]

**Integration checks**

[How will outputs and dependencies across units be checked for consistency?]

**Reproducibility checks**

[How will someone else reproduce the analysis from the documented inputs and environment?]

**Final completion criteria**

- [ ] All required implementation units are completed.
- [ ] The full analysis runs successfully in the documented order.
- [ ] Expected outputs are generated and verified.
- [ ] Results are consistent with the approved study design.
- [ ] Required software and dependencies are documented.
- [ ] The repository contains sufficient instructions to reproduce the analysis.
- [ ] Final changes are committed to Git.

## 6. Open issues and plan revisions

Record substantive changes when implementation reveals problems or new requirements.

| Affected unit(s) | Issue or proposed change | Reason | Decision |
|---|---|---|---|
| [Unit number] | [Description] | [Explanation] | Open / Approved / Rejected |

### Revision procedure

1. Identify the problem or new information.
2. Determine whether it affects the study design, implementation plan, or both.
3. Explain the proposed change and its consequences for completed or future units.
4. Obtain researcher approval before changing substantive requirements.
5. Provide only the replacement text for affected sections; preserve unrelated content and formatting.
6. Revisit previously completed units if their correctness is affected.
7. Commit approved changes to Git.

---

## 7. Plan approval

Before beginning implementation, confirm that:

- [ ] All major components of the approved study design are represented.
- [ ] Units are sufficiently small for a beginner to implement and review.
- [ ] Each unit has clear inputs, requirements, and deliverables.
- [ ] Each unit has concrete, independently checkable verification requirements.
- [ ] Dependencies and execution order are explicit.
- [ ] No unit requires implementing unfinished future units.
- [ ] Provisional methodological decisions are identified rather than silently resolved.
- [ ] The plan does not contain implementation code.

**Plan status:** Draft / Approved / Revision required

**Version or date:** [Version / YYYY-MM-DD]