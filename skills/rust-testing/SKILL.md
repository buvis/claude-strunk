---
name: rust-testing
description: Use when writing, fixing, or reviewing Rust tests. Covers unit, integration, async, property-based, mocking, coverage. Triggers on "cargo test", "rust test", "#[test]", "tokio::test", "proptest", "rstest", "mockall".
---

# Rust Testing

TDD: failing test first, then the code. Unit tests in a `#[cfg(test)] mod tests`; integration tests in `tests/`. Coverage target 80% general, 90%+ on public APIs, 100% on critical business logic; exclude generated and FFI code.

## Rulings

- **Choose the right tool:** `proptest` for invariants and round-trips (encode→decode, sort preserves length); `rstest` for table-driven cases; `mockall` only at trait boundaries, never on concrete types.
- **`#[should_panic(expected = "...")]`** — always pin the message substring. A bare `#[should_panic]` passes on the wrong panic.
- **Async:** `#[tokio::test]`. Wrap anything that could hang in `tokio::time::timeout(Duration::..., fut)` — don't trust an implicit timeout.
- **Benchmarks:** `criterion`, and wrap inputs in `std::hint::black_box(...)` so the optimizer can't delete the work you're measuring. (`criterion::black_box` is deprecated since criterion 0.6; `std::hint::black_box` is stable from Rust 1.66.)
- **Coverage:** `cargo llvm-cov --fail-under-lines 80` in CI (install via `taiki-e/install-action`).
- **Doc-tests** are tests: every public example in `///` must compile and run. Mark non-running examples `no_run` or `ignore` deliberately, not by accident.
