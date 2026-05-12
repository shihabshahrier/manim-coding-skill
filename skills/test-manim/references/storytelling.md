# STEM Animation Storytelling Guide

Core principle: the viewer should feel understanding arrive, not just receive information.

---

## The 3-Act Structure (mandatory)

### Act 1 — The Question (first chunk)
Don't start with a definition. Start with a phenomenon.

- Show the effect before naming the cause
- Pose a visual question the viewer wants answered
- Good: ball in motion, pendulum swinging, wave propagating
- Bad: "Today we will learn about Newton's First Law"

Opening frames: concrete, specific, surprising.

### Act 2 — The Build (middle chunks)
One concept per chunk. Strict.

- Introduce one new idea per chunk
- Each chunk should make the PREVIOUS chunk more meaningful
- Use "yes, but why?" structure: show result → reveal mechanism
- Never skip the intuitive step to get to the formal step

Build order: phenomenon → intuition → formalism → consequence

### Act 3 — The Synthesis (last chunk)
Return to the opening image, transformed by understanding.

- Re-show the Act 1 visual, now annotated with what was learned
- "Before we knew why. Now we do."
- End on a held frame: the key insight visible on screen
- Last 3–5 seconds: static, clean, memorable

---

## Pacing Rules

| Moment type | Pacing |
|-------------|--------|
| New object appears | slow — 1.5–2.0s |
| Familiar object moves | fast — 0.5–1.0s |
| Equation appears | slow — 1.5–2.5s |
| Key insight holds | still — wait(3) |
| Transition between ideas | fade — 0.5s |
| Closing frame | still — wait(4) |

Don't rush insights. Viewers need time to connect dots.
Slow = deliberate, not boring.

---

## Visual Language Rules

### Color is meaning, not decoration
Pick 3–4 colors max. Each color = one concept. Never reassign.

Example for Newton's Laws:
- BLUE = object / mass
- YELLOW = force vector
- RED = acceleration
- WHITE = labels, equations

If chunk 3 uses BLUE for velocity instead of mass → confusion.

### Motion direction is semantic
- Right → positive, forward, future, increase
- Left → negative, backward, past, decrease
- Up → increase, gain, higher
- Down → decrease, loss, gravity

Don't violate these unless you're making a point about violation.

### Labels arrive after the visual
Wrong order: show equation → animate what it means
Right order: animate the concept → reveal the equation that describes it

Viewer thinks: "Oh, that's what F=ma means" not "let me remember what F=ma says"

### Camera movement = perspective shift
Move camera only to:
1. Zoom in: "look closely at this detail"
2. Zoom out: "see the bigger picture"
3. Pan: "here's something related, spatially"

Never zoom just for visual variety. Each camera move should feel like turning a page.

---

## Chunk Design Checklist

Before writing code for a chunk:

- [ ] What is the ONE concept this chunk teaches?
- [ ] What is the FIRST thing the viewer sees? (opening frame)
- [ ] What is the SURPRISE or INSIGHT moment? (at ~10s)
- [ ] What does the viewer understand at second 15 that they didn't at second 0?
- [ ] Does this chunk reference the color contract?
- [ ] Does this chunk end cleanly (FadeOut or held frame)?

---

## Common Anti-Patterns

**Anti: Definition dump**
Opening with `F = ma` text before showing anything.
Fix: Show a ball accelerating under force first.

**Anti: Too many elements**
5 objects appear simultaneously.
Fix: Introduce one, establish its meaning, then introduce the next.

**Anti: Fast equations, slow everything else**
Equation flashes onscreen in 0.3s.
Fix: Write equations with `run_time=2.0` minimum.

**Anti: Color chaos**
Using BLUE for two different concepts in the same animation.
Fix: Assign colors in SCENE_PLAN.md and never deviate.

**Anti: No resolution**
Last chunk introduces a new concept instead of synthesizing.
Fix: Last chunk must reference chunk 1 visuals.

**Anti: Wall of text**
Long sentences as `TexText` objects.
Fix: Max 8 words per text object. Use multiple lines if needed.

---

## Strong Opening Patterns

These chunk-1 openings consistently work:

1. **Object in motion**: Show before force is introduced. "Why does this keep moving?"
2. **Pattern without explanation**: Show a Fourier approximation building. "How does this work?"
3. **Two contrasting cases**: Ball rolls forever on ice vs. stops on carpet. "What's different?"
4. **Scale reveal**: Zoom from macro to micro (or reverse). "What's happening here?"
5. **Paradox setup**: Show something that seems to violate intuition. "Wait, why?"

---

## Audio Note

Skill produces silent video. When audio is added later:
- Leave 0.5s silence at start of each chunk (room for voice-over sync)
- Hold frames at insight moments 3–5s minimum (narration landing time)
- Keep text on screen 1.5× longer than time to read it
