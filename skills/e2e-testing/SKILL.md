---
name: e2e-testing
description: Use when writing Playwright E2E tests. Covers Page Object Model, config, CI/CD, artifacts, and flaky test strategies. Triggers on "playwright", "e2e test".
---

# E2E Testing

Playwright. Stable beats clever. Pick a side.

## Rulings

- **Select by `data-testid` via `getByTestId()`**, never by text or CSS class. Text changes with copy; classes change with styling.
- **Auto-waiting locators, never manual sleeps.** Both `locator.click()` and `page.click(sel)` auto-wait for actionability, but prefer locator actions (`page.getByTestId('x').click()`) — they re-query and retry; `page.click(sel)` is discouraged. `waitForTimeout` is always wrong — wait for a `waitForResponse`/`waitFor({ state })` condition instead.
- **Page Object Model.** Selectors and actions live in a page class; specs read as intent. One class per page/screen.
- **Retries and `forbidOnly` on CI only.** Retries mask flake locally where you should be fixing it.
- **Trace `on-first-retry`, screenshot/video `*-on-failure`.** Artifacts cost nothing until something breaks.

## Page Object Model

```typescript
export class ItemsPage {
  constructor(private page: Page) {}
  searchInput = () => this.page.getByTestId('search-input')
  itemCards   = () => this.page.getByTestId('item-card')

  async goto() { await this.page.goto('/items') }
  async search(q: string) {
    await this.searchInput().fill(q)
    await this.page.waitForResponse(r => r.url().includes('/api/search'))
  }
}
```

## Config (the defaults worth keeping)

```typescript
export default defineConfig({
  testDir: './tests/e2e',
  fullyParallel: true,
  forbidOnly: !!process.env.CI,
  retries: process.env.CI ? 2 : 0,
  reporter: [['html'], ['junit', { outputFile: 'results.xml' }]],
  use: {
    baseURL: process.env.BASE_URL ?? 'http://localhost:3000',
    trace: 'on-first-retry',
    screenshot: 'only-on-failure',
    video: 'retain-on-failure',
  },
  projects: [
    { name: 'chromium', use: devices['Desktop Chrome'] },
    { name: 'mobile-chrome', use: devices['Pixel 5'] },
  ],
})
```

## Flaky tests

Quarantine, never ignore: `test.fixme(true, 'flaky — Issue #123')`. Reproduce with `--repeat-each=10`. Root causes are almost always (1) racing a click against load, (2) an arbitrary `waitForTimeout`, or (3) clicking mid-animation. Fix the wait, not the timeout.

## CI

```yaml
- run: npx playwright install --with-deps
- run: npx playwright test
- uses: actions/upload-artifact@v4
  if: always()
  with: { name: playwright-report, path: playwright-report/ }
```
