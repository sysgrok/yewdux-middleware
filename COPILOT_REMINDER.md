# Copilot CI Reminder

Before submitting any PR or pushing changes, always run the complete CI workflow locally to ensure the build passes:

## CI Steps (from `.github/workflows/ci.yml`)

1. **Format Check**
   ```bash
   cargo fmt -- --check
   ```

2. **Add wasm target** (if not already added)
   ```bash
   rustup target add wasm32-unknown-unknown
   ```

3. **Clippy (with warnings as errors)**
   ```bash
   cargo clippy --no-deps --target wasm32-unknown-unknown -- -Dwarnings
   ```

4. **Build main crate**
   ```bash
   cargo build --target wasm32-unknown-unknown
   ```

5. **Build macros crate**
   ```bash
   cargo build -p yewdux-middleware-macros
   ```

## Quick Check Script

Run all CI steps in sequence:
```bash
cargo fmt -- --check && \
rustup target add wasm32-unknown-unknown && \
cargo clippy --no-deps --target wasm32-unknown-unknown -- -Dwarnings && \
cargo build --target wasm32-unknown-unknown && \
cargo build -p yewdux-middleware-macros
```

## Important Notes

- Always run these checks before committing
- Fix any warnings or errors before pushing
- The CI enforces `-Dwarnings` for clippy, so all warnings must be resolved
- Tests should also be run when making functional changes: `cargo test --lib`
