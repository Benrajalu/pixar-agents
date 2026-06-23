# Component Mappings — ItemReplace Reference

## Library Reference

Components are exported from the Pixar UI library:
- **File Key**: `JjaALcWYWcqGtanufVLKYj`
- **Library URL**: https://www.figma.com/design/JjaALcWYWcqGtanufVLKYj/Pixar--UI-v1.81

### Replacement Components

To insert components from the external library, use `figma.importComponentByKeyAsync(componentKey)` for single components or `figma.importComponentSetByKeyAsync(componentKey)` for component sets with variants.

| Component | Component Key | Type |
|-----------|---------------|------|
| `Item/Default` | `12f28c1dd225f641bb28bca77bf473cacba2ae88` | component |
| `Item/Button` | `2a904d41f78338a80baddc65cc1893f076f69a24` | component_set |
| `Item/Navigation` | `f7194afbd0dacbf8385c21abb5fe0f8fe879d704` | component_set |
| `Item/Input` | `28f19bf38e201f78a18748637b627d0456c3d1a5` | component_set |

**Example usage in `use_figma`:**
```javascript
// For Item/Default (single component)
const itemDefault = await figma.importComponentByKeyAsync('12f28c1dd225f641bb28bca77bf473cacba2ae88');
const instance = itemDefault.createInstance();

// For Item/Navigation (component set with variants)
const itemNavSet = await figma.importComponentSetByKeyAsync('f7194afbd0dacbf8385c21abb5fe0f8fe879d704');
// Get a specific variant from the set
const defaultVariant = itemNavSet.defaultVariant;
const instance = defaultVariant.createInstance();
```

### Component Mappings

| Deprecated Component | Replacement |
|---------------------|-------------|
| `DEPRECATED ItemInfo/Default` | `Item/Default` |
| `DEPRECATED ItemInfo/Tag` | `Item/Default` (set Content `type: 'tagTitle'`) |
| `DEPRECATED ItemInfo/IconLarge` | `Item/Default` |
| `DEPRECATED ItemInfo/Secondary` | `Item/Default` (set Content `type: 'secondary'`) |
| `DEPRECATED ItemData/Primary/Default` | `Item/Default` (enable `show_data`, detect layout — see below) |
| `DEPRECATED ItemData/Primary/Accent` | `Item/Default` (enable `show_data`, detect layout, `semantic: 'accent'`) |
| `DEPRECATED ItemData/Primary/Success` | `Item/Default` (enable `show_data`, detect layout, `semantic: 'success'`) |
| `DEPRECATED ItemData/Primary/Danger` | `Item/Default` (enable `show_data`, detect layout, `semantic: 'danger'`) |
| `DEPRECATED ItemData/Secondary/Default` | `Item/Default` (enable `show_data`, detect layout) |
| `DEPRECATED ItemNavigate/Default` | `Item/Navigation` |
| `DEPRECATED ItemNavigate/Accent` | `Item/Navigation` |
| `DEPRECATED ItemNavigate/Recommended` | `Item/Navigation` |
| `DEPRECATED ItemNavigate/Tag` | `Item/Navigation` |
| `DEPRECATED ItemNavigate/Danger` | `Item/Navigation` |
| `DEPRECATED ItemNavigate/Success` | `Item/Navigation` |
| `DEPRECATED ItemCheckbox/Default` | `Item/Input` |
| `DEPRECATED ItemRadio/Default` | `Item/Input` |

## Property Mapping

The new Item components expose **boolean toggles** and **variants**, not text properties. To transfer text content, you must find and edit nested text nodes directly.

### Component Properties (setProperties)

**Item/Default:**
| Property | Type | Description |
|----------|------|-------------|
| `show_prefix_icon#79197:6` | boolean | Show/hide prefix icon |
| `show_data#79197:7` | boolean | Show/hide data section (displays price format) |
| `show_suffix_icon#79197:8` | boolean | Show/hide suffix icon |

**Content section (`↳ Content`):**
| Property | Type | Values | Description |
|----------|------|--------|-------------|
| `type` | variant | `default`, `secondary`, `tagTitle`, `tagMeta` | Content layout type |
| `meta_content#79159:4` | text | — | Secondary text content |
| `show_meta#79142:3` | boolean | — | Show/hide meta text |
| `tag_type#79149:0` | instance_swap | — | Tag component variant (for tag types) |

**Configuring Content for tag display:**

> **Important:** Always map the `tag_type` from the deprecated component. The deprecated `ItemInfo/Tag` carries a specific `Tag/*` variant (e.g. `Tag/Danger`, `Tag/Accent`) inside its `Tag/*` instance. Identify its node ID and pass it via `INSTANCE_SWAP` — do **not** leave the default.
>
> Known `tag_type` node IDs:
> | Tag variant | Node ID |
> |-------------|---------|
> | `Tag/Accent` | `1:463` |
> | `Tag/AccentWeak` | `140:1391` |
> | `Tag/Danger` | `14:3314` |
> | `Tag/NeutralStrong` | `140:1394` |
> | `Tag/Promote` | `140:1398` |
> | `Tag/Success` | `140:1402` |
> | `Tag/Warning` | `140:1406` |
>
> To detect which tag is used in the deprecated component, find the `Tag/*` instance and match its component name to the table above.

```javascript
// 1. Detect tag variant from the deprecated component
const oldTag = deprecated.findOne(n => n.type === 'INSTANCE' && n.name.startsWith('Tag/'));
const tagNodeId = oldTag?.mainComponent?.id ?? '14:3314'; // fallback to Tag/Danger

// 2. Configure the content section
const contentSection = newInstance.findOne(n => n.name === '↳ Content' && n.type === 'INSTANCE');
contentSection.setProperties({
  'type': 'tagTitle',             // Tag as title, meta below
  'meta_content#79159:4': 'Additional info',
  'tag_type#79149:0': tagNodeId   // Transfer the tag variant from the deprecated instance
});

// 3. To change tag label text, find the Tag's text node:
const tagText = contentSection.findOne(n => n.type === 'TEXT' && n.name.includes('label'));
if (tagText) {
  await figma.loadFontAsync(tagText.fontName);
  tagText.characters = 'Custom tag';
}
```

**Enabling data section for ItemData migrations:**

> **Important:** Always detect the layout from the deprecated component. Do **not** default to `'text'`.
> - If the deprecated instance contains `↳ Price/L` or `↳ Price/M` child nodes → use `layout: 'price'`
> - Otherwise → use `layout: 'text'`

```javascript
// When replacing DEPRECATED ItemData, enable the data section
newInstance.setProperties({ 'show_data#79197:7': true });

// Detect layout type from the deprecated component
const hasPriceLayout = !!deprecated.findOne(n => n.name === '↳ Price/L' || n.name === '↳ Price/M');

const dataSection = newInstance.findOne(n => n.name === '↳ Data' && n.type === 'INSTANCE');

if (hasPriceLayout) {
  // --- PRICE layout ---
  dataSection.setProperties({
    'layout': 'price',
    'semantic': 'neutral',     // Options: neutral, accent, danger, success, promote
    'main-data#79173:36': true,
    'price-info#43882:0': true,
    'reduction#61928:9': hasReduction,  // true if deprecated has a reduction %
    'icon#43462:19': false
  });

  // Transfer price values by setting properties on ↳ Price/.Content sub-instances
  // findAll returns [Price/L content, Price/M content] in order
  const priceContents = newInstance.findAll(n => n.name === '↳ Price/.Content' && n.type === 'INSTANCE');

  // Main price (Price/L)
  priceContents[0]?.setProperties({
    'content-value#38708:6': '18',    // integer part from deprecated
    'content-decimal#38708:8': '00',  // decimal part from deprecated
    'content-currency#38708:2': '€',  // currency symbol from deprecated
    'strike#38708:0': false
  });

  // Old/crossed price (Price/M) — if present
  priceContents[1]?.setProperties({
    'content-value#38708:6': '90',
    'content-decimal#38708:8': '00',
    'content-currency#38708:2': '€',
    'strike#38708:0': true            // always true for old price
  });

  // Reduction label (e.g. "-60%") — set via text node
  if (hasReduction) {
    const redLabel = newInstance.findOne(n => n.type === 'TEXT' && n.name === 'content-label');
    if (redLabel) {
      await figma.loadFontAsync(redLabel.fontName);
      redLabel.characters = '-60%';  // transfer from deprecated
    }
  }
} else {
  // --- TEXT layout ---
  dataSection.setProperties({
    'layout': 'text',
    'semantic': 'neutral',
    'content-data#43441:10': 'Data',           // transfer from deprecated
    'content-data-info#43441:9': 'Data info',  // transfer from deprecated
    'data-info#43441:11': true,
    'icon#43462:19': false
  });
}
```

**Data section layout variants:**
- `layout: 'price'` — Structured currency display with formatted number, decimal, currency symbol, optional old price with strikethrough and reduction %
- `layout: 'text'` — Simple plain text labels ("Data" / "Data info")

**Item/Input:**
| Property | Type | Description |
|----------|------|-------------|
| `show_data#79525:3` | boolean | Show/hide data section |
| `show_suffix#79525:2` | boolean | Show/hide suffix |
| `state` | variant | `default`, `selected`, etc. |
| `platform` | variant | `mobile`, `desktop` |

**Item/Navigation:**
| Property | Type | Description |
|----------|------|-------------|
| `show_addon#79173:31` | boolean | Show/hide addon (prices, badges) |
| `show_prefix_icon#79173:26` | boolean | Show/hide prefix icon |
| `state` | variant | `default`, `hover`, etc. |
| `viewport` | variant | `mobile`, `desktop` |

## Transferring Text Content

Text must be set by finding child TEXT nodes and overriding their `characters` property:

```javascript
async function setText(instance, nodeName, text) {
  const textNode = instance.findOne(n => n.type === 'TEXT' && n.name === nodeName);
  if (textNode) {
    await figma.loadFontAsync(textNode.fontName);
    textNode.characters = text;
    return true;
  }
  return false;
}

// Text node names in Item components:
// - Title: 'content-title'
// - Description/Meta: '↳ Meta'
await setText(newInstance, 'content-title', 'My Title');
await setText(newInstance, '↳ Meta', 'My Description');
```

## Icon Transfer

Icons use `INSTANCE_SWAP` properties with **node ID references**, not component keys. The glyph property expects a node ID like `"18:441"` that points to a glyph component in the library.

```javascript
// 1. Find the icon in the deprecated component - look for Glyph instances
const oldIcon = deprecated.findOne(n => n.name === '◇ Glyph' && n.type === 'INSTANCE');

// 2. Get the node ID that the old icon's glyph property references
const oldIconContainer = oldIcon?.parent?.parent;  // Navigate to Icon instance
let glyphNodeId = null;
if (oldIconContainer?.type === 'INSTANCE') {
  const glyphProp = Object.keys(oldIconContainer.componentProperties).find(k => k.includes('glyph'));
  if (glyphProp) {
    glyphNodeId = oldIconContainer.componentProperties[glyphProp].value;
  }
}

// 3. Find the Icon container in the new component  
const newIconContainer = newInstance.findOne(n => 
  n.name.includes('Icon') && 
  n.type === 'INSTANCE' && 
  n.componentProperties && 
  Object.keys(n.componentProperties).some(k => k.includes('glyph'))
);

// 4. Set the glyph property using the node ID reference
if (newIconContainer && glyphNodeId) {
  const glyphProp = Object.keys(newIconContainer.componentProperties).find(k => k.includes('glyph'));
  newIconContainer.setProperties({ [glyphProp]: glyphNodeId });
}
```

**Key insight:** The glyph property value is a **node ID** (e.g., `"18:441"` for AirConditioning icon) that references a glyph component in the library file, not a component key. Copy the node ID from the source icon to the target.

**For deeply nested icons (e.g., Data section icons in Item/Input):**
```javascript
const dataSection = newInstance.findOne(n => n.name === '↳ Data' && n.type === 'INSTANCE');
const iconInData = dataSection?.findOne(n => n.name.includes('Icon') && n.type === 'INSTANCE');
const innerIcon = iconInData?.findOne(n => 
  n.type === 'INSTANCE' && 
  n.componentProperties && 
  Object.keys(n.componentProperties).some(k => k.includes('glyph'))
);
if (innerIcon && glyphNodeId) {
  const glyphProp = Object.keys(innerIcon.componentProperties).find(k => k.includes('glyph'));
  innerIcon.setProperties({ [glyphProp]: glyphNodeId });
}
```

## Variant-Specific Notes

For **Item/Input** (replacing ItemCheckbox/ItemRadio):
- The input type (checkbox vs radio) is determined by the variant you select from the component set
- Use `itemInputSet.findChild(n => n.name.includes('checkbox'))` or `'radio'` to get the right variant

For **Item/Navigation** (replacing ItemNavigate):
- Addon data (prices, badges) must be configured by finding nested nodes
- The chevron icon is built-in and shows automatically

## Positioning

```javascript
// Copy position from deprecated instance
newInstance.x = deprecatedInstance.x;
newInstance.y = deprecatedInstance.y;

// Match parent if within an auto-layout frame
const parent = deprecatedInstance.parent;
if (parent) {
  const index = parent.children.indexOf(deprecatedInstance);
  if (index >= 0) {
    parent.insertChild(index, newInstance);
  }
}

// Match width
newInstance.resize(deprecatedInstance.width, newInstance.height);
```

## Complete Migration Example

```javascript
// Full migration of a DEPRECATED ItemInfo/Default
const deprecated = figma.getNodeById('1:205');
const parent = deprecated.parent;

// 1. Import component
const itemDefault = await figma.importComponentByKeyAsync('12f28c1dd225f641bb28bca77bf473cacba2ae88');
const newInstance = itemDefault.createInstance();

// 2. Position
const idx = parent.children.indexOf(deprecated);
newInstance.x = deprecated.x;
newInstance.y = deprecated.y;
parent.insertChild(idx, newInstance);
newInstance.resize(deprecated.width, newInstance.height);

// 3. Extract text from deprecated component
const oldTitle = deprecated.findOne(n => n.type === 'TEXT' && n.name.includes('title'));
const oldMeta = deprecated.findOne(n => n.type === 'TEXT' && n.name.includes('meta'));

// 4. Transfer text to new component (use exact node names)
const newTitle = newInstance.findOne(n => n.type === 'TEXT' && n.name === 'content-title');
const newMeta = newInstance.findOne(n => n.type === 'TEXT' && n.name === '↳ Meta');

if (newTitle && oldTitle) {
  await figma.loadFontAsync(newTitle.fontName);
  newTitle.characters = oldTitle.characters;
}
if (newMeta && oldMeta) {
  await figma.loadFontAsync(newMeta.fontName);
  newMeta.characters = oldMeta.characters;
}

// 5. Remove deprecated
deprecated.remove();
```

## Error Handling

- **Font loading**: Always call `figma.loadFontAsync(textNode.fontName)` before setting `characters`
- **Missing text nodes**: Text node names may vary — use `findOne` with flexible matching (`includes`)
- **Unmatched semantics**: Some deprecated variants (Tag, IconLarge) don't have direct equivalents — configure the closest match
- **Complex layouts**: If the deprecated component has nested overrides, extract and reapply them manually

### Debugging Structure

Before migrating, analyze the frame to get correct instance IDs:

```javascript
const mainFrame = figma.getNodeById('FRAME_ID');
const structure = mainFrame.children.map(c => ({
  id: c.id,
  name: c.name,
  type: c.type
}));
return structure;
```

This helps identify the actual instance IDs (which may differ from component definition IDs).
