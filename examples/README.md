# Worked example

These files come from testing the workshop prompts and templates in UU AI Chat. The example studies factors associated with OpenAlex citation counts using [SODA Open Research Teaching Data](https://zenodo.org/records/23419332) and an R implementation plan.

## Files and reading order

| Stage | Chat export | Saved document |
|---|---|---|
| 1 — Study design | [Study-design conversation (PDF)](uu_ai_chat_export_1_study_design.pdf) | [study_design.md](study_design.md) |
| 2 — Implementation plan | [Planning conversation (PDF)](uu_ai_chat_export_2_implementation_plan.pdf) | [implementation_plan.md](implementation_plan.md) |
| 3 — Implementation and verification | [Coding conversation (PDF)](uu_ai_chat_export_3_unit_implementation.pdf) | Code was transferred to the local analysis project; no implementation scripts or outputs are included here. |

The PDFs record the three conversations. The two Markdown (.md) files are the design and plan saved from that process, for use as context in subsequent chats and for local version control. They are worked examples, not blank templates or verified research findings. Some decisions remain provisional and require checks against the actual data and documentation.

## Follow the workflow

1. **Design in Chat 1.** Discuss research decisions using the [study-design prompt](../prompts/study_design_prompt.md) and [template](../templates/study_design_template.md). Review the resulting document, save it locally, and commit it.
2. **Plan in Chat 2.** Upload the saved design with the [planning prompt](../prompts/implementation_plan_prompt.md) and [template](../templates/implementation_plan_template.md). Check that tasks are small and verifiable. Save and commit the reviewed plan.
3. **Implement in Chat 3.** Upload both saved documents and use the [unit-implementation prompt](../prompts/unit_implementation_prompt.md). Ask for one numbered unit, understand the code, save it locally, and run it. Request verification separately, share errors when needed, and commit the verified change before continuing.

The workshop trial reached approximately Unit 1.3, including verification and debugging; the full analysis was not completed in that trial. Use the early units to learn the process rather than trying to finish the entire example during the workshop.

For your own study, start with the blank templates and your research context. If new information changes the design or plan, review and commit only the affected sections, then provide the updated documents to the coding chat.
