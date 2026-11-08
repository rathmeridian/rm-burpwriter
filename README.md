# Burp Report Builder

A single-page, fully client-side web app that turns a **Burp Suite issue export (XML)** into a client-ready penetration-test report. It de-duplicates findings into categories, enriches them with MITRE ATT&CK mappings, reproduction steps and remediation guidance, lets you triage and edit everything, and exports a branded **Word** report and an **Excel** findings register.

Everything runs in the browser. No data is uploaded anywhere — the Burp file you load never leaves your device.

## Features

- **Categorized findings** — e.g. 10 reflected-XSS hits become one finding with 10 evidence instances, not ten duplicates.
- **MITRE ATT&CK mapping** — each category is mapped to relevant ATT&CK techniques and tactics, with a short rationale.
- **Per-finding detail** — description, step-by-step reproduction, and remediation advice, each fully editable.
- **Editable severity** — defaults to Burp's rating (highest across instances); change it per finding.
- **Triage** — accept findings, mark false positives (per finding or per instance), remove/restore findings.
- **CWE + references** — carried through from Burp's own data.
- **Branded Word export** — cover with your logo, placeholder Executive Summary / Scope / Rules of Engagement sections, a findings summary table, and per-finding detail with affected-location tables.
- **Excel export** — Findings register, Instances sheet, and a Summary sheet.
- **Project save/load** — export the whole working state as JSON and reload it later.
- **Opens fresh** each time, with an optional "Resume" of your last session and a "New file" reset.

## Usage

1. Open `index.html` in a modern browser (Chrome, Firefox, Edge). No server or install required.
2. Drag in (or browse to) a Burp Suite XML export — produced in Burp via **Report issues → XML**.
3. Review and edit the categorized findings; set severities; mark false positives; remove anything not relevant.
4. Open **Report details** to set the report title, client, author, date, logo, and the Executive Summary / Scope / Rules of Engagement text.
5. Export the **Word report** and **Excel** findings register.

> Opening the file directly (`file://`) works fully offline. When served from a web server (see below), the Word/Excel downloads save without an extra confirmation prompt.

## Hosting (optional)

Because the app is static, you can host it anywhere that serves files, including **GitHub Pages**:

1. Push this directory to a GitHub repository.
2. In the repo, go to **Settings → Pages**, choose **Deploy from a branch**, and select your branch with the `/ (root)` folder.
3. The app will be live at `https://<your-username>.github.io/<repo>/`.

Keep the `lib/` folder next to `index.html` — the page loads the libraries from there by relative path.

## Project layout

```
.
├── index.html            # the entire application (HTML + CSS + JS)
├── lib/
│   ├── docx.umd.js        # Word (.docx) generation
│   └── xlsx.mini.min.js   # Excel (.xlsx) generation
├── README.md
├── LICENSE
└── .gitignore
```

## Third-party libraries

The following libraries are bundled in `lib/` and loaded locally (with a CDN fallback) so the app works offline:

| Library | Purpose | License |
| --- | --- | --- |
| [docx](https://github.com/dolanmiu/docx) (v8.5.0) | Word document generation | MIT |
| [SheetJS / xlsx](https://github.com/SheetJS/sheetjs) (v0.18.5, mini build) | Spreadsheet generation | Apache-2.0 |

Their licenses permit redistribution. These components remain under their own licenses; only the Burp Report Builder code is licensed under the GPL (below).

## License

Copyright (C) 2026 Rath Meridian.

This program is free software: you can redistribute it and/or modify it under the terms of the **GNU General Public License, version 3**, as published by the Free Software Foundation. See the [LICENSE](LICENSE) file for the full text.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.

## Disclaimer

This tool assists with reporting authorized security assessments. Only test systems you are authorized to test.
