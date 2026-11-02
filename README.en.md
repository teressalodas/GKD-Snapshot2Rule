<div align="center">
  <img src="./GKD.LI.svg" width="100" height="100" alt="GKD Snapshot2Rule">
  <h1>GKD Snapshot2Rule</h1>
</div>

<p align="center">
  <a href="https://raw.githubusercontent.com/teressalodas/GKD-Snapshot2Rule/main/gkd-rule-generator-prompt.md">
    <img src="https://img.shields.io/badge/GitHub-Get%20the%20Prompt-red?style=for-the-badge&logo=github" alt="Get the Prompt" />
  </a>
  <a href="./LICENSE">
    <img src="https://img.shields.io/badge/License-Apache%202.0-blue.svg?style=for-the-badge" alt="License: Apache License 2.0" />
  </a>
</p>

<p align="center"><a href="./README.md">简体中文</a> | English</p>

Turn a GKD snapshot's node-tree JSON into a working subscription rule. One structured prompt with a selector cheat sheet, `fastQuery` constraints and templates for splash ads, popups and update dialogs — the model returns strict JSON you can paste straight into a local subscription.

## Usage

1. Capture a snapshot with the floating ball, then share / export it in the snapshot inspector. The node-tree JSON inside the zip is your input.
2. Send the **entire [prompt](https://raw.githubusercontent.com/teressalodas/GKD-Snapshot2Rule/main/gkd-rule-generator-prompt.md)** together with the snapshot JSON to a model, with temperature set to 0.
3. Paste the returned rule JSON into a local GKD subscription.
4. If nothing happens, feed the failure back with the old rule and a fresh snapshot and let the model rewrite it — the wording is in the [notes](./gkd-rule-notes.md).

Screenshots alone won't work: a model can't read node attributes from an image, so it can only guess selectors. Always use the snapshot JSON.

## Files

| File | Purpose |
| ---- | ---- |
| `gkd-rule-generator-prompt.md` | Main prompt, copy the whole file into your model |
| `gkd-rule-locator-appendix.md` | Optional appendix for targets with no `id` / `vid` / `text` / `desc` |
| `gkd-rule-notes.md` | Known pitfalls, import caveats, retry wording |

## What the prompt covers

- **Selector cheat sheet** — attributes, comparison and relational operators, property methods, the `@` anchor, and the string / array shorthands.
- **fastQuery constraints** — the prompt declines `fastQuery` unless the first attribute selector uses an exact `[id=]` / `[vid=]` / `[text=]` match.
- **Scene templates** — splash ads, popups with a close button, featureless popups, update dialogs, with recommended `matchTime` / `actionMaximum` / `resetMatch` values.
- **Relational locating** — when the target has no direct feature, the model walks parent / sibling / ancestor chain / `index` / weak-feature combinations instead of returning an empty rule.
- **Strict JSON output** — rules only, no explanations, no `` ```json `` fences, ready to import.

## Privacy

- Snapshots are captured on your own device and exported as a local zip. This project collects and uploads nothing.
- The node tree contains on-screen text, which may include account nicknames, phone numbers or verification codes. Judge your model provider before sending it, and strip irrelevant nodes on sensitive screens.
- `snapshotUrls` is only a human-readable reference. Including it makes the rule do no extra network work; remove the field if you prefer.

## About

- Always verify generated rules on a real device before keeping them long-term: a selector unique within one snapshot is not necessarily unique in the live UI, and the same button can carry a different `id` prefix under a different rendering path.
- This is a prompt repository and is not affiliated with the official [GKD](https://github.com/gkd-kit/gkd) project. Syntax and fields follow [gkd.li](https://gkd.li/guide/) and the [API docs](https://gkd.li/api).
- Found a problem? Open an [Issue](https://github.com/teressalodas/GKD-Snapshot2Rule/issues). PRs and Stars are welcome.
- Auto-clicking can misfire. Don't rely on rules for payment, privacy or other consequential screens, and follow the terms of service of GKD and each app.

## License

Released under [Apache License 2.0](./LICENSE).
