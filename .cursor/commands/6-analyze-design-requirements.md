---
description: Analyze Figma design files to extract implementation requirements
globs:
alwaysApply: false
---
"do fa; Analyze the Figma design file at [FIGMA_LINK] using Figma MCP servers to extract comprehensive implementation requirements.

INTENTION: Transform visual designs into actionable technical specifications by systematically 
analyzing design tokens, components, states, interactions, and responsive behavior. This analysis 
will serve as the foundation for accurate implementation that matches design intent.

Using the Figma MCP server connection, perform the following analysis:

1. DESIGN TOKENS EXTRACTION (Priority: Use get_variable_defs tool)
   CRITICAL: Extract the actual Figma variable names using get_variable_defs for the node/page
   This ensures we capture the design system's naming conventions for reuse.
   
   For each variable category, document:
   - **Variable Name** (as defined in Figma, e.g., 'color/primary/500', 'spacing/lg')
   - **Value** (actual value, e.g., '#3B82F6', '16px')
   - **Scope** (where it's used: colors, typography, spacing, etc.)
   - **Semantic Meaning** (purpose/usage guidelines)
   
   Extract and organize:
   - Color variables (primary, secondary, semantic colors, states)
   - Typography variables (font families, sizes, weights, line heights, letter spacing)
   - Spacing variables (margins, paddings, gaps, named by scale)
   - Border radius variables
   - Shadow/elevation variables
   - Animation/transition timing variables
   - Breakpoint variables for responsive design
   - Opacity/alpha variables
   - Z-index layering variables

2. COMPONENT INVENTORY (Use get_code_connect_map when available)
   - Use get_code_connect_map to identify components already mapped to code
   - List all reusable components in the design
   - Document component hierarchy and composition
   - Identify atomic components vs. composite components
   - Note component variants and their naming conventions
   - Document component properties and their accepted values
   - For each component, note which design tokens/variables it uses
   - Cross-reference with existing codebase components (via Code Connect)

3. COMPONENT STATES ANALYSIS
   - Default state
   - Hover state
   - Active/pressed state
   - Focused state
   - Disabled state
   - Loading state
   - Error state
   - Success state
   - Document state transitions and triggers

4. INTERACTION BEHAVIOR
   - Click/tap interactions
   - Drag and drop behavior
   - Form interactions and validation patterns
   - Navigation patterns
   - Modal and overlay behavior
   - Scroll interactions
   - Animation sequences and micro-interactions
   - Gesture support (swipe, pinch, etc.)

5. RESPONSIVE DESIGN ANALYSIS
   - Mobile breakpoint behavior (< 768px)
   - Tablet breakpoint behavior (768px - 1024px)
   - Desktop breakpoint behavior (> 1024px)
   - Layout changes across breakpoints
   - Component adaptations for different screen sizes
   - Touch vs. mouse interaction considerations
   - Orientation handling (portrait/landscape)

6. ACCESSIBILITY CONSIDERATIONS
   - Color contrast ratios
   - Text sizing and readability
   - Focus indicators
   - ARIA labels and roles (where implied by design)
   - Touch target sizes

OUTPUT FORMAT:
Create a design-analysis-[DATE].md file that includes:

## Design Overview
- Brief description of the design
- Key user flows
- Design system references

## Design Tokens (Extracted from Figma Variables)
Document the actual Figma variable names for reusability:

```json
{
  "colors": {
    "figmaVariableName": "color/primary/500",
    "value": "#3B82F6",
    "cssVarName": "--color-primary-500",
    "usage": "Primary action buttons, links"
  },
  "typography": {
    "figmaVariableName": "typography/heading/h1/size",
    "value": "32px",
    "cssVarName": "--text-h1-size",
    "usage": "Page main headings"
  },
  "spacing": {
    "figmaVariableName": "spacing/lg",
    "value": "24px",
    "cssVarName": "--spacing-lg",
    "usage": "Large gaps between sections"
  },
  "borders": {
    "figmaVariableName": "border/radius/md",
    "value": "8px",
    "cssVarName": "--border-radius-md",
    "usage": "Cards, buttons"
  },
  "shadows": {
    "figmaVariableName": "shadow/elevation/2",
    "value": "0 4px 6px rgba(0,0,0,0.1)",
    "cssVarName": "--shadow-elevation-2",
    "usage": "Elevated cards"
  },
  "animations": {
    "figmaVariableName": "animation/duration/normal",
    "value": "200ms",
    "cssVarName": "--animation-duration-normal",
    "usage": "Standard transitions"
  },
  "breakpoints": {
    "figmaVariableName": "breakpoint/tablet",
    "value": "768px",
    "cssVarName": "--breakpoint-tablet",
    "usage": "Tablet layout switch"
  }
}
```

### Variable Naming Convention
Document the pattern used in Figma variables:
- Naming structure: `{category}/{subcategory}/{variant}`
- Examples: `color/primary/500`, `spacing/md`, `typography/body/regular`
- This naming should be preserved in code implementation for consistency

## Component Library
For each component, document which design tokens it uses for future reusability.

### [Component Name]
- **Purpose**: 
- **Variants**: 
- **States**: 
- **Props/Properties**: 
- **Composition**: 
- **Design Tokens Used**:
  - Colors: (list Figma variable names, e.g., `color/primary/500`)
  - Typography: (list Figma variable names, e.g., `typography/body/medium`)
  - Spacing: (list Figma variable names, e.g., `spacing/md`, `spacing/lg`)
  - Borders: (list Figma variable names, e.g., `border/radius/sm`)
  - Shadows: (list Figma variable names, e.g., `shadow/elevation/1`)
  - Animations: (list Figma variable names, e.g., `animation/duration/fast`)
- **Responsive Behavior**: 
- **Code Connect**: (if component already exists in codebase, note the mapping)

Example:
### Button Component
- **Purpose**: Primary call-to-action element
- **Variants**: Primary, Secondary, Tertiary, Destructive
- **States**: Default, Hover, Active, Disabled, Loading
- **Props/Properties**: size (sm, md, lg), variant, disabled, loading
- **Composition**: Icon (optional) + Label + Loading Spinner (conditional)
- **Design Tokens Used**:
  - Colors: `color/primary/500`, `color/primary/600`, `color/neutral/white`
  - Typography: `typography/button/medium`, `typography/button/large`
  - Spacing: `spacing/xs` (padding), `spacing/sm` (icon gap)
  - Borders: `border/radius/md`
  - Shadows: `shadow/elevation/1` (hover state)
  - Animations: `animation/duration/fast` (state transitions)
- **Responsive Behavior**: Touch targets expand to 44px min on mobile
- **Code Connect**: Mapped to `components/Button.tsx`

## Implementation Requirements
1. **Phase 1: Design Token System**
   - [ ] Create design token mapping file (e.g., `design-tokens.json`, `theme.config.js`)
   - [ ] Map Figma variable names to code variable names (preserve naming structure)
   - [ ] Implement tokens as CSS variables, theme config, or style dictionary
   - [ ] Document token usage guidelines
   - [ ] Set up token update workflow for design changes

2. **Phase 2: Design System Foundation**
   - [ ] Set up responsive breakpoint system using extracted breakpoint variables
   - [ ] Configure animation/transition utilities
   - [ ] Establish component composition patterns
   - [ ] Set up accessibility defaults (focus styles, contrast, etc.)

3. **Phase 3: Atomic Components**
   - [ ] List each atomic component with:
     - Figma component name and node ID
     - Design tokens used
     - States and variants
     - Code Connect mapping (if exists)
     - Acceptance criteria
   
4. **Phase 4: Composite Components**
   - [ ] List each composite component with:
     - Figma component name and node ID
     - Child components and composition
     - Design tokens used
     - Code Connect mapping (if exists)
     - Acceptance criteria

5. **Phase 5: Layout & Responsive Implementation**
   - [ ] Implement responsive layouts using breakpoint tokens
   - [ ] Test across all defined breakpoints
   - [ ] Verify spacing consistency with spacing tokens

6. **Phase 6: Interactions & States**
   - [ ] Implement interactive behaviors using animation tokens
   - [ ] Add micro-interactions and animations
   - [ ] Verify all component states match design

## Technical Considerations
- Framework-specific implementation notes
- State management requirements
- Performance optimization opportunities
- Browser/device compatibility concerns
- **Design Token Management Strategy**:
  - Preferred format for tokens (CSS custom properties, JS objects, style dictionary)
  - Token update workflow when designs change in Figma
  - Version control for design tokens
  - Token documentation and usage examples

## Design Token Export Reference
Create a reusable reference file mapping Figma variables to code:

```
design-tokens-reference.json
├── Figma variable name
├── CSS variable name
├── Value
├── Category/type
└── Usage context
```

This reference file should be:
- Version controlled
- Used as single source of truth for design values
- Imported/referenced by all components
- Updated when Figma design system changes
- Documented with examples of usage

FILE ORGANIZATION:
- Create analysis file in the same directory as the related story/task
- Use naming convention: design-analysis-[STORY_ID].md
- Link the analysis file in the relevant story or task file"

