# Validation, linting, and where quality checks live

Not everything that touches accessibility or HTML quality belongs in **Elements**. Some checks only make sense **after composition** (Blocks) or in the **running application** (real routes, auth, data). Split responsibilities to avoid duplicated CI and false expectations.

---

## Spec vs tooling

- **W3C [APG](https://www.w3.org/WAI/ARIA/apg/patterns/)** and the **[w3c/aria-practices](https://github.com/w3c/aria-practices)** repository are the **authoritative behavior and markup reference**. Use them for design, keyboard tables, and manual review — **not** as a drop-in npm dependency for Elements.
- **`packages-w3c.json`** in this repo mirrors APG’s own `package.json` (ESLint, HTMLHint, vnu, AVA + Selenium for **their** examples and docs). **Do not** adopt that whole stack verbatim as “Elements validation”: paths, file types, and goals differ (APG content vs your Go/templ + JS widgets).

---

## Recommended tooling (Elements)

Keep CI **narrow and relevant** to code under `Elements/`:

| Tool | Use in Elements |
|------|-------------------|
| **ESLint** (+ Prettier if desired) | `Elements/js` — style, obvious footguns, optional small a11y hints where applicable. |
| **axe-core** (CLI or test runner) | Scan **fixed HTML/DOM fixtures** or minimal pages that render Element widgets in isolation. This catches many real a11y issues better than generic HTML lint alone. |
| **vnu** (Nu Html Checker) | Optional: validate **rendered** HTML snippets for documents you treat as full pages or large fragments. |

Avoid pulling the **entire** APG devDependency tree (cspell over all APG files, their regression matrix, link-checkers for W3C site) into Elements — that is maintenance for **their** repo, not yours.

---

## Layering: who validates what

### Elements (this repo)

- **Widget contracts:** roles, keyboard behavior, focus management, `aria-*` for patterns implemented in **`Elements/js`** (and matching templ/markup when added).
- **Unit-level / fixture-level checks:** golden DOM or small harness pages + **axe** (and optional **vnu** on representative output).
- **Not responsible for:** full page landmarks composition, route-level flows, app-specific copy, or brand-only CSS regressions.

### Blocks

- **Composition:** multiple widgets + layout; integration issues (e.g. two dialogs, focus return between block sections).
- **Add:** integration tests or axe scans on **block-level** fixtures (templates that compose Elements + UI8Kit).
- **Still not:** production-only concerns (logged-in states, i18n edge cases) unless the block ships a generic pattern.

### Applications

- **End-to-end reality:** real URLs, data loading, auth, toasts, third-party embeds, locale switching.
- **Add:** E2E + axe (or similar) on critical user paths; manual keyboard passes on shipped pages.
- **Brand / marketing CSS** may live here — visual regression tools belong at app level if needed.

---

## Practical rule

If a check needs **full page context** or **app-specific data**, it belongs in **Blocks** or **Apps**, not only in Elements. Elements should stay **fast, stable, and widget-scoped** so failures map clearly to a single pattern implementation.

---

## Related docs in `.project/`

- **`APG-JS-ROADMAP.md`** — which APG patterns are covered by `UI8Kit/js` vs backlog for `Elements/js`.
