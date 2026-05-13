# ui-mock-spec-review

A Codex Skill for reviewing AI-generated UI mockups against a real app's specs, code, screenshots, and interaction rules.

Generated UI mockups can be visually strong but product-inaccurate. This skill helps Codex separate useful design ideas from incompatible ones before implementation.

## What it does

`ui-mock-spec-review` asks Codex to treat a generated UI mock as a source of ideas, not as a specification to copy. It classifies each idea as:

- `Adopt`: fits the real app and can be implemented directly.
- `Adapt`: useful, but needs changes to match specs or interaction behavior.
- `Reject`: conflicts with product behavior, available data, or platform expectations.
- `Investigate`: promising, but needs user confirmation or device testing.

It is especially useful when comparing UI images from tools like OpenAI image generation, Figma Make, Stitch, or other design generators with an existing app.

## Use cases

- Review a generated mobile UI mock against an existing Android or iOS app.
- Decide which visual ideas from an AI mock are safe to implement.
- Catch mock details that conflict with real data, navigation, destructive actions, or platform behavior.
- Turn a polished but speculative design image into a small implementation proposal.

## Installation

Clone or download this repository, then place the skill folder where Codex can discover it.

For a user-level install:

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/yuuhi2010-sap/ui-mock-spec-review.git ~/.codex/skills/ui-mock-spec-review
```

Restart Codex after installing the skill.

On Windows, use the equivalent Codex skills directory, for example:

```powershell
git clone https://github.com/yuuhi2010-sap/ui-mock-spec-review.git $env:USERPROFILE\.codex\skills\ui-mock-spec-review
```

## Example prompt

```text
Use $ui-mock-spec-review to compare this generated trash screen mock with the current app. Separate what we should adopt, adapt, reject, or test on device.
```

## Expected output

Codex will produce a short verdict, a classification table, and a practical recommendation:

```text
Overall: Good direction
Best ideas to borrow: compact retention notice, clearer destructive action styling
Main risks: bottom action bar may compete with navigation

Idea | Classification | Why | Implementation note
...
```

## Notes

This skill is intentionally conservative. Its goal is not to make every generated mock real. Its goal is to preserve the useful design signal while protecting the app's actual product behavior.

## License

MIT
