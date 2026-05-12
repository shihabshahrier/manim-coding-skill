# Contributing

Improvements to the skill prompt, API reference, or storytelling guide are welcome.

## How

1. Fork the repo
2. Edit the relevant source file:
   - **Skill behavior**: `skills/test-manim/SKILL.md`
   - **ManimGL API reference**: `skills/test-manim/references/manim-gl-api.md`
   - **Storytelling guide**: `skills/test-manim/references/storytelling.md`
3. Open a PR with:
   - **Before**: what the skill does now
   - **After**: what it does with your change
   - One sentence explaining why the change is better

## Rules

- API changes must be verified against manimgl source — no guessing
- Skill behavior changes need a before/after animation example (or clear reasoning)
- Do not add support for ManimCE — this skill is ManimGL-only by design
- Do not edit agent-specific copies (`.cursor/`, `.windsurf/`, `.clinerules/`) directly — these sync from source

## Ideas

See [issues](../../issues) for open tasks.

Small focused change > big rewrite.
