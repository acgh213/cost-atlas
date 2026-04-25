# Cost Atlas

**A token usage dashboard** — an interactive Chart.js-powered dashboard for visualizing LLM token consumption and API costs across sessions, models, and time periods. Features a dark academic theme with real-time data exploration.

## Features

- **Interactive Charts** — Bar, line, and pie charts powered by Chart.js
- **Token Usage Breakdown** — Visualize input vs. output token consumption
- **Cost Tracking** — Per-model and per-session cost analysis
- **Time-Range Filtering** — Aggregate by day, week, month, or custom ranges
- **Model Comparison** — Compare usage and costs across different LLM models
- **Dark Academic Theme** — Warm serif typography with muted amber and violet accents
- **Responsive Layout** — Adapts to any screen size
- **Static Deployment** — Fully client-side, no server required

## Screenshots

<!-- TODO: Add screenshots of the dashboard -->

| Overview Dashboard | Token Breakdown | Model Comparison |
|--------------------|-----------------|------------------|
| ![Screenshot](https://via.placeholder.com/400x250?text=Cost+Atlas+Overview) | ![Screenshot](https://via.placeholder.com/400x250?text=Token+Breakdown) | ![Screenshot](https://via.placeholder.com/400x250?text=Model+Comparison) |

## Tech Stack

- **Frontend:** HTML5, CSS3, Vanilla JavaScript
- **Charts:** Chart.js v4 (loaded from CDN)
- **Typography:** Georgia, Times New Roman, serif
- **Build:** None — served directly as a single HTML file

## Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/acgh213/cost-atlas.git ~/cost-atlas
   cd ~/cost-atlas
   ```

2. No dependencies to install. Chart.js is loaded from CDN. The dashboard is a single HTML file.

## Run

**Serve with any static file server:**

Using Python:
```bash
cd ~/cost-atlas
python3 -m http.server 8902
```

Using Node.js (npx):
```bash
cd ~/cost-atlas
npx serve .
```

Open your browser to the local server address.

## GitHub

[https://github.com/acgh213/cost-atlas](https://github.com/acgh213/cost-atlas)

## License

MIT
