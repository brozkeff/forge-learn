# Verify Your Setup

Run these three checks after starting Claude Code in your forge-user directory. If all pass, you're good to go.

## Check 1: Can the AI see your files?

Ask: **"What files are in this project?"**

It should list your directories (`steering/`, `skills/`, `modules/`) and files (`CLAUDE.md`, `README.md`, etc.). If it can't see them, make sure you started Claude Code from inside the `forge-user` directory.

## Check 2: Does /Tour work?

Type: **/Tour**

The AI should greet you and walk through your available skills. If it says "I don't know that command", check that `.claude-plugin/plugin.json` exists and points to `./skills`.

## Check 3: Does it know your name?

Ask: **"What's my name?"**

If you've edited `steering/Identity.md`, it should know. If it doesn't, double-check that you saved the file and that `CLAUDE.md` references `steering/Identity.md`.

## All Three Passed?

You're set up. Try `/Explain` on any file you're curious about, or `/Kickstart` to start a project.

## Something Failed?

Type `/FixIt` and describe what happened — your AI will help you diagnose the problem.
