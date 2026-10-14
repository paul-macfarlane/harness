---
name: grill
description: Stress-test a proposed feature or requirement change with Paul before planning. Use for new features or changes to docs/requirements.md or docs/features/, or when Paul says "grill".
---

Grill Paul about the proposal until the requirement is clear, justified and minimal.

1. Read `docs/requirements.md`, the feature docs the proposal touches, and the global standards.
2. Ask one question at a time, each with your recommended answer. Ask with the AskUserQuestion choice card, recommended option first and labelled "(Recommended)"; give evidence or context in a short message before it. Plain text only for open questions a card can't hold. Cover:
   - **Use case:** who uses this, when, and what does it get them? If the answer is vague, push for a real person and moment, or suggest cutting it.
   - **Simplicity:** what's the smallest version that solves the use case? What can be deferred?
   - **Fit:** does it contradict or overlap an existing requirement or feature? Is it consistent with the app's character?
   - **Profile:** does it change the project's profile or expected scale?
3. Stop when there are no open questions. Write the change to `docs/requirements.md` (new rows get Status `todo`) and any feature docs on a branch, and show Paul the diff for approval. Once it's settled, ask whether Paul wants a red-team (a checkpoint in the standards).

Don't discuss implementation unless it changes a requirement.
