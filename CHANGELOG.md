# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

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
