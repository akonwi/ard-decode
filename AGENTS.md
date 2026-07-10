# AGENTS.md

## Project

`decode` is a small Ard library for decoding opaque `Any` values into typed values with composable, path-aware errors. It requires Ard 0.26.0 or newer and targets Go because JSON parsing uses `go:encoding/json`.

## Layout

- `decode.ard`: public library module
- `decode_test.ard`: public behavior tests
- `ard.toml`: package metadata and minimum Ard version

## Development

Run before committing:

```sh
ard format --check .
ard test
```

Keep the library dependency-free apart from Ard's standard library and Go's standard library. Preserve the existing decoder signatures and path-aware error behavior unless intentionally making a documented API change. Add tests for every behavior change.
