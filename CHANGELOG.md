# Changelog

All notable changes to this project are documented here.

---

## [2.0.0] — March 2026

### Fixed
- **Save & reload** — reopening a saved file now correctly re-attaches all event listeners (drag, edit, delete, connect). Root cause: `outerHTML` was baking live DOM nodes into the saved file; fix empties `#nc` before capture so nodes are always rebuilt fresh on load.
- **Line crossings** — auto-layout now sorts child-row units by their parents' X position, eliminating crossings when two parent couples have children in the opposite left-right order.
- **fitView clipping** — removed an erroneous +54px offset from `vy`; the canvas element already starts at y=54 so the offset was double-counted, clipping bottom nodes.
- **Nodes snapping to wrong generation** — added upward relaxation pass so in-law nodes are pulled to the correct generation rather than staying at generation 0.

### Improved
- **Node name font** — now scales continuously with zoom (16×vs, clamped 7–16px) instead of switching at a hard threshold. No more sudden jumps.
- **Dynamic vertical gaps** — generation gap shrinks by 6px per generation beyond 3 (min 80px) so deeper trees stay compact.
- **Progressive content** — birth year and note hide gracefully below vs=0.55 rather than overflowing the node.

---

## [1.0.0] — March 2026

### Initial release
- Single-file HTML application — no server, no install
- Add / edit / delete person nodes (name, gender, birth year, note)
- Three relationship types: parent→child, spouse, sibling
- Free drag on canvas (mouse + touch)
- Auto-layout with hierarchical generation assignment
- Zoom (scroll, pinch, buttons), pan, fit-view
- PNG capture at 4× resolution via html2canvas
- Save embeds data into HTML file for portable sharing
- Inline title editing
- Dark heritage visual theme
- Mobile-responsive (touch drag, long-press to edit, pinch zoom)
