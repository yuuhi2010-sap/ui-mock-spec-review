# ui-mock-spec-review

AI生成UIモックを、実際のアプリ仕様・コード・既存UI・操作感に照らしてレビューするための Codex Skill です。

画像生成AIのUIモックは見た目が良くても、そのまま実装すると仕様に合わないことがあります。このSkillは、生成モックを「完成仕様」ではなく「デザイン案の素材」として扱い、実アプリに落とし込めるものだけを仕分けます。

## 日本語での概要

`ui-mock-spec-review` は、AIが作ったUI画像を見て、Codexに次のような判断をさせるSkillです。

- `Adopt`: そのまま採用できそうな案
- `Adapt`: 良いが、仕様に合わせて調整が必要な案
- `Reject`: 実アプリの仕様や操作と合わない案
- `Investigate`: 良さそうだが、実機確認やユーザー判断が必要な案

たとえば、OpenAI image generation、Figma Make、Stitch などで作ったUIモックを、既存アプリのスクショやコードと比較して「どこを実装候補にするか」を整理できます。

## 日本語での使い方

このリポジトリをCodexのskillsフォルダに置きます。

```powershell
git clone https://github.com/yuuhi2010-sap/ui-mock-spec-review.git $env:USERPROFILE\.codex\skills\ui-mock-spec-review
```

その後、Codexを再起動して、画像モックと一緒に次のように依頼します。

```text
$ui-mock-spec-review でこの生成UIモックを実アプリ仕様に照らして、採用・調整・却下・実機確認に仕分けてください。
```

## 向いている用途

- AI生成UIモックを、そのまま実装する前にレビューしたい
- 既存アプリの仕様に合うデザイン案だけ拾いたい
- 見た目は良いが、実装すると危ないUIを切り分けたい
- Androidの戻るボタン、外側タップ、固定ナビ、FAB、削除操作などの実操作に照らして確認したい

## English

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
