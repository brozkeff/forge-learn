# Installation

## Prerequisites

You need three things:

1. **Git** — downloads and tracks your files
   - Mac: Open Terminal, type `git --version`. If it's not installed, you'll be prompted to install it.
   - Windows: Download from [git-scm.com](https://git-scm.com/downloads). During setup, keep all defaults.
   - Linux: `sudo apt install git` (Ubuntu/Debian) or `sudo dnf install git` (Fedora)

2. **Claude Code** — the AI tool that reads your files
   - Install: `npm install -g @anthropic-ai/claude-code`
   - Requires [Node.js](https://nodejs.org/) (download the LTS version)
   - See [Claude Code docs](https://docs.anthropic.com/en/docs/claude-code) for setup

3. **A text editor** — anything you're comfortable with
   - Recommended: [VS Code](https://code.visualstudio.com/) (free, works everywhere)
   - Anything works: Notepad, TextEdit, Sublime Text, vim

## Setup

```bash
# 1. Clone the repository
git clone https://github.com/N4M3Z/forge-user.git
cd forge-user

# 2. Open steering/Identity.md in your editor and personalize it

# 3. Start Claude Code
claude

# 4. Type /Tour to see what you have
```

## Verify Your Setup

After starting Claude Code, follow the checks in [VERIFY.md](VERIFY.md) to confirm everything works.

## Optional Modules

Once you're comfortable with the basics, you can add modules to expand your AI's capabilities. Modules are independent repositories you clone into the `modules/` directory.

### Recommended Modules

| Module | What it adds |
|--------|-------------|
| [forge-council](https://github.com/N4M3Z/forge-council) | Multi-specialist code review — your AI convenes a panel of experts to debate changes |
| [forge-avatar](https://github.com/N4M3Z/forge-avatar) | Deep identity — digital avatar, beliefs, strategies, communication preferences |
| [forge-steering](https://github.com/N4M3Z/forge-steering) | Behavioral rules — teach your AI what to do and what to avoid |

### Installing a Module

```bash
# From your forge-user directory:
cd modules
git clone https://github.com/N4M3Z/forge-council.git
```

After cloning a module, ask your AI to install it for you:

> "I cloned forge-council into modules/. Can you help me set it up?"

Your AI will read the module's README and walk you through any setup steps. Some modules are standalone Claude Code plugins — check each module's README for instructions.

For automated module management (hook-based dispatch, skill discovery across modules), see [forge-core](https://github.com/N4M3Z/forge-core) below.

## Upgrading to forge-core

If you outgrow forge-user and want the full developer framework (hook system, automated dispatching, Rust-powered tools, multi-vault support), see [forge-core](https://github.com/N4M3Z/forge-core). forge-user skills and steering files are compatible — you can migrate without starting over.
