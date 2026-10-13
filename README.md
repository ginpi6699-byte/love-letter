# Handoff: Love Letter v2 (dark red vintage anniversary page)

## Overview
Single-page romantic anniversary app. Dark red background with 40 twinkling gold sparkles, a looping photo strip, a horizontal red MP3-player card ("About You" – The 1975), two gold heart buttons, an ivory envelope that opens a Vietnamese love letter, and two overlays (falling-particle text reveal, tarot card modal).

## About the design file
`Love Letter v2.dc.html` is a working HTML prototype (open it directly in a browser; it needs `support.js` beside it). Recreate it in your target stack (React, Vue, etc.); do not paste verbatim. High fidelity: colors, spacing, type and timings are final.

## Layout (top to bottom, centered column, max 520px)
1. **Background**: fixed full-viewport `assets/bg-dark-red.jpg` (cover, center), fallback `#3a0008`. Above it, 40 absolutely-positioned 4-point star SVGs (`#fde047`, 6-18px, random position, `blingBg` 3-7s, random delay 0-5s, infinite).
2. **Photo strip**: glass card (`rgba(255,255,255,.4)`, blur 18px, 1px white border, radius 28px, padding 20px 0). 5 photos `gallery-1..5-sharp.png` duplicated for a seamless loop, each 150x190px, radius 24px, object-fit cover. Row scrolls `translateX(0 -> -50%)`, 22s linear infinite. Images are pre-sharpened 600x760 sources; keep `image-rendering:auto`.
3. **MP3 player**: width `min(800px, 100vw - 32px)`, bg `#5c1010`, border 2px `#3a0606`, radius 24px, padding `clamp(12px,2.5vw,24px)`, row, no wrap, gap `clamp(12px,3vw,32px)`. Left: album art `album-art.jpeg`, 45% width, square, radius 12px. Right (flex 1): title "About You" (system-ui 700, `clamp(18px,3.6vw,30px)`, white), artist "The 1975" (70% white), progress bar (65% fill `#e2b8b8`, times 2:21 / -2:20), prev / play-pause (scaled 1.25) / next icons, volume and shuffle icons at 60% opacity. Play/pause only toggles the icon; no audio is wired. A small tab (8x64px, `#4a0a0a`) sits on the left edge.
4. **Heart buttons**: two 72px `heartgold.png` buttons, gap 24px, hover scale 1.12, active .95. Left = love burst, right = tarot.
5. **Envelope**: `envelope-lover-ivory.png`, width 90vw, max 450px (550px at >=768px), drop shadow, hover scale 1.05. Below it `pill-button-ivory.png` (220px, 260px at >=768px) with label "anh mở thư nhé!" (Cormorant Garamond 600, `clamp(18px,2.4vw,20px)`, `#7a6440`). Either click opens the letter (no re-collapse).
6. **Letter card** (shown when open): bg `#FDFBF7`, radius 28px, padding 32px, shadow `0 20px 45px rgba(214,150,170,.22)`. Opens with max-height 0 -> 9000px and opacity 0 -> 1 (.9s / .6s). Text color `#5b4540`, line-height 2, justified; headings and sign-off italic 600 `#7a4a52`. Copy is verbatim in the file; do not rewrite.

## Interactions
- **Left heart (loveBurst)**: spawns 120 falling particles from `top:-10%` to 110%. Each: random image from the 10 `particle-*-deepred/gold` and `glass-heart-deepred/gold` files, random x 0-100vw, width 80-160px, fall 1.8-3.2s linear, start delay 0-2.4s, plus sway 2.5-5s ease-in-out infinite. Container z-index 9999, `pointer-events:none`, cleared after the last one lands (+0.8s). When rain ends, show "I love you more than I can say" centered (Cinzel Decorative 400, `clamp(34px,7vw,92px)`, white) with a radial gold bloom behind it; `loveReveal` runs 6s (blur-in, gold text-shadow glow, fade out), then unmounts on animationend.
- **Right heart (openLovers)**: full-screen modal (z-index 100000, `rgba(0,0,0,.85)` + blur 10px). Shows `thelovers.png` (max 420px wide / 80vh tall, 3px gold border, radius 10px, `glowPulse` 3s, diagonal `sheen` sweep 3.5s) with `zoomCard` entrance. 30 gold sparkles (8-26px, `bling` 2-5s, random delays) twinkle around. Click backdrop or the "Trở lại ✕" pill to close.

## State
`letterOpen`, `playing` (icon only), `particles`/`isRaining`, `showLoveText`, `showLovers`, `sparkles`, `vw` (resize listener for the 768px breakpoint values). Photos are overridable props `photo1..photo5`.

## Tokens
- Fonts (Google Fonts): Cormorant Garamond 400-700 + italics; Cinzel Decorative 400/700.
- Colors: bg `#3a0008`, player `#5c1010` / `#3a0606` / `#4a0a0a`, progress `#e2b8b8`, gold `#fde047` / `#f2c94c` / `rgba(234,179,8,.6)`, letter `#FDFBF7`, ink `#5b4540`, accent `#7a4a52`, pill label `#7a6440`.
- All keyframes are in the file's `<style>` block (loveMarquee, particleFall, particleSway, scrollLoop, bling, blingBg, zoomCard, sheen, glowPulse, loveReveal, loveBloom, fadeInBd). `loveMarquee`, `floatUpElegant` and `triggerParticlesOld` are unused leftovers.

## Notes
- `lyricLines`, `leftWidth` in `renderVals` are unused.
- Responsive: player stays horizontal at all widths and scales via clamp(); layout wraps at 520px column.

## Files
- `Love Letter v2.dc.html`: source of truth (template + logic).
- `support.js`: runtime needed to open the .dc.html.
- `assets/`: bg-dark-red.jpg, album-art.jpeg, heartgold.png, envelope-lover-ivory.png, pill-button-ivory.png, thelovers.png, gallery-1..5-sharp.png, particle-1..4-deepred/gold.png, glass-heart-deepred/gold.png.
