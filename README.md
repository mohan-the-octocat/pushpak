# Pushpak — Antigravity in Gemini Enterprise Usage Simulator

Named after the **Pushpaka Vimana**—the celestial flying craft crafted by Vishwakarma for Kubera (treasurer of the gods) whose capacity dynamically scales to accommodate every passenger aboard—**Pushpak** is an interactive, zero-dependency browser simulator for modeling **Google Antigravity** token capacity, developer consumption, and budget utilization under **Gemini Enterprise**.

- **Live Simulator (GitHub Pages):** [https://mohan-the-octocat.github.io/pushpak/](https://mohan-the-octocat.github.io/pushpak/)
- **Simulator HTML:** [`antigravity_ge_usage_simulator.html`](./antigravity_ge_usage_simulator.html) (also served at [`index.html`](./index.html))
- **Product Requirements Document (PRD):** [`antigravity_ge_usage_simulator_prd.md`](./antigravity_ge_usage_simulator_prd.md) (also in [`docs/PRD.md`](./docs/PRD.md))

---

## Overview

When organizations procure **Gemini Enterprise Standard** (\$10/user/month AI credit allocation) or **Gemini Enterprise Plus** (\$15/user/month AI credit allocation), Antigravity IDE and CLI usage draws from a shared project-level token quota pool that refreshes weekly.

**Pushpak** helps Customer Engineers, Solution Architects, FinOps leads, and Enterprise IT Administrators answer four questions through a **4-step guided wizard** (with floating **Back** / **Next** navigation and automatic next-step nudges):

1. **Licensing:** Given the subscription tier (`Standard` or `Plus`), total procured Gemini Enterprise licenses, and the effective **No. of AGY users** consuming quota ($\le$ total GE licenses), how many **Total Tokens per Week** and **Tokens per User per Week** are available?
2. **User Distribution:** How does splitting active Antigravity users across **Heavy**, **Moderate**, and **Light** cohorts (default `30% / 40% / 30%`) with configurable weekly token burn per cohort (default `5M / 3M / 1M` tokens/user/week) drive total weekly token demand?
3. **Models Usage:** How do the **Thinking vs. Workhorse** model mix (`Gemini Pro` vs. `Gemini Flash`, default `20% Pro / 80% Flash`), **Input : Output Tokens Mix** (default `80% Input / 20% Output`), **Additional Spend available per month** (default `\$0`), model list prices (\$/1M tokens), and **separate Pro & Flash Discount Pricing (%)** widgets affect the effective blended token rate and weekly token capacity?
4. **Consumption Projection:** In a `75:25` vertical split, how does cumulative working-week usage (`Monday`–`Friday`) stack up against the organization's static **Weekly Token Quota** line, and what **Call to Action** is triggered?

---

## Key Features

### Step 1 — Licensing (`67:33` Vertical Split)
- **Left `2/3` Pane:**
  - **GE Subscription Tier:** Radio selection between **Gemini Enterprise Standard** (`\$2.50 / license / week`) and **Gemini Enterprise Plus** (`\$3.75 / license / week`).
  - **Total # of GE Licenses:** Total seats procured by the organization.
  - **No. of AGY users:** Effective number of users consuming Antigravity quota (automatically capped at `Total # of GE Licenses`).
- **Right `1/3` Pane:**
  - Readonly capacity displays (`+6px` enlarged typography) for **Total Tokens available per week for consumption** and **Total Tokens available per user per week for consumption**.

### Step 2 — User Distribution
- **User Category Split (%):** Interactive sliders and numeric inputs for **Heavy**, **Moderate**, and **Light** users (defaults to `30-40-30`, auto-normalized to `100%`).
- **Estimated Weekly Token Burn:** Configurable weekly token burn (`M tokens / user / week`) across each user category:
  - **Heavy Users:** Default `5.00M` tokens/week (`1.00M` tokens/workday)
  - **Moderate Users:** Default `3.00M` tokens/week (`0.60M` tokens/workday)
  - **Light Users:** Default `1.00M` tokens/week (`0.20M` tokens/workday)

### Step 3 — Models Usage
- **Model Usage Mix Slider:** Split between **Gemini Pro** (Thinking) and **Gemini Flash** (Workhorse), defaulting to `80% Flash & 20% Pro`.
- **Input : Output Tokens Mix Slider:** Split between Input and Output tokens, defaulting to `80% Input & 20% Output`.
- **Additional Spend available per month:** Optional monthly dollar budget (`USD / mo`, default `\$0`) converted into weekly token availability in **Consumption Projection**.
- **Model Family Pricing & Separate Discounts:**
  - Prepopulated with public Vertex AI pricing for **Gemini Pro** (`\$2.00` Input / `\$12.00` Output per 1M tokens) and **Gemini Flash** (`\$1.50` Input / `\$7.50` Output per 1M tokens).
  - Dedicated **Gemini Pro Discount Pricing (%)** and **Gemini Flash Discount Pricing (%)** widgets (`0%–90%` off list price, default `0%`).

### Step 4 — Consumption Projection (`75:25` Vertical Split)
- **Left `75%` Pane:**
  - Prominent **Cumulative usage** stacked line chart (`X-axis`: `Monday`–`Friday`, `Y-axis`: `Tokens in Millions (M)`) with interactive hover tooltips and a static horizontal **Weekly Token Quota** line.
  - Merged title, status badge, and legend banner directly below the chart, followed by a day-by-day breakdown table.
- **Right `25%` Pane (Ordered Top to Bottom):**
  1. **Call to Action Infographic:** Evaluates **Weekly Token Availability** ($A$) vs. **Weekly Token Usage** ($U$):
     - **`Full Utilization`** when Availability is within $\pm 5\%$ of Usage ($|A - U| / U \le 0.05$)
     - **`Capacity Available`** when Availability $>$ Usage (outside $\pm 5\%$)
     - **`Additional Spend Required`** when Availability $<$ Usage (outside $\pm 5\%$), automatically computing the **Indicative Budget Required / Month** to cover the shortfall
  2. **Token Pool Utilization:** Radial utilization gauge and pool variance (`M tokens`).
  3. **Weekly Token Availability:** Total weekly token capacity from GE licenses plus any additional monthly spend.
  4. **Weekly Token Usage:** Total weekly token consumption across active AGY users with a stacked cohort share bar.

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
