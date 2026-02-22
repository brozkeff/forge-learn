# GEMINI.md

This file provides instructional context for the Gemini AI agent when working with the **forge-user** codebase.

## Project Overview

**forge-user** is a beginner-friendly personal AI setup module for the Forge ecosystem. It provides 19 skills, 1 agent, identity steering files, and a 7-level progression system that teaches users to customize their AI assistant.

### Core Responsibilities

- **Text Transformation:** Skills for summarizing, translating, simplifying, and cleaning text.
- **Code Assistance:** Explaining errors, diagnosing problems, translating English to git commands.
- **Project Scaffolding:** Turning ideas into plans with starter files.
- **Identity:** Steering files that tell the AI who the user is and what they care about.

## Building and Testing

```bash
make install          # deploy agents + skills to all providers
make verify           # check agents + skills deployed across all providers
make test             # validate-module convention checks
make clean            # remove installed agents + skills
```

## Skills

| Skill | Responsibilities |
|:------|:-----------------|
| `Tour` | Setup walkthrough, directory explanation, getting started guidance |
| `Explain` | Plain language explanation of files, errors, and concepts |
| `ExplainSimply` | Rewriting complex content in simple, accessible language |
| `FixIt` | Problem diagnosis and fix proposals |
| `GitHelp` | Plain English to git command translation |
| `Kickstart` | Idea-to-plan conversion with starter files |
| `Summarize` | Key point extraction into structured summaries |
| `Translate` | Text translation to any target language |
| `FixGrammar` | Grammar and spelling correction |
| `MakeLonger` | Text expansion to roughly double length |
| `MakeShorter` | Text condensation to roughly half length |
| `Emojify` | Context-appropriate emoji insertion |
| `CleanText` | URL, HTML, and noise stripping |
| `GenerateGlossary` | Alphabetical glossary creation |
| `GenerateOutline` | Hierarchical outline generation |
| `RewriteAsTweet` | Content rewriting as tweet or thread |
| `Pandoc` | Document format conversion via pandoc |
| `HighImpactChanges` | Codebase change impact analysis |

Note: `Progress` is Claude Code-only and not deployed to Gemini.

## Agents

| Agent | Responsibilities |
|:------|:-----------------|
| `CodeHelper` | Beginner-friendly code explanation and minimal fixes |

Agent source files live in `agents/`. Model and tool assignments are in `defaults.yaml`.

## Skill File Convention

Each skill directory contains:

- `SKILL.md` -- AI instructions with YAML frontmatter (name, description, version)
- `SKILL.yaml` -- sidecar metadata (sources, provider-specific config)
- Optional `sample.md` demo files

## Submodule Integration

```bash
git submodule add https://github.com/N4M3Z/forge-user.git modules/forge-user
cd modules/forge-user && make install SCOPE=workspace
```

### Makefile Integration

```makefile
install-forge-user:
	@$(MAKE) -C modules/forge-user install SCOPE=$(SCOPE)
```

## Configuration

- `defaults.yaml`: provider-keyed skill roster + agent config (committed)
- `config.yaml`: user overrides (gitignored), same structure as defaults
- `module.yaml`: module metadata (name, version, description)

## Development Conventions

- **Skill naming**: PascalCase directories matching `name:` in SKILL.md frontmatter
- **Agent naming**: PascalCase filenames matching `name:` in frontmatter
- **Provider routing**: provider-keyed allowlists in `defaults.yaml` control which platforms receive each skill
- **forge-lib**: git submodule at `lib/`, provides `install-skills`, `install-agents`, and `validate-module` Rust binaries
