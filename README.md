# Claude Code subagents

Basic subagents for Git + testing.
Anthropic docs: [Claude Code → Sub-agents](https://docs.anthropic.com/en/docs/claude-code/sub-agents)

Created in collaboration with Claude, of course.

## Usage

### Git Workflow Agent

**Prerequisites:**
- Install [GitHub CLI](https://cli.github.com/): `brew install gh` or `gh auth login`
- Update `FILL_ME_IN` in the agent file with your project path

**What it does:** Complete git workflow automation. Creates feature branches, commits regularly, opens PRs, manages merges, and cleans up branches.

### Testing Agents

Both testing agents work with **React/Next.js** applications.

**Prerequisites:**
- Update `FILL_ME_IN` in agent files with your project path
- Set up your dev scripts: `npm run dev` or `pnpm turbo run dev`
- Install [Playwright](https://playwright.dev/): `npm init playwright@latest`
- Configure Browser MCP tools in Claude Code

**Web Testing Agent:** Tests web applications via localhost:3000, runs Playwright tests, performance/accessibility audits.

**Mobile Testing Agent:** Tests mobile apps via Expo web mode (localhost:8081/19006), mobile viewports, touch interactions.

**Best for:** Full-stack TypeScript apps (Next.js, Expo, Turborepo monorepos).
