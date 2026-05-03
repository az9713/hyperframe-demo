# HyperFrames Demo — Verkor Paper Video

A test of [HyperFrames](https://github.com/heygen-com/hyperframes) generating a 15-second research paper explainer video using Claude Code as the authoring agent.

## The Prompt

> use hyperframes to create a 15 second video for the paper https://arxiv.org/pdf/2603.08716

That's the complete prompt. Claude Code read the PDF, designed the composition, wrote the HTML, fixed lint warnings, and rendered the MP4 — no manual editing.

## The Paper

**"Design Conductor: An agent autonomously builds a 1.5 GHz Linux-capable RISC-V CPU"**  
Ravi Krishna, Suresh Krishna, David Chin — The Verkor Team  
arXiv:2603.08716v1 · March 2026

Design Conductor (DC) is an autonomous AI agent that built a complete RISC-V CPU ("VerCore") in 12 hours from a 219-word requirements document — the first autonomous agent to go from spec to tape-out ready GDSII layout.

## The Output

**[▶ Watch verkor.mp4](https://github.com/user-attachments/assets/ec37a9ec-d6e1-4dd0-b987-9e239ecb09de)**

| Property | Value |
|---|---|
| Duration | 15 seconds |
| Resolution | 1920 × 1080 |
| Frame rate | 30 fps |
| File size | 991 KB |
| Render time | 36s |

### Scene breakdown

| Time | Scene | Content |
|---|---|---|
| 0–4.5s | Hook | "AI Built a CPU." — big title, "In 12 hours. From a 219-word spec." |
| 4.5–9s | What | "Spec → Silicon. End-to-End." — what Design Conductor is |
| 9–13.5s | Stats | 4-card grid: 1.48 GHz · 3261 CoreMark · 7nm · 12h build time |
| 13.5–15s | Outro | "Chip Design. Reinvented." — fade to black |

## How It Was Made

### 1. Install HyperFrames skills

```bash
npx skills add heygen-com/hyperframes
```

This installs 12 skills into `.claude/skills/` (symlinked from `.agents/skills/`) that teach Claude Code how to write correct HyperFrames compositions, GSAP timelines, and transitions.

### 2. One-shot prompt

```
use hyperframes to create a 15 second video for the paper .ignore/verkor*pdf
```

Claude Code:
1. Read the 13-page PDF with PyMuPDF
2. Extracted key facts: 12h build, 1.48 GHz, 3261 CoreMark, 219-word input, first spec→GDSII agent
3. Designed a 4-scene narrative arc with fade-to-black transitions
4. Wrote `verkor/index.html` — a standalone HyperFrames composition using GSAP 3 for animation
5. Fixed all lint warnings (missing `class="clip"`, `data-start="0"` on root, tween boundary overlaps, hard-kill sets)
6. Rendered to MP4

### 3. Render

```bash
cd verkor
npx hyperframes render
# → renders/verkor_2026-05-03_07-17-02.mp4
```

## Design Choices

- **Palette:** Dark premium — `#07070f` background, `#00d4ff` cyan (circuit traces), `#7c3aed` purple (AI), `#ff6b35` orange (numbers)
- **Font:** Space Grotesk (auto-fetched and embedded by the HyperFrames compiler)
- **Transitions:** Fade-to-black overlays on separate tracks between each scene
- **Animation:** GSAP `from()` entrances only; no exit animations except the final scene fade

## Files

```
verkor/
├── index.html                              # HyperFrames composition source
└── renders/
    └── verkor_2026-05-03_07-17-02.mp4     # Rendered output (991 KB)
```

## Requirements

- Node.js ≥ 22
- FFmpeg on PATH
- Chrome (for headless rendering)
