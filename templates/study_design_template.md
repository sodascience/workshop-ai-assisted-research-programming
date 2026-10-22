# Study Design

> **Purpose:** Define what the research project aims to investigate, which data and methods will be used, and how the results will be evaluated.
>
> This document describes the research design, not the programming implementation. Complete it interactively with AI, review the proposed decisions, and save the approved version before creating an implementation plan.
>
> **Instructions:** Replace the placeholders below. Use "To be decided" when a decision cannot yet be made. Distinguish confirmed decisions from provisional choices.

## 1. Research question and scope

**Research question:**
[What question are you trying to answer?]

**Research objectives:**
[What do you hope to learn or demonstrate?]

**Study type:**
[e.g., exploratory, descriptive, explanatory, predictive, experimental]

**Target population or scope:**
[What observations, individuals, documents, or phenomena do the findings concern?]

**Intended interpretation:**
[What kinds of conclusions can and cannot be drawn? For example, associations versus causal effects.]

## 2. Data

**Data source(s):**
[Name, location, version, and relevant documentation.]

**Unit of observation:**
[What does one row or record represent?]

**Data structure:**
[e.g., tabular, text, longitudinal, multimodal; relevant files and relationships.]

**Sample and selection:**
[Which observations are included? How were they selected?]

**Known limitations:**
[e.g., missing data, selection bias, measurement limitations, access restrictions.]

**Data access and governance:**
[Can the data be accessed, processed with AI tools, and shared? Are there privacy, licensing, or institutional restrictions?]

## 3. Variables and measurements

Identify the main concepts and how they will be measured.

| Role | Concept | Variable(s) / measurement | Notes |
|---|---|---|---|
| Outcome / target | [Concept] | [Variable] | [Definition] |
| Predictor / explanatory | [Concept] | [Variable] | [Definition] |
| Adjustment / control | [Concept] | [Variable] | [Rationale] |
| Other | [Concept] | [Variable] | [Rationale] |

**Derived variables or features:**
[Are any transformations, aggregations, or text features needed?]

**Measurement concerns:**
[Are the variables valid and reliable measures of the intended concepts?]

## 4. Analysis strategy

Describe the planned analyses in conceptual terms. Specific methods may remain provisional until the data have been examined.

### 4.1 Data preparation

[What needs to be joined, filtered, cleaned, reconstructed, or transformed?]

### 4.2 Data exploration

[What summaries and visualizations will help understand the data and answer the research question?]

### 4.3 Main analysis

[What statistical, computational, or qualitative methods are proposed? Why are they appropriate?]

### 4.4 Model or method evaluation

[How will assumptions, model fit, predictive performance, or other relevant properties be assessed?]

### 4.5 Sensitivity and robustness

[Which alternative specifications, assumptions, or analytical decisions should be examined?]

## 5. Quality assurance and verification

**Data quality:**
[What properties of the data need to be checked?]

**Analytical correctness:**
[What checks are needed to establish that the analyses implement the intended methods correctly?]

**Results validation:**
[How will results be checked for plausibility, consistency, and robustness?]

**Reproducibility:**
[What information and materials must be preserved so the analysis can be rerun?]

> Specific executable checks will be developed in the implementation plan. Here, describe what needs to be verified and why.

## 6. Expected outputs

| Output | Description | Purpose |
|---|---|---|
| [Table / figure / model / dataset] | [What it contains] | [What question it addresses] |
| [Output] | [Description] | [Purpose] |

**Final deliverable:**
[e.g., reproducible analysis repository, research report, presentation, paper.]

## 7. Limitations and risks

**Methodological limitations:**
[What could limit the validity or interpretation of the findings?]

**Data limitations:**
[What important information is missing, incomplete, or potentially biased?]

**Technical or practical constraints:**
[e.g., available software, computing resources, programming experience, time.]

## 8. Decisions and open questions

Track substantive choices that have been made or still need to be resolved.

| Decision | Current choice | Status | Rationale / condition for revision |
|---|---|---|---|
| [Decision] | [Choice] | Approved / Provisional / Open | [Reason] |
| [Decision] | [Choice] | Approved / Provisional / Open | [Reason] |

**Questions to revisit after inspecting the data:**
- [Question]
- [Question]

## 9. Design approval

Before proceeding to implementation planning, confirm that:

- [ ] The research question and scope are clear.
- [ ] Data sources and important restrictions are identified.
- [ ] Key variables and measurements are specified or flagged as provisional.
- [ ] The proposed analysis strategy is methodologically defensible.
- [ ] Quality assurance and verification needs are identified.
- [ ] Expected outputs are defined.
- [ ] Unresolved decisions and assumptions are documented.

**Design status:** Draft / Approved with open decisions / Approved

**Version or date:** [Version / YYYY-MM-DD]

---

## Design change policy

The study design may evolve as new information becomes available.

When changes are proposed:

1. Explain the reason for the change.
2. Identify the affected sections and previously approved decisions.
3. Obtain researcher approval before adopting substantive changes.
4. Modify only the affected sections; preserve unrelated content and formatting.
5. Update the implementation plan if the change affects planned or completed work.

**The researcher remains responsible for approving methodological decisions. AI suggestions do not constitute approval.**