# MDC-DAN CSCWD 2026 Slidev Presentation

This repository contains the Slidev presentation for the CSCWD 2026 paper:

**MDC-DAN: Mechanism-Data Collaborative Domain Adaptation for Sim-to-Real Fault Diagnosis in Digital Twins**

The deck is designed for an academic oral presentation. It focuses on the Sim-to-Real gap in digital-twin fault diagnosis, the proposed MDC-DAN framework, the Physics-Encoding Layer, the Domain-Adversarial Module, experiments, t-SNE/SHAP interpretability, and final conclusions.

## Project Overview

- **Format:** Slidev web-based presentation
- **Theme:** `slidev-theme-academic`
- **Language:** English slides with detailed English speaker notes
- **Use case:** CSCWD/IEEE-style conference oral presentation
- **Main entry:** `slides.md`
- **Speaker script:** `CSCWD2026_MDC-DAN_speaker_script.md`

The current deck includes embedded presenter notes for every slide, so it can be presented directly in Slidev presenter mode.

## Quick Start

Install dependencies:

```bash
pnpm install
```

Start the local Slidev server:

```bash
pnpm run dev
```

The deck is served at:

```text
http://localhost:3031
```

Build the static site:

```bash
pnpm run build
```

Export the presentation to PDF:

```bash
pnpm run export
```

The export script writes the PDF to:

```text
../CSCWD2026.pdf
```

## Repository Structure

```text
.
├── slides.md                              # Main Slidev deck
├── style.css                              # Global visual styling
├── slide-bottom.vue                       # Custom bottom page-number layer
├── CSCWD2026_MDC-DAN_speaker_script.md    # Full speaker script
├── components/                            # Vue components used by slides
├── public/figures/                        # Figures, logos, and paper images
├── package.json                           # Slidev scripts and dependencies
├── pnpm-lock.yaml                         # Locked dependency versions
└── README.md                              # Project documentation
```

## Important Files

### `slides.md`

The main presentation source. It contains:

- Slide content
- Slide frontmatter
- Imported Vue components
- Speaker notes inside HTML comment blocks

Edit this file when changing slide text, layout, or slide order.

### `style.css`

Global styling for the academic presentation, including:

- Typography
- Slide layout spacing
- Tables
- Figure panels
- Architecture diagrams
- Conclusion and thank-you pages

Edit this file when changing visual style or slide-specific layout classes.

### `CSCWD2026_MDC-DAN_speaker_script.md`

The standalone full speaker script. It is intended for rehearsal and backup reading.

The same script has also been inserted into the speaker notes of `slides.md`, so presenter mode can show page-by-page spoken text.

### `components/`

Custom Vue components used for diagrams and structured academic visuals. Important components include:

- `ProblemSetting.vue`: problem formulation with stable math rendering
- `PhysicsEncodingFigure.vue`: Physics-Encoding Layer figure layout
- `DomainAdversarialFigure.vue`: Domain-Adversarial Module figure layout
- `DomainGap.vue`: Sim-to-Real domain discrepancy visualization
- `ResultBars.vue`: main results bar chart

### `public/figures/`

Static assets used in the deck. Key files include:

- `IEEELOGO.png`
- `CSCWDLOGO.gif`
- `framework.png`
- `framework-paper.png`
- `mechanism-module.png`
- `Module.png`
- `sensitivity.png`
- `tsne.png`
- `shap.png`

When adding new figures, place them under `public/figures/` and reference them from slides as:

```md
![description](/figures/example.png)
```

## Presentation Content

The deck currently follows this structure:

1. Title
2. Presentation Outline
3. Motivation: Sim-to-Real gap
4. Research Gap
5. Problem Setting
6. Key Idea
7. Contributions
8. Full MDC-DAN Architecture
9. Physics-Encoding Layer
10. Domain-Adversarial Module
11. Experimental Setup
12. Main Results
13. Robustness and Deployment Efficiency
14. Interpretability
15. Conclusion
16. Thank You / Questions

## Speaker Notes

Each slide contains detailed presenter notes in this format:

```md
<!--
Slide X: Slide Title
Time: XX seconds

Spoken script:
...

Chinese note:
...
-->
```

To rehearse with notes:

1. Run `pnpm run dev`.
2. Open the Slidev presenter view.
3. Read the speaker notes page by page.

The spoken scripts are written as complete oral scripts rather than short cue points.

## Editing Workflow

Recommended workflow for future revisions:

1. Edit `slides.md` for slide content.
2. Edit `style.css` for layout and visual details.
3. Edit component files only when a diagram or figure layout needs structural changes.
4. Update `CSCWD2026_MDC-DAN_speaker_script.md` when the oral script changes.
5. Keep the speaker notes in `slides.md` synchronized with the standalone script.
6. Run `pnpm run build` to check that the deck still compiles.

## Useful Commands

```bash
# Start local presentation server
pnpm run dev

# Build static site
pnpm run build

# Export to PDF
pnpm run export
```

## Notes for GitHub Upload

Recommended files to commit:

- `slides.md`
- `style.css`
- `slide-bottom.vue`
- `CSCWD2026_MDC-DAN_speaker_script.md`
- `components/`
- `public/figures/`
- `package.json`
- `pnpm-lock.yaml`
- `pnpm-workspace.yaml`
- `README.md`

Usually avoid committing:

- `node_modules/`
- `dist/`
- `.DS_Store`

If needed, regenerate `dist/` with:

```bash
pnpm run build
```

## Citation / Paper Context

This presentation is based on the paper:

> Chuanshan Fang, Hongyan Qian, Yongpeng Lin, Sijie Ning, and Zhuqing Xu.  
> **MDC-DAN: Mechanism-Data Collaborative Domain Adaptation for Sim-to-Real Fault Diagnosis in Digital Twins.**  
> CSCWD 2026.

## Maintainer

Presenter / first author:

**Chuanshan Fang**  
Nanjing University of Aeronautics and Astronautics  
Email: `fcshan@nuaa.edu.cn`
