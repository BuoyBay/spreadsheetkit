# Read XLSX workbooks into sparse typed cells

A read-only XLSX workbook package for importers, table viewers and conversion
utilities. `Import spreadsheetkit` uses the bundled `zip.Zip` and `xml.XML`
packages; no Excel installation, shell extraction or spreadsheet process is used.

## Install

From a Buoy consumer project with BPM installed:

```sh
bpm add spreadsheetkit --git https://github.com/BuoyBay/spreadsheetkit.git --rev refs/heads/main
```

BPM records the resolved commit in its lockfile. Keep that lockfile with the
consumer project for reproducible installs.

## API at a glance

- `workbook.Sheets`: ordered defensive copy of the sheet array.
- `sheet.Name`, `sheet.CellCount`, `sheet.Cells`: name, stored-cell count and a
  defensive array copy. Cells retain file order; they are not sorted or densified.
- `sheet.Cell(row, column)`: `Optional Of XLSXCell`, using **one-based** coordinates
  in `1..1048576` by `1..16384`. Missing coordinates return `None`.
- `cell.Row`, `Column`, `Kind`, `Text`, `Formula`: immutable data. `Kind` is one of
  `string`, `number`, `boolean`, `error`, `blank`, or `date-text`. `Text` is raw
  decoded content, not formatted display text. `Formula` has no leading `=`.

## Build from source

With the native `build-packages` driver from [devtools](https://github.com/BuoyBay/devtools)
on your `PATH`, run from this checkout:

```sh
build-packages --root "$PWD" --compile-consumer spreadsheetkit
```

The driver checks source targets and compiles an import consumer. See the
[API guide](docs/API.md) for behavior, limits and any host prerequisites.

## Local Buoy setup

On your own machine, install Buoy and run:

```sh
buoy ai init --both
```

## Contributing

[Contributing](CONTRIBUTING.md) · [License](LICENSE)
