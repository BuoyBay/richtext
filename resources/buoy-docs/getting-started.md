---
title: "RTF conversion getting started"
summary: "Install richtext and use its native API with explicit ownership."
category: "Guides"
order: 10
keywords: ["rtf", "unicode", "rich text", "conversion"]
related: ["index.md", "api.md", "typed-api.md"]
---

# Getting started

Copy `richtext-0.1.0.buipkg` into your project’s `packages/` directory and import `richtext`. This example performs an in-memory round trip. Encoding starts from plain text, so the decoded result contains the same text rather than a rich formatting model.

```buoy
Import richtext

Sub Main()
    If Not RichTextSupported() Then Exit Sub
    Dim encoded As Bytes = EncodeRTF("Hello, Buoy")
    Dim decoded As String = DecodeRTF(encoded)
    Print decoded
End Sub
```

## Handle native constraints

`DecodeRTF` rejects Nil and empty data with `InvalidArgumentException`, and invalid native RTF also throws. Check support before converting and handle exceptions at the import boundary when processing user-supplied data. Formatting is intentionally not preserved as an editable object model.

## Keep the current document when an import is rejected

Decode into a candidate value before replacing application state. This example uses empty input to demonstrate recovery; pass the bytes read from the selected file for an actual import. The capability check keeps the current document on Windows and Linux. On macOS, Nil, empty input, or input rejected by the native RTF decoder raises `InvalidArgumentException`, which this helper handles. Other exceptions propagate so an unexpected failure is not reported as invalid input.

```buoy
Import richtext

Function ImportRTFOrKeep(data As Bytes, currentText As String) As String
    If Not RichTextSupported() Then
        Print "RTF import requires macOS; the existing text was kept."
        Return currentText
    End If
    Try
        Return DecodeRTF(data)
    Catch e As InvalidArgumentException
        Print "RTF import rejected the data; the existing text was kept."
        Return currentText
    End Try
End Function

Sub Main()
    Dim currentText As String = "Unsaved draft"
    Dim incoming As New Bytes()
    currentText = ImportRTFOrKeep(incoming, currentText)
    If currentText <> "Unsaved draft" Then Throw New Exception("Draft was lost")
    Print currentText
End Sub
```

Only update the editor text and reset its selection or undo history after your application has accepted a successful decode. A decoded empty string can be valid document content, so do not use an empty result as a failure sentinel. If your UI needs a separate success flag, keep the decode and state assignment in the same `Try` block instead of using this text-only helper. Conversion does not preserve formatting or change the clipboard or the source file.

[Package overview](index.md) · [API reference](api.md)
