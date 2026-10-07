# Sanctuary City — Campaign Wiki

A campaign wiki for our Draw Steel game, built from session notes and the
heroes' Forge Steel sheets.

## How it works

```
session notes / recordings  ->  content/*.md  ->  docs/index.html
```

`content/` is an [Obsidian](https://obsidian.md) vault. Every entity (hero,
person, place, faction, item) is one markdown file with `[[wikilinks]]` to the
others. Open the folder in Obsidian to get local editing, backlinks and the
graph view.

`build.py` turns that vault into a single self-contained HTML page in
`docs/`. It uses the standard library only, with no dependencies:

```bash
python build.py
```

It fails loudly on any `[[wikilink]]` that points at a page which doesn't
exist, and renders those links in red, so a typo can't silently become a
missing page.

**The generated site is committed to `docs/`.** If you edit anything in
`content/`, run `build.py` before committing or the published page won't
change.

## Publishing

> Settings → Pages → Source: **Deploy from a branch** → Branch **main**,
> folder **/docs** → Save

That publishes to `https://ausrabbit.github.io/draw_steel_wiki/`.

## Frontmatter

```yaml
---
title: "Annabel Swordbuck"
group: "People"            # sidebar section
type: character            # hero | character | place | thing | faction | enemy | doc
conf: hi                   # hi | mid | lo — how confident we are
short: "Annabel"           # optional: the form people actually say
aliases: ["Annabelle"]     # other spellings that should resolve here
dek: "One line under the title."
---
```

Sidebar groups, in order: Campaign, Sessions, Heroes, People, Places,
Factions, Things, Bestiary, Reference.

## The two name files

`build.py` regenerates both on every run:

- **`names.txt`** lists canonical spellings only, for prompting a transcriber.
- **`corrections.json`** maps each alias to its canonical spoken form.

## What's deliberately not here

GM notes: secrets, fronts, unplayed scenes, NPCs the party hasn't met, and
planned loot. This repository is public, so that material lives locally in
`gm/`, which `.gitignore` excludes.
