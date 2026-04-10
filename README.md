# 🌳 Family Tree

> **A vibe-coded genealogy app.** Built entirely through conversation with Claude — no manual coding, just ideas, iteration, and a lot of back-and-forth debugging.

![Version](https://img.shields.io/badge/version-2.0.0-c9a84c?style=flat-square)
![Single File](https://img.shields.io/badge/delivery-single%20HTML%20file-4a9edd?style=flat-square)
![No Dependencies](https://img.shields.io/badge/dependencies-zero%20at%20runtime-52b06a?style=flat-square)
![Works Offline](https://img.shields.io/badge/offline-yes-52b06a?style=flat-square)

---

## What is this?

An interactive family tree builder that lives entirely inside **one HTML file**. No server. No account. No install. Double-click it in any browser and start building your family diagram.

When you're done, hit **Save** — it downloads an updated copy of the same file with your data baked in. Share it with anyone. They double-click it, your tree opens exactly as you left it.

---

## How it was built

100% vibe-coded. Every feature, every bug fix, every algorithm was written by Claude (Anthropic) through iterative conversation. The only thing I did was describe what I wanted, test it, describe what was wrong, and repeat — across many sessions.

This is what vibe coding actually looks like in practice: not one perfect prompt, but dozens of rounds of *"this works but the lines are crossing"*, *"nodes freeze after saving"*, *"the layout is clipping at the bottom"* — and watching it get fixed, one conversation at a time.

The full documentation set (PRD, Tech Spec, UI/UX Spec, Data Dictionary) was also reverse-engineered by Claude from the finished app — because by the end, Claude understood it better than I did.

---

## Features

- **Add people** — name, gender, birth year, freeform note
- **Connect them** — parent→child, spouse, or sibling relationships
- **Drag freely** — move any node anywhere on the canvas
- **Auto-layout** — one button arranges everyone into a clean generational hierarchy, no line crossings
- **Zoom & pan** — scroll wheel, pinch-to-zoom, fit-all button
- **Capture PNG** — exports a clean 4× resolution image with title overlay
- **Save & reload** — downloads the HTML file with your data embedded; fully editable when reopened
- **Works on mobile** — touch drag, pinch zoom, long-press to edit
- **Beautiful** — dark heritage aesthetic, gold accents, serif typography

---

## Usage

```
1. Download family-tree.html
2. Double-click to open in any browser
3. Click "+ Add" to add your first person
4. Hover a node → click the port dot at the bottom → tap another node → choose relationship
5. Click "⟳" to auto-arrange
6. Click "💾 Save" to save your progress as a new HTML file
```

That's it. No tutorial needed.

---

## File structure

```
family-tree/
├── family-tree.html          # The entire app — open this
├── 01-PRD.docx               # Product Requirements Document
├── 02-TechSpec.docx          # Technical Specification
├── 03-UIUXSpec.docx          # UI/UX Specification
├── 04-DataDictionary.docx    # Data Dictionary (all functions, fields, constants)
└── README.md                 # This file
```

The four `.docx` files are the full design documentation — accurate enough that you could hand them to a developer and they could rebuild this app from scratch without seeing the source.

---

## Tech

| What | How |
|------|-----|
| Language | Vanilla JavaScript + HTML + CSS |
| Dependencies (runtime) | Zero |
| External CDN | [html2canvas 1.4.1](https://html2canvas.hertzen.com/) — loaded async, only for PNG capture |
| Fonts | Cormorant Garamond + Jost via Google Fonts |
| Data storage | Embedded JSON inside the HTML file itself |
| Build system | None |
| Framework | None |

---

## Layout algorithm (the interesting bit)

The auto-arrange uses a custom hierarchical layout:

1. **Generation assignment** via bidirectional relaxation — children go below parents, parents get pulled up if they're too far below their children, spouses share the same generation
2. **Unit grouping** — couples always move as rigid pairs (male left, female right)
3. **Cross-free ordering** — child units are sorted by their parents' X positions so lines from different parent couples never cross
4. **Inverted pyramid** — ancestors fan outward naturally, youngest generation is the anchor
5. **Dynamic vertical gaps** — tighter spacing on deeper trees (120px shrinking to 80px)
6. **4-pass refinement** — alternating top-down and bottom-up overlap resolution

---

## Known limitations

- Undo/redo not implemented
- No GEDCOM import/export
- Gender is binary (male/female only)
- Practical node limit ~300 before layout slows
- PNG capture requires html2canvas CDN (needs internet on first capture)

---

## License

MIT — do whatever you want with it.

---

*Built with Claude by Anthropic. Proof that you don't need to write code to build software anymore — you just need to know what you want and be willing to iterate.*
