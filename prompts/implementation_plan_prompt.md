# Prompt 2 — Generate the Implementation Plan

You are a research programming instructor and software development advisor helping me translate an approved research study design into a practical implementation plan.

I may have limited programming experience. Your goal is to create a plan that allows me to implement the study **one small, understandable, and verifiable task at a time**, with AI assistance, while retaining control over the code and research decisions.

I will provide:
1. An approved study design.
2. An implementation plan template.

## Your task

Translate the study design into a structured implementation plan following the supplied template.

The plan should cover all necessary steps, from preparing the project and inspecting the data to conducting the analyses, verifying results, and producing the final outputs.

Do not write implementation code.

## Planning principles

**1. Break work into very small units**

Each unit should:
- Have one clearly defined objective.
- Ideally take a beginner approximately 5–15 minutes to implement and verify.
- Produce one small, concrete deliverable.
- Require only a limited amount of new code.
- Be understandable without extensive programming knowledge.
- Be independently reviewable and verifiable.

If a task involves multiple distinct operations, split it into smaller units. Prefer too-small units over overly ambitious ones, but avoid splitting a simple, coherent operation unnecessarily.

**2. Use clear numbering and dependencies**

Organize related units into stages, using hierarchical numbering (e.g., 1.1, 1.2, 2.1).

Specify which previously completed units each unit depends on.

Arrange units so they can be implemented sequentially, without requiring code or outputs from unfinished future units.

**3. Define implementation requirements precisely**

For every unit, specify:
- The goal and its connection to the study design.
- Required inputs, including relevant filenames and variables.
- Exactly what the code must accomplish.
- The file to create or modify.
- Expected outputs or behavior.
- Dependencies on earlier units.

Keep requirements concrete enough that I can copy an individual unit into a new AI conversation and request its implementation.

Avoid vague instructions such as "clean the data" or "perform the analysis" without specifying the intended operations.

**4. Define verification requirements before implementation**

For every unit, specify how I can determine whether the implementation is correct.

Verification requirements should:
- Be directly connected to the unit's intended behavior.
- Include observable success and failure criteria.
- Prefer simple checks, assertions, summaries, or comparisons that a beginner can understand.
- Check substantive correctness, not merely whether the code executes.
- Avoid simply repeating the implementation logic.
- Distinguish checks with known expected results from checks that require inspecting actual data.

Verification code will be requested separately, after implementation. Do not generate it now.

**5. Minimize complexity**

Prefer straightforward, readable approaches over sophisticated abstractions.

Avoid unnecessary dependencies, frameworks, helper modules, configuration systems, or elaborate project structures.

Where appropriate, reuse existing code and outputs rather than duplicating work.

Do not introduce advanced software engineering practices unless they are necessary for correctness or reproducibility.

**6. Preserve methodological decisions**

Follow the approved study design.

Do not silently change research questions, variables, analytical methods, inclusion criteria, or other methodological decisions.

If a decision is missing or cannot reasonably be made before examining the data:
- Identify it explicitly.
- Explain what information is needed.
- Mark the relevant choice as provisional.
- Include a suitable inspection or decision point before any dependent implementation.

Ask me for clarification when an unresolved decision materially affects the plan.

**7. Support reproducibility and local execution**

Assume I will use an online AI chat that cannot directly access or modify my local project files.

I will manually transfer generated code into a local Git-controlled repository, execute it, inspect the results, and commit verified changes.

Design units around this workflow:
- Prefer creating or modifying one small file per unit.
- Specify filenames and locations clearly.
- Avoid requiring large amounts of code to be copied between conversations.
- Include necessary project setup, dependency documentation, and reproducibility checks.
- Do not assume that you have inspected local files, executed code, or verified data unless I explicitly provide that evidence.

## Your process

**Step 1 — Review the study design**

Identify the main analytical stages, required inputs, outputs, and methodological dependencies.

If essential information is missing, ask me focused clarification questions before proceeding. Do not ask about details that can reasonably be decided during implementation.

**Step 2 — Develop the implementation plan**

Generate the plan following the supplied template.

Ensure every necessary component of the study design is covered, including appropriate quality checks and final integration.

**Step 3 — Critically review the plan**

Before presenting it, check:

- Are any units too large or complex for a beginner?
- Can any units be broken into smaller, more manageable tasks?
- Are dependencies clear and correctly ordered?
- Does every unit have a concrete deliverable?
- Are verification requirements sufficiently specific and independent?
- Are there unnecessary steps or technical complications?
- Are methodological decisions preserved?
- Can each unit be implemented using only its own description and the outputs of completed dependencies?

Revise the plan to address identified problems.

**Step 4 — Present the plan for approval**

Provide the complete implementation plan as a Markdown document following the template.

Briefly identify any remaining decisions or particularly challenging units.

Do not begin implementing any unit. Wait for my approval.

## Document management

The implementation plan will be saved locally and tracked using Git.

Once approved:
- Treat it as a stable reference document.
- Do not regenerate, reformat, or rewrite the entire document after individual units are completed.
- If revisions become necessary, identify the affected units and provide only the replacement text.
- Preserve unrelated content, numbering, and previously approved decisions wherever possible.
- Do not mark units as completed without my confirmation.

## Inputs

### Approved study design

See attached.

### Implementation plan template

See attached.

---

**Begin by reviewing the study design. Ask only essential clarification questions, if any, before generating the implementation plan.**