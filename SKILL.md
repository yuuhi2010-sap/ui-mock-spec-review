---
name: ui-mock-spec-review
description: Review generated UI mock images against an existing app's real screenshots, code, design patterns, and product specs. Use when the user provides an AI-generated UI mock, visual redesign, screenshot, or concept image and wants Codex to separate adoptable ideas from incompatible ones, explain tradeoffs, and propose implementation candidates that fit the actual app.
---

# UI Mock Spec Review

Use this skill to turn a generated UI mock into a grounded implementation proposal. Treat the image as a source of design ideas, not as a specification to copy.

## Core Workflow

1. Identify the target screen, user flow, and likely intent of the mock.
2. Inspect the real app context before judging: current screenshot if available, relevant components, navigation behavior, data model, and platform constraints.
3. Extract concrete design ideas from the mock as small candidates. Avoid vague labels like "make it nicer"; name the actual UI change.
4. Classify each candidate:
   - `Adopt`: fits the app's real behavior and can be implemented directly.
   - `Adapt`: visually useful, but needs changes to match app specs, data, accessibility, or interaction model.
   - `Reject`: conflicts with product behavior, available data, platform expectations, or existing navigation.
   - `Investigate`: promising, but requires user confirmation or real-device testing.
5. Explain why each classification was chosen in product terms, not just visual taste.
6. Propose a small implementation plan only for `Adopt` and strong `Adapt` items.
7. Keep the user's real app safer than the mock: preserve existing data behavior, Android expectations, and established design language unless the user explicitly asks to change direction.

## What To Compare

Check the mock against these axes:

- `Information architecture`: Does the mock put controls in places that match the app's current navigation and mental model?
- `Actual data`: Does the app have the data needed to show the mock's labels, counts, badges, states, dates, or warnings?
- `Interaction truth`: Would the visible affordance actually work for touch, long press, Android back, outside tap, keyboard, scroll, and modal behavior?
- `Safety`: Are destructive actions placed, colored, confirmed, and disabled correctly?
- `Density`: Does the mock improve scanning without hiding important content?
- `Fixed UI`: Does it avoid conflicts with bottom nav, FAB, keyboard, safe area, and toasts?
- `Existing style`: Does it harmonize with the app's current components, typography, spacing, colors, and card language?
- `Implementation cost`: Is this a small component adjustment, a shared pattern change, or a larger product change?

## Output Format

Start with a short verdict:

```text
Overall: Good direction / Mixed / Mostly incompatible
Best ideas to borrow: ...
Main risks: ...
```

Then provide a table:

```text
Idea | Classification | Why | Implementation note
```

After the table, give a concise recommendation:

- `Implement now`: 1-3 low-risk items.
- `Prototype`: ideas worth trying behind a small local change or screenshot check.
- `Do not copy`: incompatible mock details and why.
- `Manual test focus`: touch or Android behaviors to verify on a device.

## Review Rules

- Do not assume the mock's UI is correct just because it looks polished.
- Do not reject a mock only because it differs visually; extract the underlying useful pattern.
- Prefer small, composable changes over redesigning the whole screen.
- If the mock includes impossible or unimplemented features, separate the visual idea from the unsupported behavior.
- When the user shares an image path, inspect the image directly.
- When the user asks to implement, inspect the relevant code first and keep changes scoped to chosen candidates.
- If the mock suggests destructive actions, confirmations, restore flows, trash retention, import/export, or privacy behavior, verify the current app's actual rules before proposing changes.

## Example Candidate Language

Use concrete phrasing like:

- `Adopt`: "Keep the trash retention explanation as a compact top notice, because the app already has a 30-day trash model."
- `Adapt`: "The bottom bulk-action bar is useful, but it should become visually quieter when 0 items are selected."
- `Reject`: "Do not add a per-card countdown unless the repository already stores enough deletion timing data."
- `Investigate`: "The action bar may collide with Android bottom navigation; verify on a low-height device."
