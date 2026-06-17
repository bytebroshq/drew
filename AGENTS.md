# Drew

ByteBros HTML slide decks. Keep this file light: it points agents to the real context, then highlights only the constraints most likely to prevent wrong work.

## Knowledge

- **Skill**: [`skills/frontend-slides/SKILL.md`](skills/frontend-slides/SKILL.md) — the full workflow for creating HTML presentations. Load this before any slide work.
- Supporting files load on-demand: `STYLE_PRESETS.md`, `viewport-base.css`, `html-template.md`, `animation-patterns.md`, `bold-template-pack/`.
- Product rationale, decisions, and roadmap live in the workspace Folio knowledge base.

## Working stance

- **Zero dependencies**: every deck is a single, self-contained HTML file with inline CSS/JS. No npm, no build tools, no frameworks.
- Output land in [`decks/`](decks/). One file per deck.
- Follow the skill's workflow: gather content → preview styles → user picks → generate full deck.
- Do not add build steps, frameworks, or external asset dependencies unless explicitly requested.

## Skills

Before slide work, load the project-local frontend-slides skill:

- `skills/frontend-slides/SKILL.md` — always load this first.
- `skills/frontend-slides/STYLE_PRESETS.md` — 12 curated visual presets (load during style selection phase).
- `skills/frontend-slides/bold-template-pack/selection-index.json` — 34 bold template candidates.
- `skills/frontend-slides/html-template.md` — HTML structure and JS features (load during generation).
- `skills/frontend-slides/viewport-base.css` — mandatory fixed-stage CSS (load during generation).
- `skills/frontend-slides/animation-patterns.md` — CSS/JS animation reference (load on demand).
- `skills/frontend-slides/scripts/extract-pptx.py` — PPT content extraction (load for conversions).

## Key Files

```
drew/
├── AGENTS.md              ← this file
├── README.md
├── decks/                 ← output: one HTML file per deck
└── skills/
    └── frontend-slides/   ← project-local skill checkout
        ├── SKILL.md           ← workflow map (always load first)
        ├── STYLE_PRESETS.md
        ├── viewport-base.css
        ├── html-template.md
        ├── animation-patterns.md
        ├── bold-template-pack/
        └── scripts/
```

## Gotchas

- **Viewport is fixed 16:9** — `viewport-base.css` must be included in every deck.
- **No framework imports** — decks are standalone HTML. Google Fonts via `@import` in `<style>` are fine.
- **Scripts require python/npm** — `extract-pptx.py` needs `python-pptx`; `deploy.sh` and `export-pdf.sh` need Node.js. These are dev-time only, not deck dependencies.
