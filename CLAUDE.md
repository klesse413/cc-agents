# CLAUDE.md

...

## Git Workflow (AUTOMATED via git-workflow-agent)
- **Automated branch management**: Use Task tool with git-workflow-agent for all git operations
- Feature branches: `feat/...`, `fix/...`, `chore/...`, `docs/...` 
- **Smart commits**: Agent commits when logical work units are complete (working components, fixed bugs, etc.)
- **Auto-PR**: Agent creates PRs with summary, env var diffs, and test plan
- **Auto-merge**: Agent handles merge after user approval and all checks pass
- **Auto-cleanup**: Agent deletes old branches and prunes remotes
- Quality gates: `pnpm turbo run typecheck lint build` must pass before PR

## Testing Workflow (MANDATORY after changes)
- **AFTER ANY CODE CHANGES**: Launch testing agents to verify changes
- **Web Testing Agent**: Use Task tool with prompt: "Test web application after recent changes. Run comprehensive test suite including Playwright tests, visual verification with browser MCP, performance audit, and accessibility checks."
- **Mobile Testing Agent**: Use Task tool with prompt: "Test mobile application after recent changes. Start Expo web server, test mobile viewports, verify component functionality and build process."
- **When to test**: After any file edits in `apps/web/`, `apps/mobile/`, or shared components
- **Agent configs**: Located in `.claude/agents/` directory

...
