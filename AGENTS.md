# AutoDoc — Agent instructions

AutoDoc automates two Figma workflows: completing component documentation and migrating deprecated component instances.

## Architecture

```
AI Agent ──> Figma MCP ──> Figma
```

Agents read component context from Figma via MCP tools and write changes back directly using `mcp_figma_use_figma`.

## Actions

| Action | Purpose |
|--------|---------|
| `ComponentDoc` | Complete component documentation in a Figma frame (sections, accessibility, interactive demos) |
| `ItemReplace` | Scan a Figma frame for deprecated `DEPRECATED Item*` instances and replace them with their modern equivalents |

## MCP dependency

Both actions require the **Figma MCP**. The key tools used are:

| Tool | Purpose |
|------|---------|
| `mcp_figma_get_design_context` | Read component structure, variants, and states |
| `mcp_figma_get_screenshot` | Capture visual of component or frame |
| `mcp_figma_get_metadata` | Get node IDs, layer types, and positions |
| `mcp_figma_use_figma` | Write changes to Figma (text, instances, properties) |

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

## Constraints

- Start a fresh conversation for each action.
- Run one agent per Figma file at a time.
- Always ask the user to create a named version in Figma before making destructive changes (ItemReplace).
