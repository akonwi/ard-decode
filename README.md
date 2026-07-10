# decode

Composable, type-safe decoders for Ard `Any` values.

`decode` parses JSON into Ard's opaque `Any` type and provides primitive decoders and combinators that turn those values into typed data with path-aware errors.

## Requirements

- Ard 0.26.0 or newer
- Go target (JSON parsing uses Go's `encoding/json` package)

## Installation

Add the repository as an Ard dependency:

```sh
ard add <repository-url>@<tag-or-commit> as decode
```

Then import the module:

```ard
use decode/decode
```

For local development, add a path dependency to `ard.toml`:

```toml
[dependencies]
decode = { path = "../decode" }
```

## Usage

```ard
use decode/decode

fn title_from_json(text: Str) Str!Str {
  let data = try decode::from_json(text)
  decode::run(data, decode::field("title", decode::string)) -> err {
    Result::err(err.to_str())
  }
}
```

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

- `from_json` parses JSON text into `Any`
- `run` applies a decoder
- `Error.to_str()` formats failures with their nested path

## Development

```sh
ard format --check .
ard test
```
