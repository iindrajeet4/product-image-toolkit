# Product Image Toolkit

[![License: MIT](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Demo](https://img.shields.io/badge/demo-live-brightgreen.svg)](https://iindrajeet4.github.io/product-image-toolkit/)
[![Dependencies](https://img.shields.io/badge/dependencies-none-blue.svg)](#)

A **100% client-side** batch tool for e-commerce product images — rename, resize, watermark, compress, and strip EXIF metadata, all in the browser. **No files are ever uploaded**; everything runs locally via the Canvas API in a single dependency-free `index.html`.

**[🔗 Live Demo / ลองใช้เลย](https://iindrajeet4.github.io/product-image-toolkit/)**

> Built from real workflow pain at a jewelry retailer processing hundreds of product shots per campaign. Inspired by the ideas behind [Squoosh](https://github.com/GoogleChromeLabs/squoosh) (Google, Apache-2.0) and [Caesium](https://github.com/Lymphatus/caesium-image-compressor) (GPL-3.0) — no code copied from either; this is an independent implementation focused on *batch e-commerce workflows*.

## ✨ Features

| Feature | Details |
|---|---|
| **Batch rename** | Template engine with tokens `{name} {seq} {date} {size} {w} {h} {sku}` — SKU extracted via configurable regex |
| **Multi-size export** | One source → many outputs (1000×1000, 600×600, thumbnails, custom) in a single pass |
| **Fit modes** | Cover (crop), Contain (pad with colour), Longest-side |
| **Before/after preview** | Click any thumbnail to compare the original with the processed output (size + file weight) |
| **Watermark** | Text or uploaded logo, 5 positions, adjustable opacity |
| **Compression** | JPG / WebP quality slider with before→after size **estimate** |
| **EXIF stripping** | Canvas re-encode removes all metadata (GPS, camera info) automatically |
| **Privacy** | Zero uploads, zero tracking, zero external dependencies — works fully offline |
| **Config portability** | Settings persist in localStorage; export/import as JSON to share across a team |
| **ZIP download** | All outputs packaged in one archive by a built-in zero-dependency ZIP writer; duplicate names auto-deduplicated |

## 🚀 Usage

No build step, no install, no network access required:

1. Open `index.html` in any modern browser (Chrome, Edge, Firefox, Safari), **or** serve it: `npx serve .`
2. Drag & drop JPG / PNG / WebP files (or click to browse).
3. Configure naming, sizes, format, watermark in the sidebar. Click a thumbnail to preview the result.
4. Click **Process & download ZIP**.

## 🏢 Team / corporate use

- Define your naming convention once, **Export config**, and commit the JSON to your team's repo — everyone imports the same rules.
- Host the single HTML file on any static host (GitHub Pages, S3, internal intranet) — no server logic, no CDN calls, no data leaves the user's machine, so it typically passes security review easily.

## 🔧 Naming template examples

| Template | Output |
|---|---|
| `{date}_{sku}_{seq}_{size}` | `210726_SB044_001_1000x1000.jpg` |
| `{sku}_{size}` | `SB044_600x600.webp` |
| `campaign_{seq}` | `campaign_001.jpg` |

## ⚠️ Limitations

- Lossy re-encode only for JPG/WebP (PNG is lossless but larger). No AVIF yet.
- Very large images (> ~50 MP) may be slow — processing is single-threaded on canvas.
- The built-in ZIP writer stores entries uncompressed (JPEG/WebP/PNG data is already compressed, so this costs almost nothing) and does not support archives over 4 GB (ZIP64).
- If the browser cannot encode the chosen format (e.g. WebP on older Safari), the tool automatically falls back to PNG and tells you.

## 📄 License

MIT — see [LICENSE](LICENSE).

## 🙏 Credits

- Concept inspiration: Squoosh (Google Chrome Labs), Caesium Image Compressor
