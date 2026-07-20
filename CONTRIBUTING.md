# Contributing to labonair-themes

## Theme Naming Rules

- The filename is the theme's `id` inside the Labonair app — use **lowercase kebab-case only** (e.g. `my-cool-theme.json`).
- Renaming a file after release breaks existing user installs. Choose the name carefully.
- Themes bundle both light and dark in one file now — don't create `-dark`/`-light` filename pairs. Use a single unsuffixed name (e.g. `dracula.json`, not `dracula-dark.json` + `dracula-light.json`).

## Required Fields

Every theme must include these top-level fields:

```
name, variants
```

`variants` is an object of variant-key → variant-definition. Each variant requires `mode` (`"dark"` or `"light"`) and `colors`. A file is only valid if `variants` contains **at least one `"dark"`-mode entry and at least one `"light"`-mode entry** — see [`theme.schema.json`](./theme.schema.json) for the full JSON Schema.

```json
{
  "name": "My Theme",
  "author": "Your Name",
  "variants": {
    "dark": { "mode": "dark", "colors": { "...": "..." } },
    "light": { "mode": "light", "colors": { "...": "..." } }
  }
}
```

### Theme families with more than one variant per mode

Some themes (Catppuccin) ship several variants that share a mode — e.g. three `"dark"`-mode variants of differing contrast. Add extra keys to `variants` beyond `dark`/`light`, each with its own `mode` and an optional `label` for display:

```json
"variants": {
  "latte":     { "mode": "light", "label": "Latte",     "colors": { "...": "..." } },
  "frappe":    { "mode": "dark",  "label": "Frappé",     "colors": { "...": "..." } },
  "macchiato": { "mode": "dark",  "label": "Macchiato",  "colors": { "...": "..." } },
  "mocha":     { "mode": "dark",  "label": "Mocha",      "colors": { "...": "..." } }
}
```

The app shows a small variant picker automatically whenever more than one variant shares the active mode.

## Color Keys (v3)

All individual color keys are **optional** per variant — the app falls back to CSS defaults for any missing key. Well-crafted themes should define all of them, in every variant. The full key list is documented in [README.md](./README.md#color-key-reference-v3).

### Notation

- UI keys use **underscore** separators: `card_foreground`, `muted_foreground`, etc.
- Grouped keys use **dot notation**: `sidebar.background`, `terminal.background`, `terminal.ansi.black`, `border.focused`, etc.

### Legacy key names (v1)

The Labonair app accepts both old and new key names for backward compatibility. However, all themes in this repository should use v2 dot-notation keys within each variant's `colors`. Old underscore terminal keys (e.g. `terminal_black`) will trigger a **CI warning** on new PRs — please migrate them to `terminal.ansi.black` etc.

| Old key (v1) | New key (v2) |
|---|---|
| `sidebar` | `sidebar.background` |
| `terminal_background` | `terminal.background` |
| `terminal_foreground` | `terminal.foreground` |
| `terminal_black` | `terminal.ansi.black` |
| `terminal_red` | `terminal.ansi.red` |
| `terminal_green` | `terminal.ansi.green` |
| `terminal_yellow` | `terminal.ansi.yellow` |
| `terminal_blue` | `terminal.ansi.blue` |
| `terminal_magenta` | `terminal.ansi.magenta` |
| `terminal_cyan` | `terminal.ansi.cyan` |
| `terminal_white` | `terminal.ansi.white` |
| `terminal_bright_*` | `terminal.ansi.bright_*` |
| `card-foreground` | `card_foreground` |
| `muted-foreground` | `muted_foreground` |
| *(and other `-foreground` variants)* | *(underscore preferred)* |

## Color Format

All values **must** be HEX strings. Supported formats:

- `#RGB` — 3-digit shorthand
- `#RRGGBB` — standard 6-digit hex
- `#RRGGBBAA` — 8-digit hex with alpha (only for `selection` and `border.transparent`)

Do not use HSL, RGB, or named colors. The Labonair app converts HEX to HSL internally.

## Optional Metadata Fields

```json
"version": "1.0.0",
"description": "Short description",
"authorUrl": "https://github.com/yourname"
```

Per-variant, an optional `"label"` overrides the display name shown in the variant picker (defaults to the variant key, capitalized).

## How CI Works

When a PR is merged to `main`, the GitHub Actions workflow in `.github/workflows/generate-index.yml` automatically regenerates `index.json`. **Never manually edit `index.json`** — your changes will be overwritten.

The validator (`validate-themes.yml`) checks:
- Valid JSON
- Required top-level fields (`name`, `variants`)
- `variants` is a non-empty object where every entry has a valid `mode` (`"dark"` or `"light"`) and a `colors` object
- At least one `"dark"`-mode and one `"light"`-mode variant is present
- All color values are valid hex strings
- Emits a **warning** (not an error) for legacy v1 underscore terminal keys

## PR Checklist

- [ ] Filename is lowercase kebab-case, with no `-dark`/`-light` suffix
- [ ] `name` and `variants` fields are present
- [ ] `variants` includes at least one `"dark"`-mode and one `"light"`-mode entry
- [ ] All color values are valid HEX strings (`#RGB`, `#RRGGBB`, or `#RRGGBBAA`)
- [ ] Color keys use v2 dot-notation (no `terminal_black` etc.)
- [ ] The JSON is valid (run `python3 -m json.tool themes/your-theme.json`)
- [ ] Theme `id` (filename stem) is unique — not already taken by another file
