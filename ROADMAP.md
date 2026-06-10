# Customer Shopping Behavior Analytics — Project Roadmap

**Goal:** A portfolio-grade analytics project (Excel → SQL → Python → Tableau) that replaces Questor on the data-analyst version of the resume. Learn each tool by using it on real, messy data.

**Dataset:** UCI Online Retail II — `data/raw/online_retail_II.xlsx`
- Sheet "Year 2009-2010": 525,461 transactions
- Sheet "Year 2010-2011": 541,910 transactions
- Columns: Invoice, StockCode, Description, Quantity, InvoiceDate, Price, Customer ID, Country
- Real UK online retailer. Known quirks (finding these yourself is Phase 1): cancelled invoices start with "C", negative quantities, ~25% missing Customer IDs, zero-price rows, non-product StockCodes (POST, D, M, BANK CHARGES).

**Business framing (memorize this for interviews):** "An online retailer wants to understand who its customers are, what drives revenue, and which customers are worth retaining. I analyzed 1M+ transactions to segment customers, surface sales trends, and quantify repeat-purchase behavior."

---

## Phase 0 — Setup (Day 1)
- [ ] Create a GitHub repo named `online-retail-customer-analytics` (public)
- [ ] Clone it / git init this folder, add a .gitignore for `data/raw/` (file is 43MB — don't commit it; link to UCI instead)
- [ ] First commit: ROADMAP.md + folder structure

## Phase 1 — Excel: Explore & Clean (Week 1)
*Skills learned: Excel Tables, calculated columns, COUNTBLANK/COUNTIF, filtering, pivot tables, pivot charts, slicers*

- [ ] Save a working copy: `excel/retail_analysis.xlsx` (use the 2010-2011 sheet)
- [ ] Format data as an Excel Table (Ctrl+T) and explore each column
- [ ] **Data profiling — answer with formulas, write answers in a "Data Quality Log" sheet:**
  - How many rows have a blank Customer ID? (`COUNTBLANK`)
  - How many invoices start with "C"? (`COUNTIF` with wildcard) — what are they?
  - How many rows have Quantity < 0 or Price = 0? (`COUNTIFS`)
  - What StockCodes are not real products? (filter + eyeball)
- [ ] **Define cleaning rules** (we'll agree on them together) and create a "Clean" sheet
- [ ] Add calculated column: `Revenue = Quantity * Price`
- [ ] **Pivot table analyses:** monthly revenue trend · top 10 products by revenue · revenue by country · orders per customer · average order value
- [ ] **Mini dashboard sheet:** pivot charts + slicers (month, country)

## Phase 2 — SQL: Business Questions at Scale (Week 2)
*Skills learned: PostgreSQL setup, COPY/import, GROUP BY, CTEs, window functions (NTILE, LAG, ROW_NUMBER), date functions*

- [ ] Install PostgreSQL + load BOTH sheets (full 1.07M rows) into one table
- [ ] Numbered query files in `sql/`, one business question each:
  1. Monthly revenue trend + year-over-year growth
  2. Average order value by month
  3. Top 10 products by revenue and by quantity
  4. Revenue by country (excl. UK vs incl.)
  5. Repeat purchase rate: % of customers with 2+ orders
  6. **RFM segmentation** (Recency, Frequency, Monetary — NTILE(4) scores → segments like "Champions", "At Risk")
  7. Cohort retention: % of each signup-month cohort still buying N months later
- [ ] Save query outputs as CSVs in `sql/results/` for the README

## Phase 3 — Python: Reproducible Analysis (Week 3)
*Skills learned: pandas (read_excel, groupby, merge, pivot_table), matplotlib, Jupyter*

- [ ] `python/analysis.ipynb`: load → clean (same rules as Excel) → EDA
- [ ] Recreate RFM in pandas; visualize segments (bar chart of count + revenue per segment)
- [ ] Cohort retention heatmap (the classic triangle chart — interviewers love it)
- [ ] 3–5 polished charts saved to `images/`

## Phase 4 — Tableau Public: Live Dashboard (Week 4)
*Skills learned: Tableau data import, calculated fields, dashboard actions, publishing*

- [ ] Build a KPI dashboard: revenue trend, top products, country map, customer segments, AOV cards
- [ ] Publish to **Tableau Public** → this is your free LIVE LINK for the resume
- [ ] Screenshot the dashboard for the README

## Phase 5 — Documentation & Resume Swap (Days, not weeks)
- [ ] README.md: business problem → data → cleaning decisions (with counts!) → key insights (quantified) → dashboard link + screenshots → tools used
- [ ] Write 3 resume bullets (Accomplished X, measured by Y, by doing Z)
- [ ] Generate the data-analyst resume version: this project replaces Questor

---

## Rules of engagement
1. **You type everything yourself** — no copy-pasting generated formulas/queries without understanding them. Claude explains, you build.
2. Every phase ends with a **git commit + push** so the repo shows steady activity.
3. Every number you compute must answer a **business question** — "so what?" is the test.
