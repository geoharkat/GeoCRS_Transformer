<div align="center">

# 🌐 GeoCRS Transformer

**Reproject coordinates between 326 EPSG systems — instantly, in your browser.**

[![Live Demo](https://img.shields.io/badge/Live%20Demo-geoharkat.github.io-00d4aa?style=for-the-badge&logo=github)](https://geoharkat.github.io/GeoCRS_Transformer/)
[![License: MIT](https://img.shields.io/badge/License-MIT-white?style=for-the-badge)](LICENSE)
[![100% Client-Side](https://img.shields.io/badge/100%25-Client--Side-00d4aa?style=for-the-badge&logo=javascript)]()

</div>

---

## ✨ Features

- **326 EPSG coordinate systems** — geographic and projected, covering every region of the world
- **Manual mode** — transform a single coordinate pair interactively
- **Batch mode** — upload a CSV or Excel file and transform thousands of rows at once
- **Angular format support** — Decimal Degrees (DD), Degrees Minutes Seconds (DMS), Degrees Decimal Minutes (DMD), and Gradians
- **Unit conversions** — meters, feet, US survey feet, kilometers, miles
- **Per-row CRS** — in batch mode, each row can have its own input EPSG code from a dedicated column
- **EPSG.io fallback** — if a CRS is not in the local database, the tool fetches its proj4 definition from [epsg.io](https://epsg.io) automatically
- **Zero server required** — everything runs in the browser; no data is ever sent anywhere
- **Works offline** — once loaded, the page and its CRS database function without a network connection

---

## 🚀 Quick Start

Open the live app directly — no installation needed:

**[https://geoharkat.github.io/GeoCRS_Transformer/](https://geoharkat.github.io/GeoCRS_Transformer/)**

---

## 🗂️ Repository Structure

```
GeoCRS_Transformer/
├── geocrs_transformer.html   # Single-file application
├── crs_database.js           # 326 EPSG definitions (proj4 strings, wrapped as JS)
└── README.md
```

> The entire UI, logic, and styling lives in `geocrs_transformer.html`.  
> `crs_database.js` is loaded via a `<script>` tag so the tool works from `file://` without a local server.

---

## 🖥️ Manual Mode

Transform one coordinate at a time.

1. Select a **region → country → EPSG system** for the input CRS
2. Enter **X / Longitude / Easting** and **Y / Latitude / Northing**
3. Choose the **input angular format** (DD, DMS, DMD, Grad, or Auto-Detect)
4. Select the **output CRS** and desired **output format / units**
5. Click **Transform Coordinate**

Use the **⇄ swap button** to instantly reverse the input and output systems.

### Accepted input formats

| Format | Example |
|--------|---------|
| Decimal Degrees | `30.54` |
| Degrees Minutes Seconds | `30° 32' 24"` or `30 32 24` |
| Degrees Decimal Minutes | `30° 32.4'` |
| Gradians | `33.933` |
| With hemisphere letter | `30.54N`, `6.35E` |

---

## 📂 Batch Mode

Transform an entire dataset in one step.

1. **Drop or select** a CSV or Excel (.xlsx / .xls) file
2. Map the **X column**, **Y column**, and either:
   - Set a **global input CRS** (all rows use the same system), or
   - Point to an **EPSG column** to use a different input CRS per row
3. Choose the **output CRS** and output format
4. Click **Transform & Prepare Download**
5. Download the result as a CSV with `Out_X` and `Out_Y` columns appended

### Example input CSV

```csv
X,Y,EPSG
648235.9,6862268,2154
530268.1,179643.9,27700
475762.7,4202404,2100
```

---

## 🔧 Running Locally

Because the CRS database is loaded via a `<script>` tag (not `fetch`), the tool works directly from the filesystem:

```bash
# Clone the repo
git clone https://github.com/geoharkat/GeoCRS_Transformer.git
cd GeoCRS_Transformer

# Open directly in your browser — no server needed
open geocrs_transformer.html      # macOS
xdg-open geocrs_transformer.html  # Linux
start geocrs_transformer.html     # Windows
```

Alternatively, serve it with any static server:

```bash
python3 -m http.server 8000
# then open http://localhost:8000/geocrs_transformer.html
```

---

## 🧰 Tech Stack

| Library | Version | Purpose |
|---------|---------|---------|
| [proj4js](https://proj4js.org/) | 2.9.2 | Coordinate reprojection engine |
| [PapaParse](https://www.papaparse.com/) | 5.4.1 | CSV parsing |
| [SheetJS (xlsx)](https://sheetjs.com/) | 0.18.5 | Excel file parsing |
| [Tailwind CSS](https://tailwindcss.com/) | CDN | Utility-first styling |
| [Font Awesome](https://fontawesome.com/) | 6.5.1 | Icons |
| [Space Grotesk](https://fonts.google.com/specimen/Space+Grotesk) | — | Typography |

No build step. No framework. No backend.

---

## 🌍 EPSG Database

The bundled `crs_database.js` contains **326 EPSG coordinate systems** covering:

- Geographic CRS (latitude/longitude in DD, DMS, DMD, or Grad)
- Projected CRS (UTM zones, national grids, Lambert, Mercator, etc.)
- All major regions: Africa, Europe, Americas, Asia-Pacific, Middle East, and more

For any EPSG code not included, the tool automatically falls back to fetching the definition from [epsg.io](https://epsg.io).

---

## 📝 Known Limitations

- **Vertical datums** are not handled — only horizontal (2D) reprojection is supported.
- **Grid-shift transformations** (NTv2, NADCON, etc.) are not available in the browser build of proj4js; datum shifts use 7-parameter Helmert transformations only.
- The EPSG.io fallback requires an internet connection.

---

## 🤝 Contributing

Issues and pull requests are welcome. If a CRS is missing from the database or a transformation gives unexpected results, please open an issue with:

- The input EPSG code and coordinate
- The output EPSG code
- The expected vs. actual result

---

## 👤 Author

**Ismail Harkat**  
📧 [geoharkat@gmail.com](mailto:geoharkat@gmail.com)  
🌐 [geoharkat.github.io/GeoCRS_Transformer](https://geoharkat.github.io/GeoCRS_Transformer/)

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.
