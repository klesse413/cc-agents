# CLAUDE.md

...

## Git Workflow (MANDATORY AUTOMATION)
- **NEVER make direct changes to main branch**: ALL code changes MUST go through feature branches
- **ALWAYS use git-workflow-agent**: Use Task tool with git-workflow-agent for ALL git operations before any code changes
- **Required workflow for ANY code change**:
  1. First: Launch git-workflow-agent via Task tool
  2. Agent creates feature branch (`feat/...`, `fix/...`, `chore/...`, `docs/...`)
  3. Agent makes commits as work progresses
  4. Agent creates PR with summary and test plan
  5. Agent handles merge after user approval
- **Auto-cleanup**: Agent deletes old branches and prunes remotes
- Quality gates: `pnpm turbo run typecheck lint build` must pass before PR

## Testing Workflow (MANDATORY AUTOMATION)
- **AUTOMATICALLY launch testing agents**: After ANY code changes, ALWAYS launch both web and mobile testing agents
- **Required testing sequence for ANY code change**:
  1. Make code changes via git-workflow-agent
  2. IMMEDIATELY launch Web Testing Agent via Task tool
  3. IMMEDIATELY launch Mobile Testing Agent via Task tool
- **Web Testing Agent**: Use Task tool with prompt: "Test web application after recent changes. Run comprehensive test suite including Playwright tests, visual verification with browser MCP, performance audit, and accessibility checks."
- **Mobile Testing Agent**: Use Task tool with prompt: "Test mobile application after recent changes. Start Expo web server, test mobile viewports, verify component functionality and build process."
- **When to test**: After ANY file edits in `apps/web/`, `apps/mobile/`, or shared components
- **Agent configs**: Located in `.claude/agents/` directory

## MANDATORY AUTOMATION RULES (for Claude)
- **NEVER make direct changes to main**: ALL code changes MUST use git-workflow-agent first
- **ALWAYS use 3-agent workflow**: 
  1. git-workflow-agent (creates branch, commits, PRs)
  2. Web Testing Agent (tests web changes)
  3. Mobile Testing Agent (tests mobile impact)
- **ACT**: scaffolding, wiring providers/components/guards, scripts, ESLint/Prettier, README, local CORS, CI for lint/typecheck/build, **automatically launching all 3 agents for any code change**
- **ASK**: any cloud provisioning, using real secrets, running DB migrations against non-local, **merging PRs** (git-workflow-agent will ask for approval)
- **STOP**: destructive ops (`--force`, resets) or anything that would commit secrets

...
