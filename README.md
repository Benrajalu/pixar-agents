# AutoDoc for Designers

AutoDoc helps designers do three tasks faster using GitHub Copilot:

1. Fill in component documentation in Figma.
2. Replace old deprecated components with current ones.
3. Generate documentation text for Supernova.

You do not need to be an engineer to use this repo.

## What You Need

Before you start:

1. A GitHub account with access to this repository.
2. VS Code installed.
3. GitHub Copilot access.
4. A Figma account with a full seat (editing rights).
5. A Supernova account (found in 1Password).

## Step 1: Clone This Repository

Cloning means "download a local copy of this project".

### Option A (Recommended): GitHub Desktop

1. Open GitHub Desktop.
2. Go to **File > Clone Repository**.
3. Open the **URL** tab.
4. Paste this URL:

```text
https://github.com/Benrajalu/pixar-agents.git
```

5. Choose a local folder where you want the project.
6. Click **Clone**.

### Option B: Terminal

1. Open Terminal.
2. Run:

```bash
git clone https://github.com/Benrajalu/pixar-agents.git
cd pixar-agents
```

## Step 2: Open the Project in VS Code

1. Open VS Code.
2. Click **File > Open Folder...**.
3. Select the cloned `pixar-agents` folder.

VS Code may ask if you trust this workspace.

4. Click **Trust**.

This is required so Copilot can use the project configuration.

## Step 3: Connect Copilot to Figma and Supernova

This repository already includes MCP setup for VS Code in `.vscode/mcp.json`.

On your first Copilot run:

1. Open Copilot Chat.
2. Send one of the example prompts from the "How to Use" section below.
3. When prompted, sign in to Figma and Supernova.

After sign-in, Copilot can read design context and generate or update content for you.

## How to Use (Copy-Paste Prompts)

Start a fresh Copilot chat for each action.

### 1) Complete Component Documentation

Paste this (replace with your real Figma URL):

```text
Complete the documentation for this component: https://www.figma.com/design/FILE_KEY/FILE_NAME?node-id=100-200
```

Expected result:

- Copilot completes sections in the component doc frame.
- Includes behavior, usage details, and accessibility content.

### 2) Replace Deprecated Items

Before running this action, create a named Figma version first.

In Figma:

- Go to **File > Save to version history** (or create a named version in version history).

Then paste this prompt:

```text
Replace deprecated items in this frame: https://www.figma.com/design/FILE_KEY/FILE_NAME?node-id=100-200
```

Expected result:

- Copilot scans for deprecated `DEPRECATED Item*` instances.
- Replaces them with modern equivalents.

### 3) Generate Supernova Documentation

Paste this prompt:

```text
Generate Supernova documentation for this component: https://www.figma.com/design/FILE_KEY/FILE_NAME?node-id=100-200
```

Expected result:

- Copilot generates ready-to-use documentation text for:
  - Overview
  - Usage
  - Content
  - Accessibility

## Important Rules

1. Use one action per chat conversation.
2. Run one agent per Figma file at a time.
3. Always create a named Figma version before replacement tasks.

## Troubleshooting

### Copilot cannot access Figma or Supernova

- Make sure you completed the login prompts in Copilot Chat.
- Retry the same prompt once after login.

### Nothing happens after prompt

- Check that your Figma URL is valid and includes `node-id`.
- Make sure the workspace is trusted in VS Code.

### I prefer Copilot CLI instead of VS Code

You can also configure MCP servers in Copilot CLI.

Option A (interactive):

```bash
copilot
/mcp add
```

Add:

- `figma` -> `https://mcp.figma.com/mcp`
- `supernova` -> `https://mcp.supernova.io/mcp/ds/23456`

Option B (manual):

- Merge settings from `mcp-config.copilot-cli.json` into `~/.copilot/mcp-config.json`.

## Repository Structure (Quick View)

- `component-doc/` -> instructions and references for component documentation automation
- `item-replace/` -> instructions and mappings for deprecated item replacement
- `supernova-doc/` -> instructions and generated examples for Supernova documentation
- `AGENTS.md` -> high-level operating instructions for this repo

## Need Help Writing the Prompt?

Use this simple format:

```text
[Action] for this Figma frame: [paste figma URL]
```

Examples of `[Action]`:

- `Complete the documentation`
- `Replace deprecated items`
- `Generate Supernova documentation`
