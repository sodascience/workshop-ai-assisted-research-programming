# Prompts

These are reusable instructions to copy into UU AI Chat. Use a separate conversation for each stage, within the same project, and attach the saved files listed below.

| Chat | Prompt | Attach |
|---|---|---|
| 1 — Design | [study_design_prompt.md](study_design_prompt.md) | [Study-design template](../templates/study_design_template.md) and relevant research context/documentation. |
| 2 — Plan | [implementation_plan_prompt.md](implementation_plan_prompt.md) | Your reviewed `study_design.md` and the [implementation-plan template](../templates/implementation_plan_template.md). |
| 3 — Implement | [unit_implementation_prompt.md](unit_implementation_prompt.md) | Your reviewed `study_design.md` and `implementation_plan.md`. Provide current code when needed. |

Save and commit the reviewed design before Chat 2, and the reviewed plan before Chat 3. Explicitly attach the current documents rather than assuming a new chat knows earlier decisions.

## Short requests for Chat 3

After the setup prompt, use requests such as:

- **Implement:** “Implement Unit 1.1 only.”
- **Verify:** “Provide independent verification checks for Unit 1.1 against its requirements.”
- **Debug:** “Here is the error and relevant code. Explain the cause and suggest the smallest fix for Unit 1.1.”
- **Revise:** “This finding affects Unit 1.2: [finding]. Propose changes to the affected sections only, and wait for my approval.”

Read the suggested code, save it in the specified local file, and run it yourself. Report actual errors or results to the chat. Request verification separately; review the changes and commit once the checks pass. Then request the next unit.

See the [example conversations](../examples/README.md) for this workflow in practice.
