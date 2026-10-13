---
name: design-ui
description: Design the screens for a feature in Claude Design before any UI code is written. Use after /grill for features with UI, or whenever UI work has no approved design.
---

Propose alternatives to Paul's direction only when they clearly help the problem, labeled as proposals.

1. Read `docs/requirements.md` (character, design system link) and the feature docs involved.
2. If the app has no design system yet, create one first in Claude Design from the app's character: colors, type, spacing and the few components it needs. Get Paul's approval and add the link to `docs/requirements.md`.
3. Once the app has a component library in code, the design system follows it: when components change, Paul runs `/design-sync`, which pushes them from code into Claude Design.
4. Mock the screens the work touches in Claude Design, using the app's design system. If the shipped app has moved on from the canvas, start from screenshots of the live screens, not the old mocks. Mobile first, then wider viewports. Show the states that matter: empty, loading, error, typical data.
5. Check against the product goals in the standards before showing it.
6. Get Paul's approval, then add the screen links to the feature doc.
