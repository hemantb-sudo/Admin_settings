# Meritto Admin — Unified Dashboard

A single-file web application combining the **Admin Dashboard** and **Subscription & Usage** page for the Meritto platform. Built using the Meritto design system with Chart.js for data visualizations.

---

## File Structure

```
Admin settings/
├── index.html       ← Single-file app (all pages, styles, and scripts)
└── index.md         ← This documentation file
```

---

## Pages

### 1. Admin Dashboard (`#page-dashboard`)
The primary landing page after login. Displays:
- **Topnav** — Search bar, notifications, and profile avatar dropdown
- **Sidebar** — Collapsible navigation with module items
- **KPI Cards** — Key metrics at a glance (leads, enrollments, revenue, etc.)
- **Charts** — Sparklines and bar charts powered by Chart.js
- **Settings Overlay** (`#settings-view`) — Slide-in panel for system settings triggered from the sidebar

### 2. Subscription & Usage (`#page-usage`)
Accessible via the sidebar item or the profile dropdown. Displays:
- **Summary Cards** — Total modules, active users, API calls, storage used
- **Module Cards** — Per-module usage with capped progress bars, feature rows, and PAYG indicators
- **Billing Table** — Invoice history with status chips
- **Controls** — Filter bar, toggle switches, and section headers

---

## Navigation

### Sidebar
- Click any sidebar item to navigate between sections
- **Subscription & Usage** item (`#sb-usage`) navigates to the usage page

### Profile Avatar Dropdown (Top-right)
Click the **RA** avatar to open the dropdown menu:

| Option | Action |
|---|---|
| **Subscription and Usage** | Closes settings overlay (if open) → navigates to Subscription & Usage page |
| **Profile** | Placeholder |
| **Sign out** | Placeholder |

> The dropdown uses `position: fixed; z-index: 10000` and the topnav uses `z-index: 3000` to ensure it always renders above the settings overlay.

---

## Settings Overlay Behaviour

- Opened via the ⚙️ sidebar item
- Rendered at `z-index: 2000`
- Automatically **closes** when navigating to any page via `showPage()`
- Keyboard shortcut **⌘K / Ctrl+K** opens the settings search

---

## Key Functions

| Function | Description |
|---|---|
| `showPage(name)` | Switches between `'dashboard'` and `'usage'` views; also closes the settings overlay |
| `toggleProfileMenu()` | Opens / closes the profile avatar dropdown |
| `closeProfileMenu()` | Closes the profile dropdown |
| `renderUsage()` | Lazy-renders the Subscription & Usage page content (called once on first visit) |

---

## Design Tokens (CSS Custom Properties)

| Token | Usage |
|---|---|
| `--bg-app` | App background (`#f4f6fa`) |
| `--bg-surface` | Card / panel background (`#ffffff`) |
| `--brand-blue` | Primary brand colour (`#1a56db`) |
| `--status-active` | Active / success green (`#16a34a`) |
| `--status-warn` | Warning amber |
| `--status-error` | Error / danger red |
| `--text-primary` | Primary text (`#111827`) |
| `--text-secondary` | Secondary / muted text (`#6b7280`) |
| `--border` | Default border colour (`#e5e7eb`) |
| `--radius` | Base border radius (`8px`) |

---

## Dependencies

| Library | Version | CDN |
|---|---|---|
| Chart.js | 4.x | `cdn.jsdelivr.net/npm/chart.js` |

No build step required — open `index.html` directly in a browser or serve with any static file server.

```bash
# Quick local preview
python3 -m http.server 3456
# Then open http://localhost:3456
```

---

## Z-Index Layers

| Element | z-index | Notes |
|---|---|---|
| `.topnav` | 3000 | Sticky top bar; stacking context above settings overlay |
| `#settings-view` | 2000 | Slide-in settings panel |
| `.profile-dropdown` | 10000 | Fixed dropdown; inherits topnav stacking context |
| Sidebar | 100 | Left navigation |

---

## Browser Support
Chrome 90+, Firefox 88+, Safari 14+, Edge 90+
