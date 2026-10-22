# Exercises

Practise the workflow: `design → plan → implement one unit → verify → commit`.

## Before you start

Install the tools you need using the links below, then create your local repository before Exercise 1.

- Install [Python](https://www.python.org/downloads/) **or** [R](https://cran.r-project.org/).
- Choose an editor: [VS Code](https://code.visualstudio.com/download) or [RStudio](https://docs.posit.co/ide/user/download.html) (requires R).
- Install [Git](https://git-scm.com/downloads/). Optionally use [GitHub Desktop](https://desktop.github.com/) to review changes and commit without terminal commands.
- A [GitHub account](https://github.com/signup) is optional for saving your repository online; local commits do not require one.
- Sign in to [UU AI Chat](https://aichat.uu.nl/).
- Have your data documentation ready. Only upload material you are allowed to share with the AI tool.

## Teaching dataset and research questions

Use the [SoDa Open Research Teaching Datasets (SORTD)](https://zenodo.org/records/23419332). Download the teaching dataset and read its accompanying documentation; keep the data locally in your analysis project.

Choose one question: What factors are associated with

- *citation counts?*
- *open access (OA) publication?*
- *retraction?*

You can also use your own research question and data.

## Work through these in order

| Exercise | Suggested time |
|---|---|
| [1. Create and review a study design](#exercise-1--create-and-review-a-study-design) | 15 min |
| [2. Create and review an implementation plan](#exercise-2--create-and-review-an-implementation-plan) | 15 min |
| [3. Implement one unit](#exercise-3--implement-one-unit) | 15 min |
| [4. Verify the unit change](#exercise-4--verify-the-unit-change) | 15 min |
| [5. Review and commit the unit change](#exercise-5--review-and-commit-the-unit-change) | 10 min |

Use three chats in the same UU AI Chat project: **design**, **planning**, and **implementation/verification**. You transfer files and run code locally. The times are a guide; allow more time when needed.

For a quicker start, review and adopt the [example design and plan](../examples/README.md), save and commit local copies, and continue with Exercise 3 using R. The aim is to practise the workflow, not finish the full analysis.


## Preparation: Create your local Git repository

Choose one option:

- **GitHub Desktop:** select **File → New repository**, name it `my-research-project` (or any other name you prefer), choose where to save it, tick **Initialize this repository with a README**, and select **Create repository**.
- **Terminal:** run these commands in the folder where you want to keep your project:

  ```sh
  mkdir my-research-project
  cd my-research-project
  git init
  ```

Open this project folder in your editor. Save your study design, implementation plan, and code here throughout the exercises. Git records file versions when you commit them; creating the repository alone does not save a version. You do not need to publish it to GitHub.

## Exercise 1 — Create and review a study design

**Workshop time: 15 minutes to get started.** Creating and reviewing a study design can take considerably longer. Start with one question above and your data documentation.

**Short on time?** Review the [example study design](../examples/study_design.md), save it in your local repository as `study_design.md`, and commit it. Then continue to Exercise 2.

1. Create a project in [UU AI Chat](https://aichat.uu.nl/) and start Chat 1.
2. Attach the [study-design template](../templates/study_design_template.md), paste the [study-design prompt](../prompts/study_design_prompt.md), and describe your research idea.
3. Answer the questions. Review the proposed choices and ask for revisions where needed. Keep uncertain decisions labelled as provisional.
4. Approve the design when ready. Save it locally as `study_design.md`, review the saved file, and commit it.

**Finish:** a reviewed study design saved and committed. Keep implementation code out of this document.

## Exercise 2 — Create and review an implementation plan

**Workshop time: 15 minutes to get started.** Creating and reviewing an implementation plan may also take longer. Use your saved study design.

**Short on time?** Review the [example implementation plan](../examples/implementation_plan.md) together with its [matching study design](../examples/study_design.md). Save and commit both in your local repository, then continue to Exercise 3 using R. Keep the design and plan consistent.

1. Start Chat 2 in the same project. Attach `study_design.md` and the [implementation-plan template](../templates/implementation_plan_template.md), then paste the [planning prompt](../prompts/implementation_plan_prompt.md). State whether you will use Python or R.
2. Check that the plan follows the design. Review the first three units closely: does each have one small goal, clear inputs, a deliverable, and checks you can understand?
3. Ask to split any unit that feels too large. Review and approve the plan, save it locally as `implementation_plan.md`, and commit it.

**Finish:** a reviewed plan saved and committed, with manageable, verifiable units. Keep implementation code out of this document too.

## Exercise 3 — Implement one unit

**Suggested time: 15 minutes.** Use your saved design and plan.

1. Start Chat 3 in the same project. Attach both documents and paste the [unit-implementation prompt](../prompts/unit_implementation_prompt.md). Provide your current folder structure and any relevant existing code.
2. Ask: **“Implement Unit 1.1 only.”** Use the first unit number in your plan if different.
3. Read the response. Ask about anything you do not understand before copying it.
4. Save the suggested code or files locally and run any code using the supplied instructions. Inspect the result.

If the unit only creates folders or documents, inspect those deliverables instead of expecting executable code. Request verification separately in Exercise 4.

**Finish:** the first unit is saved locally and a run or inspection has been attempted. Keep any error messages for debugging.

## Exercise 4 — Verify the unit change

**Suggested time: 15 minutes.** Continue in Chat 3.

1. Ask: **“Provide independent verification checks for Unit 1.1 against its requirements.”** Use your actual unit number.
2. Read and run the checks locally. Compare outputs with the requirements; a successful run alone does not establish correctness.
3. If something fails, share the error, expected behaviour, and relevant code. Ask: **“Explain the cause and suggest the smallest fix for this unit.”** Apply a fix you understand, then rerun the unit and its checks.
4. Report which checks passed. Resolve any unexplained failures before continuing.

**Finish:** the unit passes its checks and you have inspected the outputs. Save any verification code used.

## Exercise 5 — Review and commit the unit change

**Suggested time: 10 minutes.** Review the verified work locally.

1. Inspect the changed files in your editor or GitHub Desktop, or use `git diff` and `git status`.
2. Confirm the changes match the requested unit and include no unrelated edits or data that should remain local.
3. Stage only the intended implementation and verification files. Commit with a short message describing the change.
4. Tell Chat 3 the unit is verified and committed before requesting another unit.

**Finish:** one understandable, verified unit change is committed to Git. Publishing to GitHub is optional.

## Optional / advanced exercises

Continue if time allows: [extend in small steps](#optional-a--extend-in-small-steps) or [revise the plan](#optional-b--revise-the-plan).

## Optional A — Extend in small steps

**Suggested time: 15 minutes.** Continue in Chat 3 with the next unit.

1. Ask: **“Implement Unit 1.2 only.”** Use the next unit number from your plan and provide current code when needed.
2. Read, save, and run the changes locally.
3. Separately request verification against that unit’s requirements. Run the checks and inspect the outputs.
4. Resolve any failures, review the changed files, and commit the verified work.

If the task is too large, ask to split it before continuing. If it changes an approved research decision, pause and revise the relevant documents first.

**Finish:** another small unit is verified and committed. Repeat this cycle at your own pace.

## Optional B — Revise the plan

**Suggested time: 10 minutes.** Choose a finding from your local work that affects the plan. If none has arisen, practise by proposing to split an oversized future unit.

1. In Chat 3, describe the finding and ask: **“Explain which units or study-design decisions this affects. Propose changes to those sections only; wait for my approval.”**
2. Review the proposal. Check whether completed work needs to be checked again and whether future dependencies still make sense.
3. Approve the changes you accept. Request replacement text only for the affected sections and update the local documents.
4. Review the differences and commit the revision. Provide the updated documents to the chat and identify the next unit. Recheck affected completed work before continuing.

Keep unrelated wording, formatting, and unit numbers unchanged wherever possible. Methodological changes also need to be reflected in `study_design.md`.

**Finish:** a focused revision is saved and committed, and you know what to do next.
