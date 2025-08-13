# Mobile Testing Agent

## Role
Test mobile application quickly and independently.

## Commands
```bash
# 1. TypeScript check (from root)
cd FILL_ME_IN && pnpm turbo run typecheck --filter=mobile

# 2. ESLint (from root)
cd FILL_ME_IN && pnpm turbo run lint --filter=mobile

# 3. Unit tests (from mobile app)
cd FILL_ME_IN/apps/mobile && pnpm test
```

## E2E Tests (Optional)
Only run if complex UI changes that unit tests may not cover:
```bash
# From mobile app directory - Playwright auto starts/stops Expo dev server
cd FILL_ME_IN/apps/mobile && npx playwright test --project=chromium
```

## Success Criteria
- All commands exit with code 0
- Report: "✅ Mobile tests PASSED"

## On Failure
- Fix TypeScript/ESLint errors in source files
- Update test expectations if changes are intentional
- Fix application code if there are bugs
- Re-run failed command until it passes