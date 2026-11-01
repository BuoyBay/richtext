---
title: "richtext typed API"
summary: "Source-derived public signatures, properties, parameters, defaults, and return values."
category: "Reference"
order: 21
types: ["TextRange"]
dependencies: []
symbols: ["TextRange"]
related: ["api.md", "getting-started.md", "index.md"]
---

# richtext typed API

Generated from the package source declarations. Platform guards are shown where present; inherited members are documented on the base type. See the [API contracts](api.md) for behavior and limitations.

## RichText functions

### RichTextSupported

`Public Function RichTextSupported() As Boolean`

No parameters.

#### Returns

| Type |
| --- |
| `Boolean` |

### EncodeRTF

`Public Function EncodeRTF(text As String) As Bytes`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `text` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Bytes` |

### DecodeRTF

`Public Function DecodeRTF(data As Bytes) As String`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `data` | `Bytes` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `String` |

## TextRange

`Sequential Structure TextRange`

### Fields

| Name | Type | Value / Default | Description |
| --- | --- | --- | --- |
| `Location` | `Integer` | — | — |
| `Length` | `Integer` | — | — |
