# Subscription & Usage — View Usage

**File:** `View Usage.html`
**Product:** Meritto · LeadOS Platform Console
**Page:** Subscription & Usage

---

## Overview

A self-contained HTML page that displays a customer's subscription status and full feature usage breakdown across all Meritto CRM modules. Designed for the Meritto Enrollment Cloud product using the Meritto design system tokens.

---

## Page Structure

### 1. Shell Layout
- **Sidebar** (220px, collapsible to 52px) — dark navy (`#0a1628`) with nav items for Dashboard, Lead Manager, Application Manager, Automation, Reports, Subscription & Usage, Settings
- **Topbar** (48px) — shows page title, active account selector dropdown, and avatar menu with "Subscription and Usage" shortcut
- **Content area** — scrollable, renders the usage page

### 2. Summary Cards (4-column grid)

| Card | Content |
|---|---|
| **Package** | Enrollment Cloud · Meritto CRM Platform · Growth Plan pill |
| **Subscription Period** | Days remaining + progress bar + date range (Apr 1, 2026 – Mar 31, 2027) |
| **Features Enabled** | Total count · breakdown by plan / comp / add-ons |
| **Capacity Alerts** | Count of warn/critical capped features with inline list |

### 3. Feature Breakdown Section

**Controls bar:**
- Search input — live filters features and modules
- Type filter dropdown — All / Included in plan / Complementary / Paid add-on
- Expand all / Collapse all toggle buttons

**Module cards** (21 modules, collapsible):
- Each card shows module badge, name, capacity alert badges (warn/crit), add-on pill count, feature count, expand arrow
- Collapsed state still surfaces capacity warnings (e.g. `71% Lead Fields`)

---

## Module List

| Badge | Module | Add-on module? |
|---|---|---|
| LM | Lead Management | — |
| CM | Counsellor Management | — |
| UM | User and Team Management | — |
| RA | Reports and Analytics | ✓ |
| LG | Logs | — |
| MC | Mobile CRM | — |
| DP | Developer Portal | — |
| WH | Webhook | ✓ |
| EX | Extensions | — |
| TC | Telephony Connector | — |
| WA | WABA Connector | — |
| SM | SMS Connector | — |
| EC | Email Connector | — |
| MP | Marketing Platform | — |
| RD | Raw Data | — |
| CG | Campaign Management | — |
| AP | Application Automation Platform | — |
| PM | Payment Management | — |
| MO | Mio AI | — |
| DY | Dynamic Activity | — |
| MS | Miscellaneous | — |

---

## Feature Row Types

Each feature row inside a module has three columns:

1. **Feature name** — truncated with ellipsis if too long
2. **Type badge** — one of:
   - `Plan` (green) — Included in Plan
   - `Comp` (gray) — Complementary
   - `Add-on` (purple) — Included in Addon
   - `Add-on` (amber) — Paid Addon
3. **Status** — one of:

| Feature `lt` | Display |
|---|---|
| `Flag` (Plan) | ✓ Enabled (green) |
| `Flag` (Complementary) | ✓ Complementary (gray) |
| `Flag` (Addon) | ✓ Active (purple) |
| `Flag` (Paid) | ✓ Active (amber) |
| `Capped` | Two-line progress bar (see below) |
| `Usage` | "Pay as you go · {unit}" chip |

---

## Capped Feature Row — Visual Design

Two-line layout inside the 300px status column:

**Line 1 (top):**
- Progress bar (flex-1, 6px height)
  - Track background splits: gray (plan zone) / light purple (add-on zone) when add-on exists
  - Purple `|` boundary marker at the plan limit percentage
  - Fill color: green (ok, <70%) / amber (warn, 70–89%) / red (crit, ≥90%)
- Bold percentage (`57%`) — color matches fill

**Line 2 (bottom):**
- Left: `50K plan` green chip + `+10K add-on` purple chip
- Right: `34,210 used` muted text

---

## Data Schema

Each module in the `MODS` array:

```js
{
  name: "Module Name",
  badge: "XX",          // 2-char abbreviation
  bc: "#hex",           // badge background color
  bt: "#hex",           // badge text color
  isAddon: true,        // optional — marks as Add-on module
  features: [
    {
      n: "Feature Name",
      pt: "Included in Plan" | "Complementary" | "Included in Addon" | "Paid Addon",
      lt: "Flag" | "Capped" | "Usage",
      pl: 50000,         // plan limit (Capped only)
      al: 10000,         // add-on limit (Capped only, nullable)
      con: 34210,        // current consumption (Capped only)
      unit: "per email"  // unit label (Usage only)
    }
  ]
}
```

---

## Design Tokens Used

All colors, radii, and shadows reference Meritto design system CSS variables:

| Token | Value | Usage |
|---|---|---|
| `--bg-app` | `#eef0f4` | Page background |
| `--bg-surface` | `#ffffff` | Cards, topbar |
| `--brand-blue` | `#2979d4` | Plan pill, subscription bar |
| `--status-active` | `#1a9e6e` | Enabled, ok progress |
| `--status-pause` | `#e8900a` | Warn progress, add-on dots |
| `--status-stopped` | `#d94040` | Critical progress |
| `--border-1` | `#E5E7EB` | Default borders |
| `--radius-lg` | `10px` | Module cards, summary cards |
| `--radius-pill` | `999px` | Pills, count badges |
| `--shadow-md` | `0 4px 14px rgba(0,0,0,0.09)` | Dropdowns |

---

## Interactions

| Action | Behaviour |
|---|---|
| Click module header | Expand / collapse module body |
| Click "Expand all" | Opens all visible modules; click again to reset to first only |
| Click "Collapse all" | Closes all modules; click again to reset to first only |
| Type in search | Filters feature rows and hides empty modules live |
| Select filter type | Filters to selected feature type, auto-expands matching modules |
| Click account selector | Dropdown with 3 accounts (Meritto Edu Tech Ltd., Aakash Institute, Allen Career Institute) |
| Click avatar | Dropdown with "Subscription and Usage" shortcut, Profile, Sign out |
| Click sidebar toggle | Collapses sidebar to icon-only (52px) |
