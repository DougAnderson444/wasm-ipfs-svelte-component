<script>
  import wasm from "../rust/Cargo.toml";

  async function loadWasm() {
    const exports = await wasm();

    console.log({ exports });
    // Use functions which were exported from Rust...
  }
  loadWasm();
</script>

<main>
  <h1>Recrypt Component! Open the console.</h1>
</main>
