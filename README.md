# Pushpak — Antigravity in Gemini Enterprise Usage Simulator

Named after the **Pushpaka Vimana**—the celestial flying craft crafted by Vishwakarma for Kubera (treasurer of the gods) whose capacity dynamically scales to accommodate every passenger aboard—**Pushpak** is an interactive, zero-dependency browser simulator for modeling **Google Antigravity** **Weighted Token Unit (WTU)** and token capacity, context-cached developer consumption, and budget utilization under **Gemini Enterprise**.

- **Live Simulator (GitHub Pages):** [https://mohan-the-octocat.github.io/pushpak/](https://mohan-the-octocat.github.io/pushpak/)
- **Simulator HTML:** [`antigravity_ge_usage_simulator.html`](./antigravity_ge_usage_simulator.html) (also served at [`index.html`](./index.html))
- **Product Requirements Document (PRD):** [`antigravity_ge_usage_simulator_prd.md`](./antigravity_ge_usage_simulator_prd.md) (also in [`docs/PRD.md`](./docs/PRD.md))

---

## Overview

When organizations procure **Gemini Enterprise Standard** (\$10/user/month AI credit allocation = `1.25M WTU / seat / week`) or **Gemini Enterprise Plus** (\$15/user/month AI credit allocation = `1.875M WTU / seat / week`, where `1M WTU = $2.00`), Antigravity IDE and CLI usage draws from a shared project-level **Weighted Token Unit (WTU)** quota pool (`aiusage.googleapis.com/gemini_enterprise_Included_weekly_quota_per_project`) that refreshes weekly.

Every model call is metered into WTUs across three token buckets—**Uncached Input** ($\text{prompt} - \text{cached}$), **Cached Input** ($\text{cached}$), and **Output + Thinking** ($\text{candidates} + \text{thoughts}$):

$$\text{WTU} = (\text{prompt} - \text{cached}) \cdot w_{\text{in}} + \text{cached} \cdot w_{\text{cache}} + (\text{candidates} + \text{thoughts}) \cdot w_{\text{out}}$$

**Pushpak** helps Customer Engineers, Solution Architects, FinOps leads, and Enterprise IT Administrators answer four questions through a **4-step guided wizard** (with floating **Back** / **Next** navigation, automatic next-step nudges, and a header **Dark / Light Mode Toggle** defaulting to Dark Mode):

1. **1. Plan & Seats:** Given the **Gemini Enterprise Plan** (`Standard` or `Plus`), **Endpoint Location** (`Global` vs. `Regional +10% WTU`), **Total Purchased Seats** (all seats pool together, including unassigned licenses), and **Active Antigravity Users** ($\le$ Total Purchased Seats), what are the **Total Weekly Team Capacity** (in tokens and WTUs) and **Average Weekly Capacity per Active User**?
2. **2. Team Usage Habits:** How does splitting active Antigravity users across **Power Users (Heavy)**, **Regular Users (Moderate)**, and **Occasional Users (Light)** (default `30% / 40% / 30%`) with configurable cache-inclusive **Estimated Weekly Usage per Person** (default `25M / 10M / 3M` tokens/user/week) drive **Total Estimated Team Usage / Week**, and does any Power User exceed the unpooled **10× single-seat per-user weekly cap** (`18.75M WTU` = \$37.50/wk on `Plus`; `12.50M WTU` = \$25.00/wk on `Standard`)?
3. **3. AI Model & Budget Settings:** How do the **AI Model Split** (`Gemini 4 Argon` vs. `Gemini 3.8 Flash`, default `20% / 80%`), **Prompt vs. Response Ratio (Input vs. Output + Thinking)** (default `98% Input / 2% Output`), **Context Cache Hit Rate (%)** (default `88%`, where cached tokens cost `5%` of input on `Gemini 4 Argon` and `10%` on `Gemini 3.8 Flash`), **Extra Monthly Budget (Optional)** (default `\$0`), **Rate Period Presets** (`Current Promo` to Nov 30, 2026; `Dec 2026`; `Jan 2027+`), and model **Discount (%)** widgets affect the **Overall Blended Cost & WTU Weight** (`$/1M tokens` and `WTU / 1K tokens`)?
4. **4. Weekly Forecast & Budget:** In a `75:25` vertical split, how does the **Running Weekly Total** of team usage (`Monday`–`Friday`) compare against the organization's **Weekly Capacity Limit**, when does it cross the official **80% admin alert threshold**, and what **Recommendation & Budget Status** is triggered?

---

## Key Features

### Step 1 — Plan & Seats (`67:33` Vertical Split)
- **Left `2/3` Pane:**
  - **Gemini Enterprise Plan:** Radio selection between **Standard** (`\$10 / mo · \$2.50 / wk · 1.25M WTU / wk per seat`, `10× user cap = 12.50M WTU`) and **Plus** (`\$15 / mo · \$3.75 / wk · 1.875M WTU / wk per seat`, `10× user cap = 18.75M WTU`).
  - **Endpoint Location:** Toggle between **Global** (`1.00×` base WTU weights) and **Regional Endpoint (+10% WTU)** (`1.10×` WTU uplift).
  - **Total Purchased Seats:** Total Gemini Enterprise licenses on the GCP project (all seats pool together, including unassigned seats).
  - **Active Antigravity Users:** Number of team members actively using Antigravity (automatically capped at `Total Purchased Seats`; inactive seats leave extra buffer in the shared pool).
- **Right `1/3` Pane (`Available Weekly Capacity`):**
  - Readonly capacity displays (`+6px` enlarged typography) for **Total Weekly Team Capacity** (tokens and WTU pool) and **Average Weekly Capacity per Active User**, plus summary rows for **Active Users / Purchased Seats**, **Weekly Included Pool (WTU / USD)**, and **Effective Cost per 1M Tokens (w/ Cache)** (`$0.29 / 1M · 143 WTU/1K` at defaults).

### Step 2 — Team Usage Habits
- **Team Activity Breakdown (%):** Interactive sliders and numeric inputs for **Power Users (Heavy)**, **Regular Users (Moderate)**, and **Occasional Users (Light)** (defaults to `30-40-30`, auto-normalized to `100%`).
- **Estimated Weekly Usage per Person (Cache-Inclusive):** Configurable weekly token usage (`M tokens / user / week`, including cached context) across each group:
  - **Power User — Weekly Usage:** Default `25.00M` tokens/week (`~5.00M` tokens/workday), with an inline **10× single-seat per-user limit** check (`18.75M WTU` = `130.85M tokens/wk` on `Plus` at default mix) and warning if exceeded
  - **Regular User — Weekly Usage:** Default `10.00M` tokens/week (`~2.00M` tokens/workday)
  - **Occasional User — Weekly Usage:** Default `3.00M` tokens/week (`~0.60M` tokens/workday)
- **Rollup Metrics:** Displays **Average Weekly Usage per Person** and **Total Estimated Team Usage / Week** (in both tokens and WTUs).

### Step 3 — AI Model & Budget Settings
- **AI Model Split:** Balance between **Gemini 4 Argon** for complex coding and **Gemini 3.8 Flash** for everyday coding, defaulting to `80% Flash / 20% Argon`.
- **Prompt vs. Response Ratio (Input vs. Output + Thinking):** Proportion of **Prompts (Input)** vs. **Output + Thinking**, defaulting to `98% Input / 2% Output`.
- **Context Cache Hit Rate (%):** Share of prompt tokens served from context cache, defaulting to `88%` (`11.8% uncached · 86.2% cached · 2.0% out`). Cached tokens carry **5%** of uncached input weight on `Gemini 4 Argon` and **10%** on `Gemini 3.8 Flash`.
- **Extra Monthly Budget (Optional):** Optional opt-in PAYG overage budget (`USD / mo`, default `\$0`) on top of the weekly seat pool.
- **Model Rates, WTU Weights & Rate Period Presets:**
  - Three one-click **Rate Period Presets**:
    - **Current Promo (to Nov 30, 2026):** `Gemini 4 Argon` 50% off (`$2.00 In / $0.10 Cache / $10.00 Out`), `Gemini 3.8 Flash` 50% off (`$0.75 In / $0.075 Cache / $3.75 Out`)
    - **Dec 2026:** `Gemini 4 Argon` Standard (`0% off`: `$4.00 In / $0.20 Cache / $20.00 Out`), `Gemini 3.8 Flash` 50% off (promo runs through Dec 31, 2026)
    - **Jan 2027+ (Standard Rates):** Both `Gemini 4 Argon` and `Gemini 3.8 Flash` at Standard (`0% promo`) rates

### Step 4 — Weekly Forecast & Budget (`75:25` Vertical Split)
- **Left `75%` Pane:**
  - Prominent **Weekly Team Usage vs. Available Capacity** (**Running Weekly Total**) stacked line chart (`X-axis`: `Monday`–`Friday`, `Y-axis`: `Tokens in Millions (M)`) with interactive hover tooltips and a static horizontal **Weekly Capacity Limit** line.
  - Merged title, status badge (`Within Weekly Limit` / `Over Weekly Limit`), and legend banner directly below the chart, followed by a day-by-day breakdown table.
- **Right `25%` Pane (Ordered Top to Bottom):**
  1. **Recommendation & Budget Status:** Evaluates **Total Weekly Capacity Available** ($A$) vs. **Total Weekly Team Usage** ($U$):
     - **`Optimal Capacity Match`** when available capacity is within $\pm 5\%$ of usage ($|A - U| / U \le 0.05$)
     - **`Sufficient Capacity Available`** when available capacity $>$ usage (outside $\pm 5\%$)
     - **`Additional Budget Needed`** when available capacity $<$ usage (outside $\pm 5\%$), computing the **Estimated Extra Monthly Overage Budget Needed (Opt-In)** and noting that without admin opt-in, requests over pool return `HTTP 429`
  2. **Weekly Capacity Used (%):** Radial gauge (highlighting `Near Limit` at $\ge 80\%$ to match the official GE admin alert threshold) and **Weekly Surplus / Shortfall**.
  3. **Total Weekly Capacity Available:** Total weekly tokens and WTU pool from purchased seats plus any extra monthly budget.
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
