---
name: describe
description: Add a brief description next to whatever the user selected in the IDE (or names in the arguments) - links, plugins, components, terms, tools, books. Use when the user asks to describe, annotate, or explain items in a note.
---

Target: the text selected in the IDE (the ide_selection in context). If arguments are given, treat them as the items to describe, or as a file name to process. If there is neither a selection nor arguments, ask what to describe.

For every item in the target that has no description yet:

1. Work out what the item is:
   - URL or markdown link: fetch it with WebFetch and ask for a one-sentence summary of what the page offers.
   - Plugin, component, term, tool, book, person: use WebSearch (or WebFetch if a URL is attached) to find what it is and what it does.
2. If the fetch fails (HTTP 405 or captcha from food4rhino.com, blocked domain, timeout), fall back to WebSearch. For well-known terms that need no lookup, use own knowledge. Never invent details from the name alone.
3. Edit the file in place: append ` — <description>` to the same line as the item. Keep numbering, links, wikilinks, images and any existing descriptions unchanged. Change only the selected lines.

Style:
- Write in the language of the note (Russian for this vault unless the surrounding text is English).
- One short sentence saying concretely what it does or is for, not just its category. Match the length and tone of existing descriptions in the note.
- Keep original spelling of names and technical terms (Grasshopper, NURBS, Weaverbird).

Reporting:
- Flag dead links, unexpected redirects and duplicates within the note. Do not silently delete or rewrite them.
- If a description came from search rather than the page itself, say so and list the sources.
- End with one line naming the file and how many items were described.
