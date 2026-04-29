# AutoDoc — Agent instructions

AutoDoc automates three design system workflows: completing component documentation in Figma, migrating deprecated component instances, and generating Supernova documentation copy.

## Architecture

```
AI Agent ──┬──> Figma MCP ──> Figma
           └──> Supernova MCP ──> Supernova (design system docs)
```

Agents read component context from Figma via MCP tools and write changes back directly using `mcp_figma_use_figma`. They can also query the Supernova design system documentation for existing documentation examples.

## Actions

| Action | Purpose |
|--------|---------|
| `ComponentDoc` | Complete component documentation in a Figma frame (sections, accessibility, interactive demos) |
| `ItemReplace` | Scan a Figma frame for deprecated `DEPRECATED Item*` instances and replace them with their modern equivalents |
| `SupernovaDoc` | Generate copy-paste ready Supernova documentation (Overview, Usage, Content, Accessibility) from a Figma component-doc frame |

## MCP dependency

Both actions require the **Figma MCP**. The key tools used are:

| Tool | Purpose |
|------|---------|
| `mcp_figma_get_design_context` | Read component structure, variants, and states |
| `mcp_figma_get_screenshot` | Capture visual of component or frame |
| `mcp_figma_get_metadata` | Get node IDs, layer types, and positions |
| `mcp_figma_use_figma` | Write changes to Figma (text, instances, properties) |

### Figma context retrieval default

When reading design context for AutoDoc actions, call `mcp_figma_get_design_context` with `disableCodeConnect: true` by default.

- Do not prompt to connect Code Connect mappings unless the user explicitly asks to set up or manage Code Connect.
- Prioritize direct design context retrieval to keep documentation workflows uninterrupted.

The **Supernova MCP** provides access to existing design system documentation:

| Tool | Purpose |
|------|---------|
| `mcp_supernova_get_documentation_page_list` | List all documentation pages (foundations, components, tokens) |
| `mcp_supernova_get_documentation_page_content` | Get content of specific documentation pages (max 5 at once) |
| `mcp_supernova_get_design_system_component_list` | List all design system components |
| `mcp_supernova_get_design_system_component_detail` | Get component details — Figma link, Storybook URL, statuses (max 10) |
| `mcp_supernova_get_figma_component_list` | List all Figma components from the design system file |
| `mcp_supernova_get_token_list` | Get all design tokens (IDs, paths, values) |
| `mcp_supernova_get_asset_list` | List all assets in the design system |
| `mcp_supernova_get_asset_detail` | Get asset details — name, description, thumbnail, SVG URL (max 10) |

## Setup

### VS Code

The workspace includes a `.vscode/mcp.json` config that auto-configures the Figma and Supernova MCP servers.

1. Open this workspace in VS Code
2. Accept the trust prompt when VS Code asks to start the MCP servers
3. Authenticate with Figma and Supernova when prompted on first tool use

If you already have Figma or Supernova configured at user level, VS Code merges both configs — no conflict.

### Copilot CLI

Copilot CLI uses a separate config at `~/.copilot/mcp-config.json`. Either:

**Option A — Interactive setup:**
```
copilot
/mcp add
```
Then fill in: Server Name = `figma`, Type = `HTTP`, URL = `https://mcp.figma.com/mcp`

Repeat for Supernova: Server Name = `supernova`, Type = `HTTP`, URL = `https://mcp.supernova.io/mcp/ds/23456`

**Option B — Manual config:**
Merge the content from `mcp-config.copilot-cli.json` into `~/.copilot/mcp-config.json`.

## Key files

| File | Purpose |
|------|---------|
| `component-doc/SKILL.md` | Agent behavior for completing component documentation |
| `component-doc/references/accessibility.md` | Accessibility section spec — template insertion, VoiceOver, TalkBack, ARIA |
| `component-doc/references/screenreader.md` | Screen reader analysis guide |
| `component-doc/references/aria.md` | ARIA roles, states, keyboard patterns |
| `component-doc/references/talkback.md` | TalkBack (Android / Jetpack Compose) reference |
| `component-doc/references/voiceover.md` | VoiceOver (iOS / SwiftUI) reference |
| `item-replace/SKILL.md` | Agent behavior for deprecated item migration |
| `item-replace/references/component-mappings.md` | Component keys, property mappings, migration examples |
| `supernova-doc/SKILL.md` | Agent behavior for generating Supernova documentation |
| `supernova-doc/references/overview-template.md` | Template for Overview page |
| `supernova-doc/references/usage-template.md` | Template for Usage page |
| `supernova-doc/references/content-template.md` | Template for Content page |
| `supernova-doc/references/accessibility-template.md` | Template for Accessibility page |
| `component-doc/references/implementation.md` | Architecture reference (ComponentDoc) |
| `item-replace/references/implementation.md` | Architecture reference (ItemReplace) |

## Running an action

Provide a Figma URL and describe what you need. The agent matches your request to the appropriate action:

```
Complete the documentation for this component: https://www.figma.com/design/abc123/...?node-id=100:200
```

```
Replace deprecated items in this frame: https://www.figma.com/design/abc123/...?node-id=100:200
```

```
Generate Supernova documentation for this component: https://www.figma.com/design/abc123/...?node-id=100:200
```

## Constraints

- Start a fresh conversation for each action.
- Run one agent per Figma file at a time.
- Always ask the user to create a named version in Figma before making destructive changes (ItemReplace).
