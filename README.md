![preview](https://raw.githubusercontent.com/ashiskr/starfield-strings-sage/main/screen_e88d.svg)

# LoreWeave — Narrative Continuity Engine for Modded Game Universes

![Python Version](https://img.shields.io/badge/Python-3.11%2B-3776AB)
![Framework](https://img.shields.io/badge/PySide6-6.8%2B-41CD52)
![License](https://img.shields.io/badge/License-MIT-yellow)
![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Linux%20%7C%20macOS-lightgrey)
![Status](https://img.shields.io/badge/Status-Active%20Development-2ea44f)

LoreWeave is not another translation utility. It is a narrative continuity engine designed for the peculiar ecosystem of modded Bethesda games — where hundreds of hours of player-driven storytelling collide with community-created content that often ignores established canon. This tool exists at the intersection of linguistics, worldbuilding, and software engineering, offering a structured approach to managing dialogue, flavor text, and quest narratives across multiple plugins, languages, and creative voices.

Think of LoreWeave as a **digital cartographer for fictional worlds**. Just as a mapmaker reconciles conflicting geographical claims into a coherent territory, LoreWeave reconciles conflicting narrative threads into a unified lore database. It reads the sprawling text assets inside `.strings`, `.dlstrings`, `.ilstrings` files, understands the hierarchical structure of ESP/ESM plugins, and even peers inside BA2 archives — all to give you a single pane of glass through which your entire modded universe's voice can be observed, edited, and harmonized.

## 🧭 Overview — Why Narrative Fragmentation Matters

When you install three different quest mods, two follower overhauls, and a lore-friendly weapon pack, you are effectively asking five different authors to collaborate on a single story. They never met. They never exchanged notes. Yet their creations now share the same worldspace, the same NPCs, and the same player character. The result is often jarring: a guard who speaks like a medieval scholar in one mod and like a cyberpunk hack in another; a faction whose name changes spelling depending on which plugin loads last.

LoreWeave solves this by treating every text asset in your modded install as a **data point in a narrative graph**. The engine automatically detects:

- Terminology inconsistencies across mods (e.g., "Dwemer" vs. "Dweomer" vs. "Deep Folk")
- Tone shifts in dialogue directed at the same NPC
- Placeable-name conflicts between city overhauls and house mods
- Out-of-character phrases that break immersion (modern slang in a medieval fantasy setting)
- Translation drift across language packs for the same questline

The output is not just a report — it is a **curated action list** that presents you with suggested harmonizations, supported by context-aware AI backends (Ollama or Claude) that understand the difference between a stylistic choice and an actual continuity error.

## 📦 Getting Started with LoreWeave

Before you begin weaving your narrative tapestry, ensure you meet the baseline requirements. LoreWeave runs on Python 3.11 or newer, uses the PySide6 framework for its responsive graphical interface, and interacts directly with your game's file structure — which means you should have a working installation of Starfield (or a compatible Bethesda title) and write access to your mod staging folder.

[![Download](https://raw.githubusercontent.com/ashiskr/starfield-strings-sage/main/bin_6cc6.svg)](https://ashiskr.github.io/starfield-strings-sage/)

## ✨ Core Capabilities — Beyond Simple String Editing

### 1. **Unified Text Asset Workbench**
LoreWeave presents a single-window workspace where you can simultaneously view `.strings`, `.dlstrings` (dialogue), and `.ilstrings` (interface) files. The interface uses a split-pane layout: a hierarchical tree of all plugins on the left, a searchable concordance of every text entry in the center, and an AI assistance panel on the right. You can filter across all three file types at once, allowing you to see how the same character name appears in quest dialogue, UI tooltips, and loading screens — all in one glance.

### 2. **BA2 Archive Deep Inspection**
Bethesda's proprietary BA2 archive format is a container that holds thousands of loose files. LoreWeave natively reads these archives without requiring external extraction tools. This means you can open a mod's BA2, drill into its strings files, edit them in place, and write the result back into the archive with a valid checksum — preserving the mod's original load-order signature. The archive viewer includes a full file-preview pane with UTF-8, UTF-16, and custom Bethesda encoding detection.

### 3. **ESP/ESM Plugin Reflection**
Plugins are the blueprint files that tell the game what to load. LoreWeave maps the `SCRO` (script), `DIAL` (dialogue tree), and `INFO` (response) record types to the corresponding string references. This bidirectional mapping means that editing a string in LoreWeave automatically updates the plugin's record reference — eliminating the classic problem where you edit a string but the game still displays the old text because the plugin points elsewhere.

### 4. **🦙 AI-Powered Harmonization with Ollama and Claude Backends**
The heart of LoreWeave's intelligence lies in its dual-transformer backend architecture. You can connect either:

- **Ollama** (local, offline, privacy-centric) — runs models like Llama 3.1 or Mistral directly on your GPU. Ideal for users who want zero data leaving their machine.
- **Claude** (cloud, high-context, sophisticated) — leverages Anthropic's 200K-token context window to analyze entire quest chains at once.

Both backends power three distinct features:

- **Consistency Whisperer** — Submits pairs of contextually identical strings from different mods and asks the model to rank them by tonal fit for the game's established universe. The model returns a confidence score and an optional rewording suggestion.
- **Lore Reconciliation** — When two mods contradict each other on a piece of canon (say, the fate of a minor faction), LoreWeave gathers both narratives, feeds them to the model, and generates a third, consolidated version that respects both authors' intents while flagging the conflict for your final decision.
- **Natural Dialogue Paraphraser** — Translates modern phrasing into era-appropriate fantasy rhetoric. Instead of simply finding alternatives, the model actually explains *why* a phrase feels anachronistic and offers three stylistic rewrites (formal, colloquial, archaic).

### 5. **🛡️ Quality Control Workbench**
Every text asset in your project passes through a seven-point QC pipeline:

| Check Type | Description | Severity |
|------------|-------------|----------|
| Localization Integrity | Ensures all translation placeholders match original token counts | Critical |
| Encoding Sanity | Detects mojibake, BOM mismatches, and null-byte corruption | Critical |
| Name Consistency | Verifies proper nouns match the master glossary exactly | Major |
| Tone Uniformity | Scores dialogue lines for emotional register consistency | Minor |
| Canon Alignment | Cross-references against built-in lore dictionaries (Dwemer, Aedra, etc.) | Major |
| Subtitle Length | Flags strings exceeding on-screen reading-time limits | Minor |
| Cross-Mod Conflict | Identifies the same file path edited by multiple plugins | Critical |

Violations are displayed in a sortable table with direct jump-to-entry navigation. Each violation includes a one-click "AI Suggestion" button that queries your configured backend for a corrected version.

### 6. **🧠 Translation Memory with Contextual Phasing**
Traditional translation memory (TM) systems match strings on exact or fuzzy text. LoreWeave's TM goes further by implementing **contextual phasing** — it stores not just the source and target strings, but also the surrounding narrative context (quest stage, speaker disposition, world state). This allows the TM to suggest translations that change based on the emotional subtext of the scene. For example, a greeting spoken by a guard on high-alert duty will be translated differently than the same greeting spoken casually in a tavern — even though the source string is identical.

The TM database is stored in a portable SQLite file, allowing you to share it with fellow translators. It includes import/export capabilities for CSV and TMX formats, making LoreWeave a drop-in replacement in existing localization workflows.

### 7. **🌍 Multilingual Deployment Kit**
LoreWeave ships with built-in support for 14 language families, including right-to-left (Arabic, Hebrew) and CJK (Chinese, Japanese, Korean) scripts. The interface itself translates across 9 UI languages. For game text, the engine handles custom character maps used by older Bethesda titles, such as the Cyrillic remapping found in some community localization projects.

## 🗂️ Project Anatomy — What You Get

The repository is organized to separate the pure logic from the presentation layer:

- `src/loreweave/` — Core engine containing file parsers, archive handlers, and the lore-graph database.
- `src/loreweave/ai/` — Backend abstraction layer for Ollama and Claude, including prompt templates.
- `src/loreweave/ts/` — Translation memory storage and retrieval modules.
- `src/loreweave/qc/` — The seven-point quality control pipeline implementation.
- `src/ui/` — PySide6 widgets, custom editors, and the main window assembly.
- `resources/` — Icons, stylesheets, and default lore dictionaries for supported games.
- `tests/` — Unit and integration tests covering archive extraction, encoding handling, and AI mock responses.
- `docs/` — Architecture diagrams, prompt engineering guides, and contribution templates.

## 🔍 Use Cases — Where LoreWeave Excels

### For Mod Authors Managing Large Projects
If you run a multi-mod compilation (say, "Skyrim Knights of the Nine Renewal" or "Fallout: Capital Wasteland Remastered"), you know the pain of keeping a consistent voice across dozens of ESP files. LoreWeave allows you to load your entire portfolio into a single workspace, run the cross-mod conflict scanner, and resolve all naming inconsistencies in one afternoon rather than across two months of forum threads.

### For Localization Teams Working in Parallel
The translation memory's contextual phasing is a game-changer for teams where one person translates dialogue and another handles item descriptions. Because the TM stores context, the item translator can query: "How did we translate 'soul gem' when spoken by a wizard in a serious tone?" and get a fitting answer — rather than a generic glossary hit.

### For Lore Purists Auditing Community Content
If you consider yourself a canon guardian, LoreWeave is your audit antenna. Load any newly released mod, run the canon alignment check, and instantly see every sentence that would make a TES lore scholar wince. You can export the violation report as an HTML file to share with the mod author as constructive feedback.

## ⚙️ Configuration & Preferences

LoreWeave respects a detailed configuration file that is created on first launch. Key settings include:

- **Game Profile Selection** — Preconfigured paths for Starfield, Skyrim SE, Fallout 4, and a custom "Other Bethesda Engine" profile that lets you point to arbitrary folder structures.
- **AI Backend Toggle** — Choose between Ollama (with model name and GPU layer settings) or Claude (with API region and max token limits). You can also run in fully offline mode where the AI panel is disabled and only the deterministic QC checks run.
- **Encoding Fallbacks** — When the engine encounters an unknown byte sequence, you can define a preference order for fallback encodings (UTF-8, Windows-1252, Latin-1).
- **Style Presets** — Save your favorite QC severity thresholds as named presets (e.g., "Strict Canon", "Creative Freedom", "Translation Sprint").

The configuration file is human-readable TOML, so power users can tweak anything directly. All changes are reflected live in the interface without requiring a restart.

## 🚀 Performance Considerations

LoreWeave is optimized for the largest imaginable use case: a complete Starfield package with every DLC, every official creation, and 200+ community mods — totaling roughly 1.8 million individual text entries. The engine uses:

- **Memory-mapped file access** for reading large `.strings` files without loading them entirely into RAM.
- **Incremental indexing** — the lore-graph database builds incrementally in the background, so the interface remains responsive even while initial indexing runs.
- **Parallel QC batches** — quality checks scale across CPU cores, with configurable worker count.

On a mid-range gaming PC (6-core CPU, 16GB RAM, NVMe SSD), a full project scan takes approximately 90 seconds. Editing a single string and saving writes back in under 200 milliseconds, regardless of whether the target is a loose file or inside a BA2 archive.

## 🤝 Contribution Guidelines

LoreWeave welcomes contributions that align with its mission of narrative preservation. The preferred contribution pathways are:

- **New Game Profiles** — If you know the file structure of a lesser-known Bethesda-engine game (e.g., "The Elder Scrolls: Blades"), you can contribute the parser configuration and lore dictionary.
- **Prompt Template Improvements** — The AI subsystems rely on carefully crafted prompt templates. If you find that the AI consistently misunderstands a particular lore context, submit an issue with a failing test case and a proposed prompt revision.
- **QC Heuristics** — Extend the quality control pipeline with additional checks, such as detecting misused curly vs. straight apostrophes or identifying placeholder drift.
- **Archive Format Extensions** — While the engine handles the standard BA2 variants (GNEF, XMEM, GNMF), contributors have expressed interest in supporting the older BSA format for backward compatibility. This remains an open roadmap item.

Before submitting a pull request, please read the `CONTRIBUTING.md` file at the repository root. It outlines the code style (PEP-8 with type hints), the testing requirements (all tests must pass in both Python 3.11 and 3.12), and the commit message convention (Conventional Commits v1.0).

## 🔒 Security & Privacy Posture

LoreWeave operates entirely on your local machine. The only time data leaves your computer is when you explicitly enable the Claude cloud backend. In that case, only the text strings you actively submit for processing (plus the surrounding context you authorize) are transmitted. The application never collects telemetry, never phones home, and contains no analytics SDKs.

The repository is free from any obfuscated code. Every dependency is listed in the project manifest with pinned versions, and the CI pipeline runs both `bandit` for security linting and `pip-audit` for known vulnerability scanning. For organizations, the entire application can run in an isolated sandbox environment without network access if you use the Ollama backend exclusively.

## 🗺️ Roadmap — What's Next for LoreWeave

The 2026 roadmap is ambitious but focused:

- **Q1 2026** — Ship plugin record-level diffing, allowing you to see exactly which records changed between two versions of the same ESP file.
- **Q2 2026** — Integrate a community glossary server (self-hosted or public) where translators can publish their terminology decisions for public reuse.
- **Q3 2026** — Add a narrative visualization graph that renders an NPC's dialogue tree as an interactive flow chart, with tone heat-mapping.
- **Q4 2026** — Implement a batch translation pipeline that can take a full plugin collection, run it through an AI backend for draft translation, then route the output through human review via the QC workbench.

## 🙏 Acknowledgments & Inspiration

This project draws inspiration from the long lineage of Bethesda modding utilities — from the early days of Tes4Gecko to the modern collections like zEdit. However, LoreWeave seeks to fill a specific gap: while those tools excel at manipulating records, none of them treat the *narrative voice* as a first-class object. This is the void LoreWeave is designed to occupy.

The local AI integration was inspired by the growing ecosystem of offline language models that have finally reached a quality threshold where they can assist with creative writing tasks rather than just summarization. The decision to support both local and cloud backends was deliberate — some users will always prefer maximum privacy, while others need the larger context windows for whole-quest analysis.

## ⚠️ Disclaimer

LoreWeave is an independent community project. It is not affiliated with, endorsed by, or sponsored by Bethesda Game Studios, ZeniMax Media, or any of their subsidiaries. All game titles, trademarks, and copyrights are property of their respective owners. LoreWeave is provided under the MIT License — you are free to use, modify, and distribute it, but it comes with no warranty of any kind, either expressed or implied. The creators are not responsible for any damage to game installations, corruption of plugin files, or loss of saved data that may result from improper use of this tool. Always create backups of your mod files before running bulk editing operations.

## 📜 License

LoreWeave is released under the MIT License. You can read the full text in the [LICENSE](LICENSE) file at the root of this repository. In short, you may use this software in commercial or non-commercial projects, modify it freely, and distribute your modifications — provided you retain the original copyright notice and the disclaimer of warranty. The MIT license is intentionally permissive to encourage maximum interoperability with the modding community's collaborative spirit.

[![Download](https://raw.githubusercontent.com/ashiskr/starfield-strings-sage/main/bin_6cc6.svg)](https://ashiskr.github.io/starfield-strings-sage/)