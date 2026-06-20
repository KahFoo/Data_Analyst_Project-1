# CLAUDE.md

Guidance for AI assistants (Claude Code and others) working in this repository.

## What this repository is

This is a **data-analytics portfolio project**, not a software codebase. There is
no application source code, build system, package manager, or test suite. The
repository documents and ships a single Microsoft Excel dashboard analyzing the
**Impact of Economic and Policy Factors on HDB Resale Prices in Singapore
(2017–2022)**.

The analysis correlates Singapore HDB (public housing) resale prices against
macroeconomic and policy indicators — GDP, unemployment, interest rates,
inflation (CPI) — across major events such as the China–US trade war, the
COVID-19 pandemic, and the Russia–Ukraine war.

## Repository contents

| File | Role |
|------|------|
| `README.md` | Project narrative: data sources, methodology, dashboard findings, and future improvements. The primary human-facing document. |
| `Impact of Economic and Policy Factors on HDB Resale Prices in Singapore (2017-2022) DashBoard.xlsx` | The deliverable — a ~9.6 MB Excel workbook containing the data, transformations, pivot tables, charts, slicers, and the final dashboard. |

That is the entire repository. Do not assume hidden source directories, configs,
or scripts exist.

## Inside the Excel workbook

The workbook has **16 sheets**, split into a presentation layer, an analysis
layer, and a raw-data layer:

**Dashboard / presentation**
- `DashBoard` — the final interactive dashboard (14 charts, 3 slicers).

**Analysis sheets (pivot-table backed, ~9 pivot tables total)**
- `1. Average Transaction`
- `2. GDP (Quarter)`
- `3. Unemploment Rate (Quarter)` *(spelling preserved from source)*
- `4. Interest Rate (Quarter)`
- `5. Inflation Rate (Quarter)`
- `6. Number of Transactions`
- `7. Timeline`

**Raw / cleaned source data**
- `Refined Resale Flat Price List` — cleaned HDB resale transactions.
- `GDP (Quarter)`
- `Unemployed Rate (Quarter)`
- `Domestic Interest Rates`
- `CPI (Quater)` *(spelling preserved from source)*
- `Year & Quarter Column` — helper dimension for quarterly aggregation.
- `Timeline Events` — annotated economic/policy events.
- `Check Data Quality` — validation/QA worksheet.

When referencing sheets in commits, messages, or documentation, **preserve the
existing sheet names exactly**, including the original misspellings
(`Unemploment`, `CPI (Quater)`), so links and references stay consistent.

## Data sources

Sourced from official Singapore government portals (full links in `README.md`):
1. Resale Flat Prices by Registration Date (Jan 2017 onwards) — data.gov.sg
2. GDP in Chained (2015) Dollars, by Industry (SSIC 2020) — SingStat
3. Unemployment Rate (End of Period) — SingStat
4. Consumer Price Index (CPI), 2019 base year, monthly — SingStat
5. MAS Domestic Interest Rate data — Monetary Authority of Singapore

## Working conventions

- **Excel is the source of truth for analysis.** The `.xlsx` is a binary
  artifact. You cannot meaningfully diff, line-edit, or merge it with text
  tools. Edits to the analysis itself are made in Excel and committed as a whole
  new version of the file.
- **Inspecting the workbook without Excel:** treat it as a zip archive. For
  example, `unzip -l "<file>.xlsx"` lists parts; sheet names live in
  `xl/workbook.xml`; cell text in `xl/sharedStrings.xml`; charts under
  `xl/charts/`; pivot tables under `xl/pivotTables/`. Use read-only inspection;
  do not hand-edit the internal XML.
- **Most realistic task here is documentation.** Updating `README.md` (findings,
  data sources, methodology, links) is plain Markdown and the common change.
- **Keep README and this file in sync** with the workbook. If the workbook gains
  or loses sheets, charts, or data sources, update the tables above and the
  README accordingly.
- **Mind the large binary.** The workbook is ~9.6 MB. Avoid committing
  unnecessary duplicate copies; replace in place when updating.

## Git workflow

- Active development branch for this work: `claude/claude-md-docs-p7s1u8`.
- The default branch is `main`.
- Commit history is simple and linear (README updates and file uploads). Keep
  commit messages short and descriptive, e.g. `Update README findings for 2022`.
- Push with `git push -u origin <branch-name>`.
- **Do not open a pull request unless the user explicitly asks for one.**

## What NOT to do

- Do not scaffold build tooling, CI, linters, or test frameworks — there is no
  code to build or test.
- Do not convert or "normalize" the `.xlsx` into CSV/Parquet/etc. unless asked;
  the workbook's pivot tables, slicers, and charts are the deliverable.
- Do not silently fix the historical sheet-name typos; they are load-bearing for
  existing references.
- Do not fabricate analysis numbers — cite figures only from the workbook or
  `README.md`.
