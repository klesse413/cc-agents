# CLAUDE.md

...

## Stack
- **Web:** Next.js 15 (App Router)
- **Mobile:** Expo SDK 51
- **API:** NestJS 10 + Fastify on Node 20
- **DB:** Postgres (pooled) via Prisma

## Monorepo Layout
- Turborepo + pnpm workspaces:
  - `apps/web`, `apps/mobile`, `apps/api`, `packages/ui`
- TypeScript **strict** everywhere; Node **20** (`.nvmrc`)

## DX Defaults
- Ports: web **3000**, api **4000**, Expo dev server default/tunnel
- Root scripts for `dev`, `typecheck`, `lint`, `build`
- **Commit a `.env.example` at root and in each app** (templates only)

## 🔐 Env & Secrets Policy
- Claude **must never** read/write real env files (`.env`, `.env.local`, `.env.*`, keys/certs).  
- Claude **may only** update `*.env.example` files (templates).  
- After any change to an example file, **print a loud "SECRETS TODO"** listing:
  - which variables changed
  - exactly where I must copy them locally:
    - Web: `apps/web/.env.local`
    - API: `apps/api/.env`
    - Mobile: `apps/mobile/.env`
- Baseline vars:  
  `DATABASE_URL`

## Git Workflow (MANDATORY AUTOMATION)
- **NEVER make direct changes to main branch**: ALL code changes MUST go through feature branches
- **ALWAYS use git-workflow-agent**: Use Task tool with `subagent_type: "general-purpose"` and include git-workflow-agent instructions for ALL git operations before any code changes
- **SINGLE-LINE COMMITS ONLY**: All commit messages MUST be single line using conventional format: `type: description`
- **Required workflow for ANY code change**:
  1. **ONCE at start**: Launch git-workflow-agent to create feature branch
  2. **ITERATIVELY during development**: Launch git-workflow-agent to commit after each logical unit of work (component working, test passing, bug fixed)
  3. **ONCE when feature complete**: Launch git-workflow-agent to create PR and merge
- **Auto-cleanup**: Agent deletes old branches and prunes remotes
- Quality gates: `pnpm turbo run typecheck lint build` must pass before PR

## Development Commands
- `pnpm install` - Install all dependencies
- `pnpm turbo run dev` - Start all development servers
- `pnpm turbo run typecheck` - Run TypeScript checks
- `pnpm turbo run lint` - Run ESLint
- `pnpm turbo run build` - Build all apps
- `npx playwright install` - Install Playwright browsers (required for testing)

## Browser MCP Setup (for Testing Agents)
- **Browser MCP Connection**: Ensure Browser MCP connector is running before using browser tools
- **Manual Fallback**: If MCP fails, agents should continue with Playwright and curl-based testing
- **Chrome Connection**: Use `open -a "Google Chrome" http://localhost:3000` to connect browser for MCP tools

## Testing Workflow (MANDATORY AUTOMATION)
- **AUTOMATICALLY launch testing agents**: After making code changes (before commit), ALWAYS launch both web and mobile testing agents
- **Required testing sequence**:
  1. Make code changes
  2. **BEFORE committing**: Launch Web Testing Agent + Mobile Testing Agent via Task tool
  3. **ONLY if tests pass**: Launch git-workflow-agent to commit
- **Web Testing Agent**: Use Task tool with `subagent_type: "general-purpose"` and prompt: "Test web application after recent changes. Run comprehensive test suite including Playwright tests, visual verification with browser MCP, performance audit, and accessibility checks."
- **Mobile Testing Agent**: Use Task tool with `subagent_type: "general-purpose"` and prompt: "Test mobile application after recent changes. Start Expo web server, test mobile viewports, verify component functionality and build process."
- **When to test**: After ANY file edits in `apps/web/`, `apps/mobile/`, or shared components
- **Agent configs**: Located in `.claude/agents/` directory

## Agent Invocation Instructions (for Claude)
All agents must be invoked using `Task` tool with `subagent_type: "general-purpose"` and include the specific agent instructions:

**Git Workflow Agent Examples**:
```
# Create branch (once at start):
"You are the Git Workflow Agent. Create feature branch for [describe feature]."

# Commit changes (iterative during development):
"You are the Git Workflow Agent. Commit and push current changes."

# Create PR (once when feature complete):
"You are the Git Workflow Agent. Create PR and handle merge for completed feature."
```

**Web Testing Agent Example**:
```
Task tool with:
- subagent_type: "general-purpose"
- description: "Test web application" 
- prompt: "You are the Web Testing Agent. Follow the instructions in ~/code/demoapp/.claude/agents/web-testing-agent.md exactly. Test web application after recent changes. Run comprehensive test suite including Playwright tests, visual verification with browser MCP, performance audit, and accessibility checks."
```

**Mobile Testing Agent Example**:
```
Task tool with:
- subagent_type: "general-purpose"
- description: "Test mobile application"
- prompt: "You are the Mobile Testing Agent. Follow the instructions in ~/code/demoapp/.claude/agents/mobile-testing-agent.md exactly. Test mobile application after recent changes. Start Expo web server, test mobile viewports, verify component functionality and build process."
```

## MANDATORY AUTOMATION RULES (for Claude)
- **NEVER make direct changes to main**: ALL code changes MUST use git-workflow-agent first
- **ALWAYS use 3-agent workflow**: 
  1. git-workflow-agent (creates branch, commits iteratively, PRs when complete)
  2. Web Testing Agent (tests web changes)
  3. Mobile Testing Agent (tests mobile impact)
- **ACT**: scaffolding, wiring providers/components/guards, scripts, ESLint/Prettier, README, local CORS, CI for lint/typecheck/build, **automatically launching all 3 agents for any code change**
- **ASK**: any cloud provisioning, using real secrets, running DB migrations against non-local, **merging PRs** (git-workflow-agent will ask for approval)
- **STOP**: destructive ops (`--force`, resets) or anything that would commit secrets

...
