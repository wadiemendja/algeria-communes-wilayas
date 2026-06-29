# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project status

This repository is at its inception. It currently contains only `LICENSE`, `.gitattributes`, and `ReadMe.md` — there is **no source code, build system, or tests yet**. Do not assume a toolchain exists; ask or propose one before scaffolding.

## Purpose

The project's goal is a dataset of Algeria's administrative divisions — **wilayas** (provinces) and their **communes** (municipalities) — intended to live in a file named `algeria_cities.json` (referenced in `ReadMe.md` but not yet committed).

## The work to be done (`ReadMe.md`)

`ReadMe.md` is a working note, not documentation. It records the open task: correct wilaya/commune assignment errors in `algeria_cities.json`. The cited example — Tebelbala listed under Béchar — reflects pre-2019 boundaries; Algeria's 2019/2021 administrative reorganization created 10 new wilayas (e.g. Béni Abbès, In Salah, Timimoun), reassigning many communes. **Verify each wilaya/commune mapping against current administrative boundaries**, using the French Wikipedia category cited in the note as a cross-reference:
`https://fr.wikipedia.org/wiki/Catégorie:Commune_par_wilaya_en_Algérie`

## Notes

- Be precise about Arabic/French transliteration of place names; the same locality often has multiple romanized spellings. Decide on and document a canonical spelling convention when the dataset takes shape.
- The repository has no remote configured for issues/CI; coordinate any tooling or schema decisions before committing them.
