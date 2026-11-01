---
title: "spreadsheetkit typed API"
summary: "Source-derived public signatures, properties, parameters, defaults, and return values."
category: "Reference"
order: 21
types: ["XLSXCell", "XLSXSheet", "XLSXWorkbook"]
dependencies: []
symbols: ["XLSXCell", "XLSXSheet", "XLSXWorkbook"]
related: ["api.md", "getting-started.md", "index.md"]
---

# spreadsheetkit typed API

Generated from the package source declarations. Platform guards are shown where present; inherited members are documented on the base type. See the [API contracts](api.md) for behavior and limitations.

## XLSXCell

`Public Class XLSXCell`

Immutable sparse cell. Coordinates are one-based; Text is the decoded raw value.

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Row` | `Integer` | Yes | No | — | — |
| `Column` | `Integer` | Yes | No | — | — |
| `Kind` | `String` | Yes | No | — | — |
| `Text` | `String` | Yes | No | — | — |
| `Formula` | `String` | Yes | No | — | — |

### Constructor

`Public Sub Constructor(row As Integer, column As Integer, kind As String, text As String, formula As String)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `row` | `Integer` | `ByVal` | Required |
| `column` | `Integer` | `ByVal` | Required |
| `kind` | `String` | `ByVal` | Required |
| `text` | `String` | `ByVal` | Required |
| `formula` | `String` | `ByVal` | Required |

Returns: no value.

### NumberValue

`Public Function NumberValue() As Double`

No parameters.

#### Returns

| Type |
| --- |
| `Double` |

## XLSXSheet

`Public Class XLSXSheet`

Immutable sheet. Missing coordinates return None, distinct from an explicit blank cell.

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Name` | `String` | Yes | No | — | — |
| `Cells` | `Array Of XLSXCell` | Yes | No | — | — |
| `CellCount` | `Integer` | Yes | No | — | — |

### Constructor

`Public Sub Constructor(name As String, cells As Array Of XLSXCell)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `name` | `String` | `ByVal` | Required |
| `cells` | `Array Of XLSXCell` | `ByVal` | Required |

Returns: no value.

### Cell

`Public Function Cell(row As Integer, column As Integer) As Optional Of XLSXCell`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `row` | `Integer` | `ByVal` | Required |
| `column` | `Integer` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Optional Of XLSXCell` |

## XLSXWorkbook

`Public Class XLSXWorkbook`

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Sheets` | `Array Of XLSXSheet` | Yes | No | — | — |

### Constructor

`Public Sub Constructor(sheets As Array Of XLSXSheet)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `sheets` | `Array Of XLSXSheet` | `ByVal` | Required |

Returns: no value.

## SpreadsheetKit functions

### ReadXLSX

`Public Function ReadXLSX(filePath As String, maxPartBytes As Integer = 8388608, maxTotalBytes As Integer = 33554432, maxCells As Integer = 100000, maxSheets As Integer = 128) As XLSXWorkbook`

Read transitional OOXML XLSX without extracting files or evaluating formulas.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `filePath` | `String` | `ByVal` | Required |
| `maxPartBytes` | `Integer` | `ByVal` | `8388608` |
| `maxTotalBytes` | `Integer` | `ByVal` | `33554432` |
| `maxCells` | `Integer` | `ByVal` | `100000` |
| `maxSheets` | `Integer` | `ByVal` | `128` |

#### Returns

| Type |
| --- |
| `XLSXWorkbook` |
