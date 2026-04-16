# Changelog

All notable changes to this skill will be documented in this file.

Format based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [1.2.0] — 2026-04-16

Structural cleanup and interactive-design improvements after a full skill-distillery audit.

### Added
- `references/output-format.md` — Full audit report template extracted from SKILL.md for progressive disclosure.
- `AskUserQuestion` conditional in Step 1 wait gate with plain-text fallback for non-Claude-Code agents.
- Explicit scope note in SKILL.md clarifying this skill targets web/app UI motion (frequency framework still applies to game engines, Lottie, Rive, video, but designer-specific techniques may not translate).

### Changed
- Moved `audit-checklist.md` into `references/` for consistent organization.
- Updated README.md structure diagram to reflect the new layout.
- SKILL.md reduced from 328 lines to ~204 lines via progressive disclosure (output format now loaded only when writing the report).

### Removed
- `version` field from frontmatter (not part of the official 2026 skill spec; this CHANGELOG now tracks versioning).
- `references/philosophy.md` — Content was redundant with per-designer reference files. The context-to-perspective mapping in SKILL.md and the synthesis sections inside each designer file cover the same ground without duplication.

## [1.1.0] — 2026-01-22

Expanded motion design audit capabilities.

### Added
- Motion Gap Analysis in Step 1: actively searches for conditional UI changes that lack animation (conditional renders without AnimatePresence, dynamic styles without transitions).
- Context-to-perspective mapping table linking project types to designer weightings.

## [1.0.0] — 2026-01-13

Initial release.

### Added
- Three-designer audit framework: Emil Kowalski, Jakub Krehel, Jhey Tompkins.
- Context Reconnaissance step with user confirmation wait gate.
- Reference files for each designer plus topical references (accessibility, performance, common mistakes, technical principles).
- Audit checklist with severity levels.
