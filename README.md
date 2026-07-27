# decode

Composable, type-safe decoders for Ard `Any` values, heavily inspired by Gleam's [`gleam/dynamic/decode`](https://hexdocs.pm/gleam_stdlib/gleam/dynamic/decode.html) module.

`decode` parses JSON into Ard's opaque `Any` type and provides primitive decoders and combinators that turn those values into typed data with path-aware errors.

## Requirements

- Ard 0.28.0 or newer

## Installation

Add the repository as an Ard dependency:

```sh
ard add github.com/akonwi/ard-decode@latest as decode
```

Then import the module:

```ard
use decode
```

For local development, add a path dependency to `ard.toml`:

```toml
[dependencies]
decode = { path = "../decode" }
```

## Usage

```ard
use decode

fn title_from_json(text: Str) Str!Error {
  decode::unmarshal(text, decode::field("title", decode::string))
}
```

`unmarshal` is the high-level API: it parses JSON and applies the decoder in one call. The lower-level `from_json` and `run` functions remain available when an untyped value needs to be decoded more than once.

Decoders can be composed for nested and optional values:

```ard
let names = decode::path(
  ["user", "names"],
  decode::list(decode::string),
)

let nickname = decode::field(
  "nickname",
  decode::nullable(decode::string),
)
```

## API

Primitive decoders:

- `string`
- `int`
- `float`
- `boolean`
- `any`

Combinators:

- `field`
- `path`
- `list`
- `nullable`

Utilities:

- `unmarshal` parses JSON and applies a decoder, returning Ard's built-in `Error`
- `from_json` parses JSON text into `Any`
- `run` applies a decoder to an `Any` value
- `Err.to_str()` formats decode failures with their nested path

## Development

```sh
ard format .
ard test
```
