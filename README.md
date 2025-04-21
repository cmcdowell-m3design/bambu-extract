# 📄 Product Requirements Document (PRD)

## Product Name  
**3MF Print Summary Extractor**

## Version  
**1.0.2**

---

## 🧭 Overview  
The 3MF Print Summary Extractor is a lightweight, browser-based tool for extracting print job metadata from `.3mf` files. It enables users to organize, review, and export structured summaries for use in billing, logging, or collaboration around 3D printing workflows.

---

## 🎯 Core Features

### 🔼 File Upload
- Drag-and-drop or file picker to upload `.3mf` files.
- Only `.3mf` files with a valid `slice_info.config` are processed.
- Invalid or corrupted files are skipped with warnings logged to the browser console.

### 📊 Table Display
Each processed file is summarized in a table with the following columns:
- **File Name**
- **Billing Code** (parsed from filename prefix)
- **Date** (from embedded file metadata)
- **Printer** (model ID)
- **Estimated Time (minutes)**
- **Filament 1–4**: Type + Weight (g)

### 🧾 Billing Code Segregation
Entries with billing code `M308` are visually and structurally separated:
- Primary section: all other entries
- Secondary section: entries labeled with `"Jobs with billing code: M308"`

### 📤 Export Options
Users can download the extracted data in two formats:
- **CSV (.csv)** — plain text export
- **Excel (.xlsx)** — formatted columns using SheetJS

Each export:
- Includes all column headers
- Preserves data grouping (including optional blank line and section label)
- Is triggered client-side (no server involvement)

---

## 🛠 Technical Details

- **Billing Code Extraction:** First segment of the filename split by `_` or `-`, uppercased.
- **Validation:** Billing codes are only accepted if they are 4–6 characters long; otherwise marked as `none`.
- **Centralized Logic:** Data preparation is done via `prepareGroupedData()` and `prepareExportData()` to keep exports and table rendering consistent (DRY).
- **Libraries Used:**
  - [`JSZip`](https://stuk.github.io/jszip/) for unpacking `.3mf` files
  - [`SheetJS`](https://sheetjs.com/) (`xlsx.mini`) for `.xlsx` generation

---
