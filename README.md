# nib-plugin-example

An example plugin for [nib](https://github.com/nib-editor/nib), written in Go with its [Go SDK](https://github.com/nib-editor/nib/tree/main/sdk/go). It shows how many words the shown buffer has in the status line, and answers the `wordcount.count` command with the number.

## Install

```sh
nib plugin add nib-editor/plugin-example
```

It needs no capabilities. It loads the next time nib starts.

## Build

You need [TinyGo](https://tinygo.org/) 0.42 or later (with Go 1.25 to 1.27), binaryen's `wasm-opt`, and [wasm-tools](https://github.com/bytecodealliance/wasm-tools).

```sh
tinygo build -target=wasip2 \
  --wit-package "$(go list -m -f '{{.Dir}}' github.com/nib-editor/nib/sdk/go)/wit" \
  --wit-world plugin -o plugin.wasm .
```

Try the build without installing it with `nib --plugin .`.

## Release

Set `version` in `plugin.toml`, then push a tag of the same version:

```sh
git tag v0.1.0 && git push origin v0.1.0
```

The [release workflow](.github/workflows/release.yml) builds the plugin and publishes `wordcount-0.1.0.nib.tar.gz`, which `nib plugin add` and `nib plugin update` look for.

## License

MIT
