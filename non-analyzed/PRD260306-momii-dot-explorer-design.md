# Momii Dot Explorer — Design

**Date:** 2026-03-06  
**Owner:** Codex (agent)  
**Output:** 1 file HTML interactive explorer

## Goal

Build a single lightweight HTML file that:
- Accepts user-provided information (files, images, pasted text)
- Automatically fragments (chunks) content into many “dots” (nodes)
- Infers basic relationships between dots when possible
- Lets the user click any dot to view details

## Constraints / Decisions

- **Lightweight HTML**: no embedded MOMII assets (PNG/PDF). User selects folder/files at runtime.
- **CDN allowed** to improve graph interaction and PDF rendering.
- **No fixed local path access**: browser security prevents reading `/Users/...` paths without user interaction; therefore the tool starts empty and the user selects `MOMII/` first.
- **Refresh behavior**: “Refresh” rebuilds the graph from the current in-memory selection. If files change on disk, the user re-selects the folder/files.

## Inputs

1) Folder selection via `<input type="file" webkitdirectory multiple>` (recommended for `MOMII/`)  
2) File selection via `<input type="file" multiple>`  
3) Drag & drop files into the drop zone  
4) Paste text into a modal (stored as a virtual File)

## Processing & Chunking

### Supported file types
- Text: `md`, `txt`, `json`, `html`, `csv`
- Media: `png`, `jpg`, `jpeg`, `gif`, `webp`, `svg`
- Documents: `pdf`

### Chunking strategy (maximize dots while staying usable)
- **Markdown (`.md`)**:
  - Split by headings into sections
  - Split section bodies into blocks (blank-line separated)
  - Further split long blocks into sentence-ish chunks using punctuation
  - Treat list items and table rows as separate chunks where detected
- **CSV (`.csv`)**:
  - Parse into rows (each row becomes one dot)
  - Store key-value representation for details display
- **HTML (`.html/.htm`)**:
  - Extract `document.body.textContent`
  - Chunk as text blocks and sentences
- **PDF (`.pdf`)**:
  - Create a PDF node plus per-page nodes (capped)
  - Render preview with pdf.js on click (no full-text extraction in v1)
- **Images**:
  - One node per image with preview via object URL

## Relationships (Edges)

Core edges:
- `contains`: file → section/chunk/row/pdf/image/pdf_page

Semantic edges:
- `mentions`: chunk/row → entity (keyword)

Entities are derived by:
- tokenizing chunk/row text (fold diacritics, stopwords removal)
- keeping recurring tokens (freq ≥ 2) up to a cap
- linking each chunk/row to top-N entities found in it

“Related” content is computed on-demand (shared entities), not by drawing every cross-link in the graph (to avoid clutter).

## UI

Layout: 3 panels
- Left: inputs, quick instructions, search, type filter chips
- Middle: graph (Cytoscape.js)
- Right: details panel (text preview / image preview / PDF page preview + pager)

Controls:
- Load folder / Add files / Paste text
- Refresh (rebuild from selection)
- Re-layout
- Clear

## Libraries (CDN)

- Cytoscape.js: graph rendering & layout
- PapaParse: CSV parsing
- pdf.js: PDF rendering to canvas

## Limits / Safety

- Node caps and page/row caps to prevent runaway graphs
- Details rendering uses textContent to avoid XSS

## Deliverable

- `artifacts/DATA260306-momii-dot-explorer.html`

