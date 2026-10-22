# Workshop: AI-assisted research programming

A two-hour workshop on planning, implementing, and verifying research code with [UU AI Chat](https://aichat.uu.nl) and a local [Git](https://git-scm.com)-controlled project. Designed for researchers with (limited) programming experience.

The workshop uses UU AI Chat as an instutitionally supported example. The workflow and materials are applicable to other AI-assisted coding tools. The example study uses R, but the workflow is also applicable to Python.

## Events
- **October 22, 2026** (in-person, Utrecht University Programming Café): [Google Slides](https://docs.google.com/presentation/d/1X6FjB3hIThOZ9YOduj33YmmRCrPJh-stFZtfN38Aiek/edit?usp=sharing)

## Preparation
- A local [Python](https://www.python.org/) or [R](https://www.r-project.org/) environment with [Git](https://git-scm.com/) installed.
- Access to the [UU AI Chat](https://aichat.uu.nl) platform.
- Local editor for Markdown and code files (e.g., [VS Code](https://code.visualstudio.com/), [RStudio](https://docs.posit.co/ide/user/download.html), etc.).

## Repository guide

| Location | What it contains / how to use it |
|---|---|
| [templates/](templates/README.md) | Blank study-design and implementation-plan structures. Attach the relevant template when creating each document using the UU AI Chat. |
| [prompts/](prompts/README.md) | Copy-and-paste instructions for the UU AI Chat. |
| [examples/](examples/README.md) | A worked research example: three chat exports and the resulting design and plan. Start here to see the workflow in practice. |
| [slides/workshop.md](slides/workshop.md) | Workshop slides in Marp Markdown format; read as text or present with a Marp-compatible tool. |
| [`exercises/`](exercises/README.md) | Workshop exercise instructions. |

> Keep your own analysis in a separate project with a local Python or R environment and Git. These materials support either language; the worked example uses R. Check which data may be uploaded or shared before providing it to an AI tool.


## General workflow

Use three separate chats in the same UU AI Chat project in the following order:

1. **Study design:** use the study-design prompt and template to develop your research design interactively. Review, save as `study_design.md`, and commit locally.
2. **Implementation plan:** start a new chat with the saved design, implementation-plan prompt, and template. Review the numbered tasks, save as `implementation_plan.md`, and commit locally.
3. **Code and verification:** start a third chat with both documents and the unit-implementation prompt. Request one unit at a time, review and run the code locally, then request verification separately. Check the results and commit verified changes before continuing.

> UU AI Chat does not edit or run your local files. You transfer the code, inspect the results, and approve decisions. If a decision changes, update only the affected document sections and commit the revision.