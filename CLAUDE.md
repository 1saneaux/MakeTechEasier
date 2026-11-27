# LIFE FLIP — Hand-Drawn Storybook Journal

A single-page static narrative website telling the story of a career journey from Chipotle crew member to IT AVP. No frameworks, no backend — one self-contained `index.html` with inline CSS and JS.

## Project Structure

```
pixel-tricks/
├── index.html          ← Everything: HTML + CSS + JS in one file (~1600 lines)
├── CLAUDE.md           ← This file
└── assets/
    ├── trick-1.jpg     ← Storyboard panel: kickflip attempt #1
    ├── trick-2.jpg     ← Storyboard panel: resetting, changing one variable
    ├── trick-3.jpg     ← Storyboard panel: attempt #2, closer
    ├── trick-4.jpg     ← Storyboard panel: almost landing
    ├── trick-5.jpg     ← Storyboard panel: LANDED, rolling away clean
    ├── the-climb.jpg   ← Winding road up hillside with milestones
    └── the-footer.jpg  ← Sunrise skyline, figure with skateboard
```

## Design Language

- **Style**: Hand-drawn storybook journal (restyled from original pixel-art/retro game aesthetic)
- **Typography**: Google Fonts — `Caveat` (handwritten, for titles/headers), `VT323` (monospace, for captions/body)
- **Palette**: Warm paper background (`#f3ecdf`), graphite ink (`#3a3530`), pencil gray (`#7a7268`). Dusk accent colors kept for stamps/highlights (burnt orange, teal, red, green).
- **Illustrations**: Pencil-sketch JPGs in `/assets/`. Storyboard trick panels (1–5) are loaded dynamically via JS. Climb and footer images are static `<figure>` elements.

## Page Flow (8 moments in scroll order)

1. **Opening** — "Life Flip" title in Caveat, subtitle, swaying pencil arrow
2. **The Line** — Chipotle kitchen moment (caption only, no image currently)
3. *Clipping* — "Speed is a kindness..."
4. **The Party** — Interactive speech bubbles (hover/tap to reveal conversations from balcony crew, kitchen counter, back room)
5. **The Trick** — Click-through sketchbook storyboard (5 panels with trick-1 through trick-5.jpg, overlaid stamps: BAIL!/closer/almost/LANDED!)
6. **The Realization** — Typewriter effect text sequence
7. *Clipping* — "TRY → BAIL → CHANGE ONE VARIABLE..."
8. **The Bet** — Walking away from comfortable (caption only, no image currently)
9. *Clipping* — "Everyone at the table had a reason to stay..."
10. **The Climb** — Scene image (the-climb.jpg) + interactive timeline with waypoints + fix-beat challenge (one person can't reach the VPN — pick the first move; hotspot test isolates the variable)
11. *Clipping* — "Next page is blank..."
12. **Footer** — Scene image (the-footer.jpg) + mission line + LinkedIn/email links

## Key JS Systems

- **IntersectionObserver** fade-in (700ms, 0.15 threshold) for all `.moment` sections
- **MOMENTS array** — data-driven, each with `id`, `title`, `render` function
- **Storyboard** — `STORYBOARD_PANELS` array, `showSketchPanel()` / `advanceSketch()` click-through
- **Typewriter** — `startRealizationSequence()` at 70ms/char
- **Climb waypoints** — staggered fade-in (500ms apart) via `renderClimb()`
- **Fix beat** — 3 clickable options (`FIX_OPTIONS`, each with its own BAIL/LANDED note), wrong→gray+note, correct→green+stamp
- **Changed-variable notes** — `variable` on storyboard panels and `changed` on climb waypoints render as teal handwritten "↻ changed →" notes
- **Auto-scroll chain**: Opening arrow → The Line → Storyboard end → Realization → The Bet → Fix beat correct → Footer
- **Reduced-motion toggle** — respects `prefers-reduced-motion`, toggle button top-right
- **Party touch reveal** — `initPartyTouchReveal()` for mobile tap-to-show bubbles

## Notes

- The Line and The Bet moments had SVG illustrations that were removed (user didn't like them). They currently show captions only with no images.
- Journal clippings use CSS `clip-path` for torn edges and `::before`/`::after` tape strips
- 7 clipping icons are Unicode placeholders, could be replaced with hand-drawn art
- 5 waypoint icons in the climb are simple colored dots inside circles
- Google Fonts loaded via CDN — for offline use, self-host the font files
