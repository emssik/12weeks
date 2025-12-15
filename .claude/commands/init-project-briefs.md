---
description: Creates empty project brief templates based on 12-week planning form
argument-hint: <path-to-filled-12week-form>
---

# Initialize Project Briefs

<why>
Before generating a 12-week plan, you need detailed briefs for each project. This command creates the structure - empty templates with only the obvious information pre-filled. You then fill in the details through your own analysis and planning work.
</why>

<sources>
<filled_form>
@$ARGUMENTS
</filled_form>

<template_tech>
@templates/project-brief.md
</template_tech>

<template_general>
@templates/project-brief-general.md
</template_general>
</sources>

<task>
1. Read the filled 12-week planning form
2. Extract project names from "Cele na te 12 tygodni" section (Cel 1, Cel 2, etc.)
3. For each project, determine template type:
   - **Tech template** (`project-brief.md`): if description mentions: repo, API, MCP, backend, frontend, kod, aplikacja, system, platforma
   - **General template** (`project-brief-general.md`): for everything else (marketing, lejek, dokumenty, prawne, sprzedaż, osobiste)
4. For each project:
   a) Create a copy of the appropriate template at: `projects/[slugified-name].md`
   b) Fill in ONLY these fields from the form:
      - Project name (from "What?")
      - "What is it about?" section (from "What?" description)
   c) Leave ALL other sections empty for the user to fill

Slugify rules: lowercase, spaces to dashes, remove special characters
Example: "ATD Lejek sprzedażowy" → `atd-lejek-sprzedazowy.md`
</task>

<output>
After creating files, list what was created:

```
Created briefs:
- projects/[name1].md ← [Goal 1 name] (tech/general)
- projects/[name2].md ← [Goal 2 name] (tech/general)
...

Next step: Fill out each brief, especially:
- Current state
- Implementation stages (concrete steps)
```
</output>

<efficiency>
To minimize token usage:
- Use file copy/write operations, not generation
- Edit only the specific lines that need project-specific data
- Template content stays as-is, just replace placeholders
</efficiency>
