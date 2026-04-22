# Elements — scope & ARIA/APG backlog

## Source of truth (pattern list)

- **W3C WAI-ARIA APG — Patterns:** https://www.w3.org/WAI/ARIA/apg/patterns/
- Implementations should follow **APG examples** (roles, states, keyboard, focus).

## JS layering

- **`UI8Kit/js`:** `window.ui8kit` — minimal behaviors + `core` / `theme` / `locale` (not APG widgets).
- **`Elements/js` (future):** load **`ui8kit.js` first**, then register **additional** `window.ui8kit.*` (or `window.elements.*` delegating to ui8kit) for every **behavioral** APG pattern not covered below.

Goal: **full behavioral coverage** of APG patterns that need JS; patterns satisfied by **native HTML + correct roles/markup** need docs/tests only, not necessarily a script module.

---

## UI8Kit/js — current APG-related coverage

| APG pattern            | Module        | Notes                                      |
|------------------------|---------------|--------------------------------------------|
| Accordion              | `accordion.js`|                                            |
| Combobox               | `combobox.js` | includes listbox-like popup behavior       |
| Dialog (Modal)       | `dialog.js`   | `dialog`, `sheet`, `alertdialog`           |
| Tabs                   | `tabs.js`     |                                            |
| Tooltip                | `tooltip.js`  | hover/focus basics                         |
| Alert                  | `alert.js`    | **stub only** — treat as **not covered**   |
| Alert / message dialog | `dialog.js`   | via `alertdialog`                          |

**Non-APG in `js/`:** `core.js`, `theme.js`, `locale.js`.

---

## Gap analysis → **Elements JS** owns these (backlog)

All names below match APG pattern index; order = suggested **implementation priority** (common widgets first).

1. **Disclosure** (show/hide, not full accordion)
2. **Menu Button** + **Menu** / **Menubar** (shared keyboard model)
3. **Toolbar**
4. **Listbox** (standalone; not only inside combobox)
5. **Breadcrumb** (if keyboard/roving focus beyond plain `<nav>` links)
6. **Grid** (interactive grid + layout grid)
7. **Tree View**
8. **Treegrid**
9. **Slider** + **Slider (multi-thumb)**
10. **Spinbutton**
11. **Meter** (if custom, not `<meter>`; else markup-only)
12. **Carousel**
13. **Feed**
14. **Window splitter**
15. **Checkbox** / **Radio Group** — **only** for **custom** widgets (native `<input>` = no script; tri-state / roving tabindex = Elements)
16. **Alert** — live region / assertive updates (finish what `alert.js` started)
17. **Switch** — **only** if non-native composite

**Usually markup / native (no Elements JS module unless product needs custom):**

- **Button**, **Link** — native or `<button>`/`<a>`
- **Landmarks** — roles + heading structure (docs + lint)
- **Table** — static table pattern = semantic `<table>`; sortable table = often Grid pattern → use row 6

---

## Development rules (for agents)

- New widget JS lives under **`Elements/js`**, depends on **`UI8Kit` bundle** (or concat order: `core` → kit widgets → `elements.*`).
- Do not duplicate APG logic in **Blocks**; Blocks consume Elements + UI8Kit.
- One APG pattern ≈ one focused script file + optional `templ` counterpart later.
- After each pattern: quick checklist vs APG example (keyboard, focus trap if modal, `aria-*`).

---

## Repo hygiene

- `.cursor/rules/elements-layer.mdc` — Go/templ boundaries for Elements.
- **This folder (`.project/`)** — project metadata; **APG/JS roadmap** = this file.
