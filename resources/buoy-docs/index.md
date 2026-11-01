---
title: "RTF conversion"
summary: "Convert Unicode text to RTF bytes and flatten RTF back to text."
category: "Overview"
order: 0
keywords: ["rtf", "unicode", "rich text", "conversion"]
related: ["getting-started.md", "api.md", "typed-api.md"]
---

# RTF conversion

The `richtext` package converts plain Unicode strings into native RTF bytes and decodes RTF into plain Unicode text. Decoding deliberately flattens formatting. It does not read or write files, change the clipboard, import HTML, or support RTFD and embedded file attachments.

## Platform support

Native conversion requires macOS. `RichTextSupported()` returns False on Windows and Linux, where conversion operations throw `UnsupportedOperationException`.

## Ownership and lifetime

Each operation releases its native attributed-string and data objects before returning. Callers own the returned Buoy `Bytes` or `String`; there is no converter object to retain or close.

## Read next

- [Getting started](getting-started.md)
- [API reference](api.md)
