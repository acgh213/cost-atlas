# Vesper · Cost Atlas

**A token usage dashboard** — an interactive, single-page dashboard for visualizing LLM token consumption and API costs across sessions, models, sources, and time periods. Built with Chart.js and a dark academic theme, Cost Atlas gives you real-time insight into where your tokens go and how much you're spending.

> **Live instance:** Served as a static HTML page with embedded data, updated periodically from a SQL-backed ingestion pipeline.

---

## Features

### Cost Tracking
- **Total Spend Overview** — See aggregate spend across all models (currently **$2.39**) with per-model breakdown
- **Per-Session Cost Analysis** — Average cost per session and cost per million tokens
- **Daily Cost by Model** — Stacked bar chart showing daily spend attribution across models
- **Cost Sorting** — Interactive table columns sortable by any metric (cost, sessions, tokens)

### Session Analytics
- **Session Counts** — Track total sessions (currently **129**) across all sources and models
- **Source Breakdown** — Donut chart showing session distribution by source (Telegram, Cron, CLI, TUI)
- **Activity Heatmap** — Hourly / day-of-week grid showing usage patterns and token consumption density
- **Time-Range Filtering** — Daily aggregation with per-model cost breakdown

### Token & Model Insights
- **Input vs. Output Tokens** — Horizontal bar chart comparing input and output token consumption per model
- **Cache Read Tracking** — Monitor cache hit volumes per model
- **Model Comparison Table** — Sortable table with sessions, input/output tokens, cache reads, cost, cost/1M tokens, and average tokens per session
- **Multi-Model Support** — Tracks 10+ models including DeepSeek, MoonshotAI, Mimo, OpenAI, Gemini, and custom models

### Design
- **Dark Academic Theme** — Warm serif typography (Georgia/Times New Roman), muted amber, lavender, and rose accents on a deep charcoal background
- **Card-Based Layout** — Responsive dashboard with hover effects and clean visual hierarchy
- **Responsive** — Adapts from desktop to tablet to mobile with grid reflow
- **Zero Dependencies at Build Time** — Chart.js loaded from CDN; no bundler, transpiler, or server-side processing required

---

## Screenshots

| Overview Dashboard | Source Breakdown | Activity Heatmap |
|---|---|---|
| ![Overview](https://via.placeholder.com/400x250?text=Cost+Atlas+Overview) | ![Source Breakdown](https://via.placeholder.com/400x250?text=Source+Breakdown) | ![Heatmap](https://via.placeholder.com/400x250?text=Activity+Heatmap) |

| Daily Cost by Model | Token Usage by Model | Model Comparison Table |
|---|---|---|
| ![Daily Cost](https://via.placeholder.com/400x250?text=Daily+Cost) | ![Token Usage](https://via.placeholder.com/400x250?text=Token+Usage) | ![Model Table](https://via.placeholder.com/400x250?text=Model+Comparison) |

> **Note:** Screenshot placeholders above. Replace with actual screenshots by opening the dashboard and capturing the relevant sections.

---

## Architecture

```
cost-atlas/
├── index.html          ← Single-page dashboard (HTML + CSS + JS + embedded data)
├── README.md           ← This file
└── .git/               ← Git repository
```

### Data Flow

```
SQL Database → [ingestion script] → Embedded JSON arrays in index.html → Chart.js renders charts
```

Cost Atlas is a **fully static, client-side application**:

1. **Data Ingestion** — A periodic SQL query extracts token usage, session, and cost data from a database
2. **Embedding** — The query results are inlined as JavaScript arrays (`SUMMARY_DATA`, `DAILY_DATA`, `HOURLY_DATA`, `HEATMAP_DATA`) directly into `index.html`
3. **Rendering** — On page load, Chart.js (loaded from CDN) reads the embedded data and renders:
   - Overview stat cards (total spend, total tokens, total sessions, avg cost/session)
   - Stacked daily cost bar chart
   - Input vs. output token horizontal bar chart
   - Source breakdown donut chart
   - Model comparison table (client-side sortable)
   - Activity heatmap (hour × day-of-week)

No server, no database connection, no API calls at runtime — the dashboard is a self-contained HTML file that updates when regenerated.

### Key Metrics (Current Snapshot)

| Metric | Value |
|---|---|
| Total Spend | $2.3924 |
| Total Tokens | ~6.3M |
| Total Sessions | 129 |
| Models Tracked | 8 |
| Sources | Telegram, Cron, CLI, TUI |

---

## Tech Stack

| Layer | Technology |
|---|---|
| **Frontend** | HTML5, CSS3, Vanilla JavaScript (ES6+) |
| **Charts** | [Chart.js](https://www.chartjs.org/) v4 (CDN) |
| **Typography** | Georgia, Times New Roman, serif (system stack) |
| **Build** | None — single HTML file, no bundler required |
| **Data Source** | SQL (periodic extraction) → embedded JSON |
| **Deployment** | Any static file server (Python, Node.js, Nginx, etc.) |

---

## Setup

### Prerequisites

- A web browser (Chrome, Firefox, Safari, Edge — any modern browser)
- Python 3 **or** Node.js (for local serving — not required for the dashboard itself)

### Quick Start

1. **Clone the repository:**

   ```bash
   git clone https://github.com/acgh213/cost-atlas.git
   cd cost-atlas
   ```

2. **Serve with any static file server:**

   **Option A — Python:**
   ```bash
   python3 -m http.server 8890
   ```

   **Option B — Node.js:**
   ```bash
   npx serve . -p 8890
   ```

   **Option C — Any other HTTP server** (Nginx, Apache, Caddy, etc.)

3. **Open your browser:**

   Navigate to [http://localhost:8890](http://localhost:8890)

That's it. No dependencies to install, no build step, no configuration.

### Updating the Data

To refresh the dashboard with new data:

1. Run your SQL query to extract token usage data
2. Replace the `SUMMARY_DATA`, `DAILY_DATA`, `HOURLY_DATA`, and `HEATMAP_DATA` arrays in `index.html` with the new results
3. Serve the updated file

A dedicated ingestion script can automate this step — the repository can be extended with a Python script that queries your database and rewrites the embedded data.

---

## Customization

### Theme Colors

The dark academic theme uses a consistent palette defined in the CSS and JavaScript:

- **Background:** `#0a0a0f` (deep charcoal)
- **Text:** `#d4c8b8` (warm parchment)
- **Accent Gold:** `#d4a574` (amber)
- **Accent Lavender:** `#9b8ec4` (muted purple)
- **Accent Rose:** `#c48b8b` (dusty rose)

To customize, update the `COLORS` object in the `<script>` section of `index.html` and the corresponding CSS variables in the `<style>` section.

### Adding New Charts

The architecture makes it straightforward to add new visualizations — define a new chart-building function following the existing patterns (`buildDailyChart`, `buildTokenChart`, etc.) and call it in the `DOMContentLoaded` handler.

---

## Project Status

Active. The dashboard is used daily to track LLM spending across multiple models and sources. The data is updated periodically as new sessions accumulate.

---

## GitHub

[https://github.com/acgh213/cost-atlas](https://github.com/acgh213/cost-atlas)

---

## License

MIT
