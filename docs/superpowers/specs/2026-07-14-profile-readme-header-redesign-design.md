# Profile README header redesign

**Date:** 2026-07-14
**Repo:** eomsteve/eomsteve (GitHub profile README)
**Status:** Approved — ready for implementation

## Goal

Replace the current header banner (pixel CCTV camera + terminal, `assets/header-pixel.svg` / `header-pixel-dark.svg`) with a cuter, more detailed pixel-art scene, while keeping the rest of the README (stack icons, contribution snake, email) unchanged. Archive the current header assets rather than deleting them.

## Final scene (dark theme, approved as of iteration v14)

Canvas 300×160, GitHub dark-theme palette (bg `#0d1117`, panel `#161b22`, border `#30363d`/`#484f58`, text `#f0f6fc`, muted `#8b949e`, green `#3fb950`, blue `#58a6ff`, purple `#a371f7`, amber `#ffb454`, red `#f85149`, yellow `#d29922`), plus a warm cat palette (tan `#f0a868`, tan-highlight `#ffcb96`, tan-shadow `#c97b3d`/`#d98c4a`, cream `#fff3e0`, blush `#ff8fab`) and figure accents (Claude terracotta `#da7756`).

Left to right:

1. **Desk strip** along the bottom (`#30363d`), full width.
2. **Monitor** (code-editor style): frame + dark screen, 3 title-bar dots (red/yellow/green), a divider line, 5 rows of colorful "code" bars (green/blue/purple/muted/amber, varied lengths), and a **blinking text cursor** (opacity loop) at the end of the last line.
3. **Two small desk figures** between the monitor and the cat:
   - **Codex figure** — dark rounded bot with two dot eyes and a small blue bracket mark on its chest.
   - **Claude figure** — terracotta-orange rounded bot with two dot eyes and a small white 4-point star/asterisk mark on its chest.
4. **Cat mascot**, sitting, facing forward:
   - Tan body with cream highlight band, sitting posture (wide torso, narrower shoulders).
   - **Wearing a black short-sleeve tee** sized flush to the body silhouette (no border/trim — a prior orange-trim iteration was explicitly rejected). A small tan **collar notch** at top-center shows a bit of "neck" through the collar so it reads as worn clothing rather than a flat color block.
   - **Yellow 4-point star** printed on the chest of the shirt.
   - Arms (tan) emerge from the short sleeves down to **white paws/hands** — the earlier "merged single chest patch" version was rejected for hiding the arms; paws must read as distinct hands at the end of visible arms.
   - **Pointy ears**: 3-step tapered triangle (wide base → narrow tip) per ear, each with a smaller pink inner-ear patch. (Replaces the original flat-top rectangular ears.)
   - Round head with tan-highlight band, 2 small head stripes, cream muzzle, big dark eyes each with a white sparkle highlight, blush cheeks, pink nose, small mouth curves.
   - **Whiskers** on both cheeks, positioned to overlap the head silhouette (no gap — an earlier version floated disconnected from the face and was rejected).
   - **Tail**: 3-segment tan/shadow-tan tail curling up from the torso's side, with a continuous **gentle wag animation** (`animateTransform` rotate, looping).

## Explicitly rejected alternatives (do not reintroduce without new user direction)

- Purple-colored cat (first draft) — replaced with tan/cheese coloring.
- Two disconnected floating paw blocks with a visible gap from the torso, and a separate floating mug — both read as "broken"/disconnected and were removed.
- A single merged white "chest patch" standing in for paws — hid the arms entirely; rejected in favor of visible arm+hand.
- Whiskers with a gap between them and the head silhouette — looked like they were floating; must overlap/touch the head.
- Orange trim/border around the T-shirt — first added on request, then explicitly reversed; shirt edges must sit flush with the body silhouette with no visible border.
- 3-step tapered/narrowing neckline (collar that narrows toward a point) — reverted in favor of a flat shoulder line with a small square collar notch instead.
- "Cursor" desk figure — was a misunderstanding; the intended second figure is **Claude**, not Cursor.

## Theming: dark + light variants

The existing README already switches banner assets via `<picture>`:

```html
<source media="(prefers-color-scheme: dark)" srcset="./assets/header-pixel-dark.svg" />
<source media="(prefers-color-scheme: light)" srcset="./assets/header-pixel.svg" />
```

Follow the same pattern for the new asset. The dark-theme colors above are approved as-is. A **light-theme counterpart** is required (background swapped to a light tone, and any color that loses contrast against light background adjusted — e.g., the cream muzzle/paws need a visible outline or shadow against white, and the monitor screen should keep a dark panel so the "code" bars still read regardless of page theme). The light variant is a follow-up color pass on the same layout/shapes, not a new design.

## Animation notes

Both animations are SMIL (`<animate>` / `<animateTransform>`), same technique GitHub already renders fine for the existing contribution-snake SVG in this repo:

- Monitor cursor: opacity blink loop, ~1s.
- Tail: rotate loop around its base attachment point, ~3s, small angle range.

No other elements are animated in the approved design (no eye-blink was ultimately added — out of scope unless requested later).

## Scope / file plan

- Archive current `assets/header-pixel.svg` and `assets/header-pixel-dark.svg` (move to `assets/archive/` rather than deleting) along with the never-used `header.svg`, `header-minimal.svg`, `header-balanced.svg` experiments.
- Produce new `assets/header-pixel-dark.svg` (dark, approved above) and `assets/header-pixel.svg` (light variant, colors adjusted per above) at the final banner dimensions — see Layout decision below.
- README.md's `<picture>` block, stack-icons section, and contribution-snake section are unchanged.

## Layout decision (resolved 2026-07-14)

**Option (a) — approved.** Keep the existing 1200×200 banner layout with the "SEONGHYUN EOM" name/title text block on the left (unchanged: `eomsteve.exe`, name, role line, accent bars). Replace only the right-side illustration — currently the pixel CCTV camera + terminal — with the new, larger cat scene (monitor, desk figures, cat), scaled down from the 300×160 brainstorming mockup to fit the illustration's existing slot (roughly `translate(730 23)` in the current SVG, ~470px available width × ~160px height). The name/title text block itself is not redesigned in this pass.
