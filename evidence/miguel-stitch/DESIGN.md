---
name: AgentHub Enterprise Admin
colors:
  surface: '#f8f9ff'
  surface-dim: '#d2daea'
  surface-bright: '#f8f9ff'
  surface-container-lowest: '#ffffff'
  surface-container-low: '#eff4ff'
  surface-container: '#e6eefe'
  surface-container-high: '#e1e8f8'
  surface-container-highest: '#dbe3f2'
  on-surface: '#141c27'
  on-surface-variant: '#59413b'
  inverse-surface: '#29313c'
  inverse-on-surface: '#eaf1ff'
  outline: '#8d716a'
  outline-variant: '#e1bfb7'
  surface-tint: '#ac3411'
  primary: '#932300'
  on-primary: '#ffffff'
  primary-container: '#b53a17'
  on-primary-container: '#ffdbd2'
  inverse-primary: '#ffb5a1'
  secondary: '#516072'
  on-secondary: '#ffffff'
  secondary-container: '#d2e1f6'
  on-secondary-container: '#566476'
  tertiary: '#004f8b'
  on-tertiary: '#ffffff'
  tertiary-container: '#0067b3'
  on-tertiary-container: '#d3e4ff'
  error: '#ba1a1a'
  on-error: '#ffffff'
  error-container: '#ffdad6'
  on-error-container: '#93000a'
  primary-fixed: '#ffdbd1'
  primary-fixed-dim: '#ffb5a1'
  on-primary-fixed: '#3b0800'
  on-primary-fixed-variant: '#881f00'
  secondary-fixed: '#d5e4f9'
  secondary-fixed-dim: '#b9c8dd'
  on-secondary-fixed: '#0e1c2c'
  on-secondary-fixed-variant: '#3a4859'
  tertiary-fixed: '#d3e4ff'
  tertiary-fixed-dim: '#a1c9ff'
  on-tertiary-fixed: '#001c38'
  on-tertiary-fixed-variant: '#004880'
  background: '#f8f9ff'
  on-background: '#141c27'
  surface-variant: '#dbe3f2'
typography:
  headline-xl:
    fontFamily: Hanken Grotesk
    fontSize: 32px
    fontWeight: '600'
    lineHeight: 40px
    letterSpacing: -0.02em
  headline-xl-mobile:
    fontFamily: Hanken Grotesk
    fontSize: 26px
    fontWeight: '600'
    lineHeight: 32px
    letterSpacing: -0.015em
  headline-lg:
    fontFamily: Hanken Grotesk
    fontSize: 24px
    fontWeight: '600'
    lineHeight: 32px
    letterSpacing: -0.015em
  headline-md:
    fontFamily: Hanken Grotesk
    fontSize: 18px
    fontWeight: '600'
    lineHeight: 24px
    letterSpacing: -0.01em
  headline-sm:
    fontFamily: Hanken Grotesk
    fontSize: 15px
    fontWeight: '600'
    lineHeight: 20px
    letterSpacing: -0.005em
  body-lg:
    fontFamily: Hanken Grotesk
    fontSize: 15px
    fontWeight: '400'
    lineHeight: 22px
  body-md:
    fontFamily: Hanken Grotesk
    fontSize: 13px
    fontWeight: '400'
    lineHeight: 18px
  body-sm:
    fontFamily: Hanken Grotesk
    fontSize: 12px
    fontWeight: '400'
    lineHeight: 16px
  label-md:
    fontFamily: JetBrains Mono
    fontSize: 12px
    fontWeight: '500'
    lineHeight: 16px
    letterSpacing: 0.02em
  label-sm:
    fontFamily: JetBrains Mono
    fontSize: 11px
    fontWeight: '500'
    lineHeight: 14px
    letterSpacing: 0.03em
  code-inline:
    fontFamily: JetBrains Mono
    fontSize: 12px
    fontWeight: '400'
    lineHeight: 16px
rounded:
  sm: 0.125rem
  DEFAULT: 0.25rem
  md: 0.375rem
  lg: 0.5rem
  xl: 0.75rem
  full: 9999px
spacing:
  gutter: 1rem
  gutter-compact: 0.5rem
  margin: 1.5rem
  margin-mobile: 0.75rem
  space-xs: 0.25rem
  space-sm: 0.5rem
  space-md: 0.75rem
  space-lg: 1.25rem
  space-xl: 2rem
---

## Brand & Style

This design system serves an enterprise B2B control plane for autonomous and human-assisted agent operations. The target audience includes operational administrators, infrastructure engineers, compliance officers, and team supervisors who spend full workdays managing high-throughput workflows, configuring model policies, and debugging edge cases.

The design movement is **Corporate / Modern** optimized for dense data clarity and high operational trust. Key characteristics:
- **Calm Authority**: The interface recedes into the background, prioritizing agent state observability and dense tabular data over ornamental styling.
- **High-Velocity Utility**: Workflows demand clear spatial hierarchy, compact interactive states, and unambiguous interactive triggers.
- **Architectural Rigor**: Visual structure is enforced through strict vertical rhythm, standardized structural borders, and purposeful contrast boundaries rather than heavy drop shadows or decorative gradients.

## Colors

The palette is engineered for WCAG AA/AAA compliance across data-intensive displays, with a clear separation between content chrome, persistent state surfaces, and semantic indicators.

### Surface and Structure Tokens
- **Canvas (`#F7F8FA`)**: The foundational application background behind workspace panels and dashboards.
- **Surface (`#FFFFFF`)**: Elevated planes, data tables, sheets, modal dialogues, and form containers.
- **Subtle (`#E7ECF2`)**: Secondary containers, table header fills, segmented control tracks, and zebra-striping.
- **Border (`#788598`)**: Structural partitions, cell borders, outline buttons, and idle field perimeters.

### Typography and Iconography Tokens
- **Ink (`#18202B`)**: Primary text, titles, table cell contents, and active iconography. Delivers sharp legibility against canvas and white surfaces.
- **Muted (`#505E70`)**: Secondary metadata, timestamps, input placeholders, column descriptors, and breadcrumb trails.

### Interactive and Semantic Tokens
- **Action (`#B53A17`)**: Primary actions, commit buttons, key batch executions, and active navigation indicators.
- **Focus (`#164DCC`)**: High-visibility focus indicators, active selection halos, and tab group markers.
- **Danger (`#A32A26`)**: Destructive actions, fatal execution states, and quota violation banners.
- **Success (`#236344`)**: Deployed states, passing healthchecks, verified policies, and metric gains.
- **Warning (`#765000`)**: Latency degradations, non-blocking throttles, and credential expiration alerts.
- **Info (`#204EA0`)**: Runtime logs, informational callouts, and configuration hints.

## Typography

The type scale combines **Hanken Grotesk** for clean, crisp structural hierarchy and UI scanning with **JetBrains Mono** for machine values, token keys, IDs, metrics, timestamps, and status labels.

- **Scale Rationale**: Base desktop data displays standardly run on `body-md` (13px/18px) to maximize row visibility without eye fatigue. Headings remain restrained and compact to avoid displacing critical analytical content.
- **Tabular Alignment**: All numerical values, metrics, and tabular cell records must be rendered with tabular figures enabled (`font-variant-numeric: tabular-nums`) to preserve column alignment across real-time data streams.

## Layout & Spacing

The layout is built upon an adaptive 12-column fluid grid system pinned to a persistent navigation rail on desktop viewports.

### Breakpoints & Layout Architecture
- **Desktop (≥ 1280px)**: 12-column grid. Left sidebar rail fixed at 240px or collapsable to 64px. Gutter is `gutter` (1rem / 16px). Outer padding uses `margin` (1.5rem / 24px).
- **Tablet (768px – 1279px)**: 8-column grid. Sidebar rail collapses to an off-canvas drawer. Gutter shifts to `gutter-compact` (0.5rem / 8px). Outer margin is `gutter` (1rem / 16px).
- **Mobile (< 768px)**: 4-column grid. Full-bleed data sheets stack vertically. Horizontal scroll applied to wide data grids with sticky primary ID columns. Outer margin reduces to `margin-mobile` (0.75rem / 12px).

### Spacing Cadence
Density is the primary requirement. All spacing rules follow strict 4px sub-grid multiples:
- Use `space-xs` (4px) for inline badge padding, iconography margins, and compact stack adjustments.
- Use `space-sm` (8px) for input padding, list item vertical gaps, and button horizontal margins.
- Use `space-md` (12px) for card body padding, filter toolbar gaps, and metadata rows.
- Use `space-lg` (20px) for widget boundaries, pane divisions, and drawer content sections.
- Use `space-xl` (32px) strictly for top-level page headers and section delimiters.

## Elevation & Depth

This design system avoids heavy drop shadows to prevent visual noise in dense admin contexts. Spatial hierarchy is communicated through **tonal layers** and **crisp 1px structural borders**.

- **Level 0 (Canvas Base)**: `#F7F8FA`. Serves as the backdrop for all screens.
- **Level 1 (Surface Cards & Panes)**: `#FFFFFF` bounded by a continuous 1px solid `#788598` border (or `#E7ECF2` for internal dividers). No shadow is used at rest.
- **Level 2 (Dropdowns, Popovers, & Tooltips)**: `#FFFFFF` with a 1px solid `#788598` perimeter and a minimal low-diffusion ambient shadow: `0 4px 12px rgba(24, 32, 43, 0.08)`.
- **Level 3 (Modal Dialogs & Slide-out Panels)**: `#FFFFFF` framed by a 1px solid `#788598` perimeter, backed by a scrim of `#18202B` at 40% opacity, paired with an ambient elevation shadow: `0 8px 24px rgba(24, 32, 43, 0.16)`.
- **Interactive Focus & Active Elevation**: Interactive states never move visually along the Z-axis. Focus is always delineated via a 2px outline in `#164DCC` with a 1px separation offset from the element border.

## Shapes

The interface utilizes **Soft (Level 1)** geometry to balance technical efficiency with visual approachability.

- **Base Radius (0.25rem / 4px)**: Applied uniformly to standard interactive controls, including buttons, text input fields, dropdown triggers, badges, and inline chips.
- **Container Radius (0.5rem / 8px)**: Applied to cards, data table wrappers, modal containers, and slide-over drawers (`rounded-lg`).
- **Surface Nesting Rule**: Internal containers nested within parent cards must step down their border radius to match the base radius (4px) or use straight 0px dividers to prevent optical distortion at inner corners.

## Components

### Buttons
- **Primary**: Solid background in Action (`#B53A17`), label text in `#FFFFFF`. Hover state deepens to 90% luminance. Active state sets at 80%. Height: 32px (compact) or 36px (default). Padding: 0 12px.
- **Secondary / Outline**: Transparent background, 1px solid Border (`#788598`), text in Ink (`#18202B`). Hover fills with Subtle (`#E7ECF2`).
- **Destructive**: Solid Danger (`#A32A26`) background with white text, or transparent background with Danger text and border.
- **Focus State**: All buttons receive a 2px outline in Focus (`#164DCC`) with a 1px offset on keyboard navigation.

### Inputs & Form Fields
- **Container**: Height: 32px (dense) or 36px. Background: `#FFFFFF`. Border: 1px solid `#788598`.
- **Typography**: Text in Ink (`#18202B`) using `body-md`. Placeholder in Muted (`#505E70`).
- **Focus**: Border switches to Focus (`#164DCC`), accompanied by a 1px box shadow in `#164DCC`.
- **Validation**: Error fields display a 1px solid Danger (`#A32A26`) perimeter with helper text rendered in Danger `body-sm`.

### Data Tables & Lists
- **Header Row**: Height 36px, background `#E7ECF2`, text in Muted (`#505E70`) uppercase `label-sm`. 1px bottom border in `#788598`.
- **Body Rows**: Height 40px (default) or 32px (high-density compact mode). Background `#FFFFFF`. Bottom border 1px solid `#E7ECF2`. Hover state highlights row in `#F7F8FA`.
- **Cells**: Padding 0 12px. Primary identifiers render in JetBrains Mono (`label-md`).

### Status Badges & Chips
- **Geometry**: Height 20px, 4px corner radius, padding 2px 6px.
- **Typography**: Monospaced `label-sm` in all caps.
- **Variants**:
  - *Active / Success*: Background `#EAF3ED`, text `#236344`, 1px border `#236344`.
  - *Warning*: Background `#FCF7EB`, text `#765000`, 1px border `#765000`.
  - *Critical / Danger*: Background `#FBEBEB`, text `#A32A26`, 1px border `#A32A26`.
  - *Info / Neutral*: Background `#EBF2FC`, text `#204EA0`, 1px border `#204EA0`.

### Selection Controls (Checkboxes & Radios)
- **Checkboxes**: 14x14px square, 2px radius, 1px border `#788598`. Checked state fills with Action (`#B53A17`) containing a crisp white tick.
- **Radio Buttons**: 14x14px circle, 1px border `#788598`. Selected state features an inner 6px solid circle in Action (`#B53A17`).

### Operational Cards & Panels
- **Structure**: Surface `#FFFFFF`, 1px solid border in `#788598`, 8px corner radius.
- **Padding**: Header (12px 16px), Content (16px), Footer (12px 16px with `#E7ECF2` top border).
- **Metric Cards**: Display metric value in `headline-lg`, metric label in Muted (`#505E70`) `body-sm`, and change delta tags via colored badges.