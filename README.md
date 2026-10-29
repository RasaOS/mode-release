# mode-release

**Version:** 0.1.0 · `rasa.module.mode.release` · public

An example **mode** Element (galt ADR [0071](https://github.com/Vehicle-Safety-Inspections/galt/blob/main/docs/decisions/0071-modes-are-named-replaceable-sets-of-elements.md); tenant ADR `2026-10-28-one-role-list` D5). A mode is a named, per-session set of other Elements, pinned by ref, applied as one wholesale replace of a session's or daemon's loaded Elements — not an add to whatever was loaded before.

| File | What it is |
|---|---|
| `mode.json` | The one hand-authored file: `id`, `version`, and the `elements` this mode names (by `element` + `ref`). |
| `.claude-plugin/plugin.json` | The plugin manifest, which makes the repo loadable into a session with `--plugin-dir` (a mode Element carries no plugin behaviour of its own; this file exists so every Element, mode or not, is uniformly loadable). |
| `rasa.json` | The Element manifest: `kind: module`, `rasa.shape_pattern: mode`. |
| `bin/check-mode` | The release gate: validates `mode.json`'s shape and that this repo carries nothing but a composition declaration. |

## Members

  - [`role-release-captain`](https://github.com/RasaOS/role-release-captain) @ `main`
  - [`module-releases`](https://github.com/RasaOS/module-releases) @ `main`

## What this is not

A mode carries **no `prompt.md`, no `settings.json`, no skills of its own** — everything it contributes comes from the member Elements above. `CLAUDE.md` is never part of a mode; Claude Code does not load a plugin's `CLAUDE.md`, and a mode's instructions travel only through its members' own `prompt.md`.

Apply it with `galt mode set <session|agent> mode-release`; clear it with `galt mode clear <session|agent>`.
