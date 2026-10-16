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
- PhD in NLP, MSc in Statistics, BAs in psychology and social sciences

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

---
# A Codex example

<!-- Show how writing research code with AI can quickly blow up and become unmanageable. -->

---
# Challenges of AI-assisted coding

- Lack of understanding of the generated code
- Losing control over the research process
- Difficulty in debugging and troubleshooting
- Over-reliance on AI-generated code

---

# Your role as researcher

- Own the question, data meanings and exclusions.

- Understand the change well enough to explain it.

- Choose evidence that could reveal an error.

- AI output is a proposal to inspect.

- Adjust your expectations: AI should not replace your expertise.

---
# Workshop goals

You will learn:

- Plan before code · review presented choices

- Divide work into small, testable units

- Transfer, check, inspect the diff, commit

- Resume from updated project

---
# Workshop toolkit

**UU AI Chat:** discuss, plan, propose code, debug
- The chat cannot directly read or edit your local project.

**Local editor + Python:** save files, execute, inspect outputs

**Git:** inspect changes and save checkpoints

<!-- Some R/Python familiarity is enough; no prior AI coding or Git expertise required. -->

---
# Workshop research project

**SoDa Open Research Teaching Datasets (SORTD)**: https://zenodo.org/records/23419332

- 11,700 works · 2011–2025 · 26 primary fields

- 30 works per year × field; English articles with abstracts

- Use actual `is_oa`, `cited_by_count`, `publication_year`.

---
# Example research questions
- What factors are associated with open access (OA) publication?
- What factors are associated with citation counts?
- What factors are associated with retraction?

--- 
# Proposed AI-assisted research coding workflow
1. Begin with a reviewed plan
2. Make the units verifiable
3. Implement and transfer one change deliberately
4. Verification is more than “it ran”
5. Review the actual change
6. Rinse and repeat 2-5

---
# Research question of choice
What factors are associated with citation counts?

---

# 1. Begin with a reviewed plan

- Research question → available variables → analytical choices

- Inputs → outputs → small implementation units
    - “Do not write code yet. Identify missing information.”

- Revise the plan before delegating implementation.

<!-- I will demonstrate this with a live example. -->

---

# 2. Make the units manageable and verifiable

Example units: 

- **Unit 1:** Read the works.csv → validate column names and types, number of rows, missingness and duplicates

- **Unit 2:** Read the abstracts.csv → [same as above]

- **Unit 3:** Join the works and abstracts → check that the number of rows is correct, check for missing abstracts, and all works have abstracts

Each remains manageable and verifiable.

<!-- I will demonstrate this with a live example. -->
---

# 3. Implement and transfer one change deliberately

- Supply exact current folder structure, the data and the reviewed plan.

- Ask for one unit of work.

- Read/understand → copy → save → run locally.

Optional later: a unified patch against exact contents.

<!-- I will demonstrate this with a live example. -->
---

# 4. Verification is more than “it ran”

Verification the unit of work, which can involve:

- Checking the output against expected results.
- Ensuring the code behaves as intended under various scenarios.
- Confirming that the implementation meets the specified requirements.

<!-- I will demonstrate this with a live example. -->

---

# 5. Review the actual change

- `git status` → `git diff`

- Open new files: untracked files do not appear in the diff.

- Stage named files → `git diff --cached`

- Passing checks + review → `git commit -m "message"`

<!-- I will demonstrate this with a live example. -->

---

# 6. Rinse and repeat 2-5

- Upload the verified change to the chat.
- Ask for the next unit of work.
- Repeat the process: implement, verify, review, commit.

Optional tip: for larger changes, ask for a patch against the exact current state of the project. Use `git apply` to apply the patch, then verify and commit.

<!-- I will demonstrate this with a live example. -->

---
# Exercise
Research question: What factors are associated with retraction?

---

# Exercise 1 · Make and review a plan

**15 min · exercises/01-plan.md**

1. Inspect locally; provide research context, folder structure and data into UU AI Chat.

2. Ask for a plan without code; revise a weak choice.

3. Make sure each unit is verifiable and manageable.

**Finish**: three units, inputs, outputs, independent checks.

---

# Exercise 2 · Implement one unit

**15 min · exercises/02-implement.md**

1. Ask for the first unit of work. 

2. Read/understand → copy → save → run locally.

**Finish**: local run attempted.

---

# Exercise 3 · Break, debug, commit

**15 min · exercises/03-verify.md**

1. Test and verify the first unit of work.
2. Review the actual change with `git diff` and `git status`.
3. Stage and commit the verified change.

**Finish**: unit verified and committed.

---

# Exercise 4 · Extend in small steps

**15 min · exercises/04-extend.md**

1. Ask for the next unit of work.
2. Test and verify the next unit of work.
3. Review the actual change with `git diff` and `git status`.
4. Stage and commit the verified change.

**Finish**: next unit verified and committed.

---

# Exercise 5 · Revise plan

**105–115 min · exercises/05-revise.md**

1. After a few units, ask for a plan revision to accommodate new insights.
2. Review new plan and units and commit any verified changes.
3. Ask for the next unit of work.

**Finish**: plan revised and next unit started.

---

# Take home: the verified change

**Plan → review → one unit → transfer → check → diff → commit**

Update project, then repeat.

<br>

*What caught an error today?*
*How do you like this AI-assisted coding approach?*