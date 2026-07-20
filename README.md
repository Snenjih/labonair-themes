# labonair-themes

![Themes](https://img.shields.io/badge/themes-19-blue)

Community theme registry for [Labonair](https://github.com/Snenjih/labonair) — a Tauri v2 terminal emulator. This repository powers the built-in **Theme Marketplace** inside the Labonair app.

---

## Using Themes

Open Labonair, navigate to **Settings → Themes**, and browse or install any community theme directly from within the app. The marketplace fetches the latest themes from this registry automatically.

---

## Submitting a Theme

1. **Fork** this repository.
2. Create `themes/your-theme-name.json` — the filename (lowercase kebab-case) becomes the theme's `id` inside the app.
3. Fill in the required fields (see schema below). Every theme bundles **both** a light and a dark variant in one file — there's no more `-dark.json`/`-light.json` pair.
4. Validate locally against [`theme.schema.json`](./theme.schema.json) if you like, then open a **Pull Request** — `index.json` is regenerated automatically on merge.

### Required fields in every theme file

```json
{
  "name": "My Theme",
  "author": "Your Name",
  "variants": {
    "dark": { "mode": "dark", "colors": { ... } },
    "light": { "mode": "light", "colors": { ... } }
  }
}
```

`variants` must contain **at least one entry with `mode: "dark"` and one with `mode: "light"`**. Variant keys (`dark`, `light`, `frappe`, `macchiato`, …) are arbitrary slugs — what determines light/dark is each variant's `mode` field, not its key name. Larger families (e.g. Catppuccin's four variants) add extra keys beyond just `dark`/`light`, each still needing a `mode`.

### Optional metadata fields (used by the marketplace)

```json
{
  "version": "1.0.0",
  "description": "Short description of your theme",
  "authorUrl": "https://github.com/yourname"
}
```

Each variant also accepts an optional `"label"` (e.g. `"label": "Macchiato"`), shown in the app's variant picker for themes with more than one variant per mode. Defaults to the variant key, capitalized.

---

## Color Key Reference (v3)

All color keys are **optional** per variant — the app falls back to CSS defaults for any key not present. Well-crafted themes should define all keys, **in both the light and dark variant**.

Color values must be HEX strings: `#RGB`, `#RRGGBB`, or `#RRGGBBAA` (8-digit hex with alpha, used only for `selection` and `border.transparent`).

### Core Surfaces
| Key | Purpose |
|-----|---------|
| `background` | Main app background |
| `foreground` | Default text color |
| `card` | Card / panel background |
| `card_foreground` | Card text color |
| `popover` | Popover / dropdown background |
| `popover_foreground` | Popover text color |

### Primary Action
| Key | Purpose |
|-----|---------|
| `primary` | Accent / brand color |
| `primary_foreground` | Text on primary backgrounds |

### Secondary / Muted Surfaces
| Key | Purpose |
|-----|---------|
| `secondary` | Secondary surface color |
| `secondary_foreground` | Text on secondary backgrounds |
| `muted` | Muted surface (tab bars, rows) |
| `muted_foreground` | Muted / subdued text |
| `accent` | Hover / active highlight surface |
| `accent_foreground` | Text on accent backgrounds |

### Destructive
| Key | Purpose |
|-----|---------|
| `destructive` | Destructive action color (delete, error) |
| `destructive_foreground` | Text on destructive backgrounds |

### Form / Focus
| Key | Purpose |
|-----|---------|
| `border` | Default border color |
| `input` | Input field background |
| `ring` | Legacy focus ring (used by some components) |

### Named Surface Areas
| Key | Purpose |
|-----|---------|
| `sidebar.background` | Sidebar / file tree background |
| `toolbar.background` | Top toolbar / header bar |
| `title_bar.background` | Window title bar area |
| `status_bar.background` | Bottom status bar |

### Border State Variants
| Key | Purpose |
|-----|---------|
| `border.variant` | Subtle structural borders |
| `border.focused` | Border when element is focused |
| `border.selected` | Border when element is selected |
| `border.transparent` | Transparent border — always `#00000000` |
| `border.disabled` | Border for disabled elements |

### Semantic Status Colors
| Key | Purpose |
|-----|---------|
| `modified` | Modified / changed indicator |
| `error` | Error state |
| `warning` | Warning state |
| `info` | Informational state |
| `hint` | Hint / secondary metadata |
| `success` | Success / done state |

### UI Interaction
| Key | Purpose |
|-----|---------|
| `cursor` | Text cursor / caret color |
| `selection` | Text selection background (supports `#RRGGBBAA` alpha) |

### Terminal Surface
| Key | Purpose |
|-----|---------|
| `terminal.background` | Terminal panel background |
| `terminal.foreground` | Terminal default text |
| `terminal.bright_foreground` | Bold / bright terminal text |
| `terminal.dim_foreground` | Dim terminal text |

### Terminal ANSI Colors
| Key | Purpose |
|-----|---------|
| `terminal.ansi.background` | ANSI background (usually = `terminal.background`) |
| `terminal.ansi.black` | ANSI black |
| `terminal.ansi.red` | ANSI red |
| `terminal.ansi.green` | ANSI green |
| `terminal.ansi.yellow` | ANSI yellow |
| `terminal.ansi.blue` | ANSI blue |
| `terminal.ansi.magenta` | ANSI magenta |
| `terminal.ansi.cyan` | ANSI cyan |
| `terminal.ansi.white` | ANSI white |
| `terminal.ansi.bright_black` | Bright black |
| `terminal.ansi.bright_red` | Bright red |
| `terminal.ansi.bright_green` | Bright green |
| `terminal.ansi.bright_yellow` | Bright yellow |
| `terminal.ansi.bright_blue` | Bright blue |
| `terminal.ansi.bright_magenta` | Bright magenta |
| `terminal.ansi.bright_cyan` | Bright cyan |
| `terminal.ansi.bright_white` | Bright white |
| `terminal.ansi.dim_black` | Dim black |
| `terminal.ansi.dim_red` | Dim red |
| `terminal.ansi.dim_green` | Dim green |
| `terminal.ansi.dim_yellow` | Dim yellow |
| `terminal.ansi.dim_blue` | Dim blue |
| `terminal.ansi.dim_magenta` | Dim magenta |
| `terminal.ansi.dim_cyan` | Dim cyan |
| `terminal.ansi.dim_white` | Dim white |

### Sidebar Component Colors
| Key | Purpose |
|-----|---------|
| `sidebar-foreground` | Sidebar text |
| `sidebar-primary` | Sidebar primary accent |
| `sidebar-primary-foreground` | Text on sidebar primary |
| `sidebar-accent` | Sidebar hover / active surface |
| `sidebar-accent-foreground` | Text on sidebar accent |
| `sidebar-border` | Sidebar border |
| `sidebar-ring` | Sidebar focus ring |

---

## Example Theme Skeleton

```json
{
  "name": "My Theme",
  "author": "Your Name",
  "authorUrl": "https://github.com/yourname",
  "version": "1.0.0",
  "description": "A short description",
  "variants": {
    "dark": {
      "mode": "dark",
      "label": "Dark",
      "colors": {
        "background":                    "#0f111a",
        "foreground":                    "#e4e4e5",
        "card":                          "#141722",
        "card_foreground":               "#e4e4e5",
        "popover":                       "#141722",
        "popover_foreground":            "#e4e4e5",
        "primary":                       "#6366f1",
        "primary_foreground":            "#ffffff",
        "secondary":                     "#1e2130",
        "secondary_foreground":          "#e4e4e5",
        "muted":                         "#1e2130",
        "muted_foreground":              "#6b7280",
        "accent":                        "#1e2130",
        "accent_foreground":             "#e4e4e5",
        "destructive":                   "#e06c75",
        "destructive_foreground":        "#ffffff",
        "border":                        "#252836",
        "input":                         "#252836",
        "ring":                          "#6366f1",
        "sidebar.background":            "#141722",
        "toolbar.background":            "#141722",
        "title_bar.background":          "#141722",
        "status_bar.background":         "#141722",
        "border.variant":                "#252836",
        "border.focused":                "#6366f1",
        "border.selected":               "#6366f1",
        "border.transparent":            "#00000000",
        "border.disabled":               "#3c3c3c",
        "modified":                      "#61afef",
        "error":                         "#e06c75",
        "warning":                       "#e5c07b",
        "info":                          "#61afef",
        "hint":                          "#6b7280",
        "success":                       "#98c379",
        "cursor":                        "#6366f1",
        "selection":                     "#6366f120",
        "terminal.background":           "#0f111a",
        "terminal.foreground":           "#e4e4e5",
        "terminal.bright_foreground":    "#ffffff",
        "terminal.dim_foreground":       "#9d9d9d",
        "terminal.ansi.background":      "#0f111a",
        "terminal.ansi.black":           "#1c1e2b",
        "terminal.ansi.red":             "#e06c75",
        "terminal.ansi.green":           "#98c379",
        "terminal.ansi.yellow":          "#e5c07b",
        "terminal.ansi.blue":            "#61afef",
        "terminal.ansi.magenta":         "#c678dd",
        "terminal.ansi.cyan":            "#56b6c2",
        "terminal.ansi.white":           "#abb2bf",
        "terminal.ansi.bright_black":    "#3e4451",
        "terminal.ansi.bright_red":      "#e06c75",
        "terminal.ansi.bright_green":    "#98c379",
        "terminal.ansi.bright_yellow":   "#e5c07b",
        "terminal.ansi.bright_blue":     "#61afef",
        "terminal.ansi.bright_magenta":  "#c678dd",
        "terminal.ansi.bright_cyan":     "#56b6c2",
        "terminal.ansi.bright_white":    "#ffffff",
        "terminal.ansi.dim_black":       "#151720",
        "terminal.ansi.dim_red":         "#a8515a",
        "terminal.ansi.dim_green":       "#72925b",
        "terminal.ansi.dim_yellow":      "#ac905c",
        "terminal.ansi.dim_blue":        "#4983b3",
        "terminal.ansi.dim_magenta":     "#955aa5",
        "terminal.ansi.dim_cyan":        "#408891",
        "terminal.ansi.dim_white":       "#80858f",
        "sidebar-foreground":            "#e4e4e5",
        "sidebar-primary":               "#6366f1",
        "sidebar-primary-foreground":    "#ffffff",
        "sidebar-accent":                "#1e2130",
        "sidebar-accent-foreground":     "#e4e4e5",
        "sidebar-border":                "#252836",
        "sidebar-ring":                  "#6366f1"
      }
    },
    "light": {
      "mode": "light",
      "label": "Light",
      "colors": {
        "background":                    "#f7f7fb",
        "foreground":                    "#1e2130",
        "card":                          "#ffffff",
        "card_foreground":               "#1e2130",
        "popover":                       "#ffffff",
        "popover_foreground":            "#1e2130",
        "primary":                       "#6366f1",
        "primary_foreground":            "#ffffff",
        "secondary":                     "#eef0f7",
        "secondary_foreground":          "#1e2130",
        "muted":                         "#eef0f7",
        "muted_foreground":              "#6b7280",
        "accent":                        "#eef0f7",
        "accent_foreground":             "#1e2130",
        "destructive":                   "#dc4c5c",
        "destructive_foreground":        "#ffffff",
        "border":                        "#e2e4ee",
        "input":                         "#e2e4ee",
        "ring":                          "#6366f1",
        "sidebar.background":            "#f0f1f7",
        "toolbar.background":            "#ffffff",
        "title_bar.background":          "#ffffff",
        "status_bar.background":         "#f0f1f7",
        "border.variant":                "#e2e4ee",
        "border.focused":                "#6366f1",
        "border.selected":               "#6366f1",
        "border.transparent":            "#00000000",
        "border.disabled":               "#d0d2de",
        "modified":                      "#2f6fb3",
        "error":                         "#dc4c5c",
        "warning":                       "#a9782c",
        "info":                          "#2f6fb3",
        "hint":                          "#6b7280",
        "success":                       "#4f9153",
        "cursor":                        "#6366f1",
        "selection":                     "#6366f120",
        "terminal.background":           "#f7f7fb",
        "terminal.foreground":           "#1e2130",
        "terminal.bright_foreground":    "#000000",
        "terminal.dim_foreground":       "#6b7280",
        "terminal.ansi.background":      "#f7f7fb",
        "terminal.ansi.black":           "#1e2130",
        "terminal.ansi.red":             "#dc4c5c",
        "terminal.ansi.green":           "#4f9153",
        "terminal.ansi.yellow":          "#a9782c",
        "terminal.ansi.blue":            "#2f6fb3",
        "terminal.ansi.magenta":         "#a852c4",
        "terminal.ansi.cyan":            "#2b8a95",
        "terminal.ansi.white":           "#6b7280",
        "terminal.ansi.bright_black":    "#9499a8",
        "terminal.ansi.bright_red":      "#e06c75",
        "terminal.ansi.bright_green":    "#6fae72",
        "terminal.ansi.bright_yellow":   "#c99a4a",
        "terminal.ansi.bright_blue":     "#4a8fce",
        "terminal.ansi.bright_magenta":  "#c678dd",
        "terminal.ansi.bright_cyan":     "#56b6c2",
        "terminal.ansi.bright_white":    "#1e2130",
        "terminal.ansi.dim_black":       "#c3c5d1",
        "terminal.ansi.dim_red":         "#e8a3ab",
        "terminal.ansi.dim_green":       "#a8cbaa",
        "terminal.ansi.dim_yellow":      "#d9bd8e",
        "terminal.ansi.dim_blue":        "#a3c3e0",
        "terminal.ansi.dim_magenta":     "#d8b0e6",
        "terminal.ansi.dim_cyan":        "#a0d0d6",
        "terminal.ansi.dim_white":       "#e2e4ee",
        "sidebar-foreground":            "#1e2130",
        "sidebar-primary":               "#6366f1",
        "sidebar-primary-foreground":    "#ffffff",
        "sidebar-accent":                "#eef0f7",
        "sidebar-accent-foreground":     "#1e2130",
        "sidebar-border":                "#e2e4ee",
        "sidebar-ring":                  "#6366f1"
      }
    }
  }
}
```
