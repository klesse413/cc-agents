# Claude Code subagents

Basic subagents for Git + testing.
Anthropic docs: [Claude Code → Sub-agents](https://docs.anthropic.com/en/docs/claude-code/sub-agents)

Created in collaboration with Claude, of course.

## Usage

See CLAUDE.md for snippets to add to your project's CLAUDE.md to instruct automated usage of these subagents.

### Git Workflow Agent

**Prerequisites:**
- Install [GitHub CLI](https://cli.github.com/): `brew install gh` or `gh auth login`
- Update `FILL_ME_IN` in the agent file with your project path

**What it does:** Complete git workflow automation. Creates feature branches, commits regularly, opens PRs, manages merges, and cleans up branches.

### Testing Agents

Web, Mobile & API testing agents work well with Typescript-based applications.

**Prerequisites:**
- Update `FILL_ME_IN` in agent files with your project path
- Install [Playwright](https://playwright.dev/): `npm init playwright@latest`
