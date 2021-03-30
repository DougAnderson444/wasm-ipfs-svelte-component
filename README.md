# Rust-Wasm in a Svelte component

Powered by [@wasm-tool/rollup-plugin-rust](https://www.npmjs.com/package/@wasm-tool/rollup-plugin-rust), all that you need to do to add a bit of rust into your front end code is require the `Cargo.toml`

## Use Rust methods in JS file

```js
// mycode.js
import wasm from "./path/to/Cargo.toml";
 
async function loadWasm() {
    const exports = await wasm();
 
    // Use functions which were exported from Rust...
}
```
## Rollup.config.js

In order to be able to import this, we need to add the `@wasm-tool` to the rollup.config file. 

Normally this will bundle the Rust code into a wasm file. If we did that, we'd have to copy the .wasm file into the project that consumes this component, which isn't convenient. So  since we want to bundle the whole thing into a svelte component easy for the consumer to use, to bundle everything together in our component's source, we add the `inline` option.

This `inline` option pastes the base64 wasm code right into the js file. It makes it a bit bigger (33% bigger) but that's the tradeoff for convenience:

```js
import rustPlugin from "@wasm-tool/rollup-plugin-rust";
 
export default {
    input: {
        foo: "Cargo.toml",
    },
    plugins: [
        rustPlugin({
            inlineWasm: true
        }),
    ],
};
```

## Build

Put the `rust()` plugin first so it builds the wasm code first and then includes it in the component
