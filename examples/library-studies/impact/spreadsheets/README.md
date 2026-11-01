# Spreadsheet import example

This console importer prints sheet names and sparse typed cells. Formulas are
shown with their cached values and are never evaluated. It does not modify the
workbook or implement a styled spreadsheet editor.

From this directory, run `bpm install`. Place the ZIP and XML archives from your
installed Buoy toolchain in `packages/`, then build and supply an XLSX filename:

```sh
mkdir -p dist
bpm build main.bui -o dist/example
./dist/example workbook.xlsx
```

The [package API](../../../../docs/API.md) describes the supported XLSX profile,
resource limits and remaining format differences.
