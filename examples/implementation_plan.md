# Implementation Plan

> **Purpose:** Translate the approved study design into small, manageable, independently verifiable programming tasks.
>
> **How to use:** Work through the numbered units in dependency order. For each unit, request only that implementation, run it locally, request independent verification, and commit verified changes to Git. This plan specifies what to implement and verify, not the code.

## 1. Project overview

**Project:** SODA Open Research Teaching Data analysis — factors associated with OpenAlex citation counts  
**Study design:** `study_design.md`  
**Programming language:** R  
**Development environment:** RStudio or another R-capable editor; local R installation  
**Data location:** Obtain SODA Open Research Teaching Data release 1.0.0 according to the source documentation. Keep the original source files unchanged in a local, Git-ignored data directory. The exact source filenames and table layout must be recorded during Unit 2.1; they are not specified in the approved design.  
**Final deliverable:** Reproducible Git repository containing documented data-acquisition instructions, R preparation and analysis scripts, environment information, aggregate results, figures, and a concise report. Do not put raw work-level records or abstract text in Git. [5][6]

The study concerns associations—not causal effects—between citations and open-access status, three collaboration counts, recorded study-design labels, title and abstract characteristics, with categorical publication-year and primary-field adjustment. Subfield is excluded from the predictor set. [8][4] The intended population is the source frame represented by verified sampling weights, not research worldwide. [9]

### General implementation principles

- Complete one unit at a time, in dependency order. Do not paste work-level records, dataset contents, or abstracts into AI tools.
- Preserve downloaded source files unchanged; record release/version, source location, and retrieval details without exposing private/local paths in public outputs.
- Use aggregate-only outputs in Git, after checking the data-source terms.
- Distinguish facts established by documentation from decisions that require inspection, researcher approval, or institutional confirmation.
- Do not fit or interpret the weighted primary model until the meaning of weights and the uncertainty procedure have been reviewed and approved.
- Do not automatically remove works with missing values, rare labels, or unusual citations. Record decisions and reasons; retain the supplied sample except for verified duplicates or invalid records unless approved otherwise. [9][5]
- Keep the analysis exploratory unless a separate confirmatory plan is approved. Report estimate sizes and uncertainty, not p-values alone. [7]

## 2. Project structure

```text
project/
├── README.md
├── study_design.md
├── implementation_plan.md
├── data/
│   ├── raw/                 # Local source files; Git-ignored
│   └── processed/           # Work-level derived files; Git-ignored
├── scripts/
│   ├── 00_setup.R
│   ├── 01_inventory.R
│   ├── 02_schema_and_audit.R
│   ├── 03_prepare_work_table.R
│   ├── 04_construct_features.R
│   ├── 05_define_analysis_sample.R
│   ├── 06_descriptives.R
│   ├── 07_fit_models.R
│   ├── 08_model_checks.R
│   └── 09_export_results.R
├── results/                 # Aggregate tables, figures, and report only
├── docs/                    # Data notes, decisions, and codebook
├── renv.lock                # If renv is used for the recorded environment
└── .gitignore
```

Keep `data/raw/`, `data/processed/`, abstract text, work-level exports, and any other potentially identifying or restricted files out of Git. Commit only code, documentation, package/environment metadata, and aggregate outputs permitted by the source terms. Do not assume all aggregate outputs are automatically shareable: inspect them for record-level disclosure and terms-of-use compliance before committing.

## 3. Implementation overview

| Unit | Task | Expected deliverable | Dependencies |
|---|---|---|---|
| 1.1 | Establish repository folders and Git exclusions | `.gitignore`, folders | None |
| 1.2 | Document data acquisition and provenance fields | `README.md` | 1.1 |
| 1.3 | Record R and package environment | `scripts/00_setup.R`, environment record | 1.1 |
| 1.4 | Record ethics/data-governance determination | `docs/ethics_and_data_governance.md` | 1.1 |
| 2.1 | Inventory local source files | `scripts/01_inventory.R`, aggregate inventory | 1.2 |
| 2.2 | Map source schema to study variables | `docs/data_dictionary.md` | 2.1 |
| 2.3 | Verify weight and source-variable definitions | `docs/data_decisions.md` | 2.2 |
| 2.4 | Audit identifiers, duplicates, invalid records, and sample frame | `scripts/02_schema_and_audit.R`, audit summaries | 2.2, 2.3 |
| 3.1 | Build the work-level base table | `scripts/03_prepare_work_table.R` | 2.4 |
| 3.2 | Aggregate relational data before joining | `scripts/03_prepare_work_table.R` | 3.1 |
| 3.3 | Verify one row per work after joins | audit output | 3.2 |
| 3.4 | Reconstruct abstracts and check a local sample | `scripts/03_prepare_work_table.R`, validation notes | 2.2 |
| 3.5 | Derive title and abstract word counts | `scripts/04_construct_features.R` | 3.3, 3.4 |
| 3.6 | Derive readability and flag unsuitable text | `scripts/04_construct_features.R` | 3.4 |
| 3.7 | Construct collaboration counts and label indicators | `scripts/04_construct_features.R` | 3.2 |
| 3.8 | Record exclusions and establish analysis-specific samples | `scripts/05_define_analysis_sample.R` | 3.3, 3.5–3.7 |
| 3.9 | Profile missingness and decide sparse-label handling | `scripts/05_define_analysis_sample.R`, decision record | 3.8 |
| 3.10 | Recheck weights and year–field cells after exclusions | audit table, weight decision | 2.3, 3.8 |
| 4.1 | Summarize sample coverage and year–field cells | `scripts/06_descriptives.R`, tables | 3.8–3.10 |
| 4.2 | Summarize citation counts | tables and figure | 4.1 |
| 4.3 | Summarize predictor distributions and missingness | tables and figures | 4.1 |
| 4.4 | Summarize design-label frequency and co-occurrence | tables | 3.7, 4.1 |
| 4.5 | Examine predictor overlap and relationships | tables and figures | 4.3 |
| 4.6 | Approve and record model predictor forms | `docs/data_decisions.md` update | 4.2–4.5 |
| 5.1 | Create and verify model-ready data | `scripts/05_define_analysis_sample.R` | 3.9, 3.10, 4.6 |
| 5.2 | Fit the weighted negative-binomial primary model | `scripts/07_fit_models.R` | 5.1 and approved weight/variance decision |
| 5.3 | Fit the weighted Poisson comparison | `scripts/07_fit_models.R` | 5.2 |
| 5.4 | Fit the unweighted joint-model sensitivity analysis | `scripts/07_fit_models.R` | 5.2 |
| 5.5 | Check model fit, stability, and influential works | `scripts/08_model_checks.R` | 5.2–5.4 |
| 5.6 | Run approved exclusion and missingness sensitivities | `scripts/08_model_checks.R` | 5.5 |
| 5.7 | Export model estimates and aggregate predictions | `scripts/09_export_results.R` | 5.5, 5.6 |
| 6.1 | Complete variable notes and reproducibility instructions | `docs/data_dictionary.md`, `README.md` | 2.2, 5.7 |
| 6.2 | Write concise methods/results/limitations report | `results/report.md` | 5.7, 6.1 |
| 6.3 | Run the complete analysis from a clean session | integrated scripts and outputs | 1.1–6.2 |
| 6.4 | Final repository and data-governance review | final Git-reviewed repository | 6.3 |

## 4. Implementation units

### Stage 1 — Project setup and governance

**Stage objective:** Create a safe, reproducible local project foundation before handling the source data or producing results.

#### Unit 1.1 — Establish repository folders and Git exclusions

**Goal**

Set up a minimal repository layout and prevent source records, abstracts, and work-level derived files from being committed.

**Dependencies**

None.

**Inputs**

The approved project structure in Section 2 of this plan; local Git repository.

**Implementation requirements**

1. Create the listed project folders needed for the work.
2. Add Git ignore rules for `data/raw/`, `data/processed/`, local temporary files, and any local configuration or logs that may contain private paths or record-level data.
3. Do not ignore scripts, study documentation, or permitted aggregate results.

**Deliverable**

Repository folders and `.gitignore`.

**Verification requirements**

- Check that the folders exist and Git reports intended source/processed data paths as ignored.
- A harmless test file placed under each protected data folder must not appear as a Git-tracked change; a test README or script must remain trackable.
- Failure: any raw or work-level data path appears as trackable.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git.

---

#### Unit 1.2 — Document data acquisition and provenance fields

**Goal**

Make it possible for another researcher to obtain the same release without placing data in the repository.

**Dependencies**

1.1.

**Inputs**

Study design; SODA Open Research Teaching Data release 1.0.0 source documentation and access instructions, when available.

**Implementation requirements**

1. Add README instructions identifying the dataset and version, official source/access route, and steps to place files locally under `data/raw/`.
2. List provenance details to record: retrieval date, release/version, documented source URL or citation, original filenames, and any documented snapshot dates.
3. Do not invent an access URL, filename, or citation. Mark unavailable details for confirmation from the official source.
4. State that raw work-level data and abstracts must not be committed or sent to AI tools.

**Deliverable**

`README.md` with a data-acquisition section.

**Verification requirements**

- A reader can identify the dataset/version and see where to obtain it or which official detail remains missing.
- Confirm instructions do not imply that data are bundled in Git.
- Failure: any unverified URL, invented filename, or instruction to commit source records appears.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git.

---

#### Unit 1.3 — Record R and package environment

**Goal**

Record the software environment needed to reproduce the analysis.

**Dependencies**

1.1.

**Inputs**

Local R installation; repository.

**Implementation requirements**

1. Record the R version and platform used.
2. Create a small setup script that reports the active R version and versions of packages actually used; do not install unnecessary packages at this stage.
3. Once the analysis dependencies are known, use `renv` and a lockfile if feasible, and record any reason it is not used.

**Deliverable**

`scripts/00_setup.R` and initial environment notes; later update `renv.lock` or document the alternative.

**Verification requirements**

- Running the setup script displays the same R version as the local installation and reports installed versions without errors.
- The dependency record must not list packages that are not used by project scripts.
- Failure: environment information is absent or package versions are silently assumed.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git.

---

#### Unit 1.4 — Record ethics and data-governance determination

**Goal**

Resolve and document the required institutional status before analysis proceeds; public availability alone is not treated as an exemption. The official determination is pending in the design. [2]

**Dependencies**

1.1.

**Inputs**

Supervisor or relevant institutional office’s written determination; source dataset terms.

**Implementation requirements**

1. Create a record with determination, date, office/source, any conditions, and source-data sharing restrictions.
2. If the determination has not yet been received, explicitly record “pending”; do not state or imply an exemption.
3. State that record-level data and abstracts must not be shared with AI tools.

**Deliverable**

`docs/ethics_and_data_governance.md`.

**Verification requirements**

- The note either cites the official determination and its source or clearly says it is pending.
- Confirm no unsupported exemption claim appears.
- This is a decision gate: do not begin analysis activities that institutional guidance says must wait.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git.

### Stage 2 — Source-data inspection and methodological gates

**Stage objective:** Identify the actual source files and schema, then verify definitions and sampling information needed to prepare data without guessing.

#### Unit 2.1 — Inventory local source files

**Goal**

Record exactly which local files belong to release 1.0.0, without printing record-level contents.

**Dependencies**

1.2.

**Inputs**

Files obtained from the official source and placed in `data/raw/`; README acquisition instructions.

**Implementation requirements**

1. List filenames, file types, sizes, and (where practical) checksums.
2. Identify candidate data files versus documentation files.
3. Do not print rows, abstracts, or other record contents to the console or save them in a committed inventory.
4. Save only aggregate file inventory information.

**Deliverable**

`scripts/01_inventory.R` and `docs/source_inventory.csv` or equivalent aggregate inventory.

**Verification requirements**

- Inventory filenames agree with the local files and each recorded file type/size is plausible.
- The inventory includes no work-level records or abstract text.
- Failure: missing source files are treated as present, or data contents are exposed in a tracked file.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git.

---

#### Unit 2.2 — Map source schema to study variables

**Goal**

Determine where each design variable is stored before creating transformations or joins.

**Dependencies**

2.1.

**Inputs**

Source data files identified in `docs/source_inventory.csv`; source codebook/documentation; target variables in the study design.

**Implementation requirements**

1. Record the actual source filename, table, and field name for stable work ID, `cited_by_count`, `is_oa`, publication year, primary field, subfield, weights, author/institution/country records or counts, study-design labels, title, and abstract representation.
2. Record types, units, reference categories where documented, and whether each variable is supplied or derived.
3. Include source definitions and snapshot/retrieval date for citations and open-access status when documented; flag unknown details rather than infer them.
4. Record publication-type, retraction, truncation, and missingness flags if present.

**Deliverable**

Initial `docs/data_dictionary.md` containing verified mappings and unresolved entries.

**Verification requirements**

- Every planned study variable is mapped to a documented source field or marked unavailable/unresolved.
- Field names are checked against the actual schema, not guessed from prior dataset versions.
- No study-design variable is silently replaced with a similarly named field.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git.

---

#### Unit 2.3 — Verify weight and source-variable definitions

**Goal**

Establish what the weights represent and whether the proposed weighted analysis and uncertainty calculation are defensible. The weighted model and design-appropriate standard errors are explicitly provisional until this is resolved. [9][11]

**Dependencies**

2.2.

**Inputs**

Source documentation; weight field and sampling structure mapped in `docs/data_dictionary.md`; supervisor/statistical advice as needed.

**Implementation requirements**

1. Record documented weight meaning, target population/frame, scale, totals or calibration targets, and missing/zero/negative value rules.
2. Record sampling design features available for variance estimation (for example, strata, clusters, or finite-population information) without assuming they exist.
3. Confirm definitions and snapshots for `cited_by_count` and `is_oa`, and definitions for field, label, and truncation variables.
4. Obtain approval for an estimation and uncertainty approach suitable for the actual weights and negative-binomial model. If unavailable, document the limitation and an approved alternative before interpreting weighted estimates.

**Deliverable**

`docs/data_decisions.md` with a dated, sourced weight/definition decision; mark unresolved choices as provisional.

**Verification requirements**

- Each definition is traceable to source documentation or clearly marked unverified.
- The target population is bounded by what the weights actually represent.
- No weighted standard-error method is approved solely because a generic fitting function accepts a `weights` argument.
- If method or target frame remains unknown, the primary-model interpretation gate remains closed.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git.

---

#### Unit 2.4 — Audit identifiers, duplicates, invalid records, and sample frame

**Goal**

Establish the supplied sample structure and identify only verified duplicate or invalid records, preserving the primary sample otherwise. [9]

**Dependencies**

2.2, 2.3.

**Inputs**

Mapped source files and stable work identifier; year, primary field, publication type, retraction and weight fields where available.

**Implementation requirements**

1. Summarize row counts and identifier missingness/uniqueness in each work-level file.
2. Inspect exact and key-based duplicate patterns without automatically deleting records.
3. Summarize counts by publication year and primary field; the design describes 11,700 English-language works from 2011–2025 balanced across year–field groups, to be checked against the release documentation. [8][9]
4. Summarize invalid values, publication type, and retraction status where available.
5. Produce a proposed record-level exclusion list locally if necessary, with reason codes; do not export IDs to Git.

**Deliverable**

Audit section in `scripts/02_schema_and_audit.R` and aggregate audit tables in `results/`.

**Verification requirements**

- Aggregate totals can be compared with the release documentation; any differences are explained, not silently “fixed.”
- Every proposed exclusion has a documented rule and local record-level traceability; aggregate summaries committed to Git contain no IDs.
- Verify year range, number of works, duplicate count, and year–field balance against source documentation rather than assuming all are exact after exclusions.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git.

### Stage 3 — Work-level data preparation and feature construction

**Stage objective:** Build a one-row-per-work analysis table, prepare text and relational features, and document missingness and exclusions before modeling. Relational tables must be aggregated before joins to avoid duplicate works. [4][5]

#### Unit 3.1 — Build the work-level base table

**Goal**

Create a local analysis base with one row per work and only the work-level source fields needed downstream.

**Dependencies**

2.4.

**Inputs**

Work-level source file(s), stable ID, citation count, OA status, title, publication year, primary field, subfield, weight, and documented relevant flags as available.

**Implementation requirements**

1. Read the documented source file(s) without modifying them.
2. Select the mapped fields needed for the study and retain the stable work ID locally.
3. Preserve source variables and distinguish them from derived variables.
4. Save the work-level table only under Git-ignored `data/processed/`.

**Deliverable**

`scripts/03_prepare_work_table.R` creating a local base work table.

**Verification requirements**

- Base-table row count matches the corresponding audited work-level input except for explicitly documented, approved exclusions.
- Stable work IDs remain unique at this step.
- Required mapped variables are present; values for selected sample records agree with source files when checked locally.
- Failure: source files are overwritten or derived fields replace source values without traceability.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git.

---

#### Unit 3.2 — Aggregate relational data before joining

**Goal**

Convert author, institution, country, and study-design label records to work-level summaries before joining to the base table.

**Dependencies**

3.1.

**Inputs**

Relational source tables and their work IDs; documented truncation/cap flags; source definitions in `docs/data_dictionary.md`.

**Implementation requirements**

1. For each relational table, aggregate records by stable work ID before joining.
2. Apply documented deduplication rules when counting authors, institutions, and countries; if rules are undocumented, flag and resolve them before treating counts as final.
3. Retain truncation flags and distinguish unknown/truncated counts from reliable observed counts where the source allows.
4. Summarize multi-label study-design records by work ID while preserving each recorded label.

**Deliverable**

Work-level aggregates in the preparation script and Git-ignored processed files or intermediate objects.

**Verification requirements**

- Each aggregate table has at most one row per work ID.
- Manually trace several local works from the raw relation rows to their resulting counts/labels.
- Counts follow documented deduplication and truncation rules; no unexplained many-to-many expansion occurs.
- Failure: joining raw relational rows directly multiplies a work’s citation record.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git.

---

#### Unit 3.3 — Verify uniqueness and join coverage

**Goal**

Show that prepared joins still represent one row per scholarly work and quantify unmatched records.

**Dependencies**

3.2.

**Inputs**

Base work table and aggregated relational tables from Unit 3.2.

**Implementation requirements**

1. Join each work-level aggregate to the base by stable work ID.
2. Record before/after row counts, unique work counts, and unmatched IDs as aggregate counts.
3. Preserve a local join-audit record sufficient to investigate mismatches without committing IDs.

**Deliverable**

Join checks in `scripts/03_prepare_work_table.R` and aggregate join summary under `results/`.

**Verification requirements**

- Final joined row count equals unique work count in the base table unless a documented exclusion explains the difference.
- No work ID occurs more than once after joining.
- Unmatched counts are either zero or explained from source structure; unexplained row growth is a failure.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git.

---

#### Unit 3.4 — Reconstruct abstracts and check a local sample

**Goal**

Reconstruct abstract text using the source’s documented representation and confirm the transformation before deriving text features. [5]

**Dependencies**

2.2, 3.3.

**Inputs**

Documented abstract representation and source abstract fields; joined work table.

**Implementation requirements**

1. Implement only the reconstruction specified by source documentation.
2. Keep reconstructed abstracts local and Git-ignored; do not include abstract examples in reports, logs, AI prompts, or committed files.
3. Select a small local validation subset and compare reconstructed text with the original representation by manual inspection.
4. Record validation procedure and aggregate pass/issues counts, not abstract text or work IDs.

**Deliverable**

Abstract reconstruction in `scripts/03_prepare_work_table.R` and an aggregate validation note.

**Verification requirements**

- Reconstructed text for inspected records matches the documented source representation, including ordering and punctuation as defined by the source.
- Missing or malformed representations are flagged rather than converted silently to misleading text.
- Failure: reconstructed abstracts are committed, sent to AI, or validation is reported without local inspection.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git.

---

#### Unit 3.5 — Derive title and abstract word counts

**Goal**

Create separate, reproducible title and abstract length variables.

**Dependencies**

3.3, 3.4.

**Inputs**

Title and validated reconstructed abstract in the local work table; text-processing rule documented in `docs/data_decisions.md`.

**Implementation requirements**

1. Apply one documented word-count rule to titles and abstracts separately.
2. Preserve source text fields and add distinct derived counts.
3. Define behavior for missing, empty, and whitespace-only strings; do not convert missing text to a genuine zero-word value without an explicit rule.

**Deliverable**

Word-count fields in `scripts/04_construct_features.R` and the local processed table.

**Verification requirements**

- Manually check word counts on a small, locally inspected set including punctuation, hyphenation, and empty/missing examples.
- All nonmissing counts are non-negative integers; missing source text is handled according to the documented rule.
- Title and abstract counts are not accidentally copied into one another.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git.

---

#### Unit 3.6 — Derive readability and flag unsuitable text

**Goal**

Calculate Flesch–Kincaid Grade Level only for suitable abstract text and preserve flags for short or unsuitable cases. It is a rough proxy, not a direct measure of research complexity or comprehensibility. [4][6]

**Dependencies**

3.4, 3.5.

**Inputs**

Reconstructed abstracts and word counts; documented readability method/package; short-text decision to be set before model fitting.

**Implementation requirements**

1. Record the exact implementation/source of the Flesch–Kincaid Grade Level calculation and any required text normalization.
2. Apply a documented short-text/suitability rule, mark ineligible cases, and do not treat unsupported scores as valid measurements.
3. Retain a separate suitability/flag field and explain the rule in `docs/data_decisions.md`.

**Deliverable**

Readability and suitability fields in `scripts/04_construct_features.R` and local processed data.

**Verification requirements**

- Compare calculations for a few non-sensitive test sentences against a trusted implementation or hand-checked reference.
- Confirm short/empty/missing abstract cases are flagged as specified, not assigned plausible-looking scores.
- Inspect score range and non-finite values; investigate, rather than silently delete, unusual values.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git

---

#### Unit 3.7 — Construct collaboration counts and label indicators

**Goal**

Produce the three collaboration measures and work-level indicators for recorded study-design labels without implying that missing labels prove absence of a design. [4][5]

**Dependencies**

3.2, 3.3.

**Inputs**

Aggregated author, institution, country, and design-label data; source definitions, deduplication rules, and truncation flags.

**Implementation requirements**

1. Name author, institution, and country counts separately and retain relevant truncation flags.
2. Represent study-design labels as separate indicators at work level, allowing multiple labels where recorded.
3. Distinguish no label recorded from missing/unavailable label metadata wherever the source permits.
4. Do not select a rare-label cutoff or merge categories until frequencies have been inspected and the decision is documented.

**Deliverable**

Derived variables in `scripts/04_construct_features.R` and a local work-level table.

**Verification requirements**

- Manually verify several local works’ counts and label indicators against their source relation rows.
- Count variables are non-negative where observed; label indicators contain only the permitted states.
- Multi-label works retain more than one indicator when appropriate; unknown metadata is not silently coded as “no label.”

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git.

---

#### Unit 3.8 — Record exclusions and establish analysis-specific samples

**Goal**

Keep the primary sample as supplied except for verified duplicates or invalid records, and make exclusions auditable. [9]

**Dependencies**

3.3, 3.5–3.7.

**Inputs**

Joined local work table; Unit 2.4 audit; approved inclusion/exclusion decisions.

**Implementation requirements**

1. Create a local exclusion log with work ID, reason, and source/decision reference; never commit the IDs.
2. Exclude only verified duplicate or invalid records from the primary sample unless a separately approved decision changes this rule.
3. Keep publication type and retraction status as audit variables; use them for sensitivity analyses if material rather than silently restricting the primary sample.
4. Report counts removed by reason in aggregate and preserve analysis-specific sample membership locally.

**Deliverable**

`scripts/05_define_analysis_sample.R`, local exclusion log, and aggregate exclusion summary.

**Verification requirements**

- Every removed record has an allowed, documented reason; all other supplied works remain eligible.
- Aggregate total before and after exclusions reconciles exactly.
- Rejected shortcut: dropping every work with any missing predictor at this stage.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git.

---

#### Unit 3.9 — Profile missingness and decide sparse-label handling

**Goal**

Quantify analysis-variable coverage and settle transparent handling of rare labels before model fitting. [5][6]

**Dependencies**

3.8.

**Inputs**

Primary eligible work table; outcome, predictors, adjustment factors, weight, label indicators, and text suitability flags.

**Implementation requirements**

1. Summarize missingness per variable and by relevant strata, especially year and primary field.
2. Summarize label frequencies and identify sparse categories without choosing a cutoff automatically.
3. Record an approved handling decision for rare labels and clarify whether “no label recorded” is a separate category/indicator from unavailable metadata.
4. State which records contribute to each planned analysis; do not apply a universal complete-case exclusion by default.
5. If complete-case loss or compositional change appears material, specify an approved sensitivity check.

**Deliverable**

Missingness/label profiling in `scripts/05_define_analysis_sample.R`; aggregate tables and a dated decision in `docs/data_decisions.md`.

**Verification requirements**

- Variable-specific denominators reconcile with the eligible sample size.
- Stratum summaries do not exceed their group totals; missing and observed counts sum to each denominator.
- Label frequency totals reconcile with multi-label/no-label representation rules.
- Any cutoff/category handling has researcher approval and a written rationale before model code is run.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git.

---

#### Unit 3.10 — Recheck weights and year–field cells after exclusions

**Goal**

Confirm whether exclusions affect the sampling structure or validity of the supplied weights. [9]

**Dependencies**

2.3, 3.8.

**Inputs**

Locally retained sample, year, primary field, weight, exclusion log, and documented source totals/cells.

**Implementation requirements**

1. Recompute aggregate eligible counts and weight summaries by year–primary-field cell.
2. Compare them with source documentation and original sample summaries.
3. Obtain a documented decision on whether supplied weights remain appropriate after exclusions or require an approved adjustment.
4. Do not recalculate weights ad hoc.

**Deliverable**

Post-exclusion sampling audit and updated decision in `docs/data_decisions.md`.

**Verification requirements**

- Cell counts and weight totals reconcile with the local records and documented benchmark where available.
- Any changed or empty cells are listed and explained in aggregate.
- If validity or variance method is unresolved, mark the weighted primary analysis as blocked rather than proceed as if settled.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git.

### Stage 4 — Descriptive analysis and model specification decisions

**Stage objective:** Describe the sample, outcome, predictors, and their overlap before choosing continuous-predictor forms and finalizing the model-ready sample. The outcome remains a count; it is not transformed solely to make it look symmetric. [7]

#### Unit 4.1 — Summarize sample coverage and year–field cells

**Goal**

Describe the analysis sample overall and by publication year and primary field.

**Dependencies**

3.8–3.10.

**Inputs**

Eligible work table; year, primary field, weight, and exclusion summary.

**Implementation requirements**

1. Produce unweighted work counts overall and by year, field, and year–field cell.
2. Produce weighted totals/summaries only where the weight meaning is verified; label the quantity and population target clearly.
3. Include retained/excluded totals and note any empty or changed cells.

**Deliverable**

`results/sample_coverage.csv` and corresponding code in `scripts/06_descriptives.R`.

**Verification requirements**

- Cell counts sum to the overall eligible count.
- Year and field margins agree with the year–field table.
- Weighted totals match the documented interpretation; otherwise display them as unverified/provisional and do not call them population estimates.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git.

---

#### Unit 4.2 — Summarize citation counts

**Goal**

Describe citation-count zeros, skew, and variation overall and across key groups without transforming the outcome for model selection. [7]

**Dependencies**

4.1.

**Inputs**

Eligible sample; `cited_by_count`; `is_oa`; publication year and primary field; verified weight, if applicable.

**Implementation requirements**

1. Report unweighted citation count summaries, zero proportion, and relevant quantiles overall and by OA/year/field.
2. Add weighted summaries only using the verified weight interpretation.
3. Make a raw-scale distribution display and, if helpful, an explicitly labeled log-scale visualization; do not replace raw values or model outcome.
4. Record the citation snapshot represented by the dataset if known.

**Deliverable**

`results/citation_descriptives.csv` and citation distribution figure.

**Verification requirements**

- Counts are non-negative integers or missing according to source definition; report and investigate violations.
- Zero proportion lies between 0 and 1, and subgroup denominators are stated.
- Summaries can be reproduced from aggregate counts and inspected for implausible extremes.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git.

---

#### Unit 4.3 — Summarize predictor distributions and missingness

**Goal**

Describe the distribution and coverage of OA, collaboration, title/abstract length, readability, year, and field before modeling.

**Dependencies**

4.1.

**Inputs**

Eligible feature table; missingness summaries; approved definitions and flags.

**Implementation requirements**

1. Summarize observed values and missing denominators for each predictor.
2. Display collaboration counts and text-feature distributions with appropriate summaries/plots; distinguish truncated counts and readability-ineligible abstracts.
3. Avoid deleting or winsorizing unusual values based solely on appearance.

**Deliverable**

Aggregate predictor summary table and figures under `results/`.

**Verification requirements**

- Reported denominators match the missingness profile in Unit 3.9.
- Binary OA/label values match documented categories; continuous/count variables have plausible types and ranges.
- Truncation and unsuitable-text flags can be traced to separate summaries.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git.

---

#### Unit 4.4 — Summarize study-design label frequencies and co-occurrence

**Goal**

Describe label coverage and multi-label patterns so model indicator choices are explicit. [7]

**Dependencies**

3.7, 4.1.

**Inputs**

Work-level label indicators; label missingness state; eligible sample.

**Implementation requirements**

1. Report frequency per label, number of works with multiple labels, no recorded label, and unavailable metadata separately where possible.
2. Show label co-occurrence in aggregate form.
3. Apply the sparse-label decision only as recorded in Unit 3.9.

**Deliverable**

`results/study_design_labels.csv` and co-occurrence summary.

**Verification requirements**

- Label counts are bounded by the sample size but are not incorrectly forced to sum to sample size when labels are multi-select.
- Multi-label, no-label, and metadata-missing totals follow the recorded representation rule.
- Any merged/excluded rare label is documented and traceable to approval.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git.

---

#### Unit 4.5 — Examine predictor overlap and relationships

**Goal**

Identify overlap among author, institution, and country counts and inspect continuous predictor relationships relevant to the log-link model. [11]

**Dependencies**

4.3, 4.4.

**Inputs**

Eligible sample; three collaboration measures; title/abstract counts; readability; label and adjustment variables.

**Implementation requirements**

1. Produce appropriate aggregate associations/plots among continuous predictors, especially collaboration measures.
2. Inspect plausible linearity on the model link scale for continuous predictors and check potential collinearity/stability concerns.
3. Do not choose transformations or flexible terms solely to optimize significance; present evidence and candidate choices for researcher decision.

**Deliverable**

`results/predictor_relationships` tables/figures and short interpretation note.

**Verification requirements**

- Pairwise summaries use consistent, stated available-case or complete-case denominators.
- High correlations or unstable overlap are flagged for decision, not hidden by a single aggregate score.
- No transformation is applied to the primary model until its form is recorded and approved in Unit 4.6.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git.

---

#### Unit 4.6 — Approve and record model predictor forms

**Goal**

Finalize, before fitting outcome models, transformations or functional forms for the continuous predictors and any treatment of collinearity concerns. These operational choices are pending in the design. [6][11]

**Dependencies**

4.2–4.5.

**Inputs**

Descriptive summaries and predictor relationship checks; approved study design.

**Implementation requirements**

1. For each continuous/count predictor, record the chosen model form or retain the untransformed main effect, with rationale based on distributions and relationship checks.
2. Document any centering/scaling, transformation, flexible term, or collinearity response; avoid undocumented predictor selection.
3. Preserve the main-effects joint model and year/primary-field categorical adjustment; do not add interactions by default.
4. Keep subfield out of the primary predictor set.

**Deliverable**

Dated, researcher-approved model-form section in `docs/data_decisions.md`.

**Verification requirements**

- Each continuous predictor has an explicit form, baseline/units where relevant, and rationale.
- Formula follows approved variables; no subfield predictor or unapproved interaction appears.
- If a material specification decision is unresolved, modeling does not begin.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git.

### Stage 5 — Count models, diagnostics, and sensitivity analyses

**Stage objective:** Estimate adjusted associations in the planned joint count model, compare with Poisson, evaluate fit and stability, and report approved sensitivity analyses. The negative-binomial model is provisional and must be compared with Poisson; weight uncertainty handling must be supported by the actual design. [11][12]

#### Unit 5.1 — Create and verify model-ready data

**Goal**

Create precisely defined analysis rows for the model while documenting which records contribute and why.

**Dependencies**

3.9, 3.10, 4.6.

**Inputs**

Eligible processed work table; approved model variables/forms; weight and uncertainty decisions; missingness and label decisions.

**Implementation requirements**

1. Select outcome, all approved substantive predictors, year and primary-field factors, weights/design fields required by the selected method, and stable local IDs.
2. Define model-specific inclusion based on the variables required by that model; retain broader sample for descriptives.
3. Record sample size and exclusions by reason for each model; do not export work IDs.
4. Enforce categorical year and primary field; do not include subfield or default interactions.

**Deliverable**

Model-ready local table and an aggregate model-sample flow table.

**Verification requirements**

- Every model row has nonmissing valid outcome and required model fields under the approved handling rule.
- Model sample size reconciles to eligible sample minus documented model-specific missingness/exclusions.
- Factor levels and reference categories match the documented choices; no duplicate work IDs.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git.

---

#### Unit 5.2 — Fit the weighted negative-binomial primary model

**Goal**

Estimate adjusted associations using the planned weighted joint negative-binomial count regression with log link, only after approving the method for both weights and uncertainty. [11]

**Dependencies**

5.1; Unit 2.3 weight/variance approval; Units 3.10 and 4.6 decision gates.

**Inputs**

Verified model-ready table; approved negative-binomial estimator and design-appropriate uncertainty procedure; approved predictors/forms and categorical reference levels.

**Implementation requirements**

1. Include `cited_by_count` as outcome; jointly include `is_oa`, the approved author/institution/country counts, sufficiently common study-design indicators, title/abstract length, readability, categorical publication year, and categorical primary field.
2. Use the approved weighting approach and uncertainty method; do not assume a generic weighted fit yields design-correct standard errors.
3. Fit main effects only unless a separate approved change exists.
4. Save model object locally, and produce an aggregate model summary with coefficient estimates, uncertainty intervals, and convergence status.
5. Exponentiate coefficients for incidence-rate-ratio presentation only with labels and interpretation as adjusted associations, not causal effects.

**Deliverable**

Primary model section in `scripts/07_fit_models.R`; local model object and aggregate summary in `results/`.

**Verification requirements**

- Confirm outcome is non-negative count, predictor/factor levels match the approved formula, and fitting reports convergence.
- Independently reconcile the number of model observations and missingness exclusions with Unit 5.1.
- Confirm weight and uncertainty method in output documentation equals the approved decision; if not, stop and correct.
- Inspect coefficient direction/scale and intervals for plausibility; unusual estimates trigger investigation, not automatic deletion.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git.

---

#### Unit 5.3 — Fit the weighted Poisson comparison

**Goal**

Compare the negative-binomial specification with a weighted Poisson model using the same analytic sample and predictors. [12]

**Dependencies**

5.2.

**Inputs**

Model-ready table; same predictor formula, weights, uncertainty approach, and analytic sample as the primary model, where methodologically valid.

**Implementation requirements**

1. Fit the Poisson comparison with the same outcome and predictor specification.
2. Report convergence, dispersion and comparable fit diagnostics; clearly note any diagnostic not comparable across models.
3. Do not select a model based only on significance or a single fit statistic.

**Deliverable**

Poisson model results and comparison summary in `scripts/07_fit_models.R` and `results/`.

**Verification requirements**

- Sample size, outcome, predictors, factor levels, and weight handling match the primary model where intended.
- Dispersion diagnostic is computed and interpreted against its stated definition; investigate overdispersion rather than claiming Poisson is adequate by execution success alone.
- Comparison notes any differences in estimator/uncertainty method.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git.

---

#### Unit 5.4 — Fit the unweighted joint-model sensitivity analysis

**Goal**

Assess how estimates differ in the unweighted joint model without choosing results based on smaller p-values. [12]

**Dependencies**

5.2.

**Inputs**

Same model-ready records and predictor specification; weights omitted by design for this sensitivity fit.

**Implementation requirements**

1. Fit the same negative-binomial joint model without sampling weights.
2. Keep the same outcome, sample, transformations, adjustment factors, and label handling as the weighted model to isolate weighting as the difference.
3. Compare estimates and uncertainty descriptively; do not treat either model as preferred solely because it is more statistically significant.

**Deliverable**

Unweighted model and aggregate side-by-side comparison in `results/`.

**Verification requirements**

- Formula and analytic sample align with the weighted primary fit; differences are explained if the estimator imposes distinct requirements.
- Output is explicitly labeled unweighted sensitivity analysis.
- No code silently changes sample, categories, or predictor form.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git.

---

#### Unit 5.5 — Check model fit, stability, and influential works

**Goal**

Evaluate whether model outputs are credible and identify influential observations without automatically dropping valid works. [12]

**Dependencies**

5.2–5.4.

**Inputs**

Fitted models and model-ready data; permitted diagnostics from the chosen estimator.

**Implementation requirements**

1. Check convergence, dispersion, residual patterns, zero counts, and observed-versus-predicted citation counts across year and field.
2. Assess influence and coefficient stability, particularly for collaboration counts; investigate highly influential works locally.
3. Record whether any influential records are data errors or valid extremes; do not remove a valid work without an approved sensitivity decision.
4. Do not create a train/test split; the objective is association estimation, not prediction. [7]

**Deliverable**

`scripts/08_model_checks.R`, aggregate diagnostics, and a concise diagnostic note.

**Verification requirements**

- Diagnostics correspond to the fitted model and its sample; the code does not substitute predictive validation for the planned association analysis.
- Observed and predicted aggregate counts are compared by year and field.
- Every flagged issue has a documented disposition; no valid record is automatically deleted.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git

---

#### Unit 5.6 — Run approved exclusion and missingness sensitivities

**Goal**

Assess whether material sample exclusions or missingness decisions change the estimated associations. [5][12]

**Dependencies**

5.5.

**Inputs**

Primary model; exclusion log; publication-type/retraction audit; missingness profile; approved sensitivity decisions.

**Implementation requirements**

1. Where audit indicates material relevance and approval is obtained, refit under clearly specified alternative exclusions (for example, publication type/retraction status if those fields exist).
2. If complete-case exclusions materially change sample composition, run the approved sensitivity comparison.
3. Change one decision dimension at a time where feasible and report sample sizes and composition alongside estimates.
4. Do not add unplanned exclusions or select sensitivities after seeing which gives preferred results.

**Deliverable**

Sensitivity specifications, aggregate estimates, and sample comparison in `scripts/08_model_checks.R` and `results/`.

**Verification requirements**

- Each sensitivity matches its approved rule and differs from the primary analysis only in the documented feature(s).
- Sample size and exclusion reasons reconcile to the audit.
- A no-sensitivity-needed decision is documented if the audit finds no material concern; do not invent a sensitivity result.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git

---

#### Unit 5.7 — Export model estimates and aggregate predictions

**Goal**

Create clear, shareable aggregate model tables and, where useful, adjusted predicted citation counts, without exposing work-level data.

**Dependencies**

5.5, 5.6.

**Inputs**

Verified model objects, uncertainty estimates, approved sensitivity fits, and model diagnostics.

**Implementation requirements**

1. Export coefficient estimates and confidence intervals; include exponentiated incidence-rate ratios when appropriate and label them clearly.
2. Include model type, weight/uncertainty method, analytic sample size, reference categories, and uncertainty scale in table notes.
3. Produce adjusted predicted counts only for prespecified, interpretable summaries supported by the model; identify the averaging/weighting basis.
4. Ensure tables/figures are aggregate, contain no work IDs or raw abstracts, and do not overstate causality.

**Deliverable**

`scripts/09_export_results.R`, model tables, and selected aggregate figures under `results/`.

**Verification requirements**

- Table values match the fitted model output within rounding tolerance.
- Confidence intervals are on the same scale as their displayed estimates; exponentiation is applied consistently.
- Sample size, model label, weights, and reference categories agree with the model and decision record.
- Check exports manually for record-level content before committing.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git

### Stage 6 — Documentation, integration, and final verification

**Stage objective:** Produce a repository that another researcher can understand and rerun from documented inputs, with decisions and limitations transparent.

#### Unit 6.1 — Complete variable notes and reproducibility instructions

**Goal**

Finalize the variable documentation and explain how to reproduce the analysis without sharing raw records. [7]

**Dependencies**

2.2, 5.7.

**Inputs**

Source inventory, verified data dictionary, decision log, scripts, package/environment record, aggregate outputs.

**Implementation requirements**

1. Complete `docs/data_dictionary.md` with source/derived field distinctions, units, missingness, label handling, transformations, and known limitations.
2. Update `README.md` with prerequisites, data acquisition, local file placement, execution order, output descriptions, package/environment instructions, and data/Git restrictions.
3. Record unresolved issues explicitly; do not describe provisional decisions as settled.

**Deliverable**

Updated `README.md` and `docs/data_dictionary.md`.

**Verification requirements**

- Instructions match actual filenames, scripts, and outputs.
- A reader can follow the documented sequence without access to raw data from Git.
- All model variables and exclusions in the report can be traced to the data dictionary/decision record.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git

---

#### Unit 6.2 — Write the concise methods, results, and limitations report

**Goal**

Communicate the analysis as a bounded, observational study and distinguish established findings from limitations and provisional decisions. [8][6]

**Dependencies**

5.7, 6.1.

**Inputs**

Approved study design, verified decisions, aggregate tables/figures, diagnostics, and sensitivity results.

**Implementation requirements**

1. Summarize source, target frame, sample, variable construction, weights, model specification, uncertainty method, and analysis-specific sample sizes.
2. Present estimates and uncertainty, weighted/unweighted and Poisson comparisons, and diagnostics/sensitivities as applicable.
3. State limitations: citations are not research quality; metadata and labels may be incomplete/snapshot-specific; readability is a rough proxy; observational associations are not causal; target population is limited to verified weight frame.
4. Do not generalize to all research worldwide or report unsupported ethics claims.

**Deliverable**

`results/report.md` with embedded or linked aggregate tables/figures.

**Verification requirements**

- Every reported numerical result matches a committed aggregate output.
- Methods match the final scripts and approved decisions; all limitations and population bounds are represented.
- Report contains no work-level record, abstract, or unapproved causal claim.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git

---

#### Unit 6.3 — Run the complete analysis from a clean session

**Goal**

Verify that the documented sequence regenerates all expected outputs without relying on hidden objects or manual steps.

**Dependencies**

1.1–6.2.

**Inputs**

Local raw data obtained as documented; completed scripts; recorded R/package environment; README instructions.

**Implementation requirements**

1. Restart R and run the scripts in their documented order, from setup/source inventory through result export.
2. Ensure scripts use explicit inputs/outputs and do not depend on objects created manually in a prior session.
3. Regenerate aggregate outputs without modifying source files or exposing raw data.
4. Record any required manual decision or unavoidable source-acquisition step in the README.

**Deliverable**

Verified end-to-end execution record and regenerated `results/` outputs.

**Verification requirements**

- All scripts finish in documented order with no unexpected errors.
- Key aggregate outputs (sample counts, model sample sizes, and estimates) agree with previously verified results, allowing only documented changes.
- A clean-session run does not require undeclared files, packages, or manually created objects.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git

---

#### Unit 6.4 — Review repository contents and commit the final deliverable

**Goal**

Ensure the public repository contains only intended reproducible materials and permitted aggregate outputs.

**Dependencies**

6.3.

**Inputs**

Git working tree, `.gitignore`, source terms, project outputs, ethics/data-governance note.

**Implementation requirements**

1. Review tracked files for raw data, abstracts, work IDs, local-only paths, credentials, and excessive disclosure.
2. Confirm README, study design, implementation plan, scripts, data instructions, environment record, variable notes, aggregate outputs, and report are present.
3. Confirm source terms permit each shared output; remove or suppress any output not suitable for sharing.
4. Commit final verified changes; do not mark any unit complete until the researcher confirms it.

**Deliverable**

Final Git-reviewed reproducible repository.

**Verification requirements**

- Git’s tracked-file list contains no raw/work-level dataset or abstract text.
- Every expected deliverable is present; no prohibited file is tracked.
- Final commit history corresponds to reviewed units and approved plan revisions.

**Completion criteria**

- [ ] Implementation code has been reviewed and understood.
- [ ] Code runs locally without unexpected errors.
- [ ] Verification checks have been executed and passed.
- [ ] Outputs have been inspected for plausibility.
- [ ] Changes have been reviewed and committed to Git

## 5. Integration and final verification

**End-to-end execution**

Obtain release 1.0.0 according to the official source instructions; place original files in Git-ignored `data/raw/`; start a clean R session; run `scripts/00_setup.R` through `scripts/09_export_results.R` in documented order. Any necessary manual approval/decision gate (ethics status, weight validity and uncertainty method, sparse-label handling, short-text rule, and predictor form) must be recorded before dependent modeling steps run.

**Expected outputs**

- Source inventory and aggregate audit summaries.
- Work-level processed table stored locally only.
- Aggregate sample flow, year–field coverage, missingness, citation and predictor summaries, and design-label summaries.
- Primary weighted negative-binomial model, weighted Poisson comparison, unweighted joint-model sensitivity results, diagnostics, and approved additional sensitivity analyses.
- Aggregate model tables/figures and concise report.
- README, data acquisition instructions, data dictionary, ethics/data-governance note, decision record, and R/package environment information.

**Integration checks**

- Stable work IDs and one row per work after preparation/joins.
- Counts by year–primary-field cell, weight values/totals, and exclusions reconcile with source documentation.
- Feature and label derivations follow documented source rules; abstract reconstruction and text counts have local validation evidence.
- Analysis-specific sample sizes reconcile across descriptive and model outputs.
- Weighted/Poisson/unweighted comparisons use the stated specifications; estimates in the report match exported tables.

**Reproducibility checks**

- Run the documented sequence from a fresh R session using recorded R/package versions.
- Obtain source files using README instructions; do not rely on undocumented local paths or manually created objects.
- Confirm raw and work-level files remain outside Git; confirm permitted aggregate outputs regenerate.

**Final completion criteria**

- [ ] All required implementation units are completed.
- [ ] The full analysis runs successfully in the documented order.
- [ ] Expected outputs are generated and verified.
- [ ] Results are consistent with the approved study design.
- [ ] Required software and dependencies are documented.
- [ ] The repository contains sufficient instructions to reproduce the analysis.
- [ ] Final changes are committed to Git.

## 6. Open issues and plan revisions

### Open decisions to resolve during implementation

1. **Data access and schema:** Exact filenames, table relationships, field names, release documentation, and the definitions/snapshot dates for citation and OA variables are to be confirmed from the actual release. [4][6]
2. **Weights:** Target frame, weight scale/totals, validity after exclusions, and design-appropriate uncertainty estimation for the selected model require documentation and approval. The weighted primary analysis is provisional until resolved. [9][11]
3. **Ethics/data protection:** Obtain and document official institutional determination before claiming exemption or proceeding contrary to institutional guidance. [2]
4. **Data handling choices:** Short-text suitability rule, word-count convention, rare-label handling, and missingness/sensitivity thresholds require transparent decisions before model fitting. [5][6]
5. **Model form:** Select transformations/flexible terms for count and text predictors after distribution/relationship checks; assess overlap among collaboration counts. [11]
6. **Audit findings:** Determine whether publication-type/retraction differences, duplicates, invalid records, or changed year–field cells warrant an approved sensitivity analysis. [9][12]

These are implementation decision points stated in the approved design; they do not prevent generating this plan. No substantive research decision is silently made here.

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

**Plan status:** Draft — awaiting researcher approval  
**Version or date:** 1.0 / 2026-10-21
