---
marp: true
title: AI-assisted research programming
description: Utrecht University Programming Café
theme: default
paginate: false
size: 16:9
style: |
  section[class] { display: flex; flex-direction: column; background: white; color: #292929; font-family: Arial, Helvetica, sans-serif; font-size: 36px; line-height: 1.2; padding: 76px 54px 45px; justify-content: flex-start; }
  section[class] h1 { color: #066b83; font-size: 60px; line-height: 1.12; margin: 0 0 24px; letter-spacing: -1px; }
  section[class] p { margin: 0 0 18px; }
  section[class] ul { margin: 0 0 16px; padding-left: 30px; }
  section[class] li { margin: 0 0 5px; }
  section[class] li > ul { font-size: 24px; margin-top: 5px; margin-bottom: 0; }
  section a { color: #087e8b; }
  section::after { display: none; }
  section p:has(> img) { margin: 0; padding: 0; }
  section img { position: absolute; max-width: none; max-height: none; margin: 0; object-fit: fill; }
  section.s1 { padding: 185px 140px 80px; }
  section.s1 h1 { font-size: 56px; white-space: nowrap; margin-bottom: 20px; }
  section.s1 p { font-size: 28px; }
  section.s2 > ul { width: 640px; font-size: 32px; }
  section.s2 li > ul { font-size: 23px; }
  section.s3 h1 { max-width: 1160px; font-size: 58px; }
  section.s5 h1 { position: absolute; left: 54px; top: 76px; z-index: 1; font-size: 60px; }
  section.s11 em, section.s12 > p { font-style: italic; }
  section.s14 { font-size: 32px; }
  section.s14 > p:last-of-type { margin-top: 55px; font-style: italic; }
  section.s15 h1 { position: absolute; left: 54px; top: 292px; width: 320px; }
  section.s16 strong { font-weight: 700; }
  section.s17 > p { width: 390px; }
  section.s17 > p:first-of-type { margin-top: 115px; font-size: 34px; }
  section.s18 > p:first-of-type { position: absolute; left: 453px; top: 540px; width: 740px; z-index: 1; color: #066b83; font-size: 30px; font-style: italic; }
  section.s19 { font-size: 32px; }
  section.s19 > p { font-size: 27px; }
  section.s19 > ul { width: 780px; }
  section.s19 li > ul { font-size: 22px; }
  section.s23, section.s24 { font-size: 34px; }
  section.s23 li > ul, section.s24 li > ul, section.s25 li > ul { font-size: 21px; line-height: 1.2; }
  section.s25 { font-size: 34px; }
  section.s28 { justify-content: center !important; padding-left: 54px; }
  section.s28 h1 { font-size: 62px; }
  section.s29 { background: #066b83; justify-content: center !important; align-items: center; text-align: center; }
  section.s29 h1 { color: white; font-size: 56px; }
  section.s30 > p, section.s30 > ul { width: 590px; }
  section.s30 > p:last-of-type { margin-top: 75px; }
  section.s32 > p { text-align: center; margin-top: 55px; }
  section.s32 > p:first-of-type { font-weight: bold; }
  section.s1 img[src$="pptx-image-03.png"] { left: 917.83px; top: 308.80px; width: 247.00px; height: 267.09px; }
  section.s2 img[src$="pptx-image-15.png"] { left: 730.98px; top: 0.00px; width: 549.02px; height: 720.00px; }
  section.s4 img[src$="pptx-image-10.png"] { left: 0.00px; top: 0.00px; width: 1280.00px; height: 632.23px; }
  section.s4 img[src$="pptx-image-08.png"] { left: 719.35px; top: 628.12px; width: 560.65px; height: 91.88px; }
  section.s5 img[src$="pptx-image-11.png"] { left: 229.07px; top: 0.00px; width: 1050.93px; height: 720.00px; }
  section.s6 img[src$="pptx-image-14.png"] { left: 57.56px; top: 0.00px; width: 1181.23px; height: 720.00px; }
  section.s7 img[src$="pptx-image-06.png"] { left: 30.75px; top: 3.77px; width: 1218.49px; height: 712.46px; }
  section.s8 img[src$="pptx-image-05.png"] { left: 45.48px; top: 0.00px; width: 1194.82px; height: 720.00px; }
  section.s9 img[src$="pptx-image-09.png"] { left: 34.74px; top: 0.00px; width: 1210.52px; height: 720.00px; }
  section.s13 img[src$="pptx-image-13.png"] { left: 0.00px; top: 90.29px; width: 1280.00px; height: 538.95px; }
  section.s15 img[src$="pptx-image-12.png"] { left: 424.58px; top: 0.00px; width: 855.42px; height: 720.00px; }
  section.s17 img[src$="pptx-image-16.png"] { left: 530.59px; top: 161.33px; width: 749.41px; height: 558.67px; }
  section.s18 img[src$="pptx-image-04.png"] { left: 20.64px; top: 0.00px; width: 1238.72px; height: 720.00px; }
  section.s19 img[src$="pptx-image-02.png"] { left: 867.23px; top: 293.56px; width: 319.97px; height: 346.00px; }
  section.s30 img[src$="pptx-image-03.png"] { left: 729.65px; top: 73.50px; width: 506.72px; height: 547.94px; }
  section.s1 img[src$="pptx-image-01.png"] { left: 140px; top: 120px; width: 168px; height: auto; }
  section.s1 p:nth-of-type(2) { position: absolute; top: 515px; left: 140px; font-size: 26px; color: #666; font-style: italic; }
---

<!-- _class: s1 -->

# AI-assisted research programming

**Stay in control**
*with UU AI Chat + local Python/R + Git*

<br>

Qixiang Fang
Utrecht University Programming Café · Oct 22, 2026

![Workshop repository QR code](assets/pptx-image-03.png)

![SoDa](assets/pptx-image-01.png)

---

<!-- _class: s2 -->

# About me

- Name: Qixiang [kis-jang] Fang
- Postdoc at ODISSEI Social Data Science (SoDa) Team
  - Provide research support and training
  - AI methodology research
- Academic background:
  - PhD in NLP
  - MSc in Statistics
  - BAs in behavioural and social sciences

![The SoDa Team](assets/pptx-image-15.png)

---

<!-- _class: s3 -->

# What is your experience with AI-assisted research programming?

- Who are you?
- Do you use AI for research code? For what tasks?
- How has it changed your research workflow?
- What do you like/dislike about it?

---

<!-- _class: s4 -->

![Research AI survey results](assets/pptx-image-10.png)
![Research AI survey article](assets/pptx-image-08.png)

<!-- Slide 4: Survey results: research uses of AI; Who uses AI in research, and for what? -->

---

<!-- _class: s5 -->

# A Codex example

![Codex research response](assets/pptx-image-11.png)

---

<!-- _class: s6 -->

![Codex analysis response](assets/pptx-image-14.png)

<!-- Slide 6: Codex analysis response -->

---

<!-- _class: s7 -->

![Codex files](assets/pptx-image-06.png)

<!-- Slide 7: Codex example: changed files -->

---

<!-- _class: s8 -->

![Codex changes](assets/pptx-image-05.png)

<!-- Slide 8: Codex example: generated changes -->

---

<!-- _class: s9 -->

![Codex analysis code](assets/pptx-image-09.png)

<!-- Slide 9: Codex example: generated analysis code -->

---

<!-- _class: s10 -->

# Challenges of AI-assisted coding

- Lack of understanding of the generated code
- Difficulty in debugging and troubleshooting
- Losing control over the research process
- Over-reliance on AI-generated code
- etc.

---

<!-- _class: s11 -->

# Your role as researcher

When using AI:

- AI does not replace your expertise.
- Any AI output should be inspected and challenged.
- Adjust your expectations: Maybe don't cram what in the past would be three-months of work into one day.

---

<!-- _class: s12 -->

# Your role as researcher

Using AI or not:

- Own the research questions, data and decisions.
- Understand any change (e.g., code, analysis) well enough to explain it.
- Validate the results.
- Reproduce the study.

---

<!-- _class: s13 -->

![Research reproducibility article](assets/pptx-image-13.png)

<!-- Slide 13: AI-assisted teams and research reproducibility -->

---

<!-- _class: s14 -->

# Workshop goals

Target: researchers with (limited) programming experience

You will learn:

- Plan and review plan before AI-assisted coding
- Divide work into small, verifiable units
- Transfer, check, inspect the diff, commit
- Resume from updated project state

**Disclaimer**: Personal experience and opinions; feedback welcome.

---

<!-- _class: s15 -->

# Proposed workflow

![Research workflow](assets/pptx-image-12.png)

---

<!-- _class: s16 -->

# Workshop toolkit

**Local editor + Python/R:** save files, execute, inspect outputs

**Git and GitHub desktop:** inspect changes and save checkpoints

---

<!-- _class: s17 -->

# Workshop toolkit

UU AI Chat: discuss, plan, propose code, debug

https://aichat.uu.nl


![UU AI Chat announcement](assets/pptx-image-16.png)

---

<!-- _class: s18 -->

Note: The chat cannot directly read or edit your local project.


![UU AI Chat interface](assets/pptx-image-04.png)

---

<!-- _class: s19 -->

# Workshop toolkit

**SoDa Open Research Teaching Datasets (SORTD):**

- 11,700 works · 2011–2025 · 26 primary fields
- 30 works per year × field
- English articles with abstracts
- Includes:
  - `works.csv`,
  - `abstracts.csv`,
  - `authors.csv`,
  - `funding.csv`,
  - `topics.csv`
  - etc.

![SORTD dataset QR code](assets/pptx-image-02.png)

---

<!-- _class: s20 -->

# Example research questions

What factors are associated with

- citation counts?
- open access (OA) publication?
- retraction?

---

<!-- _class: s21 -->

# Demo: Research question

What factors are associated with

- citation counts?
- ~~open access (OA) publication?~~
- ~~retraction?~~

---

<!-- _class: s22 -->

# 0. Basic local setup

- Create a local Git-tracked repository
- Gather existing work/resources/files
  - Study description
  - Data
  - Code
  - etc.

---

<!-- _class: s23 -->

# 1. Design

- Create a project in UU AI Chat and start Chat 1.
  - Attach a study design template, and use an appropriate prompt.
- Answer the questions.
  - Review the proposed choices and ask for revisions where needed.
  - Keep uncertain decisions labelled as provisional.
- Approve the design when ready.
- Save it locally, review the saved file, and commit it when ready.

---

<!-- _class: s24 -->

# 2. Plan

- Start Chat 2 in the same project.
  - Attach the approved study design and an implementation plan template, then use an appropriate prompt.
- Check that the plan follows the design.
  - Does each unit have one small goal, clear inputs, a deliverable, and checks you can understand?
- Ask to split any unit that feels too large.
- Review and approve the plan, save it locally and commit it.

---

<!-- _class: s25 -->

# 3. Implement (one unit)

- Start Chat 3 in the same project.
  - Attach both study design and implementation plan.
  - Ask: “Implement Unit # only.”
  - Read the response. Ask about anything you do not understand.

- Save, run and inspect code
  - Save the suggested code or files locally and run any code using the provided instructions.
  - Inspect the result.

- If something fails:
  - Share the error, expected behaviour, and relevant code.
  - Ask: “Explain the cause and suggest the smallest fix for this unit."
  - Apply a fix you understand, then rerun the unit and its checks.

---

<!-- _class: s26 -->

# 4. Verify!

- Ask: “Provide independent verification checks for Unit # against its requirements.”
- Read and run the checks locally. Compare outputs with the requirements.
- Report which checks passed. Resolve any unexplained failures before continuing.

---

<!-- _class: s27 -->

# 5. Commit

- Inspect the changed files in your editor or GitHub Desktop.
- Confirm the changes match the requested unit and include no unrelated edits.
- Stage only the intended implementation and verification files.
- Commit with a short message describing the change.
- Tell Chat 3 the unit is verified and committed before requesting another unit.

---

<!-- _class: s28 -->

# Rinse and repeat 2-5

---

<!-- _class: s29 -->

# Questions?

---

<!-- _class: s30 -->

# Exercise

What factors are associated with

- citation counts?
- open access (OA) publication?
- retraction?

Go to [exercises/README.md](../exercises/README.md)

![Workshop repository QR code](assets/pptx-image-03.png)

---

<!-- _class: s31 -->

# Discussion

- What worked and what didn't?
- How do you like this AI-assisted coding approach?
- Any other question?

---

<!-- _class: s32 -->

# Take home

Design → plan → implement → verify → commit

Update project, then repeat.
