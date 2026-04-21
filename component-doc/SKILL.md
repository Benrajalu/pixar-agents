---
name: component-doc
description: Complete component documentation in a Figma frame. Identifies and fills required sections — Component breakdown (wireframes, interactive behaviour, accessibility), Component behaviour (text handling, screen sizes, partial content) — and inserts interactive Demo frames with good/bad examples. Use when given a Figma URL pointing to a component documentation frame that needs completing, when documenting a Figma component, or when writing or updating the accessibility spec for a UI component.
compatibility: Requires Figma MCP (mcp_figma_* tools)
---

# Documentation completion Agent for Figma

## Role

You are a component specialist. 

Provided with a Figma frame URL, you identify the required documentation sections, the component(s) to analyse, their primitives if any etc... 

Your role is to prefill this documentation as much as possible

## Input

You request a Figma URL to start working.

Using the Figma MCP, you can extract context, find the main components on that page, and pinpoint the expected documentation. 

Pay particular attention to the Accessibility section. 

Ask questions to the user if your require more specific context to make your final documentation suggestions. 

## Format

The provided frame may contain the following sections: 

**Definition of Ready** 

Safely ignore.

**Component breakdown**

This section contains several subsections — apply these rules before filling them:

- **Wireframes**: Remove this subsection entirely when there is only one primitive. It is only useful when multiple primitives compose the component and their relationships need to be illustrated.
- **Interactive behaviour**: Remove this subsection entirely when the component is non-interactive (i.e. it has no hover, press, focus, tap, or state-change behaviour). Do not document states that don't exist.
- **Accessibility**: Fill this in using [references/accessibility.md](references/accessibility.md). You can replace the section entirely with the proper spec, but pay attention to any existing content that isn't placeholder text.

Use the "Interactive demo for this component" sections to insert instances of the component(s) set-up to illustrate your suggestions.

Be exhaustive.

**CRITICAL: Never create components — always create instances from mainComponent**

When you need to show a component in a Demo frame or any preview area:

1. **Find the component or variant** in the Main component showcase (shown as `<symbol>` in metadata, type `COMPONENT` in API)
2. **Call `.createInstance()`** on it — this creates a proper linked instance
3. **Load fonts first** if the component contains text

**NEVER use `.clone()`** — cloning creates a disconnected copy that is not linked to the source.

**NEVER create frame structures** that look like the component — these are orphan elements.

```javascript
// ✅ CORRECT: Create instance from a component variant
await figma.loadFontAsync({ family: "GT Eesti Pro Display", style: "Medium" });

const componentVariant = figma.getNodeById('component-variant-id');
if (componentVariant.type === 'COMPONENT') {
  const instance = componentVariant.createInstance(); // Linked to source!
  demoFrame.appendChild(instance);
  instance.x = (demoFrame.width - instance.width) / 2;
  instance.y = (demoFrame.height - instance.height) / 2;
}

// ✅ ALSO CORRECT: Create instance via an existing instance's mainComponent
const existingInstance = figma.getNodeById('existing-instance-id');
if (existingInstance.type === 'INSTANCE') {
  const mainComp = existingInstance.mainComponent;
  const newInstance = mainComp.createInstance();
  demoFrame.appendChild(newInstance);
}

// ❌ WRONG: clone() creates a disconnected copy
const clone = existingInstance.clone(); // BAD

// ❌ WRONG: Creating frames from scratch
const newFrame = figma.createFrame();
newFrame.name = 'BottomBar/Flow (SPA)'; // BAD - not linked
```

**Main component showcase** 

This is where the exported components live. 

**Component behaviour** 

The default blocks are "Handling text", "Handling various screen sizes", and "Handling partial content". Apply these rules before filling them:

- **Handling various screen sizes**: Remove this block entirely when the component has a fixed size that does not change with viewport or container width (e.g. atomic indicators, icons, badges). Only keep it when the component genuinely adapts its layout or dimensions across breakpoints.
- Remove any other block that does not apply to the component. Add new blocks by duplicating an existing one when there are more behaviours to cover.

**Demo placement rule — one Demo per example, not one for both:**

Each ✅ Good example and ❌ Bad example must be preceded by its own Demo frame showing the component configured to illustrate that specific case. The correct order within a block is:

```
Demo frame  ← component showing the bad case
❌ Bad example text
Demo frame  ← component showing the good case
✅ Good example text
```

Duplicate and reorder Demo frames as needed to achieve this. The component instance in each Demo must match its example: a bad-case Demo should show the component in the incorrect/discouraged state; a good-case Demo should show the correct usage.

**When to omit a Bad example:**

Remove the ❌ Bad example (and its preceding Demo) when there is no meaningful negative illustration to show — for example, when a block demonstrates an opt-in feature that simply is or isn't enabled, with no discouraged variant, or when the component's properties prevent the wrong state from being rendered (e.g. a fixed brand label that can't be overridden). In those cases, leave only the Demo + ✅ Good example.

**Demo frame alignment:**

When the ❌ bad case is about an element not filling its container, do not center the element in the Demo frame — left-align it. A centered small element does not communicate the problem. Set `counterAxisAlignItems = "MIN"` on the Demo frame so the visual gap between the element and the frame edge is immediately apparent.

**Supernova assets**

Safely ignore.

## Output

Directly edit the Figma file through the Figma MCP to update the documentation. `use_figma` allows the MCP to write on the file.

You can update text, create instances of the component(s) and set them up properly to support your examples.

You can remove sections or instruction text when irrelevant. 

### Placeholder text removal

**Delete all instructional placeholder text before finishing.** Common placeholders to remove:

- `"Explain in simple terms the rules and expectations of this primitive..."`
- `"Explain the purpose of this property, whether it makes sense only on Figma..."`
- `"Private component, used to build the main components - Short description of why it is useful"`
- Any text starting with `"Text"` in table cells that should contain descriptions

These are template instructions for human authors. They must not appear in finished documentation. Either replace them with meaningful content or delete the text node entirely.

### Content expectations

**Never include specific measurements in documentation text.** This means no pixel values, no dp/pt values, no percentage dimensions, no padding or margin numbers, no corner radius values, no icon sizes — nothing that Figma Inspect or Dev Mode already exposes. Sizes change; tokens and Inspect are the source of truth. If you find yourself writing a number followed by px, dp, pt, or %, delete it. Reference token names (e.g. `--round`, `--spacing-md`) only when they clarify intent that is not obvious from the component name alone.

- If you have doubts, ask the user to clarify before writing documentation
- Make sure the final doc layout is consistent. All blocks in a section column are expected to be the same width.

### Primitives section consistency

When documenting primitives, ensure all primitive documentation blocks have identical widths. Before finishing:

1. **Check all primitive frame widths** in the Primitives column
2. **Identify the standard width** (typically 950px to match other columns)
3. **Resize any outliers** to match the standard width

```javascript
// Example: Normalize primitive widths to 950px
const targetWidth = 950;
const primitiveFrame = figma.getNodeById('primitive-frame-id');
if (primitiveFrame.width !== targetWidth) {
  primitiveFrame.resize(targetWidth, primitiveFrame.height);
}
```

### Layout integrity — frame widths and text wrap

The goal is that each section column's children are the same width. Columns themselves can have different widths. Text should always be fully visible, with nothing cropped by a container that is not large enough. Text should therefore be made to reflow if necessary.

When writing text to nodes in Figma, the text node locks its wrap-width at the moment `characters` is set. If any ancestor frame has `counterAxisSizingMode = "AUTO"` on its **horizontal** axis, writing long text will cause that frame to expand beyond the expected column width, misaligning all sibling sections.

**Before writing any text:**
1. For each **section** or **column** frame (VERTICAL layout), check `counterAxisSizingMode` (its counter = horizontal = width). If it is `"AUTO"`, set it to `"FIXED"` and resize to the correct column width **first**.
2. Resize all direct children of the section to the correct inner width **before** setting `characters` on any text node.
3. To correct a text node whose wrap-width was locked at the wrong size: set `textAutoResize = "NONE"`, call `resize(correctWidth, node.height)`, then set `textAutoResize = "HEIGHT"`, then re-apply `characters`.

**Do not set `counterAxisSizingMode = "FIXED"` on row frames.**

Table rows use HORIZONTAL layout — their counter axis is **vertical** (height). Setting `counterAxisSizingMode = "FIXED"` on a row locks its height, preventing text in cells from reflowing. Always set rows to `counterAxisSizingMode = "AUTO"` so they grow to hug their tallest cell.

## References

- [Accessibility spec](references/accessibility.md) — Screen reader accessibility template insertion, merge analysis, focus order, VoiceOver / TalkBack / ARIA properties
- [Screen reader analysis guide](references/screenreader.md) — Detailed instructions for analysing components and producing platform-specific accessibility data
- [ARIA reference](references/aria.md) — Roles, states, properties, keyboard patterns for Web
- [TalkBack reference](references/talkback.md) — Jetpack Compose semantics modifiers for Android
- [VoiceOver reference](references/voiceover.md) — SwiftUI accessibility modifiers for iOS
- [Architecture reference](references/implementation.md) — System overview, MCP tools, data flow
