# Provenance and compatibility

Idea/source reference: [VNS XLSX Reader](https://github.com/JYPochez/VNS-XLSX-Reader),
inspected at commit `e4cde6a32885d34e50eb25de4a053e8b646b3b76`.
Its root MIT license is retained in `UPSTREAM-LICENSE.txt` for reference. The Buoy
implementation and test fixtures were written independently; no Xojo source,
application artwork or workbook assets were copied.

The inspected `Common/XLSXReader.xojo_code` reads shared strings, workbook
relationships and sheets, while `XLSXCell`, `XLSXSheet` and the larger source tree
supply formatting/editing and related behavior. The current upstream README
also advertises ODS, roundtrip writes, styles, tables, formula authoring and
Desktop/Web UIs. SpreadsheetKit intentionally begins with bounded read-only XLSX
values, normal formula text/caches and sparse lookup. It does not claim those
larger features.

OOXML part relationships and XML namespaces are parsed as data through Buoy's
bundled ZIP/XML APIs. Fixtures are independently constructed with Python's
`zipfile`; their expected typed values and malformed cases are asserted by the
Buoy consumer. No Excel/LibreOffice execution is required or claimed.
