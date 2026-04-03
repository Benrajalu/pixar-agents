# AutoDoc — Implementation Reference

> **Purpose of this file:** Architecture reference for AI agents working in this codebase. Covers how the two actions work, which MCP tools they use, and where to find per-action detail.
>
> **What belongs here:**
> - System architecture and data flow
> - MCP tool surface
> - Per-action workflow summary and reference file pointers
>
> **What does NOT belong here:**
> - Per-action schemas, property mappings, and examples — those live in each action's instruction file
> - Component keys for the Pixar UI library — those live in `ItemReplace/ItemReplace-instructions.md`
>
> **Adding a new action:** Add an instruction file in a new folder, update the actions table and reference files table below, and update `AGENTS.md`.

## Overview

AutoDoc provides two agent actions for Figma automation:

1. **ComponentDoc** — Complete component documentation in a Figma frame: sections, accessibility specs, and interactive demos
2. **ItemReplace** — Scan a Figma frame for deprecated `DEPRECATED Item*` instances and replace them with their modern equivalents from the Pixar UI library

## Actions

### ComponentDoc

The agent is given a Figma frame URL containing an in-progress component documentation page. It:

1. Uses `mcp_figma_get_design_context` and `mcp_figma_get_screenshot` to read the frame structure and identify the component(s)
2. Identifies which documentation sections are present (Definition of Ready, Component breakdown, Main component showcase, Component behaviour, Supernova assets)
3. Completes each relevant section: fills text content, inserts component instances for interactive demos, and writes the accessibility section using the spec defined in `Accessibility-instructions.md`
4. Writes all changes back to Figma via `mcp_figma_use_figma`

The accessibility section follows a structured screen reader spec (VoiceOver, TalkBack, ARIA) — see `ComponentDoc/Accessibility-instructions.md` for the full schema and agent behavior.

### ItemReplace

The agent is given a Figma frame URL containing deprecated Item component instances. It:

1. Asks the user to create a named version in Figma as a restore point before making any changes
2. Scans the frame for instances with names matching `DEPRECATED Item*` patterns using `mcp_figma_use_figma`
3. Pre-imports all required replacement component types from the Pixar UI library
4. For each deprecated instance: creates the replacement, transfers icon and text content, positions it, and removes the deprecated original
5. Validates the result with `mcp_figma_get_screenshot`

See `ItemReplace/ItemReplace-instructions.md` for component keys, property mappings, and migration rules.

## MCP Tools

Both actions use the **Figma MCP** (official `mcp_figma_*` tools). No Figma Desktop bridge or plugin is required.

Extract `fileKey` and `nodeId` directly from the Figma URL before calling any tool.

| Tool | Purpose |
|------|---------|
| `mcp_figma_get_design_context` | Primary context tool: component structure, variants, states, reference code, screenshot |
| `mcp_figma_get_screenshot` | Capture a visual of a component or frame |
| `mcp_figma_get_metadata` | Structural overview: node IDs, layer types, positions |
| `mcp_figma_use_figma` | Write changes to Figma: text, instances, properties |
| `mcp_figma_search_design_system` | Find a component by name when no specific node ID is known |

## Architecture

```
AI Agent ──> Figma MCP ──> Figma
   |              |              |
   |-- get context -->           |
   |<-- component data --        |
   |              |              |
   |-- mcp_figma_use_figma ----->|
   |              |              |-- update text
   |              |              |-- create instances
   |              |              |-- set properties
```

## Reference Files

| File | Content |
|------|---------|
| `ComponentDoc/ComponentDoc-instructions.md` | Agent behavior: section identification, content rules, demo instance creation |
| `ComponentDoc/Accessibility-instructions.md` | Accessibility spec: merge analysis, focus order, VoiceOver / TalkBack / ARIA property tables |
| `ItemReplace/ItemReplace-instructions.md` | Migration rules: deprecated component patterns, replacement component keys, property mappings |


