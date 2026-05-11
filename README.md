# Strunk

[![GitHub license](https://img.shields.io/github/license/buvis/claude-strunk)](https://github.com/buvis/claude-strunk/blob/master/LICENSE)

> "Vigorous writing is concise." — *The Elements of Style*

Code-craft skills for [Claude Code](https://claude.ai/code). Idiomatic patterns and disciplined testing for Python, Rust, and Svelte. Opinionated about style the same way Strunk & White was opinionated about prose.

## What's inside

| Skill | When it fires |
|-------|---------------|
| `python-patterns` | Editing Python; "pythonic", "PEP 8", "python best practices" |
| `python-testing` | "pytest", "python test", "fixture", "mock", "parametrize", "TDD" |
| `rust-patterns` | Editing Rust; "idiomatic rust", "rust best practices" |
| `rust-testing` | "cargo test", "rust test", "#[test]", "proptest", "mockall" |
| `frontend-patterns` | Editing `.svelte`; "svelte", "sveltekit", "runes" |
| `e2e-testing` | "playwright", "e2e test" |
| `check-python-compat` | "check python compat", "python 3.10 compatible" |
| `apply-design-system` | "design system", "visual audit", "slop check" — framework-agnostic counterpart to `frontend-patterns` |

Each skill ships with a `references/` folder of topic-specific deep dives (idioms, error handling, fixtures, mocking, ownership, parameterized tests, ...) that Claude pulls in only when needed. No always-on context cost.

## Install

```
/plugin marketplace add buvis/claude-plugins
/plugin install strunk@buvis-plugins
```

Restart Claude Code. The skills auto-trigger from file extensions and conversation keywords - you don't have to invoke anything by name.

### Update

```
/plugin update strunk@buvis-plugins
```

### Alternative: install directly from this repo

```
/plugin marketplace add buvis/claude-strunk
/plugin install strunk@claude-strunk
```

## Why "Strunk"

[*The Elements of Style*](https://en.wikipedia.org/wiki/The_Elements_of_Style) is a 100-page book of writing rules that has shaped American prose for a century. Its premise: clarity is a moral stance, not a stylistic one. Same energy for code. The skills here don't trail off into "consider the context" or "it depends" - they pick a side and tell you which one.

If you've never read it, the irony is intentional.

## License

MIT
