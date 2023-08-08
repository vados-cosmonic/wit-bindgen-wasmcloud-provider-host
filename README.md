# `wit-bindgen-wasmcloud-provider-host`

This crate contains a macro that builds [Wasmcloud Capability Providers][wasmcloud-capability-providers] that work with the [WIT][wit] ecosystem by leveraging [`wit-bindgen`][wit-bindgen]-like (and in this case, [`wasmtime::component::bindgen`][wasmtime-component-bindgen]).

## Usage

This crate can be be used by calling `wit-bindgen-wasmcloud` *in place* of `wit-bindgen`, with the following syntax:

```
...generate!(<implementation struct name>, <wasmcloud countract>, ...<arguments to wasmtime::component::bindgen>)
```

To illustrate:

```rust
/// Generate bindings for a wasmCloud provider
wit_bindgen_wasmcloud::provider::host::generate!(MyKeyvalueProvider, "wasmcloud:keyvalue", "keyvalue");
```

Note that the third argument onwards are fed directly to `wasmtime::component::bindgen` -- in this case, they indicate the name of an existing `wit` file (`"keyvalue.wit"`) that is expected to exist at the `<crate root>/wit/keyvalue.wit`.

For more details on how the WIT ecosystem and `wit-bindgen`/`wasmtime::component::bindgen` work, see [the `wit-bindgen` repository][wit-bindgen] and [`wasmtime/crates/component-macro`][wasmtime-component-macro] respectively.

[wit-bindgen]: https://github.com/bytecodealliance/wit-bindgen
[wasmtime-component-macro]: https://github.com/bytecodealliance/wasmtime/blob/main/crates/component-macro
[wasmcloud-capability-providers]: https://wasmcloud.com/docs/fundamentals/capabilities/
[wit]: https://github.com/WebAssembly/component-model/blob/main/design/mvp/WIT.md
