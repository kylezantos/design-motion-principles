# Design Motion Principles

Expert motion and interaction design auditor based on **Emil Kowalski**, **Jakub Krehel**, and **Jhey Tompkins**' techniques. Get context-aware, per-designer feedback on your animations.

## Installation

```bash
npx add-skill kylezantos/design-motion-principles
```

Works with Claude Code, Cursor, Windsurf, and other AI coding assistants.

## What It Does

This skill audits your codebase's motion design through three distinct design philosophies:

| Designer | Philosophy | Best For |
|----------|-----------|----------|
| **Emil Kowalski** | Restraint & Speed | Productivity tools, high-frequency interactions |
| **Jakub Krehel** | Production Polish | Shipped consumer apps, professional refinement |
| **Jhey Tompkins** | Creative Experimentation | Kids apps, portfolios, playful contexts |

### Key Features

1. **Context Reconnaissance** — Analyzes your project type to determine which designer's perspective to prioritize

2. **Motion Gap Analysis** — Searches for conditional UI that SHOULD be animated but isn't (conditional renders without AnimatePresence, dynamic styles without transitions)

3. **Per-Designer Audit** — Evaluates your code through three lenses with actionable recommendations categorized by severity

## Usage

Once installed, just ask:

```
Audit the motion design in this codebase
```

The skill will:
1. Do reconnaissance on your project
2. Search for motion gaps (missing animations)
3. Propose a weighting based on context
4. Wait for your confirmation
5. Provide the full per-designer audit

## Example Output

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
      ├── SKILL.md                    # Main skill with workflow
      └── references/
          ├── audit-checklist.md      # Structured audit criteria
          ├── emil-kowalski.md        # Emil's philosophy & techniques
          ├── jakub-krehel.md         # Jakub's philosophy & techniques
          ├── jhey-tompkins.md        # Jhey's philosophy & techniques
          ├── technical-principles.md # Implementation patterns
          ├── accessibility.md        # Motion accessibility guidelines
          ├── performance.md          # Performance best practices
          ├── common-mistakes.md      # Anti-patterns to flag
          └── output-format.md        # Report template for audits
```

## Manual Installation

If you prefer not to use `npx add-skill`:

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

This skill synthesizes motion design principles from:

- **Emil Kowalski** — [emilkowal.ski](https://emilkowal.ski), [animations.dev](https://animations.dev), [Sonner](https://sonner.emilkowal.ski), [Vaul](https://vaul.emilkowal.ski)
- **Jakub Krehel** — [krehel.com](https://krehel.com)
- **Jhey Tompkins** — [jhey.dev](https://jhey.dev), [@jh3yy](https://twitter.com/jh3yy)

## License

MIT
