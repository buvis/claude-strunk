# Strunk

[![GitHub license](https://img.shields.io/github/license/buvis/claude-strunk)](https://github.com/buvis/claude-strunk/blob/master/LICENSE)

> "Vigorous writing is concise." — *The Elements of Style*

Code-craft skills for [Claude Code](https://claude.ai/code). Idiomatic patterns and disciplined testing for Python, Rust, and the web. Opinionated about style the same way Strunk & White was opinionated about prose.

## What's inside

| Skill | When it fires |
|-------|---------------|
| `python-patterns` | Editing Python; "pythonic", "PEP 8", "python best practices" |
| `python-testing` | "pytest", "python test", "fixture", "mock", "parametrize", "TDD" |
| `rust-patterns` | Editing Rust; "idiomatic rust", "rust best practices" |
| `rust-testing` | "cargo test", "rust test", "#[test]", "proptest", "mockall" |
| `frontend-patterns` | Editing `.svelte`; "svelte", "sveltekit", "runes" |
| `web-patterns` | Editing `.css`/`.svelte`/`.ts`/`.tsx`/`.jsx`/`.html`/`.vue`; "css units", "component composition", "url state" — the framework-agnostic web lane |
| `web-security` | "csp", "xss", "security headers", "sri", "csrf" |
| `web-performance` | "core web vitals", "lighthouse", "bundle size", "LCP", "CLS" |
| `e2e-testing` | "playwright", "e2e test", "visual regression" |
| `check-python-compat` | "check python compat", "python 3.10 compatible" |
| `apply-design-system` | Editing frontend files; "design system", "visual audit", "slop check" — framework-agnostic counterpart to `frontend-patterns` |

Each skill is one tight file: an opinion table plus the handful of rules that override a model default or flag a real trap. No textbook restatement of things Claude already does. (`check-python-compat` keeps a version-compatibility reference table, the one place a lookup table earns its keep.)

## Install

```
/plugin marketplace add buvis/claude-plugins
/plugin install strunk@buvis-plugins
```

Restart Claude Code. Skills are model-invoked from the trigger phrases and file-edit cues in each description below — firing isn't guaranteed, so invoke a skill by name if it doesn't trigger on its own.

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

## Releasing

`dev/bin/release [patch|minor|major]` is a thin shim. The shared release
script lives in the central marketplace repo,
[buvis/claude-plugins](https://github.com/buvis/claude-plugins), and every
release also bumps this plugin's entry there. Developing this plugin
therefore needs that repo cloned beside this one:

```bash
git clone git@github.com:buvis/claude-plugins.git ../claude-plugins
```

Repo-specific pre-release checks live in `dev/bin/release-checks`.

## License

MIT
