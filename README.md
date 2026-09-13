# InsightX Finance

A working fintech analytics prototype for small and medium-sized businesses. InsightX connects financial statements, KPI monitoring, cash-flow planning, receivables, payables and decision support in one browser workspace.

## Included

- **54 financial KPIs** across profitability, costs, liquidity, working capital, balance sheet, debt coverage, efficiency and budget performance. Each opens a definition, formula, monthly chart and exportable history.
- **11 workspace sections:** overview, financial statements, cash flow, receivables, payables, budgets and forecasts, KPI library, insights and actions, finance assistant, reports, and data imports.
- Monthly and year-to-date reporting, income statements, balance sheets and direct-method cash-flow statements.
- Customer invoices and supplier bills, aging, search, status filters, partial/full receipt and payment recording, and simplified new invoice/bill entries.
- Editable monthly budgets and a deterministic three-month cash forecast with revenue, cost and collection-time assumptions.
- Rule-based financial insights and an editable action plan.
- A local financial query assistant that answers supported questions from the loaded data.
- CSV templates, validated imports, report exports, browser print/save-PDF, report snapshots and JSON workspace backup/restore.
- Responsive layouts, semantic controls, keyboard navigation, dialog focus handling and optional WebMCP actions.

## Run locally

Use **Node.js 24 or newer**:

```sh
npm start
```

Open `http://127.0.0.1:4173`. Runtime dependencies are not required. If that port is in use, set `PORT` to another value.

The app is plain HTML, CSS and browser JavaScript. Serve the `dist/` directory through any static HTTP host. Opening `index.html` directly as a local file is not supported because it uses JavaScript modules. Navigation uses hash routes, so a server-side route rewrite is not required.

## Checks

```sh
npm install
npm run check
npm test
```

The test suite covers all 11 views and 54 KPI dialogs, statement/cash reconciliation, ratio edge cases, receipt/payment and accrual posting, invalid input rejection, budgets, scenarios, exports, CSV imports, backup restoration, assistant answers and structured action contracts. It uses a simulated DOM. The three WebMCP actions were also checked with valid and invalid inputs in a live browser during the original build. This is not a claim of exhaustive cross-browser or visual testing.

## Data model

The initial company, **Namaa Trading**, and all figures are fictional. The dataset covers October 2025 through September 2026, with the sample ledger dated September 30, 2026.

Monthly records provide accrual income and costs, actual cash movements, closing balance-sheet values, budgets and basic employee/customer counts. Imported months must be consecutive, cash must roll forward, and assets must equal liabilities plus equity. A detailed invoice ledger must match the latest closing receivable and payable balances. Importing monthly figures clears the previous ledger; aging stays unavailable until a matching ledger is loaded.

Receipt/payment entries change cash and the corresponding outstanding balance without recognizing profit again. New customer invoices recognize revenue and receivables; new supplier bills recognize operating expenses and payables. These simplified entries exclude VAT and do not move money. Use the monthly import for more complex accounting entries.

KPI definitions describe the model's assumptions, including proxies for credit sales/purchases, closing-balance return ratios and non-annualized values. Undefined or non-meaningful ratios display `N/A`.

## Prototype boundaries

- Changes live **only in the current page session**. Download a workspace backup before closing or reloading. No server database or cross-device synchronization is included.
- Imports and assistant calculations run locally. No live bank, payment, accounting-system or language-model integration is connected.
- The chat is a supported-query data assistant, not a generative AI model. It acknowledges unsupported questions and unavailable causes.
- Forecasts are explicit assumption-based scenarios, not trained predictions. They model month-end balances, not daily liquidity or uncertainty intervals.
- Changing reporting currency changes the label only; it does not convert amounts.
- Reports are unaudited. This prototype does not implement a full general ledger, VAT filing, payroll, consolidated accounting or compliance certification.
- Google Fonts is used for typography; browser fallback fonts are available.

## Project structure

```text
dist/index.html       Application shell
dist/style.css        Theme, layouts, responsive and print styles
dist/app.js           Views, controls, imports, assistant and structured actions
dist/finance.js       Sample data, calculations, validation and ledger postings
scripts/serve.mjs     Dependency-free local HTTP server
tests/check.mjs       Financial and interaction regression checks
.openai/hosting.json  Sites hosting configuration for the original workspace
```

The original Sites publication timed out waiting for its TLS certificate. The source and local app are complete; no successful hosted deployment is claimed.
