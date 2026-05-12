# CLAUDE.md — manim-coding-skill

## What this repo is

This is the `test-manim` Claude Code / opencode skill. One skill, one purpose: make any AI model produce great STEM teaching animations in ManimGL.

---

## File structure — what owns what

### Source of truth — edit only these

| File | Controls |
|------|----------|
| `skills/test-manim/SKILL.md` | All skill behavior: phases, rules, templates, API notes |
| `skills/test-manim/references/manim-gl-api.md` | ManimGL object reference, error table |
| `skills/test-manim/references/storytelling.md` | Narrative structure, pacing, anti-patterns |

**Never edit agent-specific copies directly** — edit source files, then sync manually or via CI.

### Auto-generated / agent-specific (sync from source)

| File | Content |
|------|---------|
| `.cursor/rules/test-manim.mdc` | Condensed skill for Cursor |
| `.windsurf/rules/test-manim.md` | Condensed skill for Windsurf |
| `.clinerules/test-manim.md` | Condensed skill for Cline |
| `.github/copilot-instructions.md` | Condensed skill for Copilot |
| `AGENTS.md` | `@./skills/test-manim/SKILL.md` include for OpenAI agents |
| `GEMINI.md` | `@./skills/test-manim/SKILL.md` include for Gemini CLI |

---

## Key constraints

- **ManimGL only** — not ManimCE. All API references must use `manimlib` imports.
  `ShowCreation` not `Create`. `TexText` not `Text`. `Tex` not `MathTex`.
- **15s chunks** — skill enforces this. Don't change to arbitrary lengths.
- **No hooks** — skill is user-invocable only. No SessionStart/UserPromptSubmit hooks.
- **Open-weight compatible** — every rule must work with non-Claude models.
  No implicit Claude behaviors assumed.

---

## ManimGL version

Developed against manimgl 1.7.2. If updating references, verify API against installed version:
```bash
python3 -c "import importlib.metadata; print(importlib.metadata.version('manimgl'))"
```

---

## Making changes

### Skill behavior change
Edit `skills/test-manim/SKILL.md` only. Open a PR with before/after example.

### API reference update
Edit `skills/test-manim/references/manim-gl-api.md`. Verify the API against manimgl source before adding.

### Storytelling guide update
Edit `skills/test-manim/references/storytelling.md`. Changes should be grounded in animation pedagogy, not preference.

### Adding a new reference file
1. Create `skills/test-manim/references/{name}.md`
2. Add a load instruction in SKILL.md under the appropriate phase
3. Follow lazy loading — only load when the phase needs it

---

## What "good" looks like

A good animation produced by this skill:
- Has a visual hook that asks a question before any label appears
- Maintains a consistent color contract across all chunks
- Each chunk teaches exactly one concept
- Last chunk returns to opening visual, now annotated with understanding
- Renders clean at 1080p, merges without codec mismatch

A bad animation:
- Opens with a definition or equation
- Uses colors inconsistently
- Crams 3 concepts into one chunk
- Ends abruptly without synthesis
