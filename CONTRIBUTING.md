# Contributing to nexum-themes

## Theme Naming Rules

- The filename is the theme's `id` inside the Nexum app — use **lowercase kebab-case only** (e.g. `my-cool-theme.json`).
- Renaming a file after release breaks existing user installs. Choose the name carefully.

## Required Color Keys

Every theme must include all 42 keys in the `colors` object:

```
background, foreground,
card, card-foreground,
popover, popover-foreground,
primary, primary-foreground,
secondary, secondary-foreground,
muted, muted-foreground,
accent, accent-foreground,
destructive,
border, input, ring,
terminal_background, terminal_foreground,
terminal_black, terminal_red, terminal_green, terminal_yellow,
terminal_blue, terminal_magenta, terminal_cyan, terminal_white,
terminal_bright_black, terminal_bright_red, terminal_bright_green,
terminal_bright_yellow, terminal_bright_blue, terminal_bright_magenta,
terminal_bright_cyan, terminal_bright_white,
sidebar, sidebar-foreground,
sidebar-primary, sidebar-primary-foreground,
sidebar-accent, sidebar-accent-foreground,
sidebar-border, sidebar-ring
```

## Color Format

All values **must** be HEX strings (`#RRGGBB` or `#RGB`). Do not use HSL, RGB, or named colors. The Nexum app converts HEX to HSL internally.

## Optional Metadata Fields

You may include these top-level fields in your theme JSON (they are used by the marketplace index):

```json
"version": "1.0.0",
"description": "Short description",
"authorUrl": "https://github.com/yourname"
```

The `type` field must be exactly `"dark"` or `"light"`.

## How CI Works

When a PR is merged to `main`, the GitHub Actions workflow in `.github/workflows/generate-index.yml` automatically regenerates `index.json`. **Never manually edit `index.json`** — your changes will be overwritten.

## PR Checklist

- [ ] Filename is lowercase kebab-case
- [ ] `name`, `author`, and `type` fields are present
- [ ] All 42 color keys are present in `colors`
- [ ] All color values are valid HEX strings (`#RRGGBB`)
- [ ] The JSON is valid (run `python3 -m json.tool themes/your-theme.json`)
- [ ] Theme `id` (filename stem) is unique — not already taken by another file
