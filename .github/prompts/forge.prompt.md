---
mode: agent
description: "One-command Copilot setup — analyze, discover, install, and validate the best assets for your project"
tools: ["search/codebase", "execute/getTerminalOutput", "execute/runInTerminal", "edit/editFiles"]
---

# Forge — Set Up Copilot for Your Project

One command to analyze your codebase, find the best Copilot assets, install them, and validate the result.

## Flow

### Step 1: Discover

Run `discover_assets` with the project path. This returns everything in one call:
- Detected stack (languages, frameworks, CI/CD, cloud)
- Current Copilot setup score with letter grade
- Ranked asset recommendations filtered by what's already installed

Show the score and recommendations to the user as a numbered list.
Ask which assets to install: "all", specific numbers, or "none".

### Step 2: Install

Use `install_asset` with the `assets` array and `confirm: true` to install all selected assets in one batch call. All URLs are fetched in parallel.

If the user wants to preview first, call with `confirm: false`, then call again with `confirm: true`.

### Optional: Generate Instructions

If the project doesn't have a `copilot-instructions.md` and the user wants one:
Run `generate_instructions` with `confirm: true`.

### Step 3: Validate

After installing, run `score_setup` again and show a before/after comparison of the score.
If the score improved, git commit the changes with a conventional commit message.

### Iterate

Ask the user if they want to continue improving. If yes, go back to Step 1.

Stop when:
- The score reaches 8+ out of 10
- No more improvements were made
- The user says to stop

## Safety

- Show recommendations before installing
- Never overwrite without asking
- Max 5 new assets per iteration
