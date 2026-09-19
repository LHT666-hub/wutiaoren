# Design QA — 第一、二页

## Comparison targets

### 第一页封面

- Source visual truth: `C:\Users\LHT\Downloads\ChatGPT Image 2026年9月19日 18_52_40.png`
- Implementation screenshot: `C:\Users\LHT\AppData\Local\Temp\unfinished-modernity-review\cover-implementation-1672x941.png`
- Source and implementation pixels: 1672 × 941
- State: `#00.0`, entrance animation complete

### 第二页视频入口

- Source visual truth: `C:\Users\LHT\Downloads\ChatGPT Image 2026年9月19日 19_08_53.png`
- Browser-rendered implementation evidence: Codex in-app Browser tab 2 screenshot, emitted inline during QA
- Source pixels: 1673 × 940
- Browser viewport and implementation capture: 1280 × 720 CSS px, device scale factor 1
- Normalization: the 1600 × 900 deck stage was uniformly scaled to the 1280 × 720 viewport; the source was visually normalized to the same 16:9 frame
- Static state: `#00.1`, video not yet started
- Playback state: local `opening.mp4` visible and playing inside the left player region

## Full-view comparison evidence

Both pages use the complete supplied artwork as full-bleed local raster assets, preserving the collage composition, typography, photographs, paper textures, palette, and copy. State-specific CSS hides the deck header, footer, progress bar, and chapter controls on `00.0` and `00.1` so no legacy chrome overlaps either reference.

For the second page, the supplied artwork remains unchanged before playback. A transparent accessible button is positioned over the artwork's existing circular play control. After activation, the real local video replaces only the illustrated player region and exposes native playback controls; the surrounding collage remains visible.

## Focused-region comparison evidence

The second-page player region was checked separately in both states:

- Before playback: the original alley preview, circular play mark, and illustrated control bar remain visually unchanged.
- After playback: the H.264 video appears within the intended left-side frame without covering the title or right-side collage.
- Keyboard path: Space changed the live video's `paused` state from false to true and back to false.
- Navigation path: ArrowRight changed the hash to `#00.2`, removed the video element with the page transition, and displayed the opening question.

## Required fidelity surfaces

- Fonts and typography: preserved directly from the supplied raster artwork; no font substitution or browser reflow.
- Spacing and layout rhythm: full-frame composition preserved; the playable video is constrained to the existing player window.
- Colors and visual tokens: preserved directly from the source PNG files.
- Image quality and asset fidelity: original PNGs are copied locally without recompression. The video is the supplied 1920 × 1080 H.264/AAC file and plays locally without a network request.
- Copy and content: all visible reference copy is preserved. Accessible names were added without altering the visible design.

## Findings

No actionable P0, P1, or P2 mismatch remains. An initial hover treatment produced an extra ring around the baked-in play button; it was removed so the idle state matches the reference. Keyboard focus still receives a red outline for accessibility.

## Interaction and runtime verification

- Click play: passed; the video became visible, `paused: false`, `readyState: 4`, duration `68.103991` seconds.
- Space pause/resume: passed.
- ArrowRight exit to `#00.2`: passed; playback stops because the inline player is removed during navigation.
- Browser console warnings/errors: none.
- JavaScript syntax checks: `content.js` and `main.js` passed.

## Comparison history

1. Initial second-page implementation reproduced the reference at rest and successfully played the supplied video.
2. QA found a P2 hover-state mismatch: an additional white glow doubled the source play circle.
3. Fix: removed the hover glow while retaining a keyboard-only focus outline.
4. Post-fix source and implementation were emitted together at the same 16:9 state; no further P0/P1/P2 differences were found.

## Follow-up polish

- P3: The 1673 × 940 source is fractionally different from exact 16:9, so projector scaling may crop or interpolate less than one pixel at an edge.
- P3: Final classroom rehearsal should confirm speaker volume on the actual projection computer.

final result: passed
