# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.2.0] - 2026-07-13

### Added

- **web-patterns**: the framework-agnostic web lane strunk was missing. CSS units (never px for sizing), design tokens as custom properties, compositor-only animation, semantic HTML, component composition, state management, and data fetching. Fires on `.css`/`.html`/`.ts`/`.tsx`/`.vue` edits — the ground `frontend-patterns` (Svelte-only) never covered.
- **web-security**: nonce-based CSP, security headers, XSS, third-party scripts and SRI, form CSRF and rate limiting.
- **web-performance**: Core Web Vitals targets, bundle budgets, loading strategy, image and font rules.

### Changed

- **python-patterns**, **python-testing**, **rust-patterns**, **rust-testing**, **e2e-testing**, **apply-design-system**, **frontend-patterns**: absorbed the language guidance that previously lived in a parallel `~/.claude/rules/{python,rust,web}/` tree, so each topic now has exactly one home. New ground includes the Python toolchain and security rulings, the Rust naming table, module layout, `&str`/`&[T]` parameter and `Send + Sync` repository rulings, the cargo command reference, the macOS/maturin codesign trap, the "what to test, in priority order" list, and the design quality gate (4 of 10 required qualities). `apply-design-system` and `e2e-testing` gained triggers so the absorbed lanes are reachable.

## [0.1.4] - 2026-07-13

### Changed

- **apply-design-system**: rewrote into the rulings house style to match the other skills, and fixed three defects: the skipped heading level between modes, the false `/apply-design-system` slash-command instruction, and the hard browser-MCP dependency in competitor research (now optional, with a codebase-only fallback).
- **check-python-compat**: extended the compatibility reference through Python 3.14 (was 3.10-3.13) and added a freshness stamp, so a reader can tell at a glance whether it covers the current Python.

## [0.1.3] - 2026-05-31

### Changed

- Collapsed every skill to a single opinionated file. Reference folders that re-taught Python/Rust/Svelte basics the model already knows are gone; what remains is the rulings that override a default or flag a real trap. `check-python-compat` keeps its compatibility table.
- **e2e-testing**: trimmed to the durable Playwright core (POM, config defaults, flaky-test strategy) and removed app-specific Web3/wallet and financial-trade examples that didn't belong in a general skill.

### Fixed

- Fact-checked every ruling against current docs and corrected the confirmed errors: `page.click()` does auto-wait (the prior text claimed it didn't); `criterion::black_box` is deprecated in favor of `std::hint::black_box`; a bare `raise New()` still chains the traceback implicitly; the `X | Y` 3.9 fallback caveat; `thiserror`/`anyhow` is not a hard library-vs-app split. Switched Playwright selectors to `getByTestId()`, added the pytest-asyncio `strict`-mode gotcha, and fixed the `check-python-compat` scope (3.10–3.13) and a mislabeled removed-modules row.

## [0.1.2] - 2026-05-11

### Added

- **python-patterns**: PEP 8 naming-convention table (modules, classes, functions, constants) with an explicit rule that `.py` files must use snake_case, never kebab-case (kebab-cased modules are not importable).

## [0.1.1] - 2026-05-11

### Added

- `apply-design-system` — framework-agnostic visual-craft skill with three modes: generate design tokens from existing code + competitor research, score UI 0-10 across ten dimensions (color, typography, spacing, responsiveness, accessibility, polish, ...), and detect generic AI-design patterns (gratuitous gradients, purple-to-blue defaults, purposeless glass morphism). Pairs with `frontend-patterns`: one shapes the code, the other shapes what you see.

## [0.1.0] - 2026-05-11

### Added

- Initial release with seven code-craft skills:
  - `python-patterns` — pythonic idioms, PEP 8, error handling, concurrency, type hints, decorators, data modeling, project structure
  - `python-testing` — pytest, fixtures, parametrize, mocking, async testing, configuration
  - `rust-patterns` — ownership, error handling, traits & generics, iterators & concurrency, enums & matching, unsafe & modules
  - `rust-testing` — unit, integration, async, parameterized, property-based, mocking, benchmarks, doc tests, coverage
  - `frontend-patterns` — Svelte 5 / SvelteKit runes, reactivity, data loading, forms & accessibility, animations, performance
  - `e2e-testing` — Playwright Page Object Model, configuration, CI/CD, artifacts, flaky test strategies
  - `check-python-compat` — Python 3.10+ version-compatibility audit with reference table
- Each skill includes a `references/` folder of topic-specific deep dives loaded on demand.
