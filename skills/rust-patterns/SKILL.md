---
name: rust-patterns
description: Use when writing, reviewing, or refactoring Rust code. Covers ownership, error handling, traits, concurrency, and project structure. Triggers on Rust file edits, "idiomatic rust", "rust best practices".
---

# Rust Patterns

Pick a side. These are the rulings, not a tutorial.

## Core opinions

| Rule | Why |
|------|-----|
| Borrow, don't clone | Pass `&T` unless you must own. |
| Make illegal states unrepresentable | Model only valid states with enums. |
| `?` over `unwrap()` | Propagate; never panic in production paths. |
| Parse, don't validate | Convert unstructured input to typed structs at the boundary. |
| Newtype for type safety | Wrap primitives so arguments can't be swapped. |
| Iterators over loops | Declarative chains are clearer and often faster. |
| `#[must_use]` on `Result`-like returns | Force callers to handle them. |
| `Cow<'_, T>` for maybe-owned data | Skip allocation when borrowing suffices. |
| Exhaustive matching | No wildcard `_` on business-critical enums — the compiler should force new variants on you. |
| Minimal `pub` surface | `pub(crate)` for internals; re-export the public API from `lib.rs`. |

## Pick-a-side calls

- **Errors:** `thiserror` when callers must match on error variants (usually libraries); `anyhow` when errors are only reported or logged (usually apps). Not a hard split — they compose: `thiserror` types wrapped by `anyhow` at the boundary.
- **Polymorphism:** generics when types are known at compile time (no vtable); trait objects (`dyn`) for heterogeneous collections, plugins, or runtime-selected types.
- **API shape:** accept generic inputs (`impl IntoIterator`). Return a named concrete type from public library APIs (callers can't depend on `impl Trait` internals); `impl Iterator` is fine for app or internal code.
- **Builders:** once a struct mixes required and optional fields (3+), use a builder, not a 6-argument `new`.
- **Concurrency:** channels to pass values between independent tasks; `Arc<Mutex<T>>` only for short-lived shared mutable state.

## Unsafe

Every `unsafe` block gets a `// SAFETY:` comment above it stating the invariant and why it holds. No comment, no merge.
