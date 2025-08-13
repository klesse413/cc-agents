# CLAUDE.md template for a TypeScript-based Web+Mobile App

Root is at FILL_ME_IN (... fill it in)

## Stack
- **Web:** Next.js 15 + Tailwind (port 3000)
- **Mobile:** Expo 51 (port 19006 for web)
- **API:** NestJS 10 + Prisma (port 4000)
- **Shared:** packages/ui for common components

## Development
```bash
# From root directory
cd FILL_ME_IN && pnpm turbo run dev        # Start all apps
cd FILL_ME_IN && pnpm turbo run lint       # Lint all
cd FILL_ME_IN && pnpm turbo run typecheck  # TypeScript check
```

## Testing
```bash
# Core tests (always run)
cd FILL_ME_IN/apps/web && pnpm test          # Jest + RTL
cd FILL_ME_IN/apps/mobile && pnpm test       # Jest + React Native Testing Library  
cd FILL_ME_IN/apps/api && pnpm test:e2e      # NestJS E2E

# Optional E2E (Complex UI changes only)
cd FILL_ME_IN/apps/web && npx playwright test
cd FILL_ME_IN/apps/mobile && npx playwright test
```

## Claude Workflow
**CRITICAL: NEVER make changes on main branch! ALWAYS follow this workflow:**

**For ANY code changes:**

1. **Git workflow to start feature:** Follow Workflow Step 1 (Start Feature) in agents/git-workflow-agent.md
2. **Make changes** with Edit/Write tools
3. **Update tests** to match changes (always check and update automated tests)
4. **Launch testing agents:**
   ```
   Task: "Web Testing Agent - follow agents/web-testing-agent.md"
   Task: "Mobile Testing Agent - follow agents/mobile-testing-agent.md"  
   Task: "API Testing Agent - follow agents/api-testing-agent.md"
   ```
5. **Wait for all tests to pass** (all 3 testing agent tasks complete)
6. **Git workflow to commit & push feature:** Follow Workflow Step 2 (Commit & Push Changes) in agents/git-workflow-agent.md
7. **Continue repeating 2-6 until feature complete**
8. **Git workflow to create PR:** Follow Workflow Step 3 (Create PR) in agents/git-workflow-agent.md
9. **Ask for go-ahead to merge & cleanup** and when granted, follow Workflow Step 4 (Merge & Cleanup) in agents/git-workflow-agent.md

**WARNING: If Claude tries to make changes without following steps 1-3 first, STOP and follow the workflow!**

## Environment
- Claude **never** touches real `.env` files
- Only update `*.env.example` files
- Print "SECRETS TODO" after env changes
