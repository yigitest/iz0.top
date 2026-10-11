---
name: recipe-writer
description: "Create or update Hugo recipe pages from images, text, video, audio, transcripts, links, or files. Converts source material into structured recipes under content.en/docs/recipes/ and mirrors translated versions under content.tr/docs/recipes/."
---

# Recipe Writer

Convert supplied recipe material into a clear, accurate Markdown page under `content.en/docs/recipes/` and mirror the translated version under `content.tr/docs/recipes/`. This file contains the complete page format, translation requirements, and theme syntax needed for the task. Do not read example recipes, theme documentation, generated site files, or unrelated content merely to learn formatting.

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

If a new category is necessary, create `<Category>/_index.md` in both `content.en/docs/recipes/` and `content.tr/docs/recipes/` using this exact structure, replacing only the title and icon when a known suitable icon is available:

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

In `content.tr/docs/recipes/<Category>/_index.md`, keep the same category directory name, weight, and params, but translate the `title` to Turkish.

Follow it with:

```markdown
## Recipes
```

(Use `## Tarifler` for `content.tr`.)

Use a concise, human-readable category directory and recipe filename. Keep an existing recipe at its current path when updating it unless the user explicitly requests a move.

## Multilingual Structure and Mirroring

Every recipe must exist in both English and Turkish across two mirrored directory trees:

1. Primary English version under `content.en/docs/recipes/<Category>/<recipe-name>.md`.
2. Translated Turkish version under `content.tr/docs/recipes/<Category>/<recipe-name>.md`.

### Mirroring and Filename Rules

- **Mirror Folder Paths**: The category subfolder path under `content.tr/docs/recipes/` must match `content.en/docs/recipes/` exactly (e.g., `Cookies/`, `Soups/`).
- **Identical Filenames**: Do not change the filename when creating or copying to `content.tr`. The filename must be completely identical in both directories (e.g., `chocolate-chip-cookies.md`). Hugo uses matching filenames to link language translations together.
- **Frontmatter Title Is Critical**: Translate the `title` in the YAML frontmatter to Turkish in the `content.tr` file. This frontmatter `title` is what Hugo displays to users in navigation menus, search results, and page lists, **not** the filename.

## Fixed Recipe Format (English)

Every English recipe must use the following order:

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

## Turkish Translation Guidelines (content.tr)

After writing the English recipe, copy and translate the page into `content.tr/docs/recipes/<Category>/<recipe-name>.md`:

1. **Frontmatter**:
   - Translate `title` into clear, natural Turkish (e.g., `title: "Çikolata Parçacıklı Kurabiye"` or `title: "Sarımsak Çorbası (Soupe à l'Ail)"`).
2. **H1 Title**:
   - Translate the main H1 heading to match the Turkish title.
3. **Recipe Summary**:
   - Use `> [!NOTE]` with bold label `> **Tarif Özeti**`.
   - Translate the 1-2 sentence summary into Turkish.
4. **Ingredients (`## Malzemeler`)**:
   - Table headers must be `| Malzeme | Miktar | Notlar |`.
   - Translate all ingredient names and preparation notes.
   - Use standard Turkish culinary units where appropriate (`su bardağı`, `yemek kaşığı`, `tatlı kaşığı`, `çay kaşığı`, `g`, `ml`, `adet`).
5. **Instructions (`## Hazırlanışı`)**:
   - Keep the `{{% steps %}}` shortcode wrapper.
   - Translate each numbered stage header (e.g., `1. ## Hamuru Hazırlayın`, `2. ## Fırında Pişirin`).
   - Translate step instructions into clear, imperative Turkish sentences.
6. **Notes and Tips (`## Şefin Notları` or `## Faydalı Notlar`)**:
   - Translate supplementary tips and alert blocks (e.g., `> [!TIP]`, `> [!IMPORTANT]`, `> [!WARNING]`).
7. **Workflow (`## İş Akışı`)**:
   - If a Mermaid diagram is present, translate node labels into Turkish while preserving valid Mermaid syntax.

Turkish Recipe Template:

````markdown
---
title: "Tarif Adı"
---

# Tarif Adı

> [!NOTE]
> **Tarif Özeti**  
> Yemeğin lezzetini, dokusunu, porsiyon veya ayırt edici özelliklerini özetleyen 1-2 kısa cümle.

## Malzemeler

| Malzeme | Miktar | Notlar |
| :--- | :--- | :--- |
| Malzeme adı | Gram, ml, su bardağı vb. | Doğrama, oda sıcaklığı, soyma notları vb. |

## Hazırlanışı

{{% steps %}}
1. ## Aşama Başlığı
   Açık ve uygulanabilir yönergeler. Varsa süre, sıcaklık, ateş seviyesi ve görsel/dokusal kontrol işaretlerini belirtin.

2. ## Sonraki Aşama
   İşlemleri kronolojik sırayla açıklayın.
{{% /steps %}}
````

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

Add a Mermaid workflow only for recipes with branching, parallel, or otherwise complex preparation. Omit it for straightforward linear recipes. Place it after the instructions under `## Workflow` (or `## İş Akışı` in `content.tr`).

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

- Create or update the recipe in both `content.en/docs/recipes/<Category>/<recipe-name>.md` and `content.tr/docs/recipes/<Category>/<recipe-name>.md`.
- Mirror all folder paths and keep the file name identical across both directories.
- If a new category is created, create mirrored `<Category>/_index.md` files in both directories.
- Never edit generated files under `public/` or `resources/`.
- Update existing recipes instead of creating duplicates unless the user requests otherwise.
- Do not move or rename existing content without an explicit reason.

## Final Check

Before finishing, verify:

- Both files exist: `content.en/docs/recipes/<Category>/<recipe-name>.md` and `content.tr/docs/recipes/<Category>/<recipe-name>.md`.
- Category directory path and recipe filename are identical in both directories.
- The `content.tr` frontmatter contains the translated Turkish `title`.
- The `content.tr` recipe body is translated into natural Turkish (title, summary, ingredients, instructions, and notes).
- Each file has frontmatter title and exactly one matching H1.
- Summary, ingredients, and instructions appear in the required order.
- Ingredients are represented by a Markdown table (`Ingredient | Amount | Notes` in EN; `Malzeme | Miktar | Notlar` in TR).
- Instructions use the `steps` shortcode and remain chronological.
- The `steps` shortcode is paired and closed correctly.
- Hints use Markdown alert syntax, never the deprecated `hint` shortcode.
- Any Mermaid diagram is valid and agrees with the instructions.
- No unsupported details were invented.

Report the final recipe paths for both languages and any unresolved ambiguity in one concise response.
