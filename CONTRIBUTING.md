# Contributing to nexum-themes

## Theme Naming Rules

- The filename is the theme's `id` inside the Nexum app — use **lowercase kebab-case only** (e.g. `my-cool-theme.json`).
- Renaming a file after release breaks existing user installs. Choose the name carefully.

## Required Fields

Every theme must include these top-level fields:

```
name, author, type, colors
```

The `type` field must be exactly `"dark"` or `"light"`.

## Color Keys (v2)

All individual color keys are **optional** — the app falls back to CSS defaults for any missing key. Well-crafted themes should define all of them. The full key list is documented in [README.md](./README.md#color-key-reference-v2).

### Notation

- UI keys use **underscore** separators: `card_foreground`, `muted_foreground`, etc.
- Grouped keys use **dot notation**: `sidebar.background`, `terminal.background`, `terminal.ansi.black`, `border.focused`, etc.

### Legacy key names (v1)

The Nexum app accepts both old and new key names for backward compatibility. However, all themes in this repository should use v2 dot-notation keys. Old underscore terminal keys (e.g. `terminal_black`) will trigger a **CI warning** on new PRs — please migrate them to `terminal.ansi.black` etc.

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

Do not use HSL, RGB, or named colors. The Nexum app converts HEX to HSL internally.

## Optional Metadata Fields

```json
"version": "1.0.0",
"description": "Short description",
"authorUrl": "https://github.com/yourname"
```

## How CI Works

When a PR is merged to `main`, the GitHub Actions workflow in `.github/workflows/generate-index.yml` automatically regenerates `index.json`. **Never manually edit `index.json`** — your changes will be overwritten.

The validator (`validate-themes.yml`) checks:
- Valid JSON
- Required top-level fields (`name`, `author`, `type`, `colors`)
- `type` is `"dark"` or `"light"`
- All color values are valid hex strings
- Emits a **warning** (not an error) for legacy v1 underscore terminal keys

## PR Checklist

- [ ] Filename is lowercase kebab-case
- [ ] `name`, `author`, and `type` fields are present
- [ ] All color values are valid HEX strings (`#RGB`, `#RRGGBB`, or `#RRGGBBAA`)
- [ ] Color keys use v2 dot-notation (no `terminal_black` etc.)
- [ ] The JSON is valid (run `python3 -m json.tool themes/your-theme.json`)
- [ ] Theme `id` (filename stem) is unique — not already taken by another file
