title
Welcome to this week in Rust and WebAssembly!
Hello and welcome to the first issue of This Week in Rust and WebAssembly!

Rust is a systems language pursuing the trifecta: safety, concurrency, and speed.

WebAssembly is designed as a portable target for compilation of high-level languages like C, C++, and Rust, enabling deployment on the web for client and server applications.

This is a weekly summary of its progress and community.

Tweet us at @rustwasm or send us a pull request. Want to get involved? We love contributions!

News and Releases

The lld linker landed in nightly Rust! Expect faster .wasm compilation, smaller .wasm binaries when using lto = true, support for custom .wasm sections, and more.

wasm-pack packs up the .wasm and publishes it to npm

The goal of this project is to create a portable command line tool for publishing compiled wasm projects to the npm registry for the consumption of js devs using the npm CLI, yarn, or any other CLI tool that interfaces with the npm registry.
rust-dominator is a zero-cost virtual DOM library. It even already has a spec-compliant TODO-MVC implementation!

Kovan is an Ethereum-like testnet.

Tutorial
Talks
wasm-sign is a WebAssembly signing and verification tool.

edit-text is a collaborative text editor built with Rust and WebAssembly.

wasm_bindgen 0.2.0 released

Uses the new #[wasm_custom_section] attribute to produce by-default smaller binaries
JS output is by default compatible with either Node.js or the browser
The --nodejs flag's output is now natively usable by Node.js, aka uses require and loads the WebAssembly module synchronously
Lots of internal refactorings in preparation for new features like closures and futures
wee_alloc 0.2.0 released

Articles, Blog Posts, and Talks

Come Join the Rust and WebAssembly Working Group!

Making WebAssembly better for Rust & for all languages- Lin Clark

JavaScript to Rust and Back Again: A wasm-bindgen Tale

Speed Without Wiza
