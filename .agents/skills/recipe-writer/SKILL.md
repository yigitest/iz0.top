---
name: recipe-writer
description: "Create or update Hugo recipe pages from images, text, video, audio, transcripts, links, or files. Use when converting source material into a structured recipe under content.en/docs/recipes/."
---

# Recipe Writer

Convert supplied recipe material into a clear, accurate Markdown page under `content.en/docs/recipes/`. This file contains the complete page format and theme syntax needed for the task. Do not read example recipes, theme documentation, generated site files, or unrelated content merely to learn formatting.

## Input Handling

1. Inspect every supplied input before writing.
2. For video or audio, use available speech, captions, transcript, visible text, and relevant frames.
3. Merge repeated facts from multiple inputs into one coherent recipe.
4. Preserve explicit quantities, units, temperatures, times, yield, equipment settings, and operation order.
5. Remove conversational filler, sponsorship, unrelated commentary, and duplicated steps.
6. Do not invent missing ingredients, quantities, timings, temperatures, yields, or techniques.
7. If an ambiguity prevents a usable recipe, ask one concise question. Otherwise, retain the ambiguity as a clearly labeled note.

## Minimal Repository Inspection

Keep repository reads narrowly scoped:

1. List only the immediate directories and recipe filenames under `content.en/docs/recipes/`.
2. Prefer an existing category whose name clearly matches the dish.
3. Search for a likely duplicate using the dish name and close filename variants. Read only a likely duplicate before deciding whether to update it.
4. Do not open recipes solely as formatting examples. The required format is defined below.
5. Do not inspect `themes/`, `public/`, or `resources/`; the required theme syntax is defined below.
6. Create a new category only when no existing category is a reasonable semantic match.

If a new category is necessary, create `<Category>/_index.md` with this exact structure, replacing only the title and icon when a known suitable icon is available:

```yaml
---
title: Category Name
weight: 101
params:
  bookHidden: false
  bookToC: true
  bookCollapseSection: false
  bookFlatSection: false
  bookIcon: icon-name
---
```

Follow it with:

```markdown
## Recipes
```

Use a concise, human-readable category directory and recipe filename. Keep an existing recipe at its current path when updating it unless the user explicitly requests a move.

## Language

Write exclusively in the English language. Keep all titles, section headers, instructions, notes, and ingredient names in English.

## Fixed Recipe Format

Every recipe must use the following order:

1. Frontmatter with title
2. One H1 recipe title matching the frontmatter
3. A short summary hint
4. Ingredients
5. Instructions
6. Optional useful notes, serving suggestions, storage, or workflow diagram

Ingredients must always appear before instructions. Use this template and replace the placeholders:

````markdown
---
title: Title of the Recipe
---

# Title of the Recipe

> [!NOTE]
> **Recipe Summary**  
> Brief 1-2 sentence description highlighting key flavors, texture, yield/servings, or distinctive characteristics of the dish.

## Ingredients

| Ingredient | Amount | Notes |
| :--- | :--- | :--- |
| Ingredient name | Use grams, ml, cups, etc. | Dicing, room temperature, peeling notes, etc. |

## Instructions

{{% steps %}}
1. ## Step Header
   Clear and actionable instructions. Specify time, temperature, heat level, and visual or textural cues if available in the source.

2. ## Next Step Header
   Describe actions in chronological order. Include relevant ingredient amounts within the steps where helpful.
{{% /steps %}}
````

Formatting rules:

- Put one ingredient on each table row.
- Put preparation details such as "finely chopped" or "at room temperature" in the `Notes` column when practical.
- Use `-` for an amount that the source genuinely does not specify; do not estimate or invent it.
- Group instructions into meaningful stages. Each stage must contain one or more complete actions.
- Keep prose concise and practical. Use imperative instructions.
- Include equipment settings and safety-critical handling when supplied or necessary, especially for pressure cooking, hot oil, raw meat, allergens, and storage.
- Verify that every ingredient mentioned in the instructions appears in the table and that each listed ingredient is accounted for when the source explains its use.

## Hugo Book Features

The site supports the following features directly. Use them when they improve the recipe; do not read theme documentation to rediscover their syntax.

### Steps

Use the `steps` shortcode for the instruction section. Each numbered item begins with an H2 stage title, followed by indented Markdown content:

```tpl
{{% steps %}}
1. ## Prepare the Dough
   Mix ingredients until smooth and uniform.

2. ## Bake
   Bake in a preheated oven for the duration specified in the source.
{{% /steps %}}
```

Keep numbering sequential. Indent each stage description by three spaces so it belongs to the numbered item.

### Hints

Use Markdown alerts sparingly for information that should stand apart from the procedure. Do not use the deprecated `hint` shortcode.

```markdown
> [!NOTE]
> Supplementary context or the recipe summary.

> [!TIP]
> A useful serving suggestion or reliable success cue.

> [!IMPORTANT]
> Information the cook must notice before continuing.

> [!WARNING]
> An important caveat, allergen note, or handling warning.

> [!CAUTION]
> A critical burn, pressure, contamination, or food-safety warning.
```

Use `NOTE` for the recipe summary. Do not duplicate the same information in multiple alerts.

### Mermaid Diagrams

Add a Mermaid workflow only for recipes with branching, parallel, or otherwise complex preparation. Omit it for straightforward linear recipes. Place it after the instructions under `## Workflow`.

````markdown
## Workflow

```mermaid
flowchart TD
    A[Prepare Ingredients] --> B[Mix Batter]
    B --> C[Bake and Cool]
    C --> D[Serve]
```
````

Mermaid rules:

- Use `flowchart TD` by default.
- Keep node labels short and useful.
- Represent parallel preparations as separate branches that merge at the correct stage.
- Ensure the diagram matches the written instructions exactly.
- Do not add CSS classes, custom initialization, or decorative complexity.

## File Operations

- Create or update only the recipe and, when required, its category `_index.md`.
- Ensure all target files are located under `content.en/docs/recipes/`.
- Never edit generated files under `public/` or `resources/`.
- Update a likely existing recipe instead of creating a duplicate unless the user requests otherwise.
- Do not move or rename existing content without an explicit reason.

## Final Check

Before finishing, verify:

- The file is under `content.en/docs/recipes/` in the best matching category.
- The page has frontmatter title and exactly one matching H1.
- The summary, ingredients, and instructions appear in the required order.
- Ingredients are represented by a Markdown table.
- Instructions use the `steps` shortcode and remain chronological.
- The `steps` shortcode is paired and closed correctly.
- Hints use Markdown alert syntax, never the deprecated `hint` shortcode.
- Any Mermaid diagram is valid and agrees with the instructions.
- All text is written completely in English.
- No unsupported details were invented.

Report the final recipe path and any unresolved ambiguity in one concise response.
