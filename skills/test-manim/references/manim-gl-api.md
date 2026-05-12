# ManimGL API Quick Reference

Always `from manimlib import *`. Never `from manim import *`.

---

## Core Objects

### Shapes
```python
Circle(radius=1, color=BLUE)
Square(side_length=2, color=WHITE)
Rectangle(width=4, height=2, color=GREEN)
Line(start=LEFT*2, end=RIGHT*2, color=WHITE)
Arrow(start=LEFT, end=RIGHT, color=YELLOW)
Dot(point=ORIGIN, color=RED, radius=0.1)
Arc(radius=1, start_angle=0, angle=PI/2)
Polygon(np.array([...]), np.array([...]), ...)
```

### Text
```python
TexText("Regular text", font_size=36, color=WHITE)
Tex(r"\frac{d}{dx} x^2 = 2x", color=YELLOW)
TexText("F = ma", font_size=48).to_edge(UP)
```

### Math objects
```python
NumberLine(x_range=[-3, 3, 1], include_numbers=True)
NumberPlane()  # full grid
Axes(
    x_range=[-3, 3, 1],
    y_range=[-2, 2, 1],
    axis_config={"include_tip": True}
)
FunctionGraph(lambda x: x**2, x_range=[-2, 2], color=BLUE)
Vector([2, 1, 0], color=YELLOW)  # [x, y, z]
```

### Grouping
```python
VGroup(obj1, obj2, obj3)          # group, use like single object
group.arrange(DOWN, buff=0.5)     # stack vertically
group.arrange(RIGHT, buff=0.5)    # stack horizontally
group.move_to(ORIGIN)
```

---

## Positioning

```python
obj.to_edge(UP)          # snap to top edge
obj.to_edge(DOWN)        # snap to bottom
obj.to_edge(LEFT)
obj.to_edge(RIGHT)
obj.move_to(ORIGIN)      # center
obj.move_to(UP * 2)
obj.next_to(other, DOWN, buff=0.3)   # below other with gap
obj.shift(RIGHT * 2)     # move relative to current pos
obj.scale(0.8)
obj.set_color(RED)
```

**Direction constants**: `UP DOWN LEFT RIGHT UL UR DL DR ORIGIN`
**Scalar multiply**: `UP * 2`, `RIGHT * 3.5`

---

## Animations

### Appear
```python
self.play(ShowCreation(obj), run_time=1.5)      # draw border+fill
self.play(Write(text_obj), run_time=1.5)        # write text
self.play(FadeIn(obj), run_time=0.8)
self.play(FadeIn(obj, shift=UP), run_time=0.8)  # fade in from below
self.play(DrawBorderThenFill(shape), run_time=1.5)
self.add(obj)  # instant, no animation
```

### Transform
```python
self.play(Transform(obj1, obj2), run_time=1.5)              # morph obj1 into obj2
self.play(TransformMatchingShapes(obj1, obj2), run_time=1.5) # match by shape
self.play(obj.animate.shift(RIGHT * 2), run_time=1.0)
self.play(obj.animate.scale(2), run_time=1.0)
self.play(obj.animate.set_color(RED), run_time=0.5)
self.play(obj.animate.move_to(UP * 2), run_time=1.0)
```

### Disappear
```python
self.play(FadeOut(obj), run_time=0.8)
self.play(FadeOut(*self.mobjects), run_time=0.5)  # clear everything
```

### Indicate / Highlight
```python
self.play(Indicate(obj), run_time=1.0)              # pulse
self.play(Flash(obj), run_time=0.5)                 # flash ring
rect = SurroundingRectangle(obj, color=YELLOW)
self.play(ShowCreation(rect))
```

### Multiple simultaneous
```python
self.play(
    FadeIn(obj1),
    FadeIn(obj2),
    run_time=1.5
)
self.play(
    obj1.animate.shift(LEFT),
    obj2.animate.shift(RIGHT),
    run_time=1.0
)
```

### Wait
```python
self.wait(1.5)   # pause 1.5 seconds
self.wait(3)     # pause for insight moments
```

---

## Camera

```python
# Zoom in
self.play(self.camera.frame.animate.scale(0.7), run_time=1.5)
# Zoom out
self.play(self.camera.frame.animate.scale(1.5), run_time=1.5)
# Pan to object
self.play(self.camera.frame.animate.move_to(obj), run_time=1.5)
# Reset
self.play(self.camera.frame.animate.move_to(ORIGIN).set_height(8), run_time=1.0)
```

---

## Colors

```python
# Main palette
BLUE      # primary concept
YELLOW    # secondary / highlight
GREEN     # positive / correct
RED       # negative / error / force
WHITE     # labels, text
GREY      # background elements
BLACK     # background (default)

# Variants
BLUE_A BLUE_B BLUE_C BLUE_D BLUE_E  # A=lightest, E=darkest
# Same for RED, GREEN, YELLOW, GREY
```

---

## ValueTracker (for dynamic values)

```python
t = ValueTracker(0)

dot = Dot(color=BLUE)
dot.add_updater(lambda d: d.move_to(
    axes.c2p(t.get_value(), np.sin(t.get_value()))
))
self.add(dot)
self.play(t.animate.set_value(2 * PI), run_time=4)
dot.clear_updaters()
```

---

## Axes + Graphs

```python
axes = Axes(
    x_range=[-3, 3, 1],
    y_range=[-2, 2, 1],
    axis_config={
        "include_tip": True,
        "include_numbers": True,
    }
)
graph = axes.get_graph(lambda x: np.sin(x), color=BLUE)
label = axes.get_graph_label(graph, label=Tex(r"\sin(x)"))
self.play(ShowCreation(axes), run_time=1.5)
self.play(ShowCreation(graph), run_time=2.0)
```

---

## Common Patterns

### Title + content layout
```python
title = TexText("Newton's First Law", font_size=48)
title.to_edge(UP)
content = TexText("An object in motion stays in motion", font_size=36)
content.move_to(ORIGIN)
self.play(Write(title), run_time=1.0)
self.play(FadeIn(content, shift=UP * 0.3), run_time=1.0)
self.wait(2)
```

### Equation buildup
```python
eq1 = Tex(r"F")
eq2 = Tex(r"F = ma")
eq1.move_to(ORIGIN)
eq2.move_to(ORIGIN)
self.play(Write(eq1))
self.wait(1)
self.play(TransformMatchingTex(eq1, eq2), run_time=1.5)
self.wait(2)
```

### Arrow label
```python
arrow = Arrow(start=ORIGIN, end=RIGHT*2, color=YELLOW)
label = TexText("Force", font_size=32, color=YELLOW)
label.next_to(arrow, UP, buff=0.2)
self.play(ShowCreation(arrow), Write(label))
```

---

## Error → Fix Table

| Error | Cause | Fix |
|-------|-------|-----|
| `AttributeError: 'NoneType' object` | object not added before play | `self.add(obj)` or use `FadeIn` |
| `ImportError: cannot import name 'Create'` | ManimCE syntax | Use `ShowCreation` |
| `ImportError: cannot import name 'MathTex'` | ManimCE syntax | Use `Tex(r"...")` |
| `ImportError: cannot import name 'Text'` | ManimCE syntax | Use `TexText(...)` |
| `ValueError: math mode required` | Bad LaTeX string | Use raw string `r"..."`, check syntax |
| Black frame in output | Empty `construct()` or no `self.play()` | Add at least one animation |
| Merge fail: different resolution | Chunks rendered at different quality | Render all with same flags (`--hd`) |
| `AttributeError: animate` | Stale ManimGL version | Check `manimgl --version` ≥ 0.3.0 |
| Chunk longer than 15s | Too many waits or slow run_time | Reduce `self.wait()` values, check sum |
