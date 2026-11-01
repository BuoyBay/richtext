---
title: "RTF conversion API"
summary: "Public symbols and contracts for the richtext package."
category: "Reference"
order: 20
keywords: ["rtf", "unicode", "rich text", "conversion"]
symbols: ["RichTextSupported", "EncodeRTF", "DecodeRTF"]
related: ["index.md", "getting-started.md", "typed-api.md"]
---

# API reference

Import `richtext` from the sealed package. The signatures below describe its public surface.

| Symbol | Contract |
| --- | --- |
| `RichTextSupported() As Boolean` | Report whether the native conversion backend is available. |
| `EncodeRTF(text As String) As Bytes` | Encode a plain Unicode string as RTF bytes. |
| `DecodeRTF(data As Bytes) As String` | Decode valid nonempty RTF bytes to plain text; flatten formatting. |

## Errors and lifecycle

`DecodeRTF` rejects Nil and empty data with `InvalidArgumentException`, and invalid native RTF also throws. Check support before converting and handle exceptions at the import boundary when processing user-supplied data. Formatting is intentionally not preserved as an editable object model.

Each operation releases its native attributed-string and data objects before returning. Callers own the returned Buoy `Bytes` or `String`; there is no converter object to retain or close.

## Platform support

Native conversion requires macOS. `RichTextSupported()` returns False on Windows and Linux, where conversion operations throw `UnsupportedOperationException`.

[Getting started](getting-started.md) · [Package overview](index.md)


[Full typed API: properties, parameters, defaults, and returns](typed-api.md)
