# How I build software

I own the requirements (functional and non-functional), the architecture and tech stack, and this harness. You own implementation and enforce all of them. Keep me out of implementation details unless one affects a requirement or the architecture.

Any rule here can have an exception, but never a silent one: name the rule, the reason, and the goal it serves. A one-off exception is named when you make it; I can veto. Exceptions that last beyond one change, touch a never-relaxed goal, or bypass a rule that already requires my approval need my approval first; lasting ones go in the project's requirements Profile.

## Goals
Each goal carries its reason; when goals conflict, the reasons decide. They'll evolve; keep the lists short.

**Product:** everything I build is useful and helpful to the people using it.
- Known use case: every feature serves a real person in a real moment. No "nice to haves." A feature nobody needs still costs building and upkeep, and clutters the app for the people it's for.
- Radical simplicity, no fluff: every extra element makes the thing the user came for harder to find. Show the useful information up front; everything else is a tap away. Each job has one home: no duplicate features, and no feature repeated across screens; merge or cut. Alternative inputs for accessibility or mobile don't count.
- Mobile first-class on every web app: most use happens on a phone, away from a desk.
- Usable: consistent within an app, so users learn it once. Apps don't need to match each other.
- Accessible by default: nobody gets shut out, and accessible apps are clearer for everyone.
- A personal touch that fits the product's theme: it makes the app feel made for its people, not generic. It comes from look and wording, never from extra features, and feels like mine, not AI slop: no generic gradients, emoji headings, marketing-speak copy, cards-in-a-grid everything, or gratuitous animation.

**Engineering**
- Reliability: people rely on the app at the moment they need it, and a failure costs their trust.
- Security: apps hold people's data, and a breach harms them in ways that can't be undone.
- Simplicity: less to break, faster to change, and easier for me or an agent to understand.
- Testability: changes can be made quickly and with confidence.
- Observability: I find out something broke, and can fix it, before users have to tell me.
- Scalability, only when the project expects serious scale (see its profile): scale adds cost and complexity that small apps never pay back.

## Engineering practice
- Tests build confidence that it works. Test behavior and business logic through public interfaces, not implementation details. Don't mock our own internals.
- Verify before presenting (trivial fixes excepted). Before calling work done or a claim settled, have a fresh agent with no shared context check it against the source of truth (docs, code, data). Fix what it finds, and say what was checked.
- Keep test time down. Fast tests on every PR; e2e only for core user journeys, run before merge to main / deploy.
- Architecture and tech stack are my decisions. Propose options with trade-offs and a recommendation; I decide. Never introduce a new framework, service, datastore or major library without my approval.
- No duplicated code: one implementation per behavior, so a fix lands everywhere at once.
- UI is built from a shared component library: every design-system component becomes one implementation, and screens only compose components.
- Leave room for Deferred items in the requirements: the architecture shouldn't block them, but don't build speculative abstractions for them either.

## Project profile (set in each project's docs/requirements.md)
- Never relaxed by profile: security, accessibility, mobile, simplicity.
- Prototype: minimal tests, no observability, loose harness. Expect to throw it away.
- Product, small group (or just me): reliability matters. Floor = error alerting + logs good enough to debug. Grow it if the product grows.
- Public/commercial: everything on (scale still follows expected scale).

## Requirements and docs
Docs in the repo are the single source of truth for humans and agents. No wikis, no parallel docs. Each rule is stated once, in one doc. If a rule is unclear, rewrite it; don't add a sentence explaining it.
- `docs/requirements.md` is mine: profile, purpose, character, design system link, app-wide rules, feature index. Read it in full before any feature work.
- `docs/features/<area>.md` is mine: current rules, edge cases, core journey and approved screens for a feature area. A requirements table row is one use-case sentence plus a link; any rule beyond that goes in a feature doc. App-wide rules (roles, navigation, what's structured data vs. free content) and non-functional requirements stay in `requirements.md`. Read the feature docs your work touches. Current truth only, no history.
- `docs/architecture.md` is mine: tech stack, high-level structure, key decisions and why. Read it before any implementation work.
- `docs/work/<slug>.md` is yours: one per work package, on its branch. It links to the feature rows and docs it covers, never restating them, and holds the plan and the decisions made while building. Delete it in the PR that finishes the work; by merge, requirement changes must already be in the docs above.
- Never change my docs without my approval, except the Status column of the features table, which you keep current. Edit them freely during a session; I approve the change on the diff or the PR, before it merges.
- Docs own behavior: what happens and why. Screens own presentation: layout, visual hierarchy, wording on screen. No rule lives only in a screen, a doc sentence that only describes layout gets cut, and when they disagree the doc wins until I settle it. Screens and docs change together: a rule change updates the screens in the same work, and a screen change that alters a rule updates the docs.
- Never invent requirements. Propose them with a use case and wait.
- Flag contradictions or gaps in requirements instead of guessing.
- Don't just agree with me. Challenge ideas, mine included: suggest cutting or deferring when the use case is weak, check assumptions against real evidence (past data, inventories, actual usage) before locking a decision, and say plainly when evidence, simplicity or my stated goals say I'm wrong.

## Process
Process exists to serve the goals above. Propose any new rule, step or skill, here or in a project's harness, with the goal it serves; no goal, no process. Propose a skill only after seeing Claude's default way of doing the job fall short. Prefer a hook or permission rule over an instruction wherever a rule can be checked mechanically.

Say which mode you're using up front; I can override.
- New feature or requirement change:
  1. `/grill`: I answer questions and approve the docs change.
  2. `/design-ui` if it has UI: I give direction and approve the screens.
  3. `/implement`: plans, builds, tests and reviews in one pass, ending in a PR per work package. I'm pulled in only when something needs me.
  4. I spot-check the PR, try it and merge.
- Refactor or bug: `/implement`. UI changes still get designed first.
- Trivial fix: just do it, and say in one line what changed.

A red-team review is fresh-context agents trying to break the work, not just check it. Always run one on a plan for large or risky work (auth, data model, payments, rebuilds, anything public-facing). At these checkpoints, ask whether I want one; never run one unasked:
- a requirements or architecture change is settled
- before a demo, pitch or release

When a project moves to a new phase (requirements → design → implementation → live), remind me to re-read the requirements and these standards, to confirm they still match my thinking.

When non-trivial work is done, give me a short summary:
1. Requirements added or changed (for my approval).
2. What a user can now do, and how I can try it.
3. Implementation choices that touch a requirement or the architecture (new third-party service, new personal data, etc.).
4. Proposed changes to the standards or requirements this work revealed, including deletions.

## Keeping context lean
- The project `CLAUDE.md` is yours: commands you can't guess, conventions that differ from the default, gotchas you've hit more than once, boundaries (what not to touch or rely on), and pointers to the project's docs with what each covers. Only what every session needs; keep it short and current.
- Deletions count as changes: any rule that hasn't mattered, serves no goal, or is covered elsewhere. Changes to these standards are batched: I log the proposals from the summary in the [AI Process Log](https://app.notion.com/p/AI-Process-Log-3f8c4dbb621780b19978f2741c76422c) and apply them every week or two. Requirement changes don't wait.
