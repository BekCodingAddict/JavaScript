# JavaScript Documentation Repo — Claude Guide

## What This Repo Is

A professional JavaScript knowledge base built as Obsidian markdown files.
Every note is designed to look great in **Obsidian Graph View** — interconnected, organized, and easy to navigate.

This is not a code project. There is no build step, no package.json, no tests.
All files are `.md` (Markdown) documents with YAML frontmatter.

---

## Folder Structure

```
JavaScript/
├── CLAUDE.md                              ← You are here
├── README.md                              ← Git-facing summary
├── JAVASCRIPT.md                          ← Root MOC (home hub in Obsidian)
├── _templates/
│   └── note-template.md                   ← Template for new notes
│
├── Fundamentals/
│   ├── Fundamentals.md                    ← MOC for this section
│   ├── Events/
│   │   ├── prevent-default.md
│   │   └── stop-propagation.md
│   ├── Async/
│   │   ├── promises.md
│   │   └── promise-object.md
│   ├── Memory/
│   │   └── memory-management.md
│   └── Timing/
│       ├── set-timeout.md
│       └── set-interval.md
│
├── Vanilla-JavaScript/
│   ├── Vanilla-JavaSscript.md             ← MOC for this section
│   ├── dom-selection-shorthand.md
│   ├── pub-sub-event-communication.md
│   ├── global-state-store.md
│   ├── level-up-vanilla-js.md
│   └── senior-level-architecture.md
│
├── Alpine-JS/
│   └── Alpine-JS.md                       ← MOC (ready for future notes)
│
└── Interview-Questions/
    └── Interview-Questions.md             ← MOC (ready for future notes)
```

---

## File Naming Rules

| Type | Convention | Example |
|---|---|---|
| Root home file | `JAVASCRIPT.md` (ALL CAPS topic name) | `JAVASCRIPT.md` |
| Section MOC | `FolderName.md` (matches folder name exactly) | `Fundamentals.md` |
| Content notes | `kebab-case.md` (lowercase, hyphens) | `promise-object.md` |
| Template | `note-template.md` | — |

- **No special characters** in filenames — no `()`, `.`, `#`, `@`
- **No spaces** in filenames — use hyphens
- MOC files are named to match their folder so Obsidian resolves `[[Fundamentals]]` to `Fundamentals/Fundamentals.md`

---

## Every Note Must Have Frontmatter

All `.md` files (except README.md) must start with YAML frontmatter:

```yaml
---
title: "Human Readable Title"
tags: [javascript, <section-tag>, <topic-tag>]
type: concept | pattern | guide | reference | moc
related: [[linked-note]], [[another-note]]
---
```

### Section Tags

| Folder | Required tag |
|---|---|
| Fundamentals/ | `fundamentals` |
| Vanilla-JavaScript/ | `vanilla-js` |
| Alpine-JS/ | `alpine-js` |
| Interview-Questions/ | `interview-questions` |
| Any MOC file | `moc` |

### Type Values

| Value | Use for |
|---|---|
| `concept` | Explaining a JS concept (events, promises, memory) |
| `pattern` | A reusable code pattern (pub/sub, state store) |
| `guide` | Step-by-step walkthrough |
| `reference` | API/syntax reference (setTimeout, Promise methods) |
| `moc` | Map of Content — hub/index files only |

---

## Note Structure (Content Rules)

Every content note follows this layout:

```
# Title

> One-line summary of what this note covers.

---

## Overview
What it is and why it matters.

## Syntax
Code block with the basic signature.

## Examples
Working code examples — clear and commented.

## Key Points
Bullet list of the most important things to remember.

## Related
- [[linked-note]] — one-line description
- [[section-moc]] — section hub
```

MOC files follow this layout:

```
# Section Title

> One-line description of the section.

---

## Sub-section heading
- [[note]] — description

---

← [[JAVASCRIPT]]
```

---

## Wikilink Rules

Obsidian uses `[[filename]]` wikilinks (no path, no extension).

- Every content note must link to its **section MOC** in the Related section
- Every section MOC must link back to `[[JAVASCRIPT]]` at the bottom
- Related notes should cross-link each other where genuinely related
- `JAVASCRIPT.md` links to all section MOCs and has a Quick Index table

### Current Link Map

```
JAVASCRIPT.md
├── [[Fundamentals]]
│   ├── [[prevent-default]] ↔ [[stop-propagation]]
│   ├── [[promises]] ↔ [[promise-object]] ↔ [[set-timeout]]
│   ├── [[memory-management]]
│   └── [[set-interval]] ↔ [[set-timeout]]
├── [[Vanilla-JavaSscript]]
│   ├── [[dom-selection-shorthand]]
│   ├── [[level-up-vanilla-js]]
│   ├── [[pub-sub-event-communication]]
│   ├── [[global-state-store]]
│   └── [[senior-level-architecture]]
├── [[Alpine-JS]]
└── [[Interview-Questions]]
```

---

## Adding a New Note

1. Create the file in the correct folder using `kebab-case.md`
2. Copy frontmatter from `_templates/note-template.md`
3. Fill in `title`, `tags`, `type`, `related`
4. Write content following the note structure above
5. Add a link to it in the section's MOC file
6. Add a link to it in `JAVASCRIPT.md` Quick Index table if it's a key note

---

## Adding a New Section

1. Create a new folder: `FolderName/`
2. Create `FolderName/FolderName.md` as the section MOC
3. Add `type: moc` and the section tag in frontmatter
4. Add `← [[JAVASCRIPT]]` at the bottom of the MOC
5. Link it from `JAVASCRIPT.md` under Topics

---

## What NOT to Do

- Do not use GitHub-style links (`[text](url)`) for internal navigation — use `[[wikilinks]]`
- Do not put content directly in MOC files — MOCs are indexes only
- Do not create files without frontmatter
- Do not use special characters or spaces in filenames
- Do not skip the Related section — links are what make the graph view useful
