# Pushpak — Antigravity in Gemini Enterprise Usage Simulator

Named after the **Pushpaka Vimana**—the celestial flying craft crafted by Vishwakarma for Kubera (treasurer of the gods) whose capacity dynamically scales to accommodate every passenger aboard—**Pushpak** is an interactive, zero-dependency browser simulator for modeling **Google Antigravity** token capacity, developer consumption, and budget utilization under **Gemini Enterprise**.

- **Live Simulator (GitHub Pages):** [https://mohan-the-octocat.github.io/pushpak/](https://mohan-the-octocat.github.io/pushpak/)
- **Simulator HTML:** [`antigravity_ge_usage_simulator.html`](./antigravity_ge_usage_simulator.html) (also served at [`index.html`](./index.html))
- **Product Requirements Document (PRD):** [`antigravity_ge_usage_simulator_prd.md`](./antigravity_ge_usage_simulator_prd.md) (also in [`docs/PRD.md`](./docs/PRD.md))

---

## Overview

When organizations procure **Gemini Enterprise Standard** (\$10/user/month AI credit allocation) or **Gemini Enterprise Plus** (\$15/user/month AI credit allocation), Antigravity IDE and CLI usage draws from a shared project-level token quota pool that refreshes weekly.

**Pushpak** helps Customer Engineers, Solution Architects, FinOps leads, and Enterprise IT Administrators answer four questions through a **4-step guided wizard** (with floating **Back** / **Next** navigation, automatic next-step nudges, and a header **Dark / Light Mode Toggle** defaulting to Dark Mode):

1. **1. Plan & Seats:** Given the **Gemini Enterprise Plan** (`Standard` or `Plus`), **Total Purchased Seats**, and **Active Antigravity Users** ($\le$ Total Purchased Seats), what are the **Total Weekly Team Capacity** and **Average Weekly Capacity per Active User**?
2. **2. Team Usage Habits:** How does splitting active Antigravity users across **Power Users (Heavy)**, **Regular Users (Moderate)**, and **Occasional Users (Light)** (default `30% / 40% / 30%`) with configurable **Estimated Weekly Usage per Person** (default `5M / 3M / 1M` tokens/user/week) drive **Total Estimated Team Usage / Week**?
3. **3. AI Model & Budget Settings:** How do the **AI Model Split (Complex Reasoning vs. Everyday Tasks)** (`Gemini Pro` vs. `Gemini Flash`, default `20% Pro / 80% Flash`), **Prompt vs. Response Ratio (Input vs. Output)** (default `80% Prompts / 20% Responses`), **Extra Monthly Budget (Optional)** (default `\$0`), model rates (\$/1M tokens), and **separate Gemini Pro & Gemini Flash Discount (%)** widgets affect the **Overall Average Cost per 1M Tokens** and weekly capacity?
4. **4. Weekly Forecast & Budget:** In a `75:25` vertical split, how does the **Running Weekly Total** of team usage (`Monday`–`Friday`) compare against the organization's **Weekly Capacity Limit**, and what **Recommendation & Budget Status** is triggered?

---

## Key Features

### Step 1 — Plan & Seats (`67:33` Vertical Split)
- **Left `2/3` Pane:**
  - **Gemini Enterprise Plan:** Radio selection between **Standard** (`\$10 / month · \$2.50 / week per seat`) and **Plus** (`\$15 / month · \$3.75 / week per seat`).
  - **Total Purchased Seats:** Total Gemini Enterprise licenses bought by the organization.
  - **Active Antigravity Users:** Number of team members actively using Antigravity (automatically capped at `Total Purchased Seats`).
- **Right `1/3` Pane (`Available Weekly Capacity`):**
  - Readonly capacity displays (`+6px` enlarged typography) for **Total Weekly Team Capacity** and **Average Weekly Capacity per Active User**, plus summary rows for **Active Users / Purchased Seats**, **Weekly Included Plan Credit**, and **Average Cost per 1M Tokens**.

### Step 2 — Team Usage Habits
- **Team Activity Breakdown (%):** Interactive sliders and numeric inputs for **Power Users (Heavy)**, **Regular Users (Moderate)**, and **Occasional Users (Light)** (defaults to `30-40-30`, auto-normalized to `100%`).
- **Estimated Weekly Usage per Person:** Configurable weekly token usage (`M tokens / user / week`) across each group:
  - **Power User — Weekly Usage:** Default `5.00M` tokens/week (`1.00M` tokens/workday)
  - **Regular User — Weekly Usage:** Default `3.00M` tokens/week (`0.60M` tokens/workday)
  - **Occasional User — Weekly Usage:** Default `1.00M` tokens/week (`0.20M` tokens/workday)
- **Rollup Metrics:** Displays **Average Weekly Usage per Person** and **Total Estimated Team Usage / Week**.

### Step 3 — AI Model & Budget Settings
- **AI Model Split (Complex Reasoning vs. Everyday Tasks):** Balance between **Gemini Pro** (for complex problem-solving) and **Gemini Flash** (for fast, everyday tasks), defaulting to `80% Flash / 20% Pro`.
- **Prompt vs. Response Ratio (Input vs. Output):** Proportion of **Prompts (Input)** vs. **Responses (Output)**, defaulting to `80% Input / 20% Output`.
- **Extra Monthly Budget (Optional):** Additional monthly budget (`USD / mo`, default `\$0`) on top of included seat credits, showing **Extra Weekly Budget** and **Extra Weekly Capacity Added**.
- **Model Rates & Negotiated Discounts:**
  - Prepopulated with Google Cloud rates for **Gemini Pro (Advanced Reasoning)** (`\$2.00` Input / `\$12.00` Output per 1M tokens) and **Gemini Flash (Fast Everyday Tasks)** (`\$1.50` Input / `\$7.50` Output per 1M tokens).
  - Dedicated **Gemini Pro Discount (%)** (default `0%`) and **Gemini Flash Discount (%)** (default `50%`) widgets (`0%–90%` off list price), plus **Overall Average Cost per 1M Tokens** and **Tokens You Get per \$1.00**.

### Step 4 — Weekly Forecast & Budget (`75:25` Vertical Split)
- **Left `75%` Pane:**
  - Prominent **Weekly Team Usage vs. Available Capacity** (**Running Weekly Total**) stacked line chart (`X-axis`: `Monday`–`Friday`, `Y-axis`: `Tokens in Millions (M)`) with interactive hover tooltips and a static horizontal **Weekly Capacity Limit** line.
  - Merged title, status badge (`Within Weekly Limit` / `Over Weekly Limit`), and legend banner directly below the chart, followed by a day-by-day breakdown table.
- **Right `25%` Pane (Ordered Top to Bottom):**
  1. **Recommendation & Budget Status:** Evaluates **Total Weekly Capacity Available** ($A$) vs. **Total Weekly Team Usage** ($U$):
     - **`Optimal Capacity Match`** when available capacity is within $\pm 5\%$ of usage ($|A - U| / U \le 0.05$)
     - **`Sufficient Capacity Available`** when available capacity $>$ usage (outside $\pm 5\%$)
     - **`Additional Budget Needed`** when available capacity $<$ usage (outside $\pm 5\%$), automatically computing the **Estimated Extra Monthly Budget Needed** to cover the weekly gap
  2. **Weekly Capacity Used (%):** Radial gauge and **Weekly Surplus / Shortfall** (`M tokens`).
  3. **Total Weekly Capacity Available:** Total weekly tokens from purchased seats plus any extra monthly budget.
  4. **Total Weekly Team Usage:** Total weekly usage across active Antigravity users with a stacked activity group bar.

---

## Running Locally

No build step or server is required. Clone the repository and open `index.html` (or `antigravity_ge_usage_simulator.html`) in any modern browser:

```bash
git clone https://github.com/mohan-the-octocat/pushpak.git
cd pushpak
open index.html   # macOS
# or: xdg-open index.html (Linux)
```

Or serve it over HTTP:

```bash
python3 -m http.server 8080
# Open http://localhost:8080
```

---

## Repository Structure

```text
pushpak/
├── index.html                           # GitHub Pages entry point (Usage Simulator)
├── antigravity_ge_usage_simulator.html  # Standalone Usage Simulator HTML
├── antigravity_ge_usage_simulator_prd.md # Product Requirements Document (PRD)
├── docs/
│   └── PRD.md                           # Copy of PRD in docs/
├── .nojekyll                            # Bypasses Jekyll processing on GitHub Pages
└── README.md                            # Project documentation
```
