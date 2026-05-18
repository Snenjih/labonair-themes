# nexum-themes

![Themes](https://img.shields.io/badge/themes-3-blue)

Community theme registry for [Nexum](https://github.com/Snenjih/nexum) — a Tauri v2 terminal emulator. This repository powers the built-in **Theme Marketplace** inside the Nexum app.

---

## Using Themes

Open Nexum, navigate to **Settings → Theme Marketplace**, and browse or install any community theme directly from within the app. The marketplace fetches the latest themes from this registry automatically.

---

## Submitting a Theme

1. **Fork** this repository.
2. Create `themes/your-theme-name.json` — the filename (lowercase kebab-case) becomes the theme's `id` inside the app.
3. Fill in the required fields (see schema below).
4. Open a **Pull Request** — `index.json` is regenerated automatically on merge.

### Required fields in every theme file

```json
{
  "name": "My Theme",
  "author": "Your Name",
  "type": "dark",
  "colors": { ... }
}
```

### Optional metadata fields (used by the marketplace)

```json
{
  "version": "1.0.0",
  "description": "Short description of your theme",
  "authorUrl": "https://github.com/yourname"
}
```

---

## Color Key Reference

All 42 keys must be present in the `colors` object. All values must be HEX strings (`#RRGGBB`).

### UI Colors
| Key | Purpose |
|-----|---------|
| `background` | Main app background |
| `foreground` | Main text color |
| `card` | Card / panel background |
| `card-foreground` | Card text color |
| `popover` | Popover background |
| `popover-foreground` | Popover text |
| `primary` | Primary accent (buttons, highlights) |
| `primary-foreground` | Text on primary |
| `secondary` | Secondary surfaces |
| `secondary-foreground` | Text on secondary |
| `muted` | Muted background |
| `muted-foreground` | Muted text |
| `accent` | Accent color |
| `accent-foreground` | Text on accent |
| `destructive` | Destructive actions (red) |
| `border` | Border color |
| `input` | Input field background |
| `ring` | Focus ring color |

### Sidebar Colors
| Key | Purpose |
|-----|---------|
| `sidebar` | Sidebar background |
| `sidebar-foreground` | Sidebar text |
| `sidebar-primary` | Sidebar primary accent |
| `sidebar-primary-foreground` | Text on sidebar primary |
| `sidebar-accent` | Sidebar accent |
| `sidebar-accent-foreground` | Text on sidebar accent |
| `sidebar-border` | Sidebar border |
| `sidebar-ring` | Sidebar focus ring |

### Terminal ANSI Colors
| Key | Purpose |
|-----|---------|
| `terminal_background` | Terminal background |
| `terminal_foreground` | Terminal foreground |
| `terminal_black` | ANSI black |
| `terminal_red` | ANSI red |
| `terminal_green` | ANSI green |
| `terminal_yellow` | ANSI yellow |
| `terminal_blue` | ANSI blue |
| `terminal_magenta` | ANSI magenta |
| `terminal_cyan` | ANSI cyan |
| `terminal_white` | ANSI white |
| `terminal_bright_black` | Bright black |
| `terminal_bright_red` | Bright red |
| `terminal_bright_green` | Bright green |
| `terminal_bright_yellow` | Bright yellow |
| `terminal_bright_blue` | Bright blue |
| `terminal_bright_magenta` | Bright magenta |
| `terminal_bright_cyan` | Bright cyan |
| `terminal_bright_white` | Bright white |

---

## Example Theme Skeleton

```json
{
  "name": "My Theme",
  "author": "Your Name",
  "authorUrl": "https://github.com/yourname",
  "type": "dark",
  "version": "1.0.0",
  "description": "A short description",
  "colors": {
    "background":                  "#000000",
    "foreground":                  "#ffffff",
    "card":                        "#111111",
    "card-foreground":             "#ffffff",
    "popover":                     "#222222",
    "popover-foreground":          "#ffffff",
    "primary":                     "#0077ff",
    "primary-foreground":          "#ffffff",
    "secondary":                   "#333333",
    "secondary-foreground":        "#ffffff",
    "muted":                       "#333333",
    "muted-foreground":            "#aaaaaa",
    "accent":                      "#00ccff",
    "accent-foreground":           "#000000",
    "destructive":                 "#ff3333",
    "border":                      "#444444",
    "input":                       "#444444",
    "ring":                        "#0077ff",
    "terminal_background":         "#000000",
    "terminal_foreground":         "#ffffff",
    "terminal_black":              "#000000",
    "terminal_red":                "#ff3333",
    "terminal_green":              "#33ff33",
    "terminal_yellow":             "#ffff33",
    "terminal_blue":               "#3333ff",
    "terminal_magenta":            "#ff33ff",
    "terminal_cyan":               "#33ffff",
    "terminal_white":              "#ffffff",
    "terminal_bright_black":       "#555555",
    "terminal_bright_red":         "#ff6666",
    "terminal_bright_green":       "#66ff66",
    "terminal_bright_yellow":      "#ffff66",
    "terminal_bright_blue":        "#6666ff",
    "terminal_bright_magenta":     "#ff66ff",
    "terminal_bright_cyan":        "#66ffff",
    "terminal_bright_white":       "#ffffff",
    "sidebar":                     "#111111",
    "sidebar-foreground":          "#ffffff",
    "sidebar-primary":             "#0077ff",
    "sidebar-primary-foreground":  "#ffffff",
    "sidebar-accent":              "#222222",
    "sidebar-accent-foreground":   "#ffffff",
    "sidebar-border":              "#444444",
    "sidebar-ring":                "#0077ff"
  }
}
```
