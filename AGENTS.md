# AGENTS.md

This repository is the sharing space for Global Engineering's agentic SDLC community of practice. It exists to collect what each pilot team is doing and to evolve shared best practices across the organization.

## Repository Layout

```
pilots/           One markdown file per org -- goals and repo links
best-practices/   Patterns and techniques that emerge from the pilots
demos/            Demo videos from each org
presentations/    Presentations from each org
pge-review/       Topics reviewed and discussed by P&GE leadership
```

### pilots/

Each file describes one org's agentic SDLC efforts: a short description of what the team is focused on, followed by a table of repositories with one-line descriptions. Orgs maintain their own repos elsewhere; this directory indexes them.

### demos/

A collection of demo videos from each org showcasing their agentic SDLC efforts. Each entry has a title, link, and one-line description.

### presentations/

A collection of presentations from each org on their agentic SDLC efforts. Each entry has a title, link, and one-line description.

### pge-review/

Topics reviewed and discussed by P&GE leadership. Each entry records the date, topic, materials, and outcome.

### best-practices/

Shared knowledge that emerges from the pilots. Organized by topic area:

- **Skills** -- Reusable skill definitions that work across agent platforms
- **Agent definitions** -- CLAUDE.md patterns, .cursorrules, agent configs, system prompts
- **Context engineering** -- Prompt patterns, context hacks, retrieval strategies
- **Tools** -- MCP servers, tool access patterns, gateway configurations

New topics and files get added as practices actually emerge. Empty scaffolding is not welcome.

## How to Contribute

This repository is **AI-first**. Contributions are expected to come from AI agents, AI-assisted workflows, or through skills embedded in the repo itself.

### Adding or updating a pilot

Edit or create the appropriate file in `pilots/`. Follow the existing format:

1. Org name as the heading
2. A short description of the team's agentic SDLC goals
3. A table of repos: name, link, and one-line description

### Sharing a best practice

Add to or create a file in `best-practices/`. A good best practice entry includes:

1. What the practice is and when to use it
2. A concrete example or reference implementation
3. Which pilot team(s) validated it

### General contribution workflow

1. Branch from `main`
2. Make your changes using your AI coding tool of choice
3. Open a pull request with a clear description of what changed and why
4. PRs are reviewed by the community -- anyone can review, anyone can merge

## Rules of Engagement

1. **Share, don't gate.** This is a community of practice, not a governance body. The goal is to surface what works and make it easy to find, not to approve or block anyone's work.

2. **Link, don't duplicate.** Project code lives in each team's own repos. This repo indexes and cross-references. Do not copy source code here.

3. **Founding projects, not candidates.** The work each org has already invested in is treated as a founding contribution. These are not "seeds to evaluate" -- they are the starting point the community builds on.

4. **Show your work.** Best practices should come from real experience in the pilots. "We tried X on project Y and it worked because Z" is more valuable than theoretical recommendations.

5. **AI-native contributions.** Use AI agents to draft, review, and refine contributions. This repo practices what it preaches -- if your agentic workflow can't contribute here, that is useful signal about the workflow.

6. **Respect team differences.** Different product teams have different upstream communities, compliance requirements, and workflow constraints. There is no single "right" approach. Practices that work well for one team may need adaptation for another, and that is expected.

7. **Move fast, stay light.** Prefer a merged PR with a rough-but-useful practice over a perfect document that never ships. Iterate in the open.

## For AI Agents

When working in this repository:

- Read `AGENTS.md` for repo-specific context
- Read the relevant `pilots/*.md` file before modifying it
- Follow the existing format and structure of neighboring files
- Do not create empty placeholder files or directories
- Do not add governance, process, or approval-gate documentation
- Keep descriptions concise -- one line per repo, short paragraphs for overviews
- All content in this repo is public domain (Unlicense)
