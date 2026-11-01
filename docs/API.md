# RTF conversion · 0.1.0

`Import richtext`. `EncodeRTF(text)` returns native RTF bytes; `DecodeRTF(data)` returns plain Unicode text. Formatting is deliberately flattened on decode. RTFD, embedded files and HTML import are outside this package. No clipboard or files are changed. Invalid/empty data throws. NSAttributedString and data objects are released before each operation returns.

These native operations require macOS; `RichTextSupported()` returns False on Windows/Linux, and unsupported operations throw rather than silently emulating an Apple API. All six compiler targets are checked; native execution is verified on macOS arm64.

Maintainers run the private validation suite before release. See the repository README for public build instructions.

Inspired by [macoslib’s Cocoa examples](https://github.com/macoslib/macoslib); implemented independently against [Apple’s API](https://developer.apple.com/documentation/foundation/nsattributedstring).

For portable attributed text and editing, use [StyledText](https://github.com/BuoyBay/styledtext/blob/main/docs/API.md). It preserves style runs through its own binary format and imports legacy Mac `styl` data. It does not currently connect styled documents to this package’s RTF converter or to core TextArea.
