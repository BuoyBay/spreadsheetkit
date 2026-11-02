# SpreadsheetKit 0.1.0

A read-only XLSX workbook package for importers, table viewers and conversion
utilities. `Import spreadsheetkit` uses the bundled `zip.Zip` and `xml.XML`
packages; no Excel installation, shell extraction or spreadsheet process is used.

## API

`ReadXLSX(filePath, maxPartBytes = 8388608, maxTotalBytes = 33554432,
maxCells = 100000, maxSheets = 128)` returns an `XLSXWorkbook`, or throws on a
malformed, unsupported or over-limit input. ZIP/XML runtime errors may propagate
as their original exception types. The archive is closed in `Finally` on both
success and failure.

- `workbook.Sheets`: ordered defensive copy of the sheet array.
- `sheet.Name`, `sheet.CellCount`, `sheet.Cells`: name, stored-cell count and a
  defensive array copy. Cells retain file order; they are not sorted or densified.
- `sheet.Cell(row, column)`: `Optional Of XLSXCell`, using **one-based** coordinates
  in `1..1048576` by `1..16384`. Missing coordinates return `None`.
- `cell.Row`, `Column`, `Kind`, `Text`, `Formula`: immutable data. `Kind` is one of
  `string`, `number`, `boolean`, `error`, `blank`, or `date-text`. `Text` is raw
  decoded content, not formatted display text. `Formula` has no leading `=`.
- `cell.NumberValue()`: parses a `number` cell as finite Double; other kinds reject.

Explicit blank cells are retained and differ from missing coordinates. Boolean
text is `0` or `1`; errors retain text such as `#DIV/0!`. Numeric lexical text is
retained, so consumers may choose their own precision. `NumberValue()` uses Double
and may lose decimal precision or underflow. ISO date cells (`t="d"`) retain
uninterpreted text. Excel date serials stay numbers because styles are not read.
Formula text and its cached value are retained independently; **no formula is
evaluated**. A formula without a cached value yields a `blank` kind plus formula.

## Supported XLSX subset

The reader resolves the package's office-document relationship, workbook sheet
relationships and shared-string relationship. It supports relative parent steps
and archive-absolute targets, so parts need not be hardcoded under `xl/`.
Transitional OOXML spreadsheet and relationship namespaces are required.

Shared strings, direct inline strings and rich-string run text are decoded;
rich-text formatting and phonetic annotations are not retained. Cells must have
explicit A1 references and their rows explicit `r` indices. Duplicate cells and
ZIP entries, missing relationships, invalid shared indices, unsupported cell
types, nonfinite numbers and shared/array/data-table formula encodings reject.

This is a focused import API. ODS, legacy XLS, XLSX writing/editing, formula
calculation, style/number formatting, merged-cell semantics, table styles,
hyperlinks, charts, images, hidden-sheet state and full upstream compatibility
remain outside its contract. Unused parts and extension markup are ignored; no
macro or external hyperlink is executed or loaded.

## Bounds and input handling

At most 4096 ZIP entries are enumerated. Declared uncompressed sizes for **all**
entries must fit `maxTotalBytes`. Every loaded XML part must fit `maxPartBytes`,
and the sum of loaded XML sizes must also fit `maxTotalBytes`. After extraction,
actual byte count must match metadata before text decoding. `maxCells` bounds
stored cells across all sheets and also bounds shared-string count. `maxSheets`
bounds sheet count. Configurable ceilings are 64 MiB per part, 256 MiB total,
1,000,000 cells and 1024 sheets; lower limits are recommended for small imports.

**Allocation limitation:** the bundled ZIP API extracts an entire entry into
memory before returning it. The post-extraction actual-size check is not a hard
memory limit against forged ZIP metadata or decompression bombs. XML parsing also
builds a complete DOM before cell-count checks. Use process-level resource limits
or a separate restricted importer process for hostile archives; this package does
not claim constant-memory or streaming validation.

No files are extracted to disk. Part names reject traversal segments and
unsupported backslash/colon/percent forms. Relevant workbook/sheet/shared-string
relationships reject external targets or root escapes. XML DTD/entity declarations
and NUL-containing UTF-16/32 source are rejected before parsing; the parser is
namespace-aware with external entities disabled. This subset expects UTF-8 XML.

## Packaging and verification

Seal with `/usr/bin/buoy pkg seal . -o
packages/spreadsheetkit-0.1.0.buipkg`. Consumers need the installed ZIP and XML
archives in their `packages/` directory as well. On this host those are
`zip-4.0.7.buipkg` and `xml-1.0.0.buipkg` under `/usr/share/buoy/packages`.

See [provenance](../PROVENANCE.md) and the [console importer](../examples/library-studies/impact/spreadsheets/main.bui).
