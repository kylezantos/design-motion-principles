# Changelog

All notable changes to this skill will be documented in this file.

Format based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [2.1.1] — 2026-05-30

A complete worked-example report for Audit mode. No behavior changes — the audit workflow is unchanged; this release upgrades the templates the agent reads when composing the HTML report, so real audits inherit a finished, consistent design.

### Added
- **`references/report-template.html`** — a full, self-contained worked-example audit report (the fictional "Tally" habit tracker, React + Framer Motion), now the canonical visual reference for the HTML output. It establishes the report's design system end to end: a pure-CSS global dark/light theme toggle, the cool slate-graphite OKLCH neutral palette (severity is the only color signal), a "Where the timings land" duration-budget diagram, five live looping demo cards each with a 3-state Auto/Light/Dark stage toggle, and severity-grouped recommendations. The agent reads this file to match layout, tokens, and structure when building a real audit.

### Changed
- `references/demo-shell.html` rewritten as a minimal single-card template — one `.demo` card with every per-finding contract visible (stage tokens, the Auto/Light/Dark stage toggle, the `prefers-reduced-motion` guard, and the `0% / ~60% / 100%` loop-pacing cadence) and no report scaffolding. Points to `report-template.html` for the full example.
- `references/output-format.md` rewritten to name `report-template.html` as the source of truth and to document the system around it: the neutral-default, severity-driven palette; the per-demo stage tokens (`--st-bg` / `--st-fg` / `--st-line` / `--st-dim`); the timing-budget diagram; the report's no-entrance-animation motion posture; and the absolute bans (no accent border-stripes, no gradient text, no pulsing demos).

### Fixed
- Quoted the `SKILL.md` description so the `npx skills add` installer parses it — an unquoted colon in the description could break YAML frontmatter parsing on install.

## [2.1.0] — 2026-05-20

Audit mode gets a visual upgrade and a sharper quality gate. Create mode is unchanged.

### Added
- **Branded HTML report (Audit)** — the default audit output is now a self-contained `.html` file with auto-looping CSS demos beside each Critical and Important finding, so reviewers can *see* the recommended motion instead of mentally simulating it from code. Writes to `motion-audits/{project-name}-{ISO-date}.html` and opens in the default browser. Cross-platform browser-open (macOS/Linux/Windows/WSL) with a print-the-path fallback.
- `references/demo-shell.html` — the visual container template for per-finding demo cards. Defines CSS tokens, the `.demo-card` component, a loop indicator, the `prefers-reduced-motion` guard, and a suffixed-naming contract so multiple findings don't collide on keyframe/class names.
- **Anti-AI-slop checklist (Audit)** — seven named AI-slop motion categories (pulsing indicators, blur-everywhere entrances, hover-scale-on-everything, stagger-spam-on-every-list, bouncy-springs-on-utility-actions, uniform-fade-in-on-every-element, motion-on-mount-for-static-content), each with a frequency heuristic so single intentional uses don't trip the gate.
- Agent Gotchas self-check in `workflows/audit.md` for HTML-report generation failure modes.

### Changed
- Renamed `references/common-mistakes.md` → `references/anti-checklist.md` — now the audit's explicit quality gate. All prior anti-pattern content is preserved verbatim; the AI-slop categories are layered on top.
- `references/output-format.md` rewritten as a two-mode template: HTML mode (default) and terminal mode (the prior decorated-markdown report, preserved as the `--terminal` fallback).
- `workflows/audit.md` STEP 3 now writes HTML by default; terminal report is opt-in via `--terminal` / `--inline` / natural language.
- Audit description updated to mention AI-slop detection and the HTML report.

## [2.0.0] — 2026-05-15

Major release: the skill now **builds** interactive components with motion, not just audits existing ones. Audit behavior is unchanged — existing workflows are preserved verbatim — but the skill's scope and identity expand enough to warrant a major version.

### Added
- **Create mode** — Build interactive components with purposeful motion (React, Framer Motion, CSS, HTML). Light-discovery flow: infer context, confirm lens weighting, generate, self-check.
- `workflows/create.md` and `workflows/audit.md` — SKILL.md is now a router; each mode is a self-contained workflow.
- `STEP 0` mode detection in SKILL.md — routes "build/create/animate" requests to Create, "audit/review" to Audit, asks when ambiguous.
- `references/creation-gotchas.md` — Claude's failure modes when generating motion (decorative-by-default, `scale(0)` starts, bare `ease`, missing `prefers-reduced-motion`, looping attention motion).
- Attribution framing in SKILL.md and README — the three-lens framework is a distillation of the designers' publicly published work, named in tribute, not authored or endorsed by them.

### Changed
- Renamed `references/technical-principles.md` → `references/motion-cookbook.md` — now the single source of truth for all motion recipes. Fixed a duplicate section-number bug.
- Rewrote the three designer files (`emil-kowalski.md`, `jakub-krehel.md`, `jhey-tompkins.md`) to hold philosophy and decision frameworks only; recipe code is de-duplicated and cross-referenced to the cookbook (~480 lines of duplication removed).
- Audit report phrasing softened from "[Designer] would say" to "Through [Designer]'s lens" — it's a documented lens, not a quote from the person.
- SKILL.md description updated with Create-mode trigger keywords so the skill auto-invokes on build tasks.
- README rewritten for the dual-mode structure.

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
