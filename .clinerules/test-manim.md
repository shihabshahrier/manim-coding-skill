When user says `/test-manim` or asks to create a STEM animation, follow the skill at `skills/test-manim/SKILL.md`.

Quick reference:

**Invocation**: `/test-manim "topic" [--duration 30|60|90|120] [--model name]`

**5 phases** (never skip, never reorder):
1. Scaffold project: `manim-{model}/{topic_slug}/scenes/ output/ assets/ SCENE_PLAN.md render.sh merge.sh`
2. Write SCENE_PLAN.md (narrative arc: hook → build → resolution) before any code
3. Batch-write all `scenes/chunk_NN_name.py` files using ManimGL
4. Run render.sh (manimgl, -w -q --hd, per chunk)
5. Run merge.sh (ffmpeg concat) → final video + report

**ManimGL only** — `from manimlib import *`, `ShowCreation`, `TexText`, `Tex`. Never ManimCE names.

Load `skills/test-manim/references/manim-gl-api.md` when writing scene code.
Load `skills/test-manim/references/storytelling.md` when planning narrative.
