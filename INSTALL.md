# Install

Instructions for the AI agent. When the user asks to set up forge-user or troubleshoot their installation, follow these steps.

## Prerequisites Check

Before setup, verify the user has what they need:

1. **Git**: Run `git --version`. If missing, guide them:
   - Mac: "macOS will prompt you to install developer tools — say yes"
   - Windows: "Download Git from git-scm.com/downloads/win — keep all defaults during setup"
   - Linux: `sudo apt install git` or `sudo dnf install git`

2. **Claude Code** (or compatible tool): The user is already running it if they're talking to you. If they're setting up for the first time, recommend the native installer:
   - Mac/Linux: `curl -fsSL https://claude.ai/install.sh | bash`
   - Windows PowerShell: `irm https://claude.ai/install.ps1 | iex`
   - Mac Homebrew: `brew install --cask claude-code`
   - Windows WinGet: `winget install Anthropic.ClaudeCode`


## Build and Deploy

If the user wants to deploy agents and skills to all providers:

```bash
git submodule update --init lib   # initialize forge-lib (first time only)
make -C lib build                 # build Rust binaries (first time only)
make install                      # deploy 1 agent + 19 skills to all providers
make verify                       # confirm everything deployed
```

## First-Time Setup

If the user just cloned the repo and is starting for the first time:

1. Check if `steering/Identity.md` still has placeholder values (`Your Name`, `beginner`, etc.). If so, ask the user for their name and preferences, then update the file for them.

2. Check if `steering/Goals.md` still has the example goals. If so, ask what they're working toward and update it.

3. Run `/Tour` to introduce them to the setup.

## Module Installation

When the user wants to install a module from `modules/`:

1. The module is a separate repository cloned into `modules/`. It may have its own `.claude-plugin/plugin.json` or skills directory.

2. Read the module's README for setup instructions. Some modules are standalone Claude Code plugins that need to be registered separately.

3. forge-user's `plugin.json` only discovers skills from `./skills` — module skills are NOT auto-discovered. If the module has skills the user wants available as slash commands, explain that they need to either:
   - Run the module as a separate Claude Code plugin
   - Copy specific skills into `skills/` (not recommended — breaks updates)
   - Upgrade to [forge-core](https://github.com/N4M3Z/forge-core) for automated module dispatch

## Recommended Modules

| Module | What it adds |
|--------|-------------|
| [forge-council](https://github.com/N4M3Z/forge-council) | Multi-specialist code review — convenes a panel of experts to debate changes |
| [forge-avatar](https://github.com/N4M3Z/forge-avatar) | Deep identity — digital avatar, beliefs, strategies, communication preferences |
| [forge-steering](https://github.com/N4M3Z/forge-steering) | Behavioral rules — teach your AI what to do and what to avoid |

## Upgrading to forge-core

If the user outgrows forge-user (wants hooks, automated dispatching, Rust-powered tools, multi-vault support), point them to [forge-core](https://github.com/N4M3Z/forge-core). Their steering files and skills are compatible — migration doesn't require starting over.

## Platform Notes

- **Windows**: Claude Code runs natively on Windows 10 (1809+). Requires [Git for Windows](https://git-scm.com/downloads/win) for shell operations. WSL 2 also works.
- **Other tools**: The steering files and CLAUDE.md are plain markdown — useful with any AI tool. [OpenCode](https://opencode.ai) reads CLAUDE.md as a fallback. For [Codex CLI](https://developers.openai.com/codex) (uses AGENTS.md) or [Gemini CLI](https://github.com/google-gemini/gemini-cli) (uses GEMINI.md), copy CLAUDE.md content into the tool's instruction file format. Skill slash commands only work in Claude Code.
