# FLIIPD Dev Journal

> Timestamped change log for development and debugging.

---

## 2026-05-22

### Session Start — 11:00 AM ET

**Task: Create FLIIPD Triangle Circle Game**
- Initial game concept: 6 triangles in a circle, click to remove 3 consecutive matching colors
- File: `triangle-circle-game.html`
- Colors: 9-color palette (Primary: Red/Blue/Yellow, Secondary: Orange/Green/Purple, Tinted: Pink/Grey/Beige)
- Triangle orientation: isosceles, base outward, point inward (short ends toward center)
- Triangle dimensions: TRI_W=100, TRI_H=50 (wider than tall)
- Circle geometry: RADIUS=140, positions at 60° increments using polar coordinates

**Task: Triangle Flip Animation** (`animation.html`)
- Created separate animation file showing Red→Red→Yellow→Blue flip sequence
- Used HTML5 Canvas with phase-based animation system (requestAnimationFrame)
- Proper hinge-fold geometry: cos(θ) for apparent width, back-face rendering, order inversion
- Phases: idle → yellowFlip → pause → blueFall → pause → combinedFlip → done

---

## 2026-05-22 — Continued Session

### 11:46 AM ET

**Task: Add Dev Journal + Game UI Updates**

User feedback from iPad reference photo (`download (1).jpg`):
> "Triangles are short across and long downward. They should be longer across and shorter to the point. Also triangles facing inward, flip beside or directly across."
> "6 points of the circle should point inward to the longer end, organized circle looks symmetrical."
> "Triangles should rotate 90° so all the back ends line up at center."

**Changes made:**
- Triangle dimensions: TRI_W=100, TRI_H=50
- Angle rotation: `angle + Math.PI / 2` applied so short ends align at center
- Triangle drawing: `moveTo(0, TRI_H) → lineTo(-TRI_W/2, 0) → lineTo(TRI_W/2, 0)` — base outward, point inward
- Center dot drawn (subtle) instead of full circle

---

### TBD: Next Changes (pending)

- [x] Fix triangle placement — ensure proper hexagon circle with equal spacing **(DONE)**
- [x] Add Next Color preview box on right side **(DONE)**
- [x] Add High Score display at top **(DONE)**
- [x] Fix bugs in findAndRemoveMatching — use Set, clear full stacks **(DONE)**
- [ ] Add FLIIPD logo in center (from `fliipdloigo.jpg`) **(PENDING)**
- [ ] Board clash: triangle base extends past `RADIUS=135` — may need wider canvas or smaller triangles **(PENDING)**

---

## 12:00 PM ET Session Summary

Game logic was completely overhauled based on iPad rules confirm:
- Select → flip → stack mechanic
- Continuous play until no valid moves remain
- 3+ consecutive same-color → clear stack, score points
- Max stack height: 6

### 12:00 PM Session Changes

| Timestamp | File | Change | Reason |
|---|---|---|---|
| 2026-05-22 12:00 | triangle-circle-game.html | Changed game mechanic to select-then-flip (was click-to-remove) | iPad rules |
| 2026-05-22 12:00 | triangle-circle-game.html | Stacks now draw inward from slot position, not offset by height | Place triangles at fixed hexagon positions |
| 2026-05-22 12:00 | triangle-circle-game.html | draw() hexagon edges: replaced broken ctx.arc parallelogram blob with lineTo edges | Visual bug |
| 2026-05-22 12:00 | triangle-circle-game.html | Fixed valid-targets JS bug: was using `i` instead of `t` in forEach loop | JS bug |
| 2026-05-22 12:00 | triangle-circle-game.html | findAndRemoveMatching: use Set + clear full stacks, +50 pts per triangle in run | Scoring bug |
| 2026-05-22 12:00 | triangle-circle-game.html | Added STACK_GAP=4 constant replacing all hardcoded `5` | Code cleanliness |
| 2026-05-22 12:00 | triangle-circle-game.html | High Score: saved to localStorage, displayed top bar | Feature |
| 2026-05-22 12:00 | triangle-circle-game.html | Next Color panel: right side preview, `drawNext()` on 80×80 canvas | Feature |
| 2026-05-22 12:00 | triangle-circle-game.html | `currentNextColor` state + `drawNext()` function | Feature requirement |
| 2026-05-22 12:00 | DEV-JOURNAL.md | Full session change log + pending items documented | Traceability |

### Still Pending
- FLIIPD logo (`fliipdloigo.jpg`) in circle center
- Triangle dimension: base extends beyond RADIUS — may need canvas resize

## Change Log Summary

| Timestamp | File | Change | Reason |
|-----------|------|--------|--------|
| 2026-05-22 | animation.html | Created FLIIPD flip animation | Core game mechanic visualization |
| 2026-05-22 | triangle-circle-game.html | Initial game with 9 colors, 6 triangles, click-to-remove logic | Base game |
| 2026-05-22 | triangle-circle-game.html | Triangle dimensions + rotation fixed | iPad reference feedback |
| TBD | triangle-circle-game.html | Hexagon circle placement fix | Triangles not evenly spaced |
| TBD | triangle-circle-game.html | FLIIPD logo center | User request |
| 2026-05-22 | triangle-circle-game.html | Added STACK_GAP constant (4px), fixed hardcoded spacing | Code cleanliness |
| 2026-05-22 | DEV-JOURNAL.md | Created timestamped dev journal with full change log | Traceability |
| 2026-05-22 | triangle-circle-game.html | Fixed getSlotPos to use fixed hexagon positions | Triangle placement bug |
| 2026-05-22 | triangle-circle-game.html | Fixed draw() - removed broken dashed-arc lines, used hexagon edges | Visual bug |
| 2026-05-22 | triangle-circle-game.html | Fixed valid-targets variable scope bug | JS bug |
| 2026-05-22 | triangle-circle-game.html | Fixed findAndRemoveMatching - use Set, clear full stacks | Clear all matching |
| 2026-05-22 | triangle-circle-game.html | Added High Score (localStorage, top bar) | Feature request |
| 2026-05-22 | triangle-circle-game.html | Added Next Color preview panel (right side, 80x80 canvas) | Feature request |

---

*Last updated: 2026-05-22, 12:00 PM ET*
