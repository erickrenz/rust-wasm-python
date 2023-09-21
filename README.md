# WASM = Rust + Python

This is an example of how to create a library using `rust`, compile it to `wasm`, and use it within a `python` project.

## Rust

0. install wasmer

```bash
curl https://get.wasmer.io -sSfL | sh
```

1. update `cargo.toml`:
```toml
[lib]
crate-type = ["lib", "cdylib"]
```

2. build release target arch
```bash
rustup target add wasm32-unknown-unknown
cargo build --target wasm32-unknown-unknown --release
```

## Python

3. copy `wasm.wasm` file to the python file's directory
```bash
cp rust/target/wasm32-unknown-unknown/release/wasm.wasm . 
```

4. Install dependencies

```bash
pip install wasmer wasmer_compiler_cranelift
```

5. Run python file that uses the custom rust/wasm library

```bash
python wasm.py
```
_Note: If you get an "ImportError: Wasmer is not available on this system", you may need to use a different version of python. I was not able to run this code using Python 3.11, but it worked fine with Python 3.9 ([see github issues](https://github.com/jimkring/python-sandbox-wasm/issues/1))._

## Sources

GitHub for wasmer + rust + python tutorial: [wasmer-python/examples](https://github.com/wasmerio/wasmer-python/tree/master/examples/appendices)