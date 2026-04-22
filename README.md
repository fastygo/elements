# FastyGo Elements

**Official repository:** [github.com/fastygo/elements](https://github.com/fastygo/elements)

## Why Elements exists

[**UI8Kit**](https://github.com/fastygo/ui8kit) ships a **self-contained minimum**: Go/templ primitives, layout grammar, token-based styling, and a **small set** of browser behaviors (`accordion`, `combobox`, `dialog`, `tabs`, `tooltip`, …). That is enough to build UIs, but not enough to cover **every** [WAI-ARIA APG](https://www.w3.org/WAI/ARIA/apg/patterns/) pattern or every **complex widget** (menus, tree, grid keyboard model, disclosure, carousel, …) without bloating the kit.

[**Blocks**](https://github.com/fastygo/blocks) and **applications** need **reusable, stable widgets** with clear contracts — not page-specific markup scattered across products.

**Elements** sits **between** UI8Kit and Blocks:

| Layer | Responsibility |
|-------|----------------|
| **UI8Kit** | Atoms + neutral composites; **Go** primitives and **minimal** `ui8kit` JS. |
| **Elements** (this repo) | **Reusable widgets** — behavior + composition; **JS** extends `ui8kit` with **APG-aligned** patterns where the kit stops. |
| **Blocks** | Page organisms; may compose Elements + UI8Kit directly. |
| **App** | Brand, routes, data, one-off screens. |

So: **Elements exists so complexity and ARIA-heavy behavior live in one place**, with a stable API, instead of duplicating logic across blocks or apps.

---

## Standards (defaults)

- **Widgets, not scenes.** Elements encode **reusable controls** (date picker shell, menu pattern, modal shell, data table keyboard region). **Hero CTAs, marketing layout, campaign copy** belong in **Blocks** or **app** — not here.
- **Dependencies:** Elements may depend on **UI8Kit** only — not on Blocks. See [`.cursor/rules/elements-layer.mdc`](.cursor/rules/elements-layer.mdc).
- **Go / templ:** Match UI8Kit conventions — variants and props, no raw utility-class strings in library templates; semantic CSS where needed (`el-*` when you own a class).
- **JavaScript:** Ship **`Elements/js`** that assumes **`ui8kit` is loaded first**; add **new** `window.ui8kit.*` (or a thin `elements` namespace delegating to it) for APG patterns **not** covered by `UI8Kit/js`. Roadmap: [`.project/APG-JS-ROADMAP.md`](.project/APG-JS-ROADMAP.md).
- **Quality:** Widget-scoped linting and a11y (e.g. ESLint on JS, axe on fixtures). Full-page and app flows are validated in **Blocks** or **apps**. See [`.project/VALIDATION-AND-TOOLING.md`](.project/VALIDATION-AND-TOOLING.md).

---

## UI8Kit in one sentence

**Go:** typed primitives (`Button`, `Box`, `Card`, `Field`, …) and helpers — **tokens and structure**, not product chrome.  
**JS:** a **small** `window.ui8kit` surface for patterns already in the kit — **not** a full copy of every W3C APG widget.

## Elements in one sentence

**Go (future):** compositional templ components built only from UI8Kit.  
**JS:** the **rest of the APG behavioral surface** the product stack needs, implemented once and reused — aligned with [APG](https://www.w3.org/WAI/ARIA/apg/patterns/), not a fork of the APG repo’s own CI toolchain.

---

## Project metadata

| Path | Purpose |
|------|---------|
| [`.project/APG-JS-ROADMAP.md`](.project/APG-JS-ROADMAP.md) | APG pattern parity: UI8Kit vs Elements backlog |
| [`.project/VALIDATION-AND-TOOLING.md`](.project/VALIDATION-AND-TOOLING.md) | Linting / a11y split across Elements, Blocks, apps |

---

## FastyGo stack

| Repository | Role |
|------------|------|
| [**framework**](https://github.com/fastygo/framework) | Core framework and examples |
| [**ui8kit**](https://github.com/fastygo/ui8kit) | Go/templ primitives + minimal `ui8kit` JS |
| [**elements**](https://github.com/fastygo/elements) | Reusable widgets + APG-oriented JS (this repo) |
| [**blocks**](https://github.com/fastygo/blocks) | Page-level organisms |

---

## License

This project is licensed under the **MIT License** — see [`LICENSE`](LICENSE).