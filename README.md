<p align="center">
  <h1 align="center">claude-deep-research</h1>
</p>

<p align="center">
  Official-docs-first deep research for Claude Code.
</p>

<p align="center">
  <a href="https://github.com/jl-cmd/claude-deep-research/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License" /></a>
  <a href="https://code.claude.com/docs/en/plugins"><img src="https://img.shields.io/badge/Claude_Code-plugin-blueviolet" alt="Claude Code Plugin" /></a>
</p>

---

## Skills

| Skill | Command | What It Does |
|-------|---------|-------------|
| **deep-research** | `/deep-research [topic]` | Iterative multi-source research producing comprehensive Obsidian reports with full citations |
| **research-mode** | `/research-mode` | Anti-hallucination constraints with source authority hierarchy and citation requirements |

## Agents

| Agent | What It Does |
|-------|-------------|
| **deep-research** | Executes the iterative research loop -- locates official docs, surveys secondary sources, tracks state across iterations, writes final report to Obsidian |

## Install

```
/plugin marketplace add jl-cmd/claude-deep-research
/plugin install deep-research@claude-deep-research
```

Or locally:

```bash
git clone https://github.com/jl-cmd/claude-deep-research.git
claude --plugin-dir ./claude-deep-research
```

## Official-Docs-First Methodology

The core principle: when researching any external tool, library, API, or protocol, always locate and read the **official vendor/creator documentation** before consulting secondary sources.

- Official docs are tier 1 -- blog posts, tutorials, and community content are tier 5
- If no official docs exist, that is explicitly stated as a finding
- When sources conflict, official docs win
- For local project code, the codebase itself is the authority

## `/deep-research` -- Iterative Research Pipeline

Two-phase pipeline:

**Phase 1 (Interactive):** Scopes the research through 1-3 clarifying questions, builds a structured research brief, and identifies known official documentation sources.

**Phase 2 (Agent):** The deep-research agent executes iterative research:

| Phase | Iterations | Focus |
|-------|-----------|-------|
| Early | 1-3 | Official vendor/creator docs -- locate, deep read, extract quotes |
| Middle | 4-8 | Secondary source deep dives -- fill gaps, cross-reference against official docs |
| Late | 9+ | Synthesis and gap-filling -- resolve contradictions, compile report |

Sources are tagged `[official]` or `[secondary]` throughout. The final report notes whether official documentation was available.

**Depth options:**

| Depth | Iterations | Target Sources |
|-------|-----------|---------------|
| Quick overview | 8 | 5-10 |
| Standard | 15 | 15-20 |
| Exhaustive | 25 | 25+ |

Output is written to Obsidian with full YAML frontmatter, inline citations, and a numbered bibliography. Falls back to conversation output if Obsidian MCP is unavailable.

## `/research-mode` -- Anti-Hallucination Constraints

Activates three constraints that stay active until explicitly exited:

1. **Say "I don't know"** -- no credible source, no claim
2. **Cite everything** -- every claim needs a specific source with URL, named paper, or official docs
3. **Direct quotes** -- extract actual text before analyzing, ground responses in word-for-word quotes

Plus a **Source Authority Hierarchy** (highest to lowest):

1. Official vendor/creator documentation
2. Files in the current project
3. Academic papers, named researchers
4. Reputable external sources with URLs
5. Blog posts, tutorials, community content

## Prerequisites

- Claude Code 1.0.33+
- For Obsidian output: an [Obsidian MCP server](https://github.com/MarkusPfworlds/obsidian-mcp) connected to Claude Code (optional -- falls back to conversation output)

## Plugin Structure

```
claude-deep-research/
├── .claude-plugin/
│   ├── plugin.json
│   └── marketplace.json
├── skills/
│   ├── deep-research/
│   │   └── SKILL.md
│   └── research-mode/
│       └── SKILL.md
├── agents/
│   └── deep-research.md
├── README.md
├── LICENSE
└── .gitignore
```

### Sources

- [Anthropic - Reduce Hallucinations](https://docs.anthropic.com/en/docs/test-and-evaluate/strengthen-guardrails/reduce-hallucinations)
- [Plugin creation docs](https://code.claude.com/docs/en/plugins)
- [Skills authoring docs](https://code.claude.com/docs/en/skills)

## License

[MIT](LICENSE)
