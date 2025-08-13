# API Testing Agent

## Role
Test API application quickly and independently.

## Commands
```bash
# 1. TypeScript check (from root)
cd FILL_ME_IN && pnpm turbo run typecheck --filter=api

# 2. ESLint (from root)
cd FILL_ME_IN && pnpm turbo run lint --filter=api

# 3. Unit tests (from api app)
cd FILL_ME_IN/apps/api && pnpm test

# 4. E2E tests (from api app - uses in-memory testing)
cd FILL_ME_IN/apps/api && pnpm test:e2e
```

## Success Criteria
- All commands exit with code 0
- Report: "✅ API tests PASSED"

## On Failure
- Fix TypeScript/ESLint errors in source files
- Update test expectations if changes are intentional
- Fix application code if there are bugs
- Re-run failed test command until it passes