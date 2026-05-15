# Workflow: Audit Mode

Review existing motion design and produce a per-designer report. Reconnaissance first, then a full audit, then a structured report. Never apply rules blindly.

## Required Reading

Read as you reach each step (not all upfront):
1. `references/audit-checklist.md` — your systematic guide (STEP 2)
2. The weighted designer file(s) — `emil-kowalski.md`, `jakub-krehel.md`, `jhey-tompkins.md` (STEP 2)
3. `references/accessibility.md` — mandatory every audit (STEP 2)
4. `references/common-mistakes.md` — anti-patterns to check against (STEP 2)
5. `references/output-format.md` — the report template (STEP 3)

---

## STEP 1: Context Reconnaissance (DO THIS FIRST)

Before auditing any code, understand the project context.

### Gather Context

Check these sources:
1. **CLAUDE.md** — Any explicit context about the project's purpose or design intent
2. **package.json** — What type of app? (Next.js marketing site vs Electron productivity app vs mobile PWA)
3. **Existing animations** — Grep for `motion`, `animate`, `transition`, `@keyframes`. What durations are used? What patterns exist?
4. **Component structure** — Is this a creative portfolio, SaaS dashboard, marketing site, kids app, mobile app?

### Motion Gap Analysis (CRITICAL - Don't Skip)

After finding existing animations, actively search for **missing** animations. These are UI changes that happen without any transition:

**Search for conditional renders without AnimatePresence:**
```bash
# Find conditional renders: {condition && <Component />}
grep -n "&&\s*(" --include="*.tsx" --include="*.jsx" -r .

# Find ternary UI swaps: {condition ? <A /> : <B />}
grep -n "?\s*<" --include="*.tsx" --include="*.jsx" -r .
```

**For each conditional render found, check:**
- Is it wrapped in `<AnimatePresence>`?
- Does the component inside have enter/exit animations?
- If NO to both → this is a **motion gap** that needs fixing

**Common motion gap patterns:**
- `{isOpen && <Modal />}` — Modal appears/disappears instantly
- `{mode === "a" && <ControlsA />}` — Controls swap without transition
- `{isLoading ? <Spinner /> : <Content />}` — Loading state snaps
- `style={{ height: isExpanded ? 200 : 0 }}` — Height changes without CSS transition
- Inline styles with dynamic values but no `transition` property

**Where to look for motion gaps:**
- Inspector/settings panels with mode switches
- Conditional form fields
- Tab content areas
- Expandable/collapsible sections
- Toast/notification systems
- Loading states
- Error states

### State Your Inference

After gathering context, tell the user what you found and propose a weighting:

```
## Reconnaissance Complete

**Project type**: [What you inferred — e.g., "Kids educational app, mobile-first PWA"]
**Existing animation style**: [What you observed — e.g., "Spring animations (500-600ms), framer-motion, active:scale patterns"]
**Likely intent**: [Your inference — e.g., "Delight and engagement for young children"]

**Motion gaps found**: [Number] conditional renders without AnimatePresence
- [List the files/areas with gaps, e.g., "Settings panel mode switches", "Loading states"]

**Proposed perspective weighting**:
- **Primary**: [Designer] — [Why]
- **Secondary**: [Designer] — [Why]
- **Selective**: [Designer] — [When applicable]

Does this approach sound right? Should I adjust the weighting before proceeding with the full audit?
```

Use the Context-to-Perspective Mapping table in SKILL.md to propose the weighting.

### Wait for User Confirmation

**STOP and wait for the user to confirm or adjust.** Do not proceed to the full audit until they respond.

If `AskUserQuestion` is available, present the decision as tappable options:
- **Confirm weighting** — Proceed with the proposed primary/secondary/selective designers
- **Adjust primary** — Swap which designer is primary (e.g., prioritize delight over restraint)
- **Adjust secondary** — Change the secondary lens while keeping primary
- **Rebuild weighting** — The project type inference was wrong; start over

Otherwise ask in plain text: "Does this weighting sound right, or should I adjust?"

If they adjust (e.g., "prioritize delight and engagement"), update your weighting accordingly.

---

## STEP 2: Full Audit (After User Confirms)

Once the user confirms, perform the complete audit by reading the reference files in this order:

### 2a. Read the Audit Checklist First
**Read `references/audit-checklist.md`** — Use this as your systematic guide. It provides the structured checklist of what to evaluate.

### 2b. Read Designer Files for Your Weighted Perspectives
Based on your context weighting, read the relevant designer files:
- **Read `references/emil-kowalski.md`** if Emil is primary/secondary — Restraint philosophy, frequency rules, decision frameworks
- **Read `references/jakub-krehel.md`** if Jakub is primary/secondary — Production polish philosophy, what to check
- **Read `references/jhey-tompkins.md`** if Jhey is primary/secondary — Playful experimentation philosophy, opportunities to surface

### 2c. Read Topical References as Needed
- **Read `references/accessibility.md`** — MANDATORY. Always check for prefers-reduced-motion. No exceptions.
- **Read `references/common-mistakes.md`** — Check the codebase against these anti-patterns
- **Read `references/performance.md`** — If you see complex animations, check for GPU optimization issues
- **Read `references/motion-cookbook.md`** — Reference when making specific implementation recommendations (the recommended fix code)

---

## STEP 3: Output Format

**Read `references/output-format.md`** for the full report template.

The template covers:
- Quick summary box (severity counts + primary perspective)
- Overall assessment paragraph
- Three per-designer sections (Emil / Jakub / Jhey) with decorated headers
- Combined recommendations tables (Critical / Important / Opportunities)
- Designer reference summary (who was referenced most + lean-differently guidance)

Do not summarize — users want full per-designer perspectives.

---

## Success Criteria

- [ ] Context gathered (CLAUDE.md, package.json, existing animations, structure)
- [ ] Motion gap analysis run — conditional renders checked for missing animation
- [ ] Weighting proposed and confirmed by the user
- [ ] Audit checklist worked through systematically
- [ ] Accessibility checked — prefers-reduced-motion verified (mandatory)
- [ ] Report follows output-format.md with full per-designer sections
