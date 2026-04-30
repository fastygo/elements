# Commerce Elements

Copy this package as source when an application needs commerce controls.

Copy:

- `quantity_stepper.templ`
- `price_range.templ`

Do not copy generated files:

- `*_templ.go`

After copying, run `templ generate ./...` and `.ui8px` checks in the destination app.

The package depends only on UI8Kit.
