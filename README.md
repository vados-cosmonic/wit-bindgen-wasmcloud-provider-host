# `wit-bindgen-wasmcloud-provider-host`

This crate contains a macro that builds [Wasmcloud Capability Providers][wasmcloud-capability-providers] that work with the [WIT][wit] ecosystem by leveraging [`wit-bindgen`][wit-bindgen]-like (and in this case, [`wasmtime::component::bindgen`][wasmtime-component-bindgen]).

## Usage

This crate can be be used by calling `wit-bindgen-wasmcloud` *in place* of `wit-bindgen`, with the following syntax:

```rust
wit_bindgen_wasmcloud_provider_host::generate!(
    YourProvider,
    "wasmcloud:contract",
    "your-world"
);

/// Implementation that you will contribute
struct YourProvider;

impl Trait for YourProvider {
  ...
}
```

Note that arguments after the second fed directly to `wasmtime::component::bindgen`. For example, to build a provider for the [wasmCloud keyvalue WIT interface][wasmcloud-keyvalue]:

```rust
/// Generate bindings for a wasmCloud provider
wit_bindgen_wasmcloud::provider::host::generate!(
    MyKeyvalueProvider,
    "wasmcloud:keyvalue",
    "keyvalue"
);
```

> **Warning**
> You'll need to have the appropriate WIT interface file (ex. `keyvalue.wit`) in your crate root, at `<crate root>/wit/keyvalue.wit`

For more details on how the WIT ecosystem and `wit-bindgen`/`wasmtime::component::bindgen` work, see:

- [the `wit-bindgen` repository][wit-bindgen]
- [`wasmtime/crates/component-macro`][wasmtime-component-macro] respectively.

[wit-bindgen]: https://github.com/bytecodealliance/wit-bindgen
[wasmtime-component-macro]: https://github.com/bytecodealliance/wasmtime/blob/main/crates/component-macro
[wasmcloud-capability-providers]: https://wasmcloud.com/docs/fundamentals/capabilities/
[wit]: https://github.com/WebAssembly/component-model/blob/main/design/mvp/WIT.md
[wasmtime-component-bindgen]: https://docs.rs/wasmtime/latest/wasmtime/component/macro.bindgen.html
[wasmcloud-keyvalue]: https://github.com/wasmCloud/interfaces/blob/main/wit/keyvalue.wit
