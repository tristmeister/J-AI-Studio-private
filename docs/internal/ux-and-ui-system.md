# UX And UI System

## UX Principles

### Prompt First

The prompt is the user's primary creative instrument. The bottom prompt bar is the stable home base in both gallery mode and Zen mode. Important generation controls may sit beside it, but they should not compete with it.

### Progressive Control

The default loop should expose only the controls needed for fast generation:

- model or workflow
- aspect or size
- steps
- variants for images
- generate

Advanced controls belong in the side panel unless they are part of the core loop. LoRA should follow this pattern: a compact status/control in the prompt bar can show whether LoRA is active, while detailed selection and strengths belong in the controls panel.

### Visual Review Is The Center

Outputs are the main content. The UI should recede around images and videos, especially in Zen mode and the fullscreen viewer. Controls should be dense, precise, and predictable.

### Local Transparency

When something depends on ComfyUI, the UI should say so through available options, disabled states, or settings status. Missing files or nodes should never feel mysterious.

### Reuse Beats Reconfiguration

The viewer's "Copy All Settings" and "Use as Start Image" flows are important because they turn browsing into iteration. LoRA selections should join saved generation settings so a user can reproduce or branch from an output.

## Information Architecture

### Gallery Mode

Gallery mode is a working board. It prioritizes recent outputs, queued cards, live previews, cancel controls, and quick opening into the viewer.

### Zen Mode

Zen mode is a focused creative loop. It prioritizes fullscreen output, the prompt bar, minimal inline controls, and a collapsible side panel.

### Viewer

The viewer is for inspection and reuse. It supports zoom, pan, navigation, details, copying, downloading, deleting, and using an image as a start image.

### Settings

Settings are operational, not decorative. They cover connection, workflows, generation preferences, gallery maintenance, and updates.

## UI System

### Visual Language

- Dark, neutral, low-chroma interface.
- Images and videos carry the visual energy.
- Controls are compact, scan-friendly, and utilitarian.
- Borders and subtle backgrounds create hierarchy; avoid decorative surfaces.
- Motion should feel responsive and brief.

### Color Tokens

Core color tokens live in `src/styles/01-base.css`:

- `--background`: app canvas
- `--card`: panels, prompt container, settings surfaces
- `--input`: controls and input wells
- `--border` / `--border-strong`: structure and hover emphasis
- `--foreground`: primary text
- `--muted-foreground`: secondary text and labels
- `--primary`: active/primary action
- `--destructive`: destructive state

Use tokens instead of raw colors for app UI.

### Typography

- Font: Inter.
- Most control text is 12-14px.
- Labels use 11-12px with medium weight.
- Buttons use 12-13px with medium or semibold weight.
- Preserve tabular numerals for numeric controls and generation progress.
- Avoid oversized headings inside control panels.

### Shape And Spacing

- Base radius: `--radius` (`0.625rem`).
- Compact controls use radius minus 2-3px.
- Floating shells use `calc(var(--radius) + 4px)` or `+ 6px`.
- Common gaps are 6, 8, 10, 12, and 14px.
- Cards should be individual functional surfaces, not nested decorative containers.

### Components

#### Prompt Bar

The prompt bar is fixed at the bottom and contains:

- main prompt textarea
- optional negative prompt drawer
- model picker
- aspect picker
- compact numeric controls
- generate button

LoRA should integrate without making the bar crowded. Preferred pattern:

- Compact "LoRA" button or badge in inline settings.
- Badge shows inactive, active count, or active stack name.
- Detailed picker opens in the side controls panel or a small popover.

#### NumberPicker

Use for numeric generation controls. It supports:

- step buttons
- click-to-edit
- wheel adjustment
- press-and-hold stepping
- compact and fill variants

Use it for LoRA strength values, with precision around `0.05` or `0.01`.

#### StudioSelect

Use for option lists from ComfyUI metadata. For LoRA names, a searchable select will likely be needed because local LoRA lists can be long.

#### ModelPicker And AspectPicker

These are custom compact popovers. Follow their interaction style for any LoRA picker:

- click trigger
- popover menu above prompt bar when used inline
- active state is visually obvious
- tooltip on unfamiliar controls

#### Sidebar Controls

The sidebar is the right place for detailed generation controls:

- seed
- start image
- text encoder
- VAE
- weight dtype
- CFG
- sampler
- scheduler

LoRA stack controls belong here initially.

## LoRA UX Requirements

Minimum useful version:

- Show LoRA controls only when current workflow can apply LoRAs.
- Allow selecting one installed LoRA.
- Allow model strength and CLIP strength.
- Allow disabling without losing selection.
- Persist settings in local draft.
- Save LoRA settings into gallery metadata.
- "Copy All Settings" should restore LoRA settings.

Preferred expanded version:

- Multi-LoRA stack.
- Add/remove/reorder LoRAs.
- Per-LoRA enabled toggle.
- Shared strength mode and separate model/CLIP mode.
- Search/filter by folder or filename.
- Indicate incompatible workflow/node state.

## Accessibility And Interaction

- Every icon-only control needs an accessible label and tooltip.
- Keyboard escape should close transient surfaces.
- Pointer drag should not accidentally open viewer details.
- Avoid text truncation that hides important file names without tooltip backup.
- Maintain reduced-motion behavior.

## Copy Voice

Use plain operational language:

- "Choose model"
- "Aspect ratio"
- "Generate"
- "Use as Start Image"
- "Clear all cache"
- "LoRA"
- "Strength"

Avoid explaining implementation details in the main UI unless needed for troubleshooting.
