# Contributing to StellarForge

Thanks for your interest in contributing. This guide covers everything you need to get set up, run tests, meet code style requirements, and submit a pull request.

---

## Prerequisites & Local Setup

You will need the following tools installed before you can build or test the contracts.

### Rust

- **Edition:** 2021
- **Target:** `wasm32v1-none`

Install the required target:

```bash
rustup target add wasm32v1-none
```

If you don't have Rust installed, follow the official guide at <https://www.rust-lang.org/tools/install>.

### Stellar CLI

**v25.2.0 or higher** is required.

```bash
cargo install --locked stellar-cli
```

Full installation docs: <https://developers.stellar.org/docs/smart-contracts/getting-started/setup>

### Clone and Build

```bash
git clone https://github.com/your-org/stellarforge.git
cd stellarforge
cargo build --workspace
```

---

## Running Tests

Run the full test suite across all workspace members:

```bash
cargo test --workspace
```

Run tests for a single contract using the `-p` flag:

```bash
cargo test -p forge-governor
cargo test -p forge-multisig
cargo test -p forge-oracle
cargo test -p forge-stream
cargo test -p forge-vesting
```

All tests must pass before you submit a PR.

---

## Code Style

### Formatting

```bash
cargo fmt --all
```

This must produce no changes. Run it before committing.

### Linting

```bash
cargo clippy --all-targets -- -D warnings
```

This must produce zero warnings.

### Additional Rules

- New public functions and types require `///` doc comments.
- No `unsafe` code is permitted in any contract.
- No external crate dependencies beyond `soroban-sdk` are permitted without prior discussion with maintainers.

---

## Pull Request Process

1. Fork the repository and create a feature branch off `main`.
2. Make your changes, keeping commits logically atomic (or squash before opening the PR).
3. Ensure all CI checks pass locally before requesting review:
   - `cargo fmt --all` — no changes
   - `cargo clippy --all-targets -- -D warnings` — zero warnings
   - `cargo test --workspace` — all tests pass
4. Open a PR against `main`. Your PR description must summarise what changed and why.
5. If your PR introduces a new contract or public API, include tests covering error paths and state transitions.
6. At least one maintainer approval is required before a PR is merged.

---

## License

By contributing, you agree that your contributions will be licensed under the [MIT License](LICENSE).
