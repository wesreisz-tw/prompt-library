---
description: Generate AEM Content Fragment Model implementation guide from story requirements
globs:
alwaysApply: false
---
"do fas; Generate an AEM Content Fragment Model implementation guide for [STORY_ID].

INTENTION: Transform story requirements into step-by-step AEM authoring instructions that enable content authors to create and configure CFMs correctly. Analyze existing models for reuse opportunities and provide clear, actionable implementation steps.

PROCESS:

1. Read specifications/[STORY_ID]/story.md and extract all content structure requirements
2. Review docs/aem/content-fragment-models.md to identify reusable models
3. For each field requirement, determine if it should use an existing model (Fragment Reference) or be a new field
4. Apply AEM best practices: prefer Fragment References for reusable concepts (images, links, rich text)
5. If ambiguous whether to reuse an existing model, ask the user interactively
6. Recommend folder structure following /content/dam/dceo/ patterns
7. For accessibility fields, ensure images have altText and interactive elements have proper labels

OUTPUT FORMAT:

Create specifications/[STORY_ID]/[STORY_ID]-AEM-CFM-GUIDE.md with:

# AEM Content Fragment Model Implementation Guide
## Story: [STORY_ID]

### Executive Summary
- Number of new models to create
- Existing models to reuse
- Number of content fragments needed
- Estimated setup time

### 1. Model Reuse Analysis
Tables showing which existing models to use and why, which new models to create and why

### 2. Folder Structure Setup
- Model configuration paths (/conf/dceo/settings/dam/cfm/models/)
- Content storage paths (/content/dam/dceo/)
- Rationale for organization

### 3. Model Creation Instructions
For each new model:
- Configuration path and description
- Step-by-step AEM navigation instructions
- For each field, provide boxed specifications with:
  * Field Label and Property Name
  * Field Type (Single line text, Fragment Reference, etc.)
  * Required/Optional
  * Description for AEM UI
  * Validation rules (character limits, patterns, etc.)
  * Default values
  * Help text for authors
  * Explanation of why this field type/approach was chosen

### 4. Content Fragment Creation
- Ordered steps (create dependencies first)
- Specific fragment names and field values based on story
- Location recommendations

### 5. GraphQL Query Reference
- Example query the frontend will use
- Expected response structure

### 6. Testing Checklist
- AEM author environment validation
- GraphQL testing steps
- Frontend integration checks
- Accessibility verification
- Responsive testing

### 7. Common Issues & Solutions
- Typical problems authors might encounter
- Clear resolution steps

### 8. Maintenance Notes
- How to update content later
- Reordering content
- Future extensibility considerations

### 9. Acceptance Criteria Validation
- Map back to story acceptance criteria with checkboxes

### 10. Next Steps
- Post-implementation actions
- Estimated time breakdown

Keep instructions clear for users with minimal AEM experience. Use visual formatting (boxes, tables, numbered lists) for clarity."

