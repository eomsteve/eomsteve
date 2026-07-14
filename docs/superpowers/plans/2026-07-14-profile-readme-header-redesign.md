# Profile README Header Redesign Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace the pixel-art illustration in `eomsteve/eomsteve`'s profile README header banner with the approved cat-mascot scene (cat in a black tee + star, pointy ears, wagging tail, Codex/Claude desk figures, animated code monitor), in both dark and light theme variants, while archiving the old illustration assets instead of deleting them.

**Architecture:** Two standalone SVG files (`assets/header-pixel-dark.svg`, `assets/header-pixel.svg`), each a 1200×200 banner: the existing left-side name/title text block (unchanged) plus a new illustration `<g>` group (the cat scene) on the right, replacing the old camera+terminal `<g>` group. No build step — these are static files referenced directly by `README.md`'s existing `<picture>` element, so no README changes are needed.

**Tech Stack:** Hand-written SVG (`rect`/`g`/`animate`/`animateTransform`), no tooling/build step. Verification is XML well-formedness (Python's stdlib `xml.dom.minidom`) plus manual visual confirmation in a browser.

## Global Constraints

- Repo: `~/dev/eomsteve` (a clone of `eomsteve/eomsteve`), not the `career-ops` repo.
- Design source of truth: `docs/superpowers/specs/2026-07-14-profile-readme-header-redesign-design.md` — every color/shape/animation decision below is copied from there; if anything here seems to contradict it, the spec wins and this plan has a bug.
- Do not delete the current header assets — move them to `assets/archive/`.
- Do not modify `README.md`'s stack-icons section or contribution-snake section.
- Canvas stays `1200×200`, `viewBox="0 0 1200 200"`, `shape-rendering="crispEdges"` (matches existing banners).
- Neither file has a full-canvas background rect — both rely on the surrounding page background staying transparent (matches the existing two files, confirmed by reading them: no `<rect>` covers the full `0 0 1200 200` canvas in either).

---

### Task 1: Archive the old header illustration assets

**Files:**
- Create: `assets/archive/` (new directory)
- Move: `assets/header-pixel.svg` → `assets/archive/header-pixel.svg`
- Move: `assets/header-pixel-dark.svg` → `assets/archive/header-pixel-dark.svg`
- Move: `assets/header.svg` → `assets/archive/header.svg`
- Move: `assets/header-minimal.svg` → `assets/archive/header-minimal.svg`
- Move: `assets/header-balanced.svg` → `assets/archive/header-balanced.svg`

**Interfaces:**
- Consumes: nothing (first task).
- Produces: `assets/archive/header-pixel.svg` and `assets/archive/header-pixel-dark.svg` are the exact byte-for-byte originals — Task 2 and Task 3 read the text block out of these archived copies rather than reconstructing it from memory.

- [ ] **Step 1: Create the archive directory and move all five files with `git mv`**

```bash
cd ~/dev/eomsteve
mkdir -p assets/archive
git mv assets/header-pixel.svg assets/archive/header-pixel.svg
git mv assets/header-pixel-dark.svg assets/archive/header-pixel-dark.svg
git mv assets/header.svg assets/archive/header.svg
git mv assets/header-minimal.svg assets/archive/header-minimal.svg
git mv assets/header-balanced.svg assets/archive/header-balanced.svg
```

- [ ] **Step 2: Verify the move**

Run: `ls assets/ assets/archive/`
Expected:
```
assets/:
archive

assets/archive/:
header-balanced.svg  header-minimal.svg  header-pixel-dark.svg  header-pixel.svg  header.svg
```

- [ ] **Step 3: Verify README still resolves (it references files that no longer exist at the old path — this is expected and fixed in Task 2)**

Run: `grep -n "assets/header" README.md`
Expected: two lines, both still pointing at `./assets/header-pixel-dark.svg` and `./assets/header-pixel.svg` (the non-archived path) — this is the broken intermediate state Task 2 fixes by creating new files at exactly those paths.

- [ ] **Step 4: Commit**

```bash
git add -A
git commit -m "Archive old header illustration assets before redesign"
```

---

### Task 2: Build the new dark-theme banner (`assets/header-pixel-dark.svg`)

**Files:**
- Create: `assets/header-pixel-dark.svg`
- Read (reference only, do not modify): `assets/archive/header-pixel-dark.svg`

**Interfaces:**
- Consumes: the text-block markup (lines 5–12) from `assets/archive/header-pixel-dark.svg`, copied verbatim.
- Produces: `assets/header-pixel-dark.svg`, a complete standalone 1200×200 SVG — Task 4's README check depends on this file existing at exactly this path.

- [ ] **Step 1: Write the complete file**

Create `assets/header-pixel-dark.svg` with this exact content (text block copied verbatim from the archived original; illustration group is the approved v14 cat scene, wrapped in `translate(815 20)` to sit inside the existing right-hand illustration slot):

```xml
<svg xmlns="http://www.w3.org/2000/svg" width="1200" height="200" viewBox="0 0 1200 200" role="img" aria-labelledby="title desc" shape-rendering="crispEdges">
  <title id="title">Seonghyun Eom — Software Engineer</title>
  <desc id="desc">A transparent banner with large type and a pixel-art scene of a cat mascot at a desk with an animated code monitor.</desc>

  <g font-family="ui-monospace, SFMono-Regular, Menlo, Consolas, monospace">
    <text x="38" y="42" fill="#8b949e" font-size="18">eomsteve.exe</text>
    <text x="36" y="104" fill="#f0f6fc" font-size="52" font-weight="800" letter-spacing="0.5">SEONGHYUN EOM</text>
    <text x="38" y="145" fill="#8b949e" font-size="23">software engineer</text>
    <rect x="38" y="169" width="84" height="7" fill="#3fb950"/>
    <rect x="130" y="169" width="28" height="7" fill="#a371f7"/>
    <rect x="166" y="169" width="12" height="7" fill="#f0f6fc"/>
  </g>

  <g transform="translate(815 20)">
    <rect x="0" y="140" width="300" height="20" fill="#30363d"/>
    <rect x="10" y="40" width="120" height="80" fill="none" stroke="#484f58" stroke-width="6"/>
    <rect x="18" y="48" width="104" height="56" fill="#161b22"/>
    <rect x="24" y="54" width="6" height="6" fill="#f85149"/>
    <rect x="34" y="54" width="6" height="6" fill="#d29922"/>
    <rect x="44" y="54" width="6" height="6" fill="#3fb950"/>
    <rect x="24" y="64" width="88" height="3" fill="#30363d"/>
    <rect x="24" y="72" width="30" height="5" fill="#3fb950"/>
    <rect x="58" y="72" width="14" height="5" fill="#58a6ff"/>
    <rect x="24" y="80" width="16" height="5" fill="#a371f7"/>
    <rect x="44" y="80" width="40" height="5" fill="#8b949e"/>
    <rect x="24" y="88" width="50" height="5" fill="#ffb454"/>
    <rect x="24" y="96" width="20" height="5" fill="#3fb950"/>
    <rect x="48" y="96" width="24" height="5" fill="#a371f7"/>
    <rect x="24" y="104" width="34" height="5" fill="#58a6ff"/>
    <rect x="60" y="104" width="5" height="5" fill="#f0f6fc">
      <animate attributeName="opacity" values="1;1;0;0;1" dur="1s" repeatCount="indefinite"/>
    </rect>
    <rect x="58" y="120" width="24" height="8" fill="#30363d"/>
    <rect x="48" y="128" width="44" height="6" fill="#30363d"/>

    <rect x="132" y="124" width="16" height="16" fill="#21262d"/>
    <rect x="135" y="114" width="10" height="12" fill="#30363d"/>
    <rect x="137" y="118" width="2" height="2" fill="#f0f6fc"/>
    <rect x="142" y="118" width="2" height="2" fill="#f0f6fc"/>
    <rect x="136" y="132" width="3" height="2" fill="#58a6ff"/>
    <rect x="143" y="132" width="3" height="2" fill="#58a6ff"/>

    <rect x="159" y="118" width="6" height="6" fill="#da7756"/>
    <rect x="160" y="120" width="2" height="2" fill="#21262d"/>
    <rect x="163" y="120" width="2" height="2" fill="#21262d"/>
    <rect x="154" y="124" width="16" height="10" fill="#da7756"/>
    <rect x="157" y="134" width="10" height="6" fill="#da7756"/>
    <rect x="160" y="126" width="4" height="8" fill="#fff3e0"/>
    <rect x="156" y="129" width="12" height="3" fill="#fff3e0"/>

    <g>
      <rect x="238" y="110" width="14" height="14" fill="#d98c4a"/>
      <rect x="248" y="96" width="12" height="14" fill="#d98c4a"/>
      <rect x="254" y="82" width="12" height="14" fill="#f0a868"/>
      <animateTransform attributeName="transform" type="rotate" values="0 240 124; 10 240 124; 0 240 124; -6 240 124; 0 240 124" dur="3s" repeatCount="indefinite"/>
    </g>

    <rect x="174" y="88" width="64" height="14" fill="#f0a868"/>
    <rect x="168" y="102" width="76" height="30" fill="#f0a868"/>

    <rect x="174" y="88" width="64" height="14" fill="#21262d"/>
    <rect x="168" y="102" width="76" height="30" fill="#21262d"/>

    <rect x="199" y="88" width="18" height="6" fill="#f0a868"/>

    <rect x="203" y="104" width="6" height="20" fill="#ffd166"/>
    <rect x="193" y="111" width="26" height="6" fill="#ffd166"/>
    <rect x="197" y="107" width="18" height="4" fill="#ffd166"/>
    <rect x="197" y="117" width="18" height="4" fill="#ffd166"/>

    <rect x="176" y="118" width="14" height="18" fill="#f0a868"/>
    <rect x="218" y="118" width="14" height="18" fill="#f0a868"/>
    <rect x="174" y="130" width="18" height="14" fill="#f0f6fc"/>
    <rect x="216" y="130" width="18" height="14" fill="#f0f6fc"/>

    <rect x="175" y="36" width="24" height="8" fill="#f0a868"/>
    <rect x="179" y="28" width="16" height="8" fill="#f0a868"/>
    <rect x="183" y="20" width="8" height="8" fill="#f0a868"/>
    <rect x="180" y="32" width="10" height="10" fill="#ff8fab"/>

    <rect x="221" y="36" width="24" height="8" fill="#f0a868"/>
    <rect x="225" y="28" width="16" height="8" fill="#f0a868"/>
    <rect x="229" y="20" width="8" height="8" fill="#f0a868"/>
    <rect x="228" y="32" width="10" height="10" fill="#ff8fab"/>

    <rect x="174" y="44" width="72" height="44" fill="#f0a868"/>
    <rect x="174" y="44" width="72" height="8" fill="#ffcb96"/>
    <rect x="180" y="50" width="8" height="4" fill="#c97b3d"/>
    <rect x="232" y="50" width="8" height="4" fill="#c97b3d"/>
    <rect x="188" y="68" width="44" height="18" fill="#fff3e0"/>
    <rect x="188" y="58" width="12" height="12" fill="#0d1117"/>
    <rect x="220" y="58" width="12" height="12" fill="#0d1117"/>
    <rect x="191" y="60" width="4" height="4" fill="#f0f6fc"/>
    <rect x="223" y="60" width="4" height="4" fill="#f0f6fc"/>
    <rect x="178" y="76" width="9" height="7" fill="#ff8fab"/>
    <rect x="233" y="76" width="9" height="7" fill="#ff8fab"/>
    <rect x="206" y="74" width="8" height="6" fill="#ff8fab"/>
    <rect x="202" y="82" width="6" height="4" fill="#c97b3d"/>
    <rect x="212" y="82" width="6" height="4" fill="#c97b3d"/>
    <rect x="152" y="71" width="28" height="3" fill="#8b949e"/>
    <rect x="152" y="79" width="28" height="3" fill="#8b949e"/>
    <rect x="240" y="71" width="28" height="3" fill="#8b949e"/>
    <rect x="240" y="79" width="28" height="3" fill="#8b949e"/>
  </g>
</svg>
```

- [ ] **Step 2: Validate the XML is well-formed**

Run:
```bash
python3 -c "import xml.dom.minidom; xml.dom.minidom.parse('assets/header-pixel-dark.svg'); print('OK')"
```
Expected: `OK` (a malformed-XML parse error here means a typo'd/unclosed tag — fix and re-run before continuing).

- [ ] **Step 3: Visually confirm in a browser**

```bash
open assets/header-pixel-dark.svg
```
Expected: the banner renders with "SEONGHYUN EOM" text on the left and the cat scene (monitor with blinking cursor, Codex + Claude desk figures, cat in a black tee with a star, pointy ears, wagging tail) on the right, against your browser's background. Confirm the tail is wagging and the cursor is blinking (wait ~3 seconds).

- [ ] **Step 4: Commit**

```bash
git add assets/header-pixel-dark.svg
git commit -m "Add redesigned dark-theme header banner with cat mascot scene"
```

---

### Task 3: Build the light-theme banner (`assets/header-pixel.svg`)

**Files:**
- Create: `assets/header-pixel.svg`
- Read (reference only): `assets/archive/header-pixel.svg`, `assets/header-pixel-dark.svg` (from Task 2)

**Interfaces:**
- Consumes: `assets/header-pixel-dark.svg`'s full structure from Task 2 (same shapes, same coordinates) — Task 3 only substitutes the color values below and copies the light-theme text block verbatim from the archived original.
- Produces: `assets/header-pixel.svg` — Task 4's README check depends on this file existing at exactly this path.

**Color substitution table (dark → light), derived from comparing the two archived originals' palettes:**

| Element | Dark value | Light value | Reason |
|---|---|---|---|
| Body/heading text | `#f0f6fc` | `#1f2328` | matches archived light text color |
| Muted text | `#8b949e` | `#57606a` | matches archived light muted color |
| Green accent | `#3fb950` | `#1f883d` | matches archived light green |
| Purple accent | `#a371f7` | `#8250df` | matches archived light purple |
| Red accent | `#f85149` | `#cf222e` | matches archived light red |
| Yellow accent | `#d29922` | `#bf8700` | matches archived light yellow |
| Border/divider fill | `#30363d` | `#d0d7de` | matches archived light border |
| Blue accent (new) | `#58a6ff` | `#0969da` | GitHub Primer light-theme blue |
| Amber accent (new) | `#ffb454` | `#953800` | distinguishable from the yellow window-dot on a light background |
| Monitor frame stroke | `#484f58` | `#57606a` | mid-grey readable against a white page |
| Monitor screen fill | `#161b22` | `#161b22` (unchanged) | deliberately a dark IDE screen regardless of page theme |
| Eye/pupil black | `#0d1117` | `#0d1117` (unchanged) | reads as "black" on either page background |
| Codex body | `#21262d` | `#21262d` (unchanged) | dark figure body is deliberate, reads fine on white |
| Codex head | `#30363d` | `#30363d` (unchanged) | same reasoning |
| White paws / eye sparkle | `#f0f6fc` | `#d0d7de` | pure near-white nearly disappears against an actual white page; swap to light grey |
| Claude terracotta / star / cat tan tones / blush pink / cream | unchanged | unchanged | mid-saturation colors read fine on both dark and light pages |

- [ ] **Step 1: Write the complete file**

Create `assets/header-pixel.svg` — same structure as `assets/header-pixel-dark.svg` from Task 2, with the text block copied verbatim from `assets/archive/header-pixel.svg` and the color substitutions from the table above applied throughout the illustration group:

```xml
<svg xmlns="http://www.w3.org/2000/svg" width="1200" height="200" viewBox="0 0 1200 200" role="img" aria-labelledby="title desc" shape-rendering="crispEdges">
  <title id="title">Seonghyun Eom — Software Engineer</title>
  <desc id="desc">A transparent banner with large type and a pixel-art scene of a cat mascot at a desk with an animated code monitor.</desc>

  <g font-family="ui-monospace, SFMono-Regular, Menlo, Consolas, monospace">
    <text x="38" y="42" fill="#57606a" font-size="18">eomsteve.exe</text>
    <text x="36" y="104" fill="#1f2328" font-size="52" font-weight="800" letter-spacing="0.5">SEONGHYUN EOM</text>
    <text x="38" y="145" fill="#57606a" font-size="23">software engineer</text>
    <rect x="38" y="169" width="84" height="7" fill="#1f883d"/>
    <rect x="130" y="169" width="28" height="7" fill="#8250df"/>
    <rect x="166" y="169" width="12" height="7" fill="#1f2328"/>
  </g>

  <g transform="translate(815 20)">
    <rect x="0" y="140" width="300" height="20" fill="#d0d7de"/>
    <rect x="10" y="40" width="120" height="80" fill="none" stroke="#57606a" stroke-width="6"/>
    <rect x="18" y="48" width="104" height="56" fill="#161b22"/>
    <rect x="24" y="54" width="6" height="6" fill="#cf222e"/>
    <rect x="34" y="54" width="6" height="6" fill="#bf8700"/>
    <rect x="44" y="54" width="6" height="6" fill="#1f883d"/>
    <rect x="24" y="64" width="88" height="3" fill="#d0d7de"/>
    <rect x="24" y="72" width="30" height="5" fill="#1f883d"/>
    <rect x="58" y="72" width="14" height="5" fill="#0969da"/>
    <rect x="24" y="80" width="16" height="5" fill="#8250df"/>
    <rect x="44" y="80" width="40" height="5" fill="#57606a"/>
    <rect x="24" y="88" width="50" height="5" fill="#953800"/>
    <rect x="24" y="96" width="20" height="5" fill="#1f883d"/>
    <rect x="48" y="96" width="24" height="5" fill="#8250df"/>
    <rect x="24" y="104" width="34" height="5" fill="#0969da"/>
    <rect x="60" y="104" width="5" height="5" fill="#d0d7de">
      <animate attributeName="opacity" values="1;1;0;0;1" dur="1s" repeatCount="indefinite"/>
    </rect>
    <rect x="58" y="120" width="24" height="8" fill="#d0d7de"/>
    <rect x="48" y="128" width="44" height="6" fill="#d0d7de"/>

    <rect x="132" y="124" width="16" height="16" fill="#21262d"/>
    <rect x="135" y="114" width="10" height="12" fill="#30363d"/>
    <rect x="137" y="118" width="2" height="2" fill="#d0d7de"/>
    <rect x="142" y="118" width="2" height="2" fill="#d0d7de"/>
    <rect x="136" y="132" width="3" height="2" fill="#0969da"/>
    <rect x="143" y="132" width="3" height="2" fill="#0969da"/>

    <rect x="159" y="118" width="6" height="6" fill="#da7756"/>
    <rect x="160" y="120" width="2" height="2" fill="#21262d"/>
    <rect x="163" y="120" width="2" height="2" fill="#21262d"/>
    <rect x="154" y="124" width="16" height="10" fill="#da7756"/>
    <rect x="157" y="134" width="10" height="6" fill="#da7756"/>
    <rect x="160" y="126" width="4" height="8" fill="#fff3e0"/>
    <rect x="156" y="129" width="12" height="3" fill="#fff3e0"/>

    <g>
      <rect x="238" y="110" width="14" height="14" fill="#d98c4a"/>
      <rect x="248" y="96" width="12" height="14" fill="#d98c4a"/>
      <rect x="254" y="82" width="12" height="14" fill="#f0a868"/>
      <animateTransform attributeName="transform" type="rotate" values="0 240 124; 10 240 124; 0 240 124; -6 240 124; 0 240 124" dur="3s" repeatCount="indefinite"/>
    </g>

    <rect x="174" y="88" width="64" height="14" fill="#f0a868"/>
    <rect x="168" y="102" width="76" height="30" fill="#f0a868"/>

    <rect x="174" y="88" width="64" height="14" fill="#21262d"/>
    <rect x="168" y="102" width="76" height="30" fill="#21262d"/>

    <rect x="199" y="88" width="18" height="6" fill="#f0a868"/>

    <rect x="203" y="104" width="6" height="20" fill="#ffd166"/>
    <rect x="193" y="111" width="26" height="6" fill="#ffd166"/>
    <rect x="197" y="107" width="18" height="4" fill="#ffd166"/>
    <rect x="197" y="117" width="18" height="4" fill="#ffd166"/>

    <rect x="176" y="118" width="14" height="18" fill="#f0a868"/>
    <rect x="218" y="118" width="14" height="18" fill="#f0a868"/>
    <rect x="174" y="130" width="18" height="14" fill="#d0d7de"/>
    <rect x="216" y="130" width="18" height="14" fill="#d0d7de"/>

    <rect x="175" y="36" width="24" height="8" fill="#f0a868"/>
    <rect x="179" y="28" width="16" height="8" fill="#f0a868"/>
    <rect x="183" y="20" width="8" height="8" fill="#f0a868"/>
    <rect x="180" y="32" width="10" height="10" fill="#ff8fab"/>

    <rect x="221" y="36" width="24" height="8" fill="#f0a868"/>
    <rect x="225" y="28" width="16" height="8" fill="#f0a868"/>
    <rect x="229" y="20" width="8" height="8" fill="#f0a868"/>
    <rect x="228" y="32" width="10" height="10" fill="#ff8fab"/>

    <rect x="174" y="44" width="72" height="44" fill="#f0a868"/>
    <rect x="174" y="44" width="72" height="8" fill="#ffcb96"/>
    <rect x="180" y="50" width="8" height="4" fill="#c97b3d"/>
    <rect x="232" y="50" width="8" height="4" fill="#c97b3d"/>
    <rect x="188" y="68" width="44" height="18" fill="#fff3e0"/>
    <rect x="188" y="58" width="12" height="12" fill="#0d1117"/>
    <rect x="220" y="58" width="12" height="12" fill="#0d1117"/>
    <rect x="191" y="60" width="4" height="4" fill="#d0d7de"/>
    <rect x="223" y="60" width="4" height="4" fill="#d0d7de"/>
    <rect x="178" y="76" width="9" height="7" fill="#ff8fab"/>
    <rect x="233" y="76" width="9" height="7" fill="#ff8fab"/>
    <rect x="206" y="74" width="8" height="6" fill="#ff8fab"/>
    <rect x="202" y="82" width="6" height="4" fill="#c97b3d"/>
    <rect x="212" y="82" width="6" height="4" fill="#c97b3d"/>
    <rect x="152" y="71" width="28" height="3" fill="#57606a"/>
    <rect x="152" y="79" width="28" height="3" fill="#57606a"/>
    <rect x="240" y="71" width="28" height="3" fill="#57606a"/>
    <rect x="240" y="79" width="28" height="3" fill="#57606a"/>
  </g>
</svg>
```

- [ ] **Step 2: Validate the XML is well-formed**

Run:
```bash
python3 -c "import xml.dom.minidom; xml.dom.minidom.parse('assets/header-pixel.svg'); print('OK')"
```
Expected: `OK`

- [ ] **Step 3: Visually confirm in a browser, specifically checking light-background contrast**

```bash
open assets/header-pixel.svg
```
Expected: renders on your browser's (light) background with dark "SEONGHYUN EOM" text, and — the specific thing this task changed — the cat's two front paws and the monitor's blinking cursor are a visible light grey (`#d0d7de`), not invisible white-on-white. Everything else should look the same shapes/positions as the dark version, just recolored.

- [ ] **Step 4: Commit**

```bash
git add assets/header-pixel.svg
git commit -m "Add redesigned light-theme header banner with cat mascot scene"
```

---

### Task 4: Confirm the README wires up correctly and push

**Files:**
- Read only: `README.md`

**Interfaces:**
- Consumes: `assets/header-pixel-dark.svg` and `assets/header-pixel.svg` from Tasks 2–3 (must exist at these exact paths — `README.md` is not modified since it already references these paths).

- [ ] **Step 1: Confirm README's `<picture>` element already points at the new files**

Run: `grep -n "assets/header-pixel" README.md`
Expected:
```
3:    <source media="(prefers-color-scheme: dark)" srcset="./assets/header-pixel-dark.svg" />
4:    <source media="(prefers-color-scheme: light)" srcset="./assets/header-pixel.svg" />
5:    <img src="./assets/header-pixel.svg" width="100%" alt="Seonghyun Eom — Software Engineer" />
```
No edits needed — Tasks 2 and 3 created files at exactly these paths.

- [ ] **Step 2: Full working-tree sanity check before pushing**

Run: `git status --short`
Expected: empty (everything from Tasks 1–3 already committed). If anything unexpected shows up, stop and investigate before continuing.

- [ ] **Step 3: Push**

```bash
git push
```

- [ ] **Step 4: Confirm on GitHub**

Open `https://github.com/eomsteve/eomsteve` in a browser (toggle GitHub's own light/dark theme switch, bottom-right profile menu → "Appearance", if you want to check both variants) and confirm the new cat scene renders with the tail wagging and monitor cursor blinking, in place of the old camera+terminal illustration.
