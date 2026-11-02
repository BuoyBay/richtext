# RTF encode and extract

`Import richtext`. `EncodeRTF(text)` returns native RTF bytes; `DecodeRTF(data)` returns plain Unicode text. Formatting is deliberately flattened on decode. RTFD, embedded files and HTML import are outside this package. No clipboard or files are changed. Invalid/empty data throws. NSAttributedString and data objects are released before each operation returns.

These native operations require macOS; `RichTextSupported()` returns False on Windows/Linux, and unsupported operations throw rather than silently emulating an Apple API. All six compiler targets are checked; native execution is verified on macOS arm64.

## Install

From a Buoy consumer project with BPM installed:

```sh
bpm add richtext --git https://github.com/BuoyBay/richtext.git --rev refs/heads/main
```

BPM records the resolved commit in its lockfile. Keep that lockfile with the
consumer project for reproducible installs.

## Example

```basic
Import richtext

Sub Main()
    If Not RichTextSupported() Then Exit Sub
    Dim encoded As Bytes = EncodeRTF("Hello, Buoy")
    Dim decoded As String = DecodeRTF(encoded)
    Print decoded
End Sub
```

## Build from source

With the native `build-packages` driver from [devtools](https://github.com/BuoyBay/devtools)
on your `PATH`, run from this checkout:

```sh
build-packages --root "$PWD" --compile-consumer richtext
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
