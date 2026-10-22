The Markdown artifact service failed to authenticate, so I can’t attach a separate file. Here is the complete document in Markdown:

# Study Design: Factors Associated with OpenAlex Citation Counts

**Project:** SODA Open Research Teaching Data analysis  
**Document status:** Study design decisions consolidated; operational details requiring source-data or institutional verification are listed as pending.  
**Design type:** Observational, quantitative secondary-data analysis.

## 1. Study summary

This study will examine how OpenAlex citation counts are associated with open-access status, collaboration, recorded study-design labels, and title and abstract characteristics. Publication year and primary field will be included as categorical adjustment factors. The analysis is observational and will estimate associations, not causal effects.

The dataset contains 11,700 English-language works published from 2011 to 2025 [K6]. The sampling design is balanced across publication-year and primary-field groups [K2]. The intended target is the source population represented by the documented sampling weights, once those weights and their target frame have been verified. Results will not be generalized to all research worldwide [K3].

## 2. Research question

> Among works in SODA Open Research Teaching Data release 1.0.0, how are OpenAlex citation counts associated with open-access status, collaboration counts, recorded study-design labels, title and abstract length, and abstract readability, after accounting for publication year and primary field?

Subfield will **not** be a predictor. Primary field is an adjustment factor only; therefore, the study will not estimate subfield-specific citation differences. This avoids attempting to estimate nested subfield and primary-field fixed effects as separate effects in an ordinary categorical model.

## 3. Objectives

1. Describe the analytic sample, variable coverage, missingness, and citation-count distribution using weighted and unweighted summaries.
2. Estimate adjusted associations between citation counts and the selected predictors in one joint model.
3. Assess how conclusions change under a Poisson comparison model and an unweighted sensitivity model.
4. Document data quality, sampling-weight interpretation, model limitations, and reproducible analysis steps.

## 4. Study population, sampling, and unit of analysis

### 4.1 Source and target population

The source dataset is SODA Open Research Teaching Data [K1]. The target population is the source population represented by the dataset’s documented sampling weights, conditional on verifying what those weights encode. The target is not all scholarly research globally [K3].

### 4.2 Sampling structure

The dataset contains 11,700 English-language works published from 2011 through 2025 [K6]. It is balanced across year–primary-field groups [K2], so the sample composition should not be treated as the natural composition of the wider source population. The primary analysis will use the available sampling weights. Weight definitions, target totals, and appropriate variance estimation must be checked against the source documentation before interpreting weighted estimates.

### 4.3 Eligibility and exclusions

Retain all records in the supplied sample. Exclude only verified duplicate records or records shown to be invalid for analysis, recording each exclusion and reason. Audit publication types and retraction status. If these characteristics are present and materially affect the sample, report sensitivity analyses rather than silently narrowing the primary sample. Recheck year–field cell counts and weights after any exclusions.

### 4.4 Unit of analysis

The unit is one scholarly work. The analysis table will contain one row per work, keyed by a stable work identifier. Relational tables will be aggregated to the work level before joining to prevent many-to-many joins from duplicating works.

## 5. Variables and operational definitions

| Role | Variable | Operationalization and notes |
|---|---|---|
| Outcome | `cited_by_count` | OpenAlex citation count as represented in the dataset. Record the dataset/version and citation-count snapshot or retrieval date if available. |
| Predictor | `is_oa` | Binary open-access status as supplied or derived according to the dataset documentation. Verify the precise definition and reference category. |
| Predictor | Author count | Number of authors associated with the work. Audit any truncation or cap flags; interpret flagged counts cautiously. |
| Predictor | Institution count | Number of institutions associated with the work. Verify aggregation and deduplication rules. |
| Predictor | Country count | Number of countries associated with the work. Verify aggregation and deduplication rules. |
| Predictor | Study-design labels | Separate binary indicators for sufficiently common recorded labels. Treat labels as metadata classifications, not verified descriptions of the work’s actual design. Keep “no label recorded” distinct from a confirmed absence of a design. Handle rare labels transparently after inspecting counts. |
| Predictor | Title length | Word count derived from the title, stored separately from abstract length. |
| Predictor | Abstract length | Word count derived from the reconstructed abstract. |
| Predictor | Abstract readability | Flesch–Kincaid Grade Level, used as a rough proxy for readability. Apply short-text checks and flag scores based on very short or unsuitable text. |
| Adjustment | Publication year | Categorical factor, with a year-specific baseline rather than a single linear trend. |
| Adjustment | Primary field | Categorical factor. Used for adjustment, not as a topic effect. |
| Excluded from predictor set | Subfield | Not included as a predictor in the primary model. |

The planned predictors follow the project variable specification [K8]. The score for abstract readability is a proxy, not a direct measure of scientific complexity or comprehensibility.

## 6. Data preparation and missingness

1. Preserve the supplied source files unchanged and document their version and provenance.
2. Create a one-row-per-work analysis table. Check uniqueness before and after joins; aggregate author, institution, country, and label records before joining.
3. Reconstruct abstracts using the source’s documented representation. Validate a sample of reconstructions against the original representation.
4. Derive title and abstract word counts separately. Calculate Flesch–Kincaid Grade Level only where the text is suitable for the measure; flag short-text cases and document the rule before fitting outcome models.
5. Profile missingness by variable and relevant strata before exclusions. Do not automatically remove a work because any one predictor is missing. Use the records available for each analysis, document complete-case counts, and run sensitivity checks if exclusions materially affect results.
6. Distinguish an absent study-design label from missing or unavailable metadata wherever the source permits. Do not interpret “no label recorded” as proof that a design feature is absent.
7. Verify the meaning, scale, and coverage of the sampling weights. If exclusions alter the sampling cells, verify whether weights remain appropriate or require recalculation.

## 7. Descriptive analysis

Before fitting models, summarize:

- Sample counts overall and by publication year and primary field.
- Weighted and unweighted distributions of citation counts, including the proportion of zero counts and the degree of skew.
- Citation-count summaries by open-access status, year, and primary field.
- Distributions and missingness for collaboration counts, title and abstract lengths, and readability scores.
- Study-design label frequencies, co-occurrence, and the number of works with no label recorded.
- The association and overlap among the collaboration measures and other continuous predictors.

Use raw citation-count summaries and plots, with a log-scale display where useful for visualization. Do not transform the outcome merely to make the distribution look symmetric before choosing the count model.

## 8. Statistical analysis

### 8.1 Primary model

The primary analysis will be a **weighted negative-binomial count regression**, provisionally, with a log link. The outcome is `cited_by_count`. Include all selected substantive predictors jointly, along with categorical publication-year and primary-field adjustment factors. The planned specification has main effects only; no complete set of year-by-field interactions or other interactions will be included by default.

Conceptually, the model includes:

- `is_oa`;
- author, institution, and country counts;
- indicators for sufficiently common recorded study-design labels, with the no-label group represented distinctly;
- title word count;
- abstract word count;
- abstract Flesch–Kincaid Grade Level; and
- categorical publication year and primary field.

Interpret coefficients as adjusted associations conditional on the other included variables. For a log-link count model, exponentiated coefficients can be presented as incidence-rate ratios, alongside confidence intervals and, where useful, adjusted predicted citation counts. These are associational summaries, not causal effects.

The functional form for continuous predictors will be finalized after distribution and relationship checks. In particular, inspect whether collaboration counts and text features have plausible approximately linear relationships on the model’s link scale; document any transformations or flexible terms chosen before interpreting results. Check for collinearity and coefficient stability, especially among the three collaboration counts.

### 8.2 Weights and uncertainty

Use the documented sampling weights in the primary model. Before final reporting, verify that the estimation and uncertainty procedure is appropriate for the actual sampling design and available weight information. Do not assume that a generic weighted fit automatically produces design-correct standard errors. If the exact design-based procedure cannot be implemented for the selected model, document the limitation and use an appropriate, transparently described alternative.

### 8.3 Model comparison and sensitivity analyses

- Fit a weighted Poisson comparison model and compare fit and dispersion diagnostics with the negative-binomial model.
- Fit an unweighted version of the joint model as a sensitivity analysis. Do not choose between weighted and unweighted results based on which produces smaller p-values.
- Reassess results if exclusions for invalid records, publication type, or retraction status materially change the analytic sample.
- Report how missingness and complete-case exclusions affect the number and composition of works contributing to each model.

### 8.4 Model evaluation and reporting

Check convergence, model fit, dispersion, zero counts, residual patterns, influential observations, and observed-versus-predicted citation counts across year and field. Investigate highly influential works without automatically deleting valid observations. A train/test split is not planned because the purpose is association estimation, not prediction.

Emphasize estimate size and uncertainty rather than treating statistical significance as the sole basis for interpretation. Because multiple predictors and label indicators are examined, describe the analysis as exploratory unless a separate confirmatory plan is established.

## 9. Quality assurance and reproducibility

Before interpreting results, verify:

- Stable work identifiers and one row per work after all joins.
- Expected counts by year–field sampling cell and consistency with the dataset’s documented sample structure [K2].
- Weight values, missing weights, and weight totals against source documentation.
- Citation counts are non-negative and plausible, and the outcome’s snapshot is recorded.
- Author, institution, and country counts follow documented aggregation rules, including any truncation flags.
- Reconstructed abstracts and derived word counts on a checked subset.
- Study-design label frequencies, multi-label handling, and the no-label category.
- The final analytic sample size at each analysis step, with exclusions and reasons recorded.

Use version-controlled R scripts and documentation; record R and package versions, preferably with a lockfile. The repository should include a README, instructions for obtaining the source data, data-preparation and analysis code, codebook or variable notes, and aggregate tables and figures. Do not commit the raw work-level dataset or abstract text. This matches the project’s reproducibility and data-sharing plan [K4].

## 10. Ethics and data governance

The study uses secondary bibliographic and citation data and does not involve direct contact or intervention. However, public availability alone does not determine whether institutional review or a data-protection assessment is required. The official institutional determination is **pending**; confirm it with the supervisor or appropriate institutional office before proceeding and record the outcome and source. The project must not claim an exemption without that determination [K5].

Do not send dataset contents, work-level records, or abstracts to AI tools. Keep the source data outside the public repository; share code, documentation, and aggregate outputs only, subject to checking the source terms.

## 11. Limitations

- The target population is limited to the source frame represented by verified weights, not all research worldwide [K3].
- Citation counts are an imperfect indicator of scholarly attention and are not a direct measure of research quality.
- Although publication year is adjusted categorically, citation counts remain affected by citation opportunity, database coverage, and citation practices.
- Open-access status and other metadata may reflect the dataset’s recorded snapshot rather than the status at publication or throughout the citation period; verify the source definitions.
- Study-design labels may be incomplete, inconsistently assigned, or absent; they describe recorded metadata rather than confirmed designs.
- Flesch–Kincaid Grade Level is a rough proxy and may behave poorly for short abstracts, technical language, or text with unusual formatting.
- Missing values, abstract reconstruction, authorship truncation, and possible record-type or retraction differences may affect estimates.
- The observational design does not identify causal effects; residual confounding and selection remain possible.

## 12. Deliverable

A reproducible R repository containing:

- A project README and data-source instructions.
- Scripts for validation, cleaning, feature construction, descriptive analysis, and modeling.
- Package and environment information.
- Aggregate sample, coverage, and descriptive outputs.
- Model tables and figures.
- A concise report documenting methods, results, limitations, and decisions.

Raw work-level data and abstract text will not be included in the repository.

## 13. Items to verify before analysis

1. **Sampling weights:** What population and totals they represent; whether weights are valid after any exclusions; and how the sampling design should inform standard errors.
2. **Ethics/data protection:** Obtain and record the official institutional determination [K5].
3. **Source definitions:** Confirm the definitions and snapshot dates for `cited_by_count` and `is_oa`, as well as the field, subfield, label, and truncation variables.
4. **Sample audit:** Inspect publication-type and retraction fields, duplicate/invalid records, and year–field cells after any exclusions.
5. **Text processing:** Set and document short-text handling for readability and any transformations of count and text-length predictors before fitting the primary model.
6. **Sparse labels and missingness:** Determine the transparent handling of rare study-design labels and report the resulting analysis-specific sample sizes.

The primary sample is to remain as supplied except for verified duplicates or invalid records; any additional exclusions or changes should be documented and accompanied by sensitivity analyses where relevant.