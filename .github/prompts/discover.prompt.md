---
mode: agent
description: "Find Copilot assets by describing what you want to implement — e.g. /discover EntraID authentication"
tools: ["edit/editFiles"]
---

# Discover — Find Assets by Description

Find relevant Copilot assets by describing what you want to implement or improve.

## Usage

```
/discover <what you want>
```

Examples:
- `/discover EntraID authentication`
- `/discover container deployment with Kubernetes`
- `/discover React testing patterns`

## Flow

### Step 1: Search

Run `discover_assets` with the user's description as `query`.
If the user is in a project directory, also pass `path` to combine stack detection with the query.

### Step 2: Present Results

Show the matching assets as a numbered list with type, name, description, and trust badge.

If no results found, suggest broadening the query or running `/forge` for full stack-based discovery.

### Step 3: Install

Ask which assets to install: "all", specific numbers, or "none".
Use `install_asset` with `confirm: false` to preview, then `confirm: true` to write.
