# test-manim

A Claude Code / opencode skill that turns any AI model into a STEM animation teacher.

Give it a topic. Get back a ManimGL video.

---

## What it does

`/test-manim "Newton's Laws of Motion"` →

```
manim-claude/
  newtons_laws_of_motion/
    scenes/         ← chunk_01_hook.py, chunk_02_build.py, ...
    output/final/   ← newtons_laws_of_motion_final.mp4
    SCENE_PLAN.md   ← narrative plan written before any code
    render.sh
    merge.sh
```

The model writes a narrative plan first, then generates 15-second animation chunks, renders each with ManimGL, and merges into one final video. Every chunk targets one concept. Story arc: hook → build → synthesis.

---

## Install

### Claude Code (plugin)

```bash
claude plugin install shihabshahrier/manim-coding-skill
```

Then in any session:

```
/test-manim "Fourier Series"
```

### opencode

```bash
npx skills add shihabshahrier/manim-coding-skill
```

Then in any opencode session with any model:

```
/test-manim "Fourier Series"
```

### Manual (any agent)

Copy `skills/test-manim/SKILL.md` into your agent's rules / context. Invoke by saying:
> "Follow the test-manim skill and create an animation about Fourier Series"

---

## Usage

```
/test-manim "topic"
/test-manim "topic" --duration 60
/test-manim "topic" --duration 90 --model minimax
```

| Arg | Default | Options |
|-----|---------|---------|
| topic | required | any STEM subject |
| --duration | 30s | 30, 60, 90, 120 |
| --model | session model | used for folder name |

Output goes to `./manim-{model}/{topic_slug}/` in the current directory.

---

## Requirements

- [ManimGL](https://github.com/3b1b/manim) (`pip install manimgl`) — v1.7+
- `ffmpeg` (for merging chunks)
- LaTeX installation (for rendering equations)

---

## What you get

| Feature | Detail |
|---------|--------|
| Narrative-first | SCENE_PLAN.md written before any code — story arc enforced |
| 15s chunks | Each chunk = one concept, clean cuts, merged at end |
| ManimGL correct | Uses `ShowCreation`, `TexText`, `Tex` — not ManimCE names |
| Token efficient | Batch writes all chunks before rendering, no mid-task questions |
| Open-weight ready | Explicit rules for non-Claude models via opencode |
| Audio-ready | Silence buffers and long holds built in for future voice-over |

---

## Animation ideas

- Newton's Laws / classical mechanics
- Fourier series / signal decomposition
- Neural network forward pass
- Gradient descent visualization
- Eigenvalues and eigenvectors
- Projectile motion / orbital mechanics
- Calculus: limits, derivatives, integrals
- Sorting algorithms

---

## How it works

The skill enforces a 5-phase pipeline:

```
Phase 0: Parse args, scaffold project folders
Phase 1: Write SCENE_PLAN.md (narrative arc, color contract, per-chunk plan)
Phase 2: Batch-write all scene .py files (ManimGL)
Phase 3: Render all chunks via render.sh
Phase 4: Merge with merge.sh (ffmpeg)
Phase 5: Structured report with rating
```

Story structure every animation must follow:
- **Hook** (first chunk): striking visual that poses a question
- **Build** (middle): one concept per chunk, each making the prior more meaningful
- **Resolution** (last): synthesis — return to opening image, transformed by understanding

---

## Supported agents

| Agent | How to use |
|-------|-----------|
| Claude Code | `/test-manim "topic"` after plugin install |
| opencode | `/test-manim "topic"` after `npx skills add` |
| Cursor | Add `skills/test-manim/SKILL.md` as a rule, prompt with `/test-manim` |
| Windsurf | Same as Cursor |
| Cline | Same — `.clinerules/test-manim.md` included |
| Copilot | `.github/copilot-instructions.md` included |
| Any agent | Paste SKILL.md into system context |

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).
