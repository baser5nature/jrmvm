# JRMVM — JRM Vehicle Manager

A self-hosted, client-side Progressive Web App (PWA) for tracking vehicle fuel fill-ups, expenses, maintenance reminders, and efficiency analytics across one or more vehicles.

Built as a single-page application with no build step and no backend server—all data stays locally in your browser's `localStorage`.

---

## Features

- **Dashboard Overview**
  - Active vehicle banner displaying vehicle name, license plate, current odometer, and fuel type.
  - Summary cards for average fuel efficiency, total spending, recorded distance, and cost rate.
  - Quick actions to log fuel, expenses, or reminders, plus upcoming reminders and a recent activity feed.
- **Fuel Fill-up Log**
  - Record date/time, odometer reading, fuel quantity (up to 3 decimal places), total cost, and auto-calculated price per unit.
  - Supports **Full Tank** and **Missed previous fill** flags for accurate consumption calculations, along with station/location and notes.
- **Expense Tracking**
  - Categorized vehicle expenses: `Maintenance`, `Insurance`, `Parking`, `Tolls`, `Car Wash`, `Fine`, and `Other`.
  - Optional odometer tracking per expense entry.
- **Service & Maintenance Reminders**
  - Track upcoming maintenance by target date and/or odometer reading.
  - Supports custom recurring intervals (**every N months** and/or **every N km/miles**, whichever comes first) with a completion modal that advances recurring schedules.
- **Statistics & Analytics**
  - Interactive [Chart.js](https://www.chartjs.org/) charts with `6mo`, `12mo`, `24mo`, and `All` range filters:
    - **Fuel Efficiency Trend** (`L/100km` or `MPG`) with a smoothing toggle.
    - **Monthly Spending** broken down by `Fuel`, `Expenses`, or `Both`.
- **Multi-Vehicle Garage**
  - Manage multiple vehicles (`Hybrid`, `Petrol`, `Diesel`, `EV`, `LPG`) and switch the active vehicle from the header or garage tab.
  - Upload a vehicle photo and use **Color Match from Photo** to sample a custom accent color from the image.
- **Themes, Units & Currency**
  - Dark and light modes.
  - Three theme styles: **TMOG** (monochrome black & white), **Cookie** (purple & blue), and **Match Active Vehicle Color**.
  - **Metric** (`km`, `Liters`, `L/100km`) or **Imperial** (`miles`, `Gallons`, `MPG`) units.
  - Selectable currency symbols: `$`, `€`, `£`, `¥`, `₹`, `C$`.
- **Backup & Data Portability**
  - **JSON Export / Import** for full backups (`jrmvm_backup_YYYY-MM-DD.json`).
  - **Fuelio CSV Export / Import** supporting `## Vehicle`, `## Log`, `## CostCategories`, and `## Costs` sections.
- **Offline-Capable PWA**
  - Installable via `manifest.json` and cached for offline fallback via `sw.js`.

---

## Project Structure

```text
.
├── index.html      # Full application UI, styling (Tailwind CDN), charts, and state logic
├── manifest.json   # PWA manifest metadata
├── sw.js           # Service worker (network-first with cache fallback)
└── icon.svg        # Application vector icon
```

---

## Running Locally

Because service workers and `manifest.json` require an HTTP/HTTPS origin (rather than `file://`), serve the repository with any static file server:

```bash
# Python 3
python3 -m http.server 8080
```

Or with Node.js:

```bash
npx serve .
```

Then open `http://localhost:8080` in your browser. To install as a standalone app on desktop or mobile, use your browser's **Install App** / **Add to Home Screen** option.

> **Note:** UI styling, charts, and typography load Tailwind CSS, Chart.js (`chartjs-adapter-date-fns`), and the Inter font from public CDNs when online.

---

## Data Storage & Privacy

- All vehicles, fuel logs, expenses, reminders, and preferences are stored locally in browser `localStorage` under the key `jrmvm_state_v1`.
- No accounts, telemetry, or external databases are used.
- Clearing browser site data will remove your stored records—use **Settings → Export JSON** regularly to keep a backup.
