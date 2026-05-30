# Design Motion Principles

A motion and interaction design skill with **two modes** — **build** interactive components with purposeful motion, or **audit** existing animations. Both modes give context-aware, per-designer guidance drawn from three distinct motion-design lenses.

Distilled from the publicly published work of **Emil Kowalski**, **Jakub Krehel**, and **Jhey Tompkins** (see [Credits](#credits)).

## Installation

```bash
npx skills add kylezantos/design-motion-principles
```

Works with Claude Code, Cursor, Windsurf, and other AI coding assistants.

## What It Does

The skill applies three distinct motion-design philosophies, weighted by your project's context:

| Lens | Philosophy | Key question | Best for |
|------|-----------|--------------|----------|
| **Emil Kowalski** | Restraint & speed | "Should this animate at all?" | Productivity tools, high-frequency interactions |
| **Jakub Krehel** | Production polish | "Is this subtle enough?" | Shipped consumer apps, professional refinement |
| **Jhey Tompkins** | Creative experimentation | "What could this become?" | Kids apps, portfolios, playful contexts |

The point isn't a single set of rules — it's the productive tension between three lenses that genuinely disagree. Emil would cut an animation Jhey would add. The skill weights them to your context instead of applying one philosophy everywhere.

### Two Modes

**Create** — Build interactive components with motion baked in. The skill runs a light discovery (project context + which lenses to weight), then generates components — React, Framer Motion, CSS, or HTML — applying the right recipes, accessibility, and performance defaults.

**Audit** — Review existing motion design. The skill does reconnaissance on your project, runs a motion-gap analysis (finds UI that *should* animate but doesn't), checks the code against an anti-AI-slop checklist (pulsing indicators, hover-scale-on-everything, stagger-spam, and other 2026 AI-generated motion tells), proposes a per-lens weighting, and delivers a **branded HTML report** with auto-looping CSS demos beside each Critical and Important finding. Pass `--terminal` for the inline markdown report instead.

The skill detects which mode you want from your request. If it's ambiguous, it asks.

### Key Features

1. **Context-aware weighting** — Maps your project type (productivity tool, kids app, marketing site, dashboard…) to a primary/secondary/selective lens weighting before doing anything.

2. **Motion gap analysis** (Audit) — Searches for conditional UI that should be animated but isn't: conditional renders without `AnimatePresence`, dynamic styles without transitions, instant state swaps.

3. **Anti-AI-slop checklist** (Audit) — A quality gate that flags the recognizable motion fingerprints of AI-generated UIs: pulsing indicators, blur-everywhere entrances, hover-scale-on-everything, stagger-spam, bouncy springs on utility actions, uniform fade-ins, motion-on-mount for static content. Each category has a frequency heuristic so single intentional uses don't trip it.

4. **Branded HTML report** (Audit) — The default audit output is a self-contained HTML file with auto-looping CSS demos beside each Critical and Important finding, so you can *see* the recommended motion instead of reading code. Writes to `motion-audits/`, opens in your browser. `--terminal` falls back to the inline markdown report for headless/CI use.

5. **Motion cookbook** (Create) — A single, consolidated recipe library: enter/exit animations, easing, springs, clip-path, `@property`, shared-layout/FLIP, scroll-driven animation.

6. **Creation gotchas** (Create) — Built-in self-check against the common failure modes of AI-generated motion: decorative-by-default animation, `scale(0)` starts, bare `ease`, missing `prefers-reduced-motion`.

## Usage

Once installed, just ask in natural language.

**To build:**
```
Add a polished enter/exit animation to this modal
Build an animated toast component for this dashboard
```

**To audit:**
```
Audit the motion design in this codebase
Review the animations in this component
```

### Example: Audit output

```
## Reconnaissance Complete

**Project type**: Kids educational app, mobile-first PWA
**Existing animation style**: Spring animations (500-600ms), framer-motion
**Motion gaps found**: 4 conditional renders without AnimatePresence

**Proposed perspective weighting**:
- **Primary**: Jakub Krehel — Production polish for a shipped consumer app
- **Secondary**: Jhey Tompkins — Playful experimentation for kids
- **Selective**: Emil Kowalski — Only for high-frequency game interactions

Does this approach sound right?
```

## What's Included

```
skills/
  └── design-motion-principles/
      ├── SKILL.md                     # Router: mode detection + shared principles
      ├── workflows/
      │   ├── create.md                # Build interactive components
      │   └── audit.md                 # Review existing motion design
      └── references/
          ├── motion-cookbook.md       # All motion recipes (single source of truth)
          ├── creation-gotchas.md      # Failure modes when generating motion
          ├── audit-checklist.md       # Structured audit criteria
          ├── anti-checklist.md        # Quality gate: AI-slop categories + anti-patterns
          ├── demo-shell.html          # Minimal single-card template for HTML-report demos
          ├── report-template.html     # Full worked-example audit report (HTML output reference)
          ├── emil-kowalski.md         # Emil's philosophy & decision frameworks
          ├── jakub-krehel.md          # Jakub's philosophy & decision frameworks
          ├── jhey-tompkins.md         # Jhey's philosophy & decision frameworks
          ├── accessibility.md         # Motion accessibility guidelines
          ├── performance.md           # Performance best practices
          └── output-format.md         # Report template (HTML + terminal modes)
```

## Manual Installation

If you prefer not to use `npx skills add`:

**Global (all projects):**
```bash
git clone https://github.com/kylezantos/design-motion-principles.git
cp -r design-motion-principles/skills/design-motion-principles ~/.claude/skills/
```

**For Cursor:**
```bash
cp -r design-motion-principles/skills/design-motion-principles ~/.cursor/skills/
```

## Credits

This skill is an interpretation and distillation of motion-design principles from the **publicly published** work — courses, articles, talks, and open-source projects — of three designers. The three-lens weighting framework and the "through X's lens" framing are this skill's own synthesis, named in tribute. The skill is **not authored or endorsed** by the designers below; for their actual work, go to the source:

- **Emil Kowalski** — [emilkowal.ski](https://emilkowal.ski), [animations.dev](https://animations.dev), [Sonner](https://sonner.emilkowal.ski), [Vaul](https://vaul.emilkowal.ski)
- **Jakub Krehel** — [krehel.com](https://krehel.com)
- **Jhey Tompkins** — [jhey.dev](https://jhey.dev), [@jh3yy](https://twitter.com/jh3yy)

## License

MIT
