<div align="center">

# 🚗 Trip Master

### Real-Time EV Trip Computer & Energy Analytics Dashboard

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![MapLibre GL](https://img.shields.io/badge/MapLibre%20GL-396CB2?style=for-the-badge&logo=maplibre&logoColor=white)](https://maplibre.org/)
[![Chart.js](https://img.shields.io/badge/Chart.js-FF6384?style=for-the-badge&logo=chartdotjs&logoColor=white)](https://www.chartjs.org/)
[![PWA](https://img.shields.io/badge/PWA-5A0FC8?style=for-the-badge&logo=pwa&logoColor=white)](https://web.dev/progressive-web-apps/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)

> A **single-file, offline-capable Progressive Web App** that turns any smartphone or browser into a professional-grade electric vehicle trip computer — tracking GPS position, computing physics-based energy consumption in real time, visualizing live charts, and displaying live weather data.

---

<img src="https://img.shields.io/badge/Status-Production%20Ready-00e676?style=flat-square" />
<img src="https://img.shields.io/badge/Platform-Web%20%7C%20iOS%20%7C%20Android-29b6f6?style=flat-square" />
<img src="https://img.shields.io/badge/Dependencies-Zero%20Build%20Step-b39ddb?style=flat-square" />

</div>

---

## 📑 Table of Contents

1. [Overview](#-overview)
2. [Core Features](#-core-features)
3. [Physics Engine](#-physics-engine)
4. [GPS & Geolocation](#-gps--geolocation)
5. [Energy & Range Estimation](#-energy--range-estimation)
6. [Live Charts](#-live-charts)
7. [Power Breakdown Panel](#-power-breakdown-panel)
8. [Weather Integration](#-weather-integration)
9. [Configuration Parameters](#️-configuration-parameters)
10. [User Profiles](#-user-profiles)
11. [UI & Theming](#-ui--theming)
12. [Progressive Web App](#-progressive-web-app)
13. [Stat Cards Reference](#-stat-cards-reference)
14. [Trip Summary Modal](#-trip-summary--efficiency-scoring)
15. [Map Modes: 2D & 3D](#️-map-modes-2d--3d)
16. [Dependencies](#-dependencies)
17. [Getting Started](#-getting-started)
18. [Mathematical Reference](#-mathematical-reference)

---

## 🌐 Overview

**Trip Master** is a zero-backend, single-file web application designed for **electric vehicle drivers** who want real-time telemetry, energy analytics, and route visualization without installing a native app. It leverages the browser's native **Geolocation API**, a physics-based energy model, live weather data from **Open-Meteo**, and interactive charts powered by **Chart.js**.

Both the flat **2D view** and the immersive **3D perspective view** are rendered by **MapLibre GL JS** — a single, unified WebGL-based vector map engine — with tiles served by **OpenFreeMap**.

The app runs entirely client-side. There is no server, no database, and no build pipeline. Drop the `index.html` file onto any web host and it works immediately.

---

## ✨ Core Features

| Feature | Description |
|---|---|
| 🛰️ **Real-time GPS Tracking** | Polls the device's GPS at user-selected intervals |
| ⚡ **Physics-based Energy Model** | Computes consumption from first principles on every GPS step |
| 🔋 **SOC & Range Estimator** | Live battery state-of-charge widget with adaptive range forecast |
| 🗺️ **2D Route Map** | MapLibre GL flat top-down view with live route polyline on OpenFreeMap vector tiles |
| 🌐 **3D Perspective Map** | MapLibre GL 3D tilted-perspective view with identical route data and WebGL rendering |
| 🔄 **2D / 3D Map Toggle** | One-click button to switch between flat 2D view and immersive 3D view |
| 📊 **4 Live Charts** | Elevation profile, consumption vs. distance, speed profile, energy balance |
| 🌡️ **Live Weather Panel** | Auto-fetches Open-Meteo for temperature, humidity, wind, and pressure |
| 🌙 **Dark / Light Theme** | Full dual-theme UI with smooth CSS variable transitions |
| 📱 **PWA / Installable** | Service Worker + Web Manifest for offline use and home-screen install |
| 🔒 **Wake Lock** | Prevents device screen from sleeping during active tracking |
| 🏁 **Trip Summary Modal** | Post-trip analytics with efficiency scoring badge |

---

## ⚙️ Physics Engine

The core of Trip Master is `calculatePhysics()`, a segment-by-segment energy model that runs on every GPS fix. It decomposes the energy consumed into three physical components and handles regenerative braking with a fixed round-trip efficiency coefficient.

### 🔬 Total Segment Energy

$$E_{\text{step}} = E_{\text{resistance}} + E_{\text{potential}}$$

where the **resistance energy** aggregates rolling resistance, aerodynamic drag, and headwind losses:

$$E_{\text{resistance}} = \frac{\left(120 + 0.8 \cdot v_w + 0.012 \cdot m\right)}{\eta_T} \cdot d $$

| Symbol | Description | Unit |
|---|---|---|
| $v_w$ | Headwind speed (user-configured) | Km/h |
| $m$ | Vehicle + occupant mass | kg |
| $\eta_T$ | Temperature efficiency factor | dimensionless $\in [0.55, 1.0]$ |
| $d$ | Segment distance | Km |

The constant **120** represents the combined baseline resistive losses (powertrain friction, HVAC, auxiliary loads) expressed in Wh/Km at zero wind and normalized vehicle mass.

### 🏔️ Potential Energy (Gravity Term)

$$E_{\text{potential}} = \frac{m \cdot g \cdot \Delta h}{3600} $$

| Symbol | Description |
|---|---|
| $m$ | Vehicle mass [kg] |
| $g$ | Gravitational acceleration $= 9.81\ \text{m/s}^2$ |
| $\Delta h$ | Altitude change for the segment [m] (positive = uphill) |

### ♻️ Regenerative Braking

When $E_{\text{step}} < 0$ (net energy from descent), the energy is **not consumed** but instead credited to the regeneration accumulator with a **70% recovery efficiency**:

$$E_{\text{regen,accumulated}} += \left| E_{\text{step}} \right| \cdot 0.70 \quad \text{if } E_{\text{step}} < 0$$

The segment consumption is then clamped to zero for the consumed accumulator:

$$E_{\text{consumed,accumulated}} += E_{\text{step}} \quad \text{if } E_{\text{step}} \geq 0$$

### ⚡ Instantaneous Power

At each GPS interval of duration $\Delta t$ [s], the instantaneous power is:

$$P_{\text{instant}} = \frac{E_{\text{step}}}{\Delta t / 3600} $$

### 📐 Specific Consumption

The per-segment consumption figure displayed in Wh/Km is:

$$C_{\text{instant}} = \left\lfloor \frac{E_{\text{step}}}{d} + 0.5 \right\rfloor $$

---

## 🛰️ GPS & Geolocation

Trip Master uses the **W3C Geolocation API** with `enableHighAccuracy: true` to request fine-grained GNSS position fixes.

### 📍 Polling Architecture

- At trip start, `setInterval` fires every `T_poll` seconds (configurable: 1, 5, 10, 30, or 60 s).
- Each tick triggers `navigator.geolocation.getCurrentPosition()`.
- A **minimum displacement filter of 5 m** discards GPS noise: segments shorter than 5 m are silently ignored to prevent spurious energy spikes when the vehicle is stationary.

### 🌍 Haversine Distance Formula

The great-circle distance between two consecutive GPS fixes is computed with the **Haversine formula**:

$$a = \sin^2\left(\frac{\Delta\phi}{2}\right) + \cos\phi_1 \cdot \cos\phi_2 \cdot \sin^2\left(\frac{\Delta\lambda}{2}\right)$$

$$d = 2R \cdot \mathrm{arctan2}\left(\sqrt{a},\ \sqrt{1 - a}\right) $$

where $R = 6{,}371{,}000\ \text{m}$ is the mean Earth radius, $\phi$ is latitude in radians, and $\lambda$ is longitude in radians.

### 📏 Road Grade

The road grade (slope percentage) is computed at each segment as:

$$G = \frac{\Delta h}{d} \times 100 $$

### 🚀 Speed Computation

GPS speed is obtained preferentially from `pos.coords.speed` (native GNSS Doppler speed, typically more accurate). When unavailable, it is derived from displacement:

$$v = \frac{d_{\text{segment}}}{T_{\text{poll}}} \times 3.6 $$

### 📊 Average Speed

$$\bar{v} = \frac{D_{\text{total}}}{t_{\text{elapsed}}}$$

where $t_{\text{elapsed}}$ is measured from trip start via `Date.now()`.

---

## 🔋 Energy & Range Estimation

### 🔌 Battery State-of-Charge Widget

The SOC bar renders visually with three color states driven by CSS classes:

| SOC Range | Visual State | Color |
|---|---|---|
| $> 30\%$ | Normal | 🟢 `#00e676` → `#69f0ae` |
| $15\% < \text{SOC} \leq 30\%$ | Warning | 🟡 `#ffd740` → `#ffee58` |
| $\leq 15\%$ | Critical | 🔴 `#ff1744` → `#ff5252` |

### 📡 Range Estimation Algorithm

**Phase 1 — Adaptive (after enough data has been collected):**

$$R_{\text{estimated}} = \frac{W_{\text{available}}}{C_{\text{avg}}} $$

$$W_{\text{available}} = C_{\text{battery}} \times 1000 \times \frac{\text{SOC}}{100} $$

$$C_{\text{avg}} = \frac{E_{\text{consumed,total}}}{D_{\text{total}}} $$

**Phase 2 — Baseline (cold start / insufficient data):**

When $E_{\text{consumed}} \leq 1\ \text{Wh}$ or $D_{\text{total}} \leq 100\ \text{m}$, a default consumption of **180 Wh/Km** is used as the baseline:

$$R_{\text{estimated}} = \frac{W_{\text{available}}}{180} $$

**Remaining range** is then:

$$R_{\text{remaining}} = \max\left(0,\ R_{\text{estimated}} - D_{\text{traveled}}\right) $$

---

## 📊 Live Charts

All charts are rendered via **Chart.js v4** with `animation: false` for zero-latency real-time updates. Charts are appended with new data points at every GPS fix using `chart.update('none')` to suppress transition animations.

### ⛰️ Elevation Profile

- **Type:** Line chart with area gradient fill
- **X-axis:** Distance traveled [Km]
- **Y-axis:** Altitude above sea level [m]
- **Color:** `#ffd740` (amber) with gradient fill fading to transparent
- **Tension:** 0.4 (smooth cubic Bézier interpolation)
- **Point radius:** 0 (no dots, continuous trace)

### ⚡ Consumption vs Distance

- **Type:** Line chart
- **X-axis:** Distance [Km]
- **Y-axis:** Instantaneous consumption [Wh/Km]
- **Color:** `#ff1744` (danger red) — high consumption is immediately visible
- A **zero-baseline annotation** is drawn at $y = 0$ via `chartjs-plugin-annotation`

### 🏎️ Speed Profile

- **Type:** Line chart
- **X-axis:** Distance [Km]
- **Y-axis:** Speed [Km/h]
- **Color:** `#b39ddb` (accent purple)
- Plots `lastSpeedKmh` at each GPS-valid segment

### 🔋 Energy Balance

- **Type:** Horizontal bar chart (grouped)
- **Dataset 0:** Total energy consumed [Wh] — color `#ff1744`
- **Dataset 1:** Total energy regenerated [Wh] — color `#00e676`
- Updates cumulatively at each GPS fix, displaying the full running total
- Below the canvas, three inline stats are shown:
  - ⬇️ **Consumed** — `totalConsumedWh` [Wh]
  - ⬆️ **Recovered** — `totalRegenWh` [Wh]
  - ⚡ **Regen Efficiency** — computed as:

$$\eta_{\text{regen}} = \frac{E_{\text{regen,total}}}{E_{\text{consumed,total}}} \times 100 $$

---

## 📊 Power Breakdown Panel

The **Power Breakdown** widget decomposes the instantaneous power demand into four physical contributors, rendered as animated horizontal bar indicators. Each bar is normalized to the maximum power component in that GPS step.

### 🔄 Rolling Resistance Power

$$P_{\text{rolling}} = \frac{m \cdot 0.012 \cdot d}{\eta_T \cdot \left(\Delta t / 3600\right)} $$

The coefficient $\mu_r = 0.012$ is a dimensionless rolling resistance factor typical of modern EV tires on asphalt.

### ⛰️ Gravity / Hill-Climb Power

$$P_{\text{gravity}} = \frac{m \cdot g \cdot \max(0, \Delta h)}{3600 \cdot \left(\Delta t / 3600\right)} $$

Only **positive altitude gains** contribute to gravity power consumption (descents are handled by the regen branch).

### 💨 Aerodynamic / Wind Power

$$P_{\text{aero}} = \frac{0.8 \cdot v_w \cdot d}{\eta_T \cdot \left(\Delta t / 3600\right)} $$

The coefficient 0.8 is an empirical drag factor relating headwind speed [Km/h] to additional Wh/Km load.

### ♻️ Instantaneous Regen Power

Active only when $\Delta h < 0$ (downhill):

$$P_{\text{regen}} = \frac{\left| m \cdot g \cdot \Delta h \right| \cdot 0.70}{3600 \cdot \left(\Delta t / 3600\right)} $$

The **bar fill width** for each component is:

$$w_i = \min\left(100,\ \frac{P_i}{P_{\max}} \times 100\right) $$

where $P_{\max} = \max(P_{\text{rolling}},\ P_{\text{gravity}},\ P_{\text{aero}},\ P_{\text{regen}},\ 100)$.

---

## 🌡️ Weather Integration

Trip Master integrates with the **Open-Meteo API** (free, no API key required) to fetch real-time meteorological data.

### 🌐 API Endpoint

```
GET https://api.open-meteo.com/v1/forecast
  ?latitude={lat}
  &longitude={lon}
  &current=temperature_2m,relative_humidity_2m,weather_code,
           surface_pressure,wind_speed_10m,wind_direction_10m
  &daily=temperature_2m_max,temperature_2m_min
  &timezone=auto
```

### 📡 Fetch Triggers

1. **On app load** — fires once when the first GPS fix is obtained.
2. **Every 2 Km of travel** — triggered when `Math.floor(totalDistance / 2000)` increments.

### 🌬️ Weather Fields Displayed

| Field | Source | Unit |
|---|---|---|
| 🌡️ Current Temperature | `current.temperature_2m` | °C |
| 🌡️ Daily Min | `daily.temperature_2m_min[0]` | °C |
| 🌡️ Daily Max | `daily.temperature_2m_max[0]` | °C |
| 💧 Humidity | `current.relative_humidity_2m` | % |
| 💨 Wind Speed | `current.wind_speed_10m` | Km/h |
| 🧭 Wind Direction | `current.wind_direction_10m` | Cardinal / Arrow |
| 📉 Pressure | `current.surface_pressure` | hPa |
| ☀️ Weather Icon | `current.weather_code` (WMO codes) | Emoji |

### 🌈 Delta Color Highlighting

Each weather value is compared against its previous reading. Values that have **increased** render in `--up-color` (`#00e676` green); values that have **decreased** render in `--down-color` (`#ff1744` red); unchanged values use the default text color. This delta coloring is implemented in `applyValueStyle()`.

### 🌡️ Automatic Thermal Efficiency Calibration

On the first weather sync, `updateEfficiencyByTemp()` auto-selects the thermal efficiency factor $\eta_T$ based on the retrieved ambient temperature:

| Temperature Range | $\eta_T$ | Label |
|---|---|---|
| $T \geq 20\ °C$ | $1.00$ | ✅ Nominal |
| $10\ °C \leq T < 20\ °C$ | $0.85$ | 🟡 Mild |
| $0\ °C \leq T < 10\ °C$ | $0.70$ | 🟠 Cold |
| $T < 0\ °C$ | $0.55$ | 🔴 Extreme Cold |

---

## ⚙️ Configuration Parameters

All parameters are configurable from the **Config Grid** panel at the top of the UI. No page reload is required; values are read live on each GPS step.

### 🚗 Vehicle Weight

- **Input:** Numeric field (`id="vehicleWeight"`)
- **Default:** not shown (user must set)
- **Role:** Appears directly in rolling resistance, gravity, and aero power formulas
- **Unit:** kg (vehicle + estimated occupant mass)

### 🌡️ Temperature Efficiency Factor ($\eta_T$)

A **segmented control** with four discrete values:

| Button Label | $\eta_T$ | Color |
|---|---|---|
| `100@20+` | $1.00$ | 🟢 Green |
| `85@10` | $0.85$ | 🟡 Yellow |
| `70@0` | $0.70$ | 🟠 Orange |
| `55@-10` | $0.55$ | 🔴 Red |

This factor reduces all energy estimates to account for reduced battery efficiency, increased HVAC load, and higher internal resistance at low temperatures.

### 💨 Headwind Speed

- **Input:** Numeric field (`id="windSpeed"`)
- **Default:** 0 Km/h
- **Role:** Feeds directly into $E_{\text{resistance}}$ as $0.8 \cdot v_w \cdot d / \eta_T$

### ⏱️ GPS Polling Interval

A **segmented control** with five options:

| Interval | Trade-off |
|---|---|
| `1 s` | Maximum resolution, highest battery drain |
| `5 s` *(default)* | Balanced accuracy and battery use |
| `10 s` | Moderate sampling |
| `30 s` | Low battery use, coarser data |
| `60 s` | Minimal drain, low-resolution route |

### 🔋 Battery Capacity & SOC

- **Battery kWh:** Numeric field — total usable pack energy [kWh]
- **SOC %:** Numeric input (0–100) linked to the visual battery bar via `updateBattery()` → `computeRangeEstimate()`. The SOC percentage and the battery bar are **dynamically updated in real time** at every GPS fix by `updateBatterySoC()`: the function computes the net energy drawn (`totalConsumedWh − totalRegenWh`), derives the new SOC from the initial charge level set at trip start (`initialSoc`), writes the result back to `#socInput`, and calls `updateBattery()` to refresh both the bar fill width and the color-coded state, keeping the visual indicator always consistent with the actual energy consumption.

---

## 👤 User Profiles

Trip Master includes a built-in **User Profiles** system that allows drivers to save, load, and delete named configuration snapshots. Profiles are stored in the browser's `localStorage` under the key `tripmaster_profiles` and persist indefinitely across sessions on the same device.

### 🗄️ Storage Model

Profiles are serialized as a JSON object where each key is the user-defined profile name and each value is a configuration record:

```json
{
  "My Tesla Model 3": {
    "vehicleWeight": 1850,
    "gpsPolling": 5,
    "batteryKwh": 75,
    "theme": "dark"
  },
  "Light City Run": {
    "vehicleWeight": 1600,
    "gpsPolling": 10,
    "batteryKwh": 60,
    "theme": "light"
  }
}
```

### 💾 Saved Parameters

Each profile snapshot captures exactly four configuration fields:

| Field | Source Element ID | Description |
|---|---|---|
| `vehicleWeight` | `vehicleWeight` | Vehicle + occupant mass [Kg] |
| `gpsPolling` | `gpsPolling` | GPS polling interval [s] |
| `batteryKwh` | `batteryCapacity` | Total usable battery capacity [kWh] |
| `theme` | `currentTheme` | Active UI theme (`"light"` or `"dark"`) |

> 💡 **Note:** Temperature efficiency and headwind speed are intentionally excluded — they represent real-time environmental conditions rather than vehicle-specific parameters.

### ⚙️ Profile Functions

| Function | Description |
|---|---|
| `getProfiles()` | Reads and parses the `localStorage` entry; returns `{}` on error or empty state |
| `saveProfiles(profiles)` | Serializes the full profiles object and writes it back to `localStorage` |
| `openProfilesModal()` | Renders the profiles list and shows the profiles modal |
| `closeProfilesModal()` | Hides the profiles modal |
| `renderProfilesList()` | Iterates all saved profiles and injects them as `profile-item` cards into the modal; shows an empty-state message when no profiles exist |
| `saveProfile()` | Reads the profile name input and the three config fields, merges them into the profiles object, and persists via `saveProfiles()` |
| `loadProfile(name)` | Restores `vehicleWeight` and `batteryCapacity` fields, updates the `batteryKwh` display via `updateBattery()`, syncs the GPS polling segmented control by toggling the matching `.active` segment, and restores the saved Light/Dark theme preference by calling `toggleTheme()` if the stored `theme` value differs from the current one |
| `deleteProfile(name)` | Removes the named key from the profiles object and refreshes the list |

### 🔄 Load Behavior

When a profile is loaded via `loadProfile()`, the UI is updated atomically:

1. `vehicleWeight` input value is set directly.
2. `batteryCapacity` input value is set, then `updateBattery()` is called to refresh the SOC bar and recompute the range estimate.
3. The GPS polling segmented control iterates all `.segment` buttons in `#gpsPollingGroup`, removes the `active` class from all of them, and re-applies it to the button whose `data-value` attribute matches the stored `gpsPolling` value. The hidden `#gpsPolling` input is also updated to keep it in sync.
4. If the profile contains a `theme` value that differs from the current `currentTheme`, `toggleTheme()` is called to switch the UI to the saved Light/Dark mode.
5. The modal is closed automatically.

### 🖥️ UI Entry Point

The profiles modal is accessible from the **👤 button** in the application header. The modal contains:

- A scrollable list of saved profile cards, each showing the profile name and a compact summary (`Weight · GPS · Battery · Theme`), along with **Load** and **✕ (Delete)** action buttons.
- A text input field (max 40 characters) and a **💾 Save Current** button to persist the active configuration under a new name.

---

## 🎨 UI & Theming

### 🌙 Dark / Light Mode

Themes are implemented entirely via **CSS custom properties** on the `<body>` element's `data-theme` attribute. Toggling calls `toggleTheme()` which flips `currentTheme` and re-runs `updateChartTheme()` to recolor Chart.js axes and grid lines programmatically.

**☀️ Light theme** key variables:

```css
--bg-color: #f0f2f5;
--card-bg: #ffffff;
--text-color: #0d0d12;
```

**🌙 Dark theme** key variables:

```css
--bg-color: #080b10;
--card-bg: #0f1318;
--text-color: #e8edf2;
```

The MapLibre GL map style is switched per theme at initialization time (see [Map Modes](#️-map-modes-2d--3d)):
- ☀️ **Light:** `liberty` style — vivid, high-contrast vector cartography
- 🌙 **Dark:** `dark` style — low-contrast, moody dark vector cartography

### 🖋️ Typography

| Font | Usage |
|---|---|
| `Syne` (800, 600, 400) | Headings, labels, body text |
| `JetBrains Mono` (700, 600, 400) | All numeric readouts, chart ticks, stat cards |

### 🎨 Color Palette

| Token | Hex | Role |
|---|---|---|
| `--primary` | `#00e676` | Regen, recovered energy, positive states |
| `--secondary` | `#29b6f6` | Distance, GPS indicators |
| `--danger` | `#ff1744` | Consumption, power, negative states |
| `--warning` | `#ffd740` | Altitude, grade |
| `--tesla-red` | `#e21017` | App branding, route polyline |
| `--accent-purple` | `#b39ddb` | Speed chart, net energy |

### 📐 Layout Structure

```
┌─────────────────────── HEADER ─────────────────────────┐
│  🔴 TRIP MASTER          [👤][🧮] [☀️/🌙] [⭐]      │
├──────────────── CONFIG GRID (4 cols) ──────────────────┤
│  Weight │ Temp Efficiency │ Headwind │ GPS Polling     │
├──────────────── STAT CARDS (8 cols) ───────────────────┤
│ Dist │ Avg Spd │ Cons │ Regen │ Alt │ Grade │ Pwr │ ⏱ │
├──────────────── RANGE ESTIMATOR ───────────────────────┤
│  [kWh] [SOC%] [═══Battery Bar═══] [Range] [Remaining]  │
├────────────── MAP ──────┬───── CHARTS PANEL ───────────┤
│                         │  Elevation Profile           │
│  MapLibre GL 2D / 3D    │  Consumption vs Distance     │
│  Route Map              │  Speed Profile               │
│  [3D ↔ 2D toggle btn]   │  Energy Balance              │
│                         │  Power Breakdown             │
│                         │  Weather Panel               │
├─────────────────────── CONTROLS ───────────────────────┤
│           [▶ Start Trip]    [⏹ Stop Trip]             │
└────────────────────────────────────────────────────────┘
```

---

## 📱 Progressive Web App

Trip Master ships as a fully installable PWA.

### 📄 Web Manifest (`manifest.json`)

Enables the "Add to Home Screen" prompt on Android and iOS. Configures:
- 📛 App name: **Trip Master**
- 🖥️ Display mode: `standalone` (full-screen, no browser chrome)
- 🎨 Status bar: `black-translucent`
- 🖼️ Icons: `icon-192x192.png`, `favicon.ico`

### 🔧 Service Worker (`sw.js`)

Registered in the `load` event listener:

```javascript
navigator.serviceWorker.register('/sw.js')
```

Provides:
- 📦 **Offline caching** of the app shell
- 🔁 **Background sync** capability
- 🚀 Enables re-launch without an internet connection

### 🔒 Wake Lock API

On initialization, Trip Master requests a **screen wake lock**:

```javascript
navigator.wakeLock.request('screen')
```

This prevents the device OS from dimming or locking the screen during active trip recording — critical for long-distance EV journeys.

---

## 📊 Stat Cards Reference

Eight real-time stat cards are updated via `refreshUI()` on every valid GPS segment:

| # | Label | ID | Unit | Formula |
|---|---|---|---|---|
| 1 | 🗺️ Trip Distance | `distDisplay` | Km | $D_{\text{total}} / 1000$ |
| 2 | 🏎️ Average Speed | `avgSpeedDisplay` | Km/h | $D\,\text{(Km)} / t\,\text{(h)}$ |
| 3 | ⚡ Run Consumption | `consDisplay` | Wh/Km | $\lfloor E_{\text{step}} / d + 0.5 \rfloor$ |
| 4 | ♻️ Brake Regen | `regenDisplay` | Wh | $\sum E_{\text{regen}} \cdot 0.70$ |
| 5 | ⛰️ Route Altitude | `altDisplay` | m | `pos.coords.altitude` |
| 6 | 📐 Route Grade | `gradeDisplay` | % | $\Delta h / d \times 100$ |
| 7 | 🔌 Estimated Power | `powerDisplay` | W | $E_{\text{step}} / (\Delta t / 3600)$ |
| 8 | ⏱️ Trip Time | `tripTimeDisplay` | HH:MM:SS | wall-clock from `setInterval` |

---

## 🏁 Trip Summary & Efficiency Scoring

Clicking the **📋 Summary** button opens a modal with a post-trip analytics snapshot. It is available only when `totalDistance > 10 m`.

### 📋 Summary Fields

| Metric | Formula |
|---|---|
| 🗺️ Total Distance | $D_{\text{total}} / 1000$ (Km) |
| ⏱️ Trip Duration | HH:MM:SS from `tripSeconds` |
| ⚡ Avg Consumption | $E_{\text{consumed,total}} / D_{\text{total}}\,\text{(Km)}$ (Wh/Km) |
| 🔋 Total Consumed | $E_{\text{consumed,total}}$ (Wh) |
| ♻️ Total Recovered | $E_{\text{regen,total}}$ (Wh) |
| 📈 Regen Efficiency | $E_{\text{regen}} / E_{\text{consumed}} \times 100$ (%) |
| 📍 Data Points | `altChart.data.datasets[0].data.length` |
| 🔌 Net Energy | $E_{\text{consumed}} - E_{\text{regen}}$ (Wh) |

### 🏆 Efficiency Badge

The average consumption $\bar{C}$ (Wh/Km) triggers one of three badges:

| Condition | Badge |
|---|---|
| $\bar{C} < 150\ \text{Wh/Km}$ | 🏆 **Excellent Efficiency** |
| $150 \leq \bar{C} < 220\ \text{Wh/Km}$ | 👍 **Good Efficiency** |
| $\bar{C} \geq 220\ \text{Wh/Km}$ | ⚡ **High Consumption** |

---

## 🗺️ Map Modes: 2D & 3D

Trip Master provides two distinct map rendering modes that can be toggled at any time during a trip — even while recording is active. **Both modes are powered by MapLibre GL JS**, using a single WebGL-based rendering engine with OpenFreeMap vector tiles. The two modes share the same GPS coordinate stream and the same GeoJSON route data source.

### 🔄 Toggle Button

A floating **`3D` / `2D` button** is permanently overlaid in the **top-right corner** of the map panel. Clicking it switches between modes instantly:

- 🗺️ **Label `3D`** → the map is currently in **2D mode**; clicking will activate the 3D view
- 🌐 **Label `2D`** (highlighted in `--secondary` blue) → the map is currently in **3D mode**; clicking will return to the flat 2D view

```
┌─────────── MAP WRAPPER ────────────────┐
│                              ┌───────┐ │
│   (map content here)         │  3D   │ │  ← toggle button (top-right)
│                              └───────┘ │
└────────────────────────────────────────┘
```

---

### 🗺️ 2D Mode — MapLibre GL + OpenFreeMap

The default map mode uses **MapLibre GL JS v4.7.1** rendering a flat, top-down vector map. This is a fully WebGL-rendered view with no raster tile fallback.

| 🔧 Property | 📋 Value |
|---|---|
| 🏗️ Engine | MapLibre GL JS `4.7.1` |
| 🌍 Tile provider | OpenFreeMap |
| ☀️ Light style | `https://tiles.openfreemap.org/styles/liberty` |
| 🌙 Dark style | `https://tiles.openfreemap.org/styles/dark` |
| 📐 Camera pitch | `0°` (flat top-down view) |
| 🧭 Camera bearing | `0°` (north-up) |
| ✨ Antialiasing | `true` |
| 🛣️ Route layer type | `line` (GeoJSON `LineString`) — source ID `trip-path-2d` |
| 🎨 Route color | `#e21017` |
| 📏 Route line width | `5` px |
| 🔍 Initial zoom | `15` (set on first GPS fix) |
| 🧭 Map follows GPS | `map.setCenter([longitude, latitude])` on each GPS step |

The 2D map is contained in the `<div id="map">` element and initialized at page load via `setupMap()`. The route is built incrementally: each new GPS coordinate is pushed into the shared `map3dCoords` buffer and applied to the GeoJSON source via `pathLine.setData(...)`.

---

### 🌐 3D Mode — MapLibre GL + OpenFreeMap

The 3D mode reuses **MapLibre GL JS v4.7.1** with a pitched, tilted camera that gives a perspective-projected terrain view. It uses the same tile provider and the same GeoJSON route data as the 2D mode.

| 🔧 Property | 📋 Value |
|---|---|
| 🏗️ Engine | MapLibre GL JS `4.7.1` |
| 🌍 Tile provider | OpenFreeMap |
| ☀️ Light style | `https://tiles.openfreemap.org/styles/liberty` |
| 🌙 Dark style | `https://tiles.openfreemap.org/styles/dark` |
| 📐 Camera pitch | `60°` (tilted perspective) |
| 🧭 Camera bearing | `-20°` (slightly rotated north) |
| ✨ Antialiasing | `true` (smooth WebGL rendering) |
| 🛣️ Route layer type | `line` (GeoJSON `LineString`) — source ID `trip-path` |
| 🎨 Route color | `#e21017` |
| 📏 Route line width | `5` px |
| 🔍 Initial zoom | `15` |

The 3D map is rendered inside `<div id="map3d">`, which is overlaid absolutely on top of the 2D map container via `z-index: 5` and initially hidden (`display: none`). When 3D mode is activated, the 2D `#map` is hidden and `#map3d` is revealed.

#### 🏗️ Initialization — `setupMap()` and `setup3DMap(lat, lng)`

- The **2D map** (`#map`) is initialized unconditionally at page load via `setupMap()`. It is always ready and consumes minimal GPU resources when hidden.
- The **3D map** (`#map3d`) is **lazily initialized** on the first activation — it is not created at page load. This preserves WebGL context budget and avoids resource allocation when the user never switches to 3D mode.
- On subsequent activations (after the first), the 3D map is **not re-created**. Instead, only the center position and route data are refreshed.

#### 🔄 Toggle Logic — `toggle3DMap()`

| 🔀 Direction | ⚙️ Actions |
|---|---|
| ➡️ **2D → 3D** | Sets `is3DMode = true` · Changes button label to `2D` · Adds `.active` CSS class · Hides `#map` · Shows `#map3d` · Initializes or recenters the 3D MapLibre instance |
| ⬅️ **3D → 2D** | Sets `is3DMode = false` · Changes button label to `3D` · Removes `.active` CSS class · Hides `#map3d` · Shows `#map` · The 2D MapLibre map resumes rendering immediately from its preserved state |

> ✅ **Note:** Unlike raster-based map libraries, MapLibre GL JS does not require an explicit resize/invalidation call when the container is re-shown. The WebGL canvas re-renders correctly as soon as the element becomes visible again.

---

### 📡 Live Route Synchronization

Both map modes consume the **same coordinate buffer**: `map3dCoords` — an array of `[longitude, latitude]` pairs accumulated at every GPS fix.

```
GPS Fix → map3dCoords.push([lng, lat])
             │
             ├─► 2D map: pathLine.setData({ type: 'LineString', coordinates: map3dCoords })
             └─► 3D map: map3dSource.setData({ type: 'LineString', coordinates: map3dCoords })
```

This ensures that switching between 2D and 3D at any point during a trip displays the **complete route recorded so far** in both views without any data loss or re-processing.

---

### 🎨 Theme-Aware Map Styles

Both the 2D and 3D MapLibre instances select their vector tile style based on the active UI theme at initialization time:

| 🌙 Theme | 🗺️ MapLibre Style | 🏷️ Description |
|---|---|---|
| ☀️ Light | `https://tiles.openfreemap.org/styles/liberty` | Bright, detailed vector cartography |
| 🌙 Dark | `https://tiles.openfreemap.org/styles/dark` | Low-contrast, dark vector cartography |

> 💡 **Tip:** If you switch themes **after** a map instance has already been initialized, the map style is updated live via `map.setStyle()` / `map3d.setStyle()` and the route GeoJSON layer is re-injected automatically via the `styledata` event listener. No manual toggle is required.

---

### 📦 Map State Variables

| 🔤 Variable | 📋 Type | 📖 Description |
|---|---|---|
| `map` | `maplibregl.Map` | MapLibre GL instance for the 2D flat view; initialized at page load |
| `pathLine` | `GeoJSONSource \| null` | Reference to the `trip-path-2d` GeoJSON source for live 2D route updates |
| `map3d` | `maplibregl.Map \| null` | MapLibre GL instance for the 3D perspective view; `null` until first 3D activation |
| `map3dSource` | `GeoJSONSource \| null` | Reference to the `trip-path` GeoJSON source for live 3D route updates |
| `is3DMode` | `boolean` | `true` while the 3D view is active |
| `map3dCoords` | `[number, number][]` | Shared coordinate buffer (`[lng, lat]` pairs) consumed by both map instances |

---

## 📦 Dependencies

All dependencies are loaded from CDN — no `npm install` required.

| Library | Version | Purpose | CDN |
|---|---|---|---|
| 🌐 MapLibre GL JS | `4.7.1` | WebGL-powered vector map engine for both 2D and 3D modes | unpkg |
| 📊 Chart.js | `latest` | All real-time charts | jsDelivr |
| 📌 chartjs-plugin-annotation | `3.0.1` | Zero-baseline line on charts | jsDelivr |
| 🌦️ Open-Meteo API | — | Live weather data | Free REST API |
| 🌍 OpenFreeMap Tiles | — | Vector map styles (`liberty` / `dark`) for both 2D and 3D | OpenFreeMap CDN |
| 🔤 Google Fonts (Syne) | — | UI typography | Google CDN |
| 🔤 Google Fonts (JetBrains Mono) | — | Numeric readouts | Google CDN |

> 🚫 **No Leaflet.js.** The entire mapping stack — both flat 2D and perspective 3D — is handled by a single MapLibre GL JS instance per view, with no secondary mapping library.

---

## 🚀 Getting Started

### 🛠️ Prerequisites

- 🌐 A modern browser (Chrome 80+, Firefox 75+, Safari 14+, Edge 80+) with WebGL support
- 🔐 HTTPS host (required for Geolocation API in production)
- 📂 `manifest.json`, `sw.js`, `icon-192x192.png`, `favicon.ico` in the same directory

### 💻 Local Development

```bash
# Clone or download the project
git clone https://github.com/your-username/trip-master.git
cd trip-master

# Serve over HTTPS locally (required for GPS)
npx serve .
# or
python3 -m http.server 8080
```

> ⚠️ **Note:** The Geolocation API requires a **secure context** (`https://` or `localhost`). Serving over plain `http://` on a remote host will not work.

### 🌐 Production Deployment

Upload the following files to any static web host (GitHub Pages, Netlify, Vercel, Cloudflare Pages):

```
trip-master/
├── index.html        ← Main application (all JS, CSS, and map logic)
├── manifest.json     ← PWA manifest
├── sw.js             ← Service Worker
├── favicon.ico
└── icon-192x192.png
```

> 🗺️ **No tile server required.** Map tiles are served on-demand by OpenFreeMap's public CDN directly to the browser.

---

## 📐 Mathematical Reference

A consolidated reference of all formulas used in the application.

### 🌍 Haversine Distance

$$a = \sin^2\left(\frac{\Delta\phi}{2}\right) + \cos\phi_1 \cdot \cos\phi_2 \cdot \sin^2\left(\frac{\Delta\lambda}{2}\right)$$

$$d = 2R \cdot \mathrm{arctan2}\left(\sqrt{a},\ \sqrt{1 - a}\right) $$

### ⚡ Total Segment Energy

$$E_{\text{step}} = \frac{120 + 0.8\,v_w + 0.012\,m}{\eta_T} \cdot d + \frac{m \cdot 9.81 \cdot \Delta h}{3600}$$

### ♻️ Regen Branch

$$E_{\text{regen}} = \left|E_{\text{step}}\right| \cdot 0.70 \quad \text{if } E_{\text{step}} < 0$$

### 🔌 Instantaneous Power

$$P = \frac{E_{\text{step}}}{\Delta t / 3600}$$

### 🔋 Estimated Range

$$R = \frac{C_{\text{bat}} \times 10^3 \times \text{SOC}/100}{\bar{C}_{\text{Wh/Km}}}$$

### 📈 Regen Efficiency

$$\eta_{\text{regen}} = \frac{\sum E_{\text{regen}}}{\sum E_{\text{consumed}}} \times 100$$

### 📐 Road Grade

$$G = \frac{\Delta h}{d} \times 100$$

---

## 📄 License

Distributed under the **MIT License**. Feel free to use, modify, and share.

---

> _⚡ Developed for the sustainable mobility community. If you find this tool helpful, please leave a ⭐ on GitHub!_
