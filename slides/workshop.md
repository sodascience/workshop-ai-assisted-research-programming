---
marp: true
title: AI-assisted research programming
description: Utrecht University Programming Café
theme: default
paginate: true
size: 16:9
---

# AI-assisted research programming
**From a research question to verified changes**
*with UU AI Chat + local Python/R + Git*

<br>
<br>

Utrecht University Programming Café · Oct 22, 2026

---
# About me
- Qixiang [kis-jang] Fang
- Postdoc researcher, ODISSEI Social Data Science Team
    - Provide research support and training for social scientists
    - AI methodology research
- PhD in NLP
- MSc in Statistics
- BAs in behavioural and social sciences

---
# What is your experience with AI-assisted coding?

- Do you use AI for research code?
- For what tasks?
- How has it changed your research workflow?
- What do you like about it?
- Do you encounter any issues?

---
# Examples of AI-assisted coding in research

- Automating data cleaning and preprocessing
- Generating code snippets for statistical analysis
- Code documentation and commenting
- Debugging and error handling
- etc.

---
# A Codex example

<!-- Show how writing research code with AI can quickly blow up and become unmanageable. -->
<!-- Even with the planning mode, each change can be substantial. -->


---
# Challenges of AI-assisted coding

- Lack of understanding of the generated code
- Losing control over the research process
- Difficulty in debugging and troubleshooting
- Over-reliance on AI-generated code
- etc.

---

# Your role as researcher

Using AI or not:

- Own the research questions, data and decisions.
- Understand any change (e.g., code, analysis) well enough to explain it.
- Validate the results.
- Reproduce the study. 

---
# Your role as researcher
When using AI:

- AI does not replace your expertise. 
- Any AI output should be inspected and challenged.
- Adjust your expectations: *Maybe don't cram what in the past would be three-months of work into one day.*

---
# Workshop goals

You will learn:

- Plan and review plan before AI-assisted coding
- Divide work into small, testable units
- Transfer, check, inspect the diff, commit
- Resume from updated project state

<br>
**Disclaimer**: Personal experience and opinions; feedback welcome. 

---
# Workshop toolkit

**UU AI Chat:** discuss, plan, propose code, debug
- Note: The chat cannot directly read or edit your local project.

**Local editor + Python/R:** save files, execute, inspect outputs

**Git and GitHub desktop:** inspect changes and save checkpoints

<!-- Some R/Python familiarity is enough; no prior AI coding or Git expertise required. -->

---
# Workshop research project

**SoDa Open Research Teaching Datasets (SORTD)**: 
- https://zenodo.org/records/23419332

- 11,700 works · 2011–2025 · 26 primary fields

- 30 works per year × field; English articles with abstracts

- Includes: `works.csv`, `abstracts.csv`, `authors.csv`, `funding.csv`, `topics.csv` etc.

---
# Example research questions
What factors are associated with 
- citation counts?
- open access (OA) publication?
- retraction?

--- 
# Proposed AI-assisted research coding workflow
1. Begin with a carefully reviewed plan
2. Make the units manageable and verifiable
3. Implement and transfer one change deliberately
4. Verify!
5. Review the actual change
6. Rinse and repeat 2-5

---
# Research question of choice
What factors are associated with citation counts?

---

# 1. Begin with a reviewed plan

- Research question → available variables → analytical choices
- Inputs → outputs → small implementation units
    - “Do not write code yet. Identify missing information. Ask me for input.”
- Revise the plan before delegating implementation.

<!-- I will demonstrate this with a live example. -->

---

# 2. Make the units manageable and verifiable

Example units: 

- **Unit 1:** Read the `works.csv` → validate column names and types, number of rows, missingness and duplicates
- **Unit 2:** Read the `abstracts.csv` → [same as above]
- **Unit 3:** Join the works and abstracts → check that the number of rows is correct, check for missing abstracts, and all works have abstracts

Each remains manageable and verifiable.

<!-- I will demonstrate this with a live example. -->
---

# 3. Implement and transfer one change deliberately

- Supply exact current folder structure, the data and the reviewed plan.
- Ask for one unit of work.
- Read/understand → copy → save → run locally.

<!-- I will demonstrate this with a live example. -->
---

# 4. Verify!

Verification the unit of work, which can involve:

- Checking the output against expected results.
- Ensuring the code behaves as intended under various scenarios.
- Confirming that the implementation meets the specified requirements.

<!-- I will demonstrate this with a live example. -->

---

# 5. Review the actual change

- `git status` → `git diff`
- New/untracked files do not appear in the diff.
- Stage named files → `git diff --cached`
- Passing checks + review → `git commit -m "message"`

<!-- I will demonstrate this with a live example. -->

---

# 6. Rinse and repeat 2-5

- Upload the verified change to the chat.
- Ask for the next unit of work.
- Repeat the process: implement, verify, review, commit.

**Optional tip:** for larger changes, ask for a patch against the exact current state of the project. Use `git apply` to apply the patch, then verify and commit.

<!-- I will demonstrate this with a live example. -->

---
# Questions?

---
# Exercise · Example research questions
Example research questions: What factors are associated with 
- citation counts?
- open access (OA) publication?
- retraction?

---

# Exercise 1 · Create and review a study design

**15 min · [exercises/README.md](../exercises/README.md#exercise-1--create-and-review-a-study-design)**

1. Start Chat 1 with the study-design prompt and template.
2. Review the research decisions; keep open choices explicit.
3. Save and commit study_design.md.

**Finish**: reviewed study design saved and committed.

---

# Exercise 2 · Create and review an implementation plan

**15 min · [exercises/README.md](../exercises/README.md#exercise-2--create-and-review-an-implementation-plan)**

1. Start Chat 2 with the saved design, planning prompt and template.
2. Check the first three units: small goals, inputs, outputs and checks.
3. Save and commit implementation_plan.md.

**Finish**: reviewed implementation plan saved and committed.

---

# Exercise 3 · Implement one unit

**15 min · [exercises/README.md](../exercises/README.md#exercise-3--implement-one-unit)**

1. Start Chat 3 with both documents and the unit-implementation prompt.
2. Request the first unit only.
3. Read and understand → copy → save → run locally.

**Finish**: local run or inspection attempted.

---

# Exercise 4 · Verify the unit change

**15 min · [exercises/README.md](../exercises/README.md#exercise-4--verify-the-unit-change)**

1. Request independent checks against the unit requirements.
2. Run the checks locally and inspect the outputs.
3. Debug failures and rerun the checks.

**Finish**: unit verified; unexplained failures resolved.

---

# Exercise 5 · Review and commit the unit change

**10 min · [exercises/README.md](../exercises/README.md#exercise-5--review-and-commit-the-unit-change)**

1. Review changed files with GitHub Desktop or git diff and git status.
2. Stage only the intended files.
3. Commit the verified change and report completion to Chat 3.

**Finish**: unit change reviewed and committed.

---

# Optional A · Extend in small steps

**15 min · [exercises/README.md](../exercises/README.md#optional-a--extend-in-small-steps)**

1. Request the next unit whose dependencies are complete.
2. Implement, run and verify locally.
3. Review and commit the verified change.

**Finish**: another unit verified and committed.

---

# Optional B · Revise the plan

**10 min · [exercises/README.md](../exercises/README.md#optional-b--revise-the-plan)**

1. Describe a new finding or propose splitting a large unit.
2. Review changes to affected sections only.
3. Save and commit the revision; recheck affected work.

**Finish**: focused plan revision saved and committed.

---

# Take home: the verified change

**Plan → review → one unit → transfer → check → diff → commit**

Update project, then repeat.

<br>

>*What worked and what didn't?*
>*How do you like this AI-assisted coding approach?*