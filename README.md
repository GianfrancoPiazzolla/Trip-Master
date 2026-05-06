<div align="center">

# 🚗 Trip Master

### Real-Time EV Trip Computer & Energy Analytics Dashboard

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![MapLibre GL](https://img.shields.io/badge/MapLibre%20GL-396CB2?style=for-the-badge&logo=maplibre&logoColor=white)](https://maplibre.org/)
[![Chart.js](https://img.shields.io/badge/Chart.js-FF6384?style=for-the-badge&logo=chartdotjs&logoColor=white)](https://www.chartjs.org/)
[![PWA](https://img.shields.io/badge/PWA-5A0FC8?style=for-the-badge&logo=pwa&logoColor=white)](https://web.dev/progressive-web-apps/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)

> A **single-file Progressive Web App** that turns any smartphone or browser into a professional-grade electric vehicle trip computer — tracking GPS position, computing physics-based energy consumption in real time, visualizing live charts, and displaying live weather data.

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
11. [Last Settings Auto-Save](#-last-settings-auto-save)
12. [UI & Theming](#-ui--theming)
13. [Progressive Web App](#-progressive-web-app)
14. [Stat Cards Reference](#-stat-cards-reference)
15. [Trip Summary Modal](#-trip-summary--efficiency-scoring)
16. [Map Modes: 2D & 3D](#️-map-modes-2d--3d)
17. [GPS Position Marker](#-gps-position-marker)
18. [Start & End Markers](#-start--end-markers)
19. [Map Zoom Controls](#-map-zoom-controls)
20. [Map Fullscreen Mode](#️-map-fullscreen-mode)
21. [Heading Mode](#-heading-mode)
22. [POI Overlay](#-poi-overlay)
23. [POI Panel Minimize & Expand](#-poi-panel-minimize--expand)
24. [POI Watchdog System](#-poi-watchdog-system)
25. [POI Map Synchronization](#-poi-map-synchronization)
26. [POI Overlay Switch on Map Mode Change](#-poi-overlay-switch-on-map-mode-change)
27. [POI Preference Persistence](#-poi-preference-persistence)
28. [Battery SOC Auto-Update](#-battery-soc-auto-update)
29. [Blue GPS Position Marker](#-gps-position-marker)
30. [Trip Time Display](#-trip-time-display)
31. [Dark Theme Map Filter](#-dark-theme-map-filter)
32. [Stepper Buttons](#-stepper-buttons)
33. [Action Button Shine Effect](#-action-button-shine-effect)
34. [Weather Pictogram Mapping](#️-weather-pictogram-mapping)
35. [Automated Headwind Calculation](#-automated-headwind-calculation)
36. [Wind Direction Display](#-wind-direction-display)
36. [Modal Click-Outside-To-Close](#-modal-click-outside-to-close)
37. [Energy Balance Chart Gradient Bars](#-energy-balance-chart-gradient-bars)
38. [Energy Flow Dashboard](#️-energy-flow-dashboard)
39. [Driving Style Analyzer](#-driving-style-analyzer)
40. [Real-Time Cost Meter](#-real-time-cost-meter)
41. [Responsive Layout Adaptations](#-responsive-layout-adaptations)
42. [Card Folding & Maximized Map View](#-card-folding--maximized-map-view)
43. [Dependencies](#-dependencies)
44. [Getting Started](#-getting-started)
45. [Mathematical Reference](#-mathematical-reference)

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
| 🧭 **Heading / North-Up Toggle** | One-click button to switch the active map between heading-up (travel direction) and north-up orientation |
| ↕️ **Map Fullscreen Mode** | One-click button to expand the map to the full viewport, hiding all UI panels |
| 🔍 **Map Zoom Controls** | Floating `−` / `⊕` / `+` buttons to zoom out, re-center on GPS, or zoom in on the active map |
| 📍 **Live GPS Position Marker** | Custom blue dot marker tracking real-time position on both 2D and 3D maps |
| 🟢 **Start & End Markers** | Green `S` and red `E` circular markers placed automatically at the first and last coordinate of any imported trip file |
| 📊 **4 Live Charts** | Elevation profile, heat-map style consumption profile, speed profile, energy balance |
| 🌡️ **Live Weather Panel** | Auto-fetches Open-Meteo for temperature, humidity, wind, and pressure |
| 🌧️ **Weather Radar Overlay** | One-click RainViewer precipitation radar projected on both 2D and 3D maps |
| 📌 **POI Overlay** | One-click overlay showing Road Closures, Mobile Patrols, Speed Cameras, and EV Charging stations on both 2D and 3D maps, sourced from OpenStreetMap Overpass API and Waze Live Map |
| 🗂️ **POI Panel Auto-Minimize** | The POI layer selection panel auto-minimizes after 5 seconds of inactivity and expands on click |
| 🐕 **POI Watchdog** | Background timer that detects and automatically re-plots missing POI markers if they fail to appear |
| 🔁 **POI Map Sync** | Synchronizes POI markers from one map instance to the other when switching between 2D and 3D modes |
| 🌙 **Dark / Light Theme** | Full dual-theme UI with smooth CSS variable transitions |
| 📱 **PWA / Installable** | Service Worker + Web Manifest for offline use and home-screen install |
| 💰 **Real-time Cost Meter** | Tracks electricity costs and compares savings against ICE vehicles using live fuel prices |
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

### ⚡ Consumption Profile

- **Type:** Line chart with **Heat-Map Style** segment coloring 🌈
- **X-axis:** Distance traveled [Km] 🏁
- **Y-axis:** Instantaneous consumption [Wh/Km] ⚡
- **Dynamic Segment Coloring:** The chart line uses a **real-time segment engine**. Each individual line segment is dynamically colored to match the **exact same color scale** used by the map's route heat map (see [Heat Color Scale](#-heat-color-scale)). 🎨
- **Visual Synchronization:** This creates a unified visual language across the dashboard, allowing the driver to instantly correlate geographical peaks on the map with telemetry peaks on the chart using identical colors. 🔗
- **Adaptive Area Fill:** The area under the line is also dynamically filled with a matching translucent version of the segment color (20% opacity), providing a rich, multi-colored area chart effect. 🌊
- **Zero-baseline annotation:** A horizontal line is drawn at $y = 0$ (via `chartjs-plugin-annotation`), making it easy to distinguish between energy consumption (above the line) and regenerative braking / energy recovery (below the line). ♻️

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

## ⚡️ Energy Flow Dashboard

Trip Master provides two complementary real-time visualizations that give drivers immediate insight into energy consumption: a **live energy flow diagram** showing power distribution between vehicle components, and a **color-coded heat map** applied directly on the route polyline to identify high-consumption segments at a glance.

---

### ⚡️ Live Energy Flow Diagram

A **SVG-based live diagram** renders the instantaneous power flow between the battery, motor, wheels, HVAC system, and auxiliary loads. It is updated at every valid GPS fix via `updateEnergyFlow(instantPowerW, regenW, tempC)`.

#### 📐 SVG Layout

```
┌───────────────────────────────────────────────────┐
│                                                   │
│   ┌─────────┐                      ┌─────────┐    │
│   │    🔋   │                      │    🧿   │    │
│   │ Battery │═════ ⚡ Motor ══════►│ Wheels  │    │
│   │         │  (⚡ Motor Power W)  │         │    │
│   │         │                      │         │    │
│   └────╬────┘                      └─────────┘    │
│        ║                                          │
│        ║ ❄️ HVAC                                  │
│        ║ (HVAC Power W)                           │
│        ▼                                          │
│   ┌─────────┐                      ┌─────────┐    │
│   │   ❄️    │                      │   💡    │    │
│   │  HVAC   │══════════════════════│  Aux    │    │
│   │         │                      │  300W   │    │
│   └─────────┘                      └─────────┘    │
│                                                   │
│   ↩ Regen (green arrow, when braking)             │
│                                                   │
└───────────────────────────────────────────────────┘
```

#### 🔢 Energy Distribution Formulas

| Component | Emoji | Formula | Description |
|---|---|---|---|
| Battery | 🔋 | — | Source/sink node |
| Motor | ⚡ | `motorW = max(0, instantPowerW)` | Instantaneous power to motor [W] |
| Wheels | 🧿 | — | Output/mechanical node |
| HVAC | ❄️ | `hvacW = max(0, abs(tempC - 22) × 50)` | HVAC load — 50W per °C deviation from 22°C |
| Aux | 💡 | `auxW = 300` | Fixed auxiliary load [W] (infotainment, lights, etc.) |
| Regen | ↩ | `regenW = lastInstantPowerW < 0 ? abs(lastInstantPowerW) × 0.7 : 0` | Regenerative braking power [W] |

#### 🎨 Flow Line Styling

Flow lines use **linear gradients** whose thickness is proportional to power:

```javascript
// Motor flow line (Battery → Motor → Wheels)
stroke-width = max(2, (motorW / totalDraw) × 6)

// HVAC flow line (Battery → HVAC)
stroke-width = max(1, (hvacW / totalDraw) × 4)

// Regen arrow (Wheels → Battery, when braking)
stroke-width = max(2, (regenW / totalDraw) × 6)
```

| Line | Gradient | Direction | Width Factor |
|---|---|---|---|
| 🔴 Motor | `#ff1744` → `#ff5252` | Left → Right | ×6 |
| 🔵 HVAC | `#29b6f6` → `#0288d1` | Left → Right | ×4 |
| 🟢 Regen | `#00e676` → `#69f0ae` | Right → Left (reverse!) | ×6 + glow |

#### 🌙 Theme Adaptation

All SVG colors adapt to the active UI theme:

| Element | 🌙 Dark | ☀️ Light |
|---|---|---|
| Node background | `#1a2030` | `#e8eaed` |
| Node border | `#2a3040` | `#d0d4da` |
| Text color | `#e8edf2` | `#0d0d12` |
| Subtext color | `#4a5568` | `#8892a0` |

#### 🔄 Update Frequency

`updateEnergyFlow()` is called from `updateFeatures()` at every valid GPS fix (after the 5 m displacement filter):

---

### 🗺️ Route Heat Map

Each GPS segment is **individually colored** on the 2D/3D map based on its instantaneous energy consumption, creating a continuous gradient that highlights efficient vs. energy-intensive segments at a glance.

#### 🎨 Heat Color Scale

| Consumption (Wh/Km) | Color | Hex | Meaning |
|---|---|---|---|
| < 0 | 🔵 Blue | `#29b6f6` | Regenerative braking active |
| 0 – 120 | 🟢 Green | `#00e676` | Highly efficient |
| 120 – 180 | 🟢 Light green | `#69f0ae` | Efficient |
| 180 – 250 | 🟡 Yellow | `#ffff00` | Moderate consumption |
| 250 – 350 | 🟠 Orange | `#ff9100` | High consumption |
| > 350 | 🔴 Red | `#ff1744` | Very high consumption |

```javascript
function getHeatColor(consWhKm) {
    if (consWhKm < 0)   return '#29b6f6';  // 🔵 Regen
    if (consWhKm < 120) return '#00e676';  // 🟢 Excellent
    if (consWhKm < 180) return '#69f0ae';  // 🟢 Good
    if (consWhKm < 250) return '#ffff00';  // 🟡 Moderate
    if (consWhKm < 350) return '#ff9100';  // 🟠 High
    return '#ff1744';                      // 🔴 Very high
}
```

#### 📍 Visual Pattern

The heat map reveals driving patterns instantly:
- **Downhill stretches** → 🔵 blue segments (energy recovered)
- **Uphill climbs** → 🔴 red/🟠 orange segments (high drain)
- **Flat cruise** → 🟢 green segments (efficient steady-state)
- **City traffic** → 🟢 mixed green/🟡 yellow (frequent stops, regen bursts)

#### 🚄 Tiered Rendering Architecture (Optimized)

Unlike standard implementations that re-render the entire path on every update, Trip Master uses a **high-performance tiered rendering strategy** to ensure 60 FPS fluid performance even on long trips:

- ⚡ **Live Source (`route-heatmap-live`):** Stores only the most recent **10 segments**. This source is updated on every GPS fix. Since it is extremely small, `setData()` operations are near-instantaneous.
- 🏗️ **Static Source (`route-heatmap-static`):** Once the live buffer reaches its limit (**Batch Size = 10**), segments are consolidated into the static source. This source is updated 10x less frequently, drastically reducing CPU overhead and battery drain.
- 🚀 **Hardware Acceleration:** By splitting the data, we minimize the time spent in GeoJSON serialization and WebGL tessellation, preventing UI "stuttering" during active tracking.

> 💡 **Note:** Segments accumulate for the entire trip duration. The heat map is not reset between GPS fixes — each segment is permanent and layered sequentially on the map.

---

## 🎯 Driving Style Analyzer

Trip Master continuously evaluates driving behavior across **three independent dimensions** and computes an **overall Driving Score (0–100)**, displayed as both a set of progress bars and a semi-circular gauge.

---

### 🎯 Scoring Dimensions

The `drivingStyle` state object tracks three scores simultaneously:

```javascript
let drivingStyle = {
    accelScore:  100,    // Acceleration bias score
    brakeScore:  100,    // Braking bias score
    smoothScore: 100,    // Speed smoothness score
    accelEvents: 0,      // Count of aggressive acceleration events
    brakeEvents: 0,      // Count of hard braking events
    speedVarSum: 0,      // Running sum of speed samples
    speedSamples: 0,     // Number of speed samples
    lastSpeedForAccel: 0 // Previous speed for delta calculation
};
```

#### 📐 Scoring Algorithm

| Score | Trigger | Penalty Formula | Notes |
|---|---|---|---|
| **Acceleration Bias** | `abs(Δspeed) > 15 km/h` | `accelScore -= abs(Δspeed) × 0.5` | Measures aggressive throttle usage |
| **Braking Bias** | `Δspeed < 0` AND `abs(Δspeed) > 10 km/h` | `brakeScore -= abs(Δspeed) × 0.3` | Measures hard deceleration |
| **Smoothness Bias** | Every sample | `smoothScore -= abs(speed - avgSpeed) × 0.05` | Measures speed consistency |

**Natural recovery:** All scores slowly recover toward 100 over time:
```javascript
ds.accelScore  = Math.min(100, ds.accelScore  + 0.02);
ds.brakeScore  = Math.min(100, ds.brakeScore  + 0.02);
ds.smoothScore = Math.min(100, ds.smoothScore + 0.02);
```

**Overall Score:**
```javascript
overall = Math.round((accelScore + brakeScore + smoothScore) / 3);
```

#### 🏆 Score Badges

| Overall Score | Badge | Color | Meaning |
|---|---|---|---|
| ≥ 80 | 🏆 **Excellent** | 🟢 `var(--primary)` | Smooth, efficient driving |
| ≥ 60 | 👍 **Good** | 🟡 `var(--warning)` | Generally acceptable driving |
| < 60 | ⚡ **Aggressive** | 🔴 `var(--danger)` | Heavy acceleration/braking |

---

### 📊 UI Components

#### 📐 Driving Score Card Layout

```
┌───────────────────────────────────────────────────────────┐
│  🎯 Driving Style Analyzer                                │
│  ┌────────────────────────────────────┐  ┌─────────────┐  │
│  │ Acceleration  ████████████░░  85   │  │    ╭───╮    │  │
│  │ Braking       ██████████████  100  │  │   ╱ 82  ╲   │  │
│  │ Smoothness    ████████░░░░░░  60   │  │  ╱ SCORE    │  │
│  └────────────────────────────────────┘  └─────────────┘  │
└───────────────────────────────────────────────────────────┘
```

| Element | ID | Description |
|---|---|---|
| Accel bar + value | `#dsAccelBar`, `#dsAccelVal` | Width = `accelScore%`, text = `score/100` |
| Brake bar + value | `#dsBrakeBar`, `#dsBrakeVal` | Width = `brakeScore%`, text = `score/100` |
| Smooth bar + value | `#dsSmoothBar`, `#dsSmoothVal` | Width = `smoothScore%`, text = `score/100` |
| Badge | `#dsBadge` | Shows 🏆/👍/⚡ with color coding |
| Gauge SVG | `#dsGaugeSvg` | Semi-circular arc gauge |

#### 🎨 Gauge Visualization

The **semi-circular SVG gauge** (`#dsGaugeSvg`, viewBox: 0 0 100 60) draws an arc from 180° to 360°:

```javascript
// Arc color based on score
if (score >= 80) arcColor = '#00e676';  // 🟢 Green
else if (score >= 60) arcColor = '#ffd740';  // 🟡 Yellow
else arcColor = '#ff1744';  // 🔴 Red

// Arc angle = (score / 100) × 180°
const angle = (score / 100) * 180;
```

The gauge includes a **glow filter** (`#gaugeGlow`) for the score arc and uses `JetBrains Mono` for the numeric display.

---

### 🔄 Update Frequency

`updateDrivingStyle(speedKmh)` is called from `updateFeatures()` at every valid GPS fix:

---
## 💰 Real-Time Cost Meter

Trip Master features a **dynamic financial analytics engine** that calculates the real-time cost of your trip and provides a direct comparison with equivalent internal combustion engine (ICE) vehicle costs.

### 📉 Live Fuel Price Integration ⛽

To provide accurate comparisons, the app automatically fetches the latest **average diesel prices** (Italy) from external APIs:
- **Source:** `fuel-prices.eu` 📡
- **Update Frequency:** Every 6 hours (cached in `localStorage`) ⏱️
- **Fallback:** Uses a baseline of **1.80 €/L** if the API is unreachable 🛠️

### 🏎️ ICE Efficiency Calibration 🧪

The app derives a "typical" ICE efficiency based on official **EEA (European Environment Agency)** CO2 performance data:
- **Source:** EEA CO2 emissions reports 📄
- **Logic:** Converts average $g\text{CO}_2/\text{km}$ targets into a real-world adjusted **Km/L** figure (defaulting to ~17.2 Km/L for modern diesel fleets) 📉

### 🔢 Financial Formulas 🧮

| Metric | Formula | Description |
|---|---|---|
| 💶 **Trip Cost** | $E_{\text{kWh}} \times \text{ElecPrice}$ | Total cost of electricity consumed so far |
| 🛣️ **Cost per Km** | $\text{Trip Cost} / \text{Distance}$ | Real-time unit cost of travel |
| ⛽ **Equivalent ICE Cost** | $(\text{Distance} / \text{ICE Efficiency}) \times \text{Fuel Price}$ | Estimated cost for a diesel vehicle |
| 🤑 **Money Saved** | $\text{ICE Cost} - \text{Trip Cost}$ | Financial gain of driving electric |

### 🎨 Visual Indicators 📈

The cost data is displayed in a dedicated panel and in the final trip summary, using **dynamic coloring**:
- 🟢 **Green:** Positive savings (Electric is cheaper)
- 🔴 **Red:** Higher cost than ICE (Rare, but possible with high electricity prices)

---

## 🌡️ Weather Integration

Trip Master provides two complementary weather visualization features: a **Weather Condition Panel** that displays real-time meteorological data fetched from Open-Meteo, and a **Weather Radar Overlay** that projects live precipitation radar tiles directly onto the 2D and 3D maps using the RainViewer API.

---

### 🌤️ Weather Condition Panel

Trip Master integrates with the **Open-Meteo API** (free, no API key required) to fetch real-time meteorological data.

#### 🌐 API Endpoint

```
GET https://api.open-meteo.com/v1/forecast
  ?latitude={lat}
  &longitude={lon}
  &current=temperature_2m,relative_humidity_2m,weather_code,
           surface_pressure,wind_speed_10m,wind_direction_10m
  &daily=temperature_2m_max,temperature_2m_min
  &timezone=auto
```

#### 📡 Fetch Triggers

1. **On app load** — fires once when the first GPS fix is obtained.
2. **Every 2 Km of travel** — triggered when `Math.floor(totalDistance / 2000)` increments.

#### 🌬️ Weather Fields Displayed

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

#### 🌈 Delta Color Highlighting

Each weather value is compared against its previous reading. Values that have **increased** render in `--up-color` (`#00e676` green); values that have **decreased** render in `--down-color` (`#ff1744` red); unchanged values use the default text color. This delta coloring is implemented in `applyValueStyle()`.

#### 🌡️ Automatic Thermal Efficiency Calibration

On every weather sync (every ~2 km of travel), `updateEfficiencyByTemp()` auto-selects the thermal efficiency factor $\eta_T$ based on the retrieved ambient temperature, ensuring the energy model adapts to changing weather conditions throughout the trip:

| Temperature Range | $\eta_T$ | Label |
|---|---|---|
| $T \geq 20\ °C$ | $1.00$ | ✅ Nominal |
| $10\ °C \leq T < 20\ °C$ | $0.85$ | 🟡 Mild |
| $0\ °C \leq T < 10\ °C$ | $0.70$ | 🟠 Cold |
| $T < 0\ °C$ | $0.55$ | 🔴 Extreme Cold |

> ⚠️ **Manual Override Priority**: If the driver manually selects an efficiency value via the UI segmented control during a trip, the automatic calibration logic is **permanently bypassed** for the remainder of that session. The user's choice is treated as an intentional override (managed via the `isEfficiencyManualOverride` flag) and will persist until the trip is concluded with a **Stop Trip** command.

---

### 🌧️ Weather Radar Overlay

Trip Master can project a **live precipitation radar layer** directly onto both the 2D and 3D maps. The overlay is powered by the **RainViewer API** (free, no API key required) and rendered as a raster tile layer on top of the active MapLibre GL JS map instance.

#### 🔘 Toggle Button

A floating **`⛈️` button** is permanently overlaid in the **top-right area of the map panel**, between the 🌍 3D toggle and the 📌 POI overlay button:

```
┌─────────────────────────── MAP WRAPPER ────────────────────────────────┐
│    ┌───┐  ┌───┐  ┌───┐      ┌─────┐ ┌─────┐ ┌─────┐ ┌─────┐ ┌─────┐    │
│    │ − │  │🧿 │  │ + │      │ 🔺 │ │ 🌍  │ │ 📌 │ │ ⛈  │ │  ↕️ │    │
│    └───┘  └───┘  └───┘      └─────┘ └─────┘ └─────┘ └─────┘ └─────┘    │
└────────────────────────────────────────────────────────────────────────┘
```

#### 🌐 RainViewer API — Timestamp Fetch

Before the first overlay render, `fetchRainViewerTimestamp()` retrieves the timestamp of the most recent available radar frame:

```
GET https://api.rainviewer.com/public/weather-maps.json
```

The function reads `data.radar.past` and returns the `time` value of the **last element** (most recent frame). This timestamp is stored in `weatherOverlayTimestamp` and reused for subsequent overlay operations without re-fetching.

#### 🗺️ Radar Tile Source

The precipitation radar is served as standard raster tiles. The tile URL pattern used is:

```
https://tilecache.rainviewer.com/v2/radar/{timestamp}/256/{z}/{x}/{y}/2/1_1.png
```

| Parameter | Value / Description |
|---|---|
| `{timestamp}` | UNIX timestamp of the selected radar frame, obtained from the RainViewer API |
| `{z}/{x}/{y}` | Standard XYZ tile coordinates |
| Tile size | 256 px |
| Min zoom | 0 |
| Max zoom | 7 |
| Raster opacity | `0.6` |
| Attribution | `RainViewer` |

#### ⚙️ Toggle Logic — `toggleWeatherOverlay()`

```javascript
async function toggleWeatherOverlay()
```

| Direction | Actions |
|---|---|
| **Off → On** | Sets `isWeatherOverlayOn = true` · Adds `.active` CSS class to the button · Fetches the RainViewer timestamp if not yet cached · Calls `addWeatherOverlayToMap(activeMap, timestamp)` on the currently active map instance; if the map style is not yet loaded, defers via `map.once('styledata', ...)` |
| **On → Off** | Sets `isWeatherOverlayOn = false` · Removes `.active` CSS class · Calls `removeWeatherOverlayFromMap(map)` and `removeWeatherOverlayFromMap(map3d)` to clean up both map instances simultaneously |

#### 🔧 Internal Helper Functions

| Function | Description |
|---|---|
| `fetchRainViewerTimestamp()` | Async function that fetches `https://api.rainviewer.com/public/weather-maps.json` and returns the UNIX timestamp of the most recent radar frame from `data.radar.past`; returns `null` on error |
| `addWeatherOverlayToMap(targetMap, timestamp)` | Adds the `rainviewer-source` raster source and `rainviewer-layer` raster layer to `targetMap`; no-ops if the source already exists on that instance |
| `removeWeatherOverlayFromMap(targetMap)` | Removes both `rainviewer-layer` and `rainviewer-source` from `targetMap` if they exist; safe to call even if neither is present |

#### 🔄 Integration with Map Mode Switching

The radar overlay is automatically synchronized whenever the map mode or theme changes:

- **2D ↔ 3D toggle (`toggle3DMap()`):** When switching to 3D, the overlay is removed from the 2D map instance and re-applied to the 3D instance (deferred via `styledata` if needed). When switching back to 2D, the reverse applies.
- **Theme toggle (`toggleTheme()`):** After the map style is reloaded (via `map.setStyle()` / `map3d.setStyle()`), the overlay is re-injected via the `styledata` event listener if `isWeatherOverlayOn` is `true`, ensuring the radar layer survives theme changes.

#### 📦 State Variables

| Variable | Type | Description |
|---|---|---|
| `isWeatherOverlayOn` | `boolean` | `true` while the radar overlay is active; `false` when hidden |
| `weatherOverlayTimestamp` | `number \| null` | UNIX timestamp of the most recently fetched RainViewer radar frame; `null` until the first overlay activation |

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

---

## 🌬️ Automated Headwind Calculation

Trip Master features a **real-time, physics-aware automatic headwind computation** system that continuously derives the effective headwind component acting on the vehicle from live weather data and the vehicle's instantaneous travel direction. This replaces the need for the driver to manually estimate and enter a headwind value — the `#windSpeed` field is updated automatically on every weather sync and on every GPS fix where a valid heading is available.

---

### 🔄 Overview & Trigger Points

`computeAndApplyHeadwind()` is a lightweight, stateless function that is invoked from **two distinct trigger points** in the application lifecycle:

| 📍 Trigger | 🔁 Context | 🔧 Caller |
|---|---|---|
| 🌤️ **Weather sync** | Fires every ~2 Km of travel or on first GPS fix | `fetchWeather()` — immediately after storing `lastWeatherWindSpeed` and `lastWeatherWindDir` |
| 🛰️ **GPS fix** | Fires at every valid GPS segment (after the 5 m displacement filter) | `updateLocation()` — immediately after recomputing `lastHeading` from the last two coordinates |

This dual-trigger design ensures that the headwind value is **always up to date** — it adapts both when the weather changes (new wind speed/direction data) and when the vehicle changes direction (new travel bearing).

---

### 📦 State Variables

The computation depends on three module-level state variables:

| 🔤 Variable | 📋 Type | 📖 Description |
|---|---|---|
| `lastWeatherWindSpeed` | `number` | Most recently fetched wind speed from Open-Meteo [Km/h]; initialized to `0` |
| `lastWeatherWindDir` | `number \| null` | Most recently fetched meteorological wind direction from Open-Meteo [°, 0 = N, clockwise]; `null` until the first weather fetch |
| `lastHeading` | `number` | Most recently computed vehicle travel bearing [°, 0 = N, clockwise]; updated at every valid GPS step |

---

### ⚙️ `computeAndApplyHeadwind()` — Algorithm

```javascript
function computeAndApplyHeadwind() {
    if (lastWeatherWindDir === null) return;
    const windVectorDir = (lastWeatherWindDir + 180) % 360;
    const angleDiff = (lastHeading - windVectorDir + 360) % 360;
    const angleRad = angleDiff * Math.PI / 180;
    const headwindComponent = lastWeatherWindSpeed * Math.cos(angleRad);
    const headwindKmh = Math.round(headwindComponent * 10) / 10;
    document.getElementById('windSpeed').value = headwindKmh;
}
```

#### 🔢 Step-by-Step Derivation

**Step 1 — Guard clause:**

The function exits immediately if no wind direction has been received yet (`lastWeatherWindDir === null`), preventing NaN propagation into the energy model before the first weather fetch.

**Step 2 — Meteorological → mathematical wind vector direction:**

Meteorological convention defines wind direction as the azimuth *from which the wind blows* (e.g., 270° = wind coming from the West, blowing East). To compute the dot product with the vehicle's heading vector, the direction is converted to the azimuth *toward which the wind moves*:

$$\theta_{\text{wind}} = (\theta_{\text{met}} + 180°) \mod 360°$$

**Step 3 — Angular difference between vehicle heading and wind vector:**

$$\Delta\theta = (\theta_{\text{heading}} - \theta_{\text{wind}} + 360°) \mod 360°$$

The `+ 360°` and `mod 360°` idiom normalizes the result to the range $[0°, 360°)$, avoiding negative-angle ambiguity.

**Step 4 — Headwind component via dot product:**

The effective headwind speed along the vehicle's axis of travel is the projection of the wind velocity vector onto the heading direction:

$$v_{\text{headwind}} = v_{\text{wind}} \cdot \cos(\Delta\theta)$$

| $\Delta\theta$ | $\cos(\Delta\theta)$ | Physical Meaning |
|---|---|---|
| $0°$ | $+1.0$ | 💨 Pure headwind — full resistance |
| $90°$ or $270°$ | $0.0$ | ➡️ Pure crosswind — zero net component |
| $180°$ | $-1.0$ | 🔙 Pure tailwind — full assistance |
| $(0°, 90°)$ | $(0, +1)$ | 🌬️ Partial headwind |
| $(90°, 180°)$ | $(-1, 0)$ | 🍃 Partial tailwind |

**Step 5 — Rounding and UI update:**

The computed value is rounded to one decimal place and written directly to the `#windSpeed` input field:

$$v_{\text{headwind,rounded}} = \mathrm{round}(v_{\text{headwind}} \times 10) / 10$$

```javascript
document.getElementById('windSpeed').value = headwindKmh;
```

This single write immediately affects the physics engine on the very next GPS segment, since `calculatePhysics()` reads `#windSpeed` live at each step.

---

### 🔁 Data Flow Diagram

```
┌──────────────────────────────────────────────────────────────────────────────┐
│                          WEATHER SYNC (~2 Km)                                │
│                                                                              │
│  fetchWeather(lat, lon)                                                      │
│       │                                                                      │
│       ├─► lastWeatherWindSpeed = data.current.wind_speed_10m     [Km/h]      │
│       ├─► lastWeatherWindDir   = data.current.wind_direction_10m [°, met]    │
│       └─► computeAndApplyHeadwind()                                          │
│                   │                                                          │
│                   └─► #windSpeed.value = f(lastWeatherWindSpeed,             │
│                                            lastWeatherWindDir,               │
│                                            lastHeading)                      │
├──────────────────────────────────────────────────────────────────────────────┤
│                          GPS FIX (every T_poll seconds)                      │
│                                                                              │
│  updateLocation(pos)                                                         │
│       │                                                                      │
│       ├─► lastHeading = atan2(dLon, dLat) → [0°, 360°)                       │
│       └─► computeAndApplyHeadwind()                                          │
│                   │                                                          │
│                   └─► #windSpeed.value = f(lastWeatherWindSpeed,             │
│                                            lastWeatherWindDir,               │
│                                            lastHeading)   ← updated heading  │
├──────────────────────────────────────────────────────────────────────────────┤
│                    PHYSICS ENGINE (every GPS step)                           │
│                                                                              │
│  calculatePhysics()                                                          │
│       └─► vw = parseFloat(document.getElementById('windSpeed').value)        │
│               → used in E_resistance = (120 + 0.8·vw + 0.012·m) / ηT · d     │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

### ➕ Signed Value Semantics

The headwind component $v_{\text{headwind}}$ is a **signed quantity**:

- **Positive values** → actual headwind → increases `#windSpeed` → increases energy consumption in `E_resistance`
- **Negative values** → tailwind → the value written to `#windSpeed` is negative → the `0.8 · v_w · d / η_T` term in the resistance formula becomes negative, effectively reducing the computed energy cost for that segment

This means the physics engine naturally handles tailwind as an energy *benefit*, without any special-casing — simply by allowing $v_w < 0$ in the resistance formula.

> 💡 **Note:** The `#windSpeed` field remains **fully editable by the user** at any time. If the user types a manual override, it will be used for subsequent GPS steps — until the next call to `computeAndApplyHeadwind()` (triggered by the next weather sync or GPS fix) overwrites it with the freshly computed value. For stable manual control, the user should wait until after a weather sync before editing the field.

---

### 🧮 Worked Example

Suppose:
- 🌬️ Open-Meteo reports `wind_speed_10m = 30 Km/h`, `wind_direction_10m = 270°` (wind from the West, blowing East)
- 🚗 Vehicle is heading `lastHeading = 90°` (traveling East)

**Step 2:** $\theta_{\text{wind}} = (270 + 180) \mod 360 = 90°$ (wind vector points East)

**Step 3:** $\Delta\theta = (90 - 90 + 360) \mod 360 = 0°$

**Step 4:** $v_{\text{headwind}} = 30 \cdot \cos(0°) = 30 \cdot 1.0 = 30\ \text{Km/h}$

**Result:** `#windSpeed` is set to `30` → full headwind penalty applied. ✅

Now suppose the vehicle turns around and heads West (`lastHeading = 270°`):

**Step 3:** $\Delta\theta = (270 - 90 + 360) \mod 360 = 180°$

**Step 4:** $v_{\text{headwind}} = 30 \cdot \cos(180°) = 30 \cdot (-1.0) = -30\ \text{Km/h}$

**Result:** `#windSpeed` is set to `-30` → full tailwind benefit applied. 🍃

---

### ⚡ Integration with the Physics Engine

The auto-computed headwind value $v_w$ feeds directly into `calculatePhysics()` as part of the resistance energy term:

$$E_{\text{resistance}} = \frac{120 + 0.8 \cdot v_w + 0.012 \cdot m}{\eta_T} \cdot d$$

Since $v_w$ is updated at **every GPS fix** (via the heading-triggered call to `computeAndApplyHeadwind()`), the energy model is always operating with the most current aerodynamic context — even during turns, U-turns, or complex urban routes where the vehicle's heading relative to the wind changes frequently.

---

### ⚠️ Edge Cases & Guards

| 🚦 Condition | 🔒 Guard | 📋 Behavior |
|---|---|---|
| No weather data yet | `lastWeatherWindDir === null` | Function returns immediately; `#windSpeed` is not modified |
| No GPS heading yet | `lastHeading = 0` (default) | Computation proceeds using 0° (North); may be inaccurate until the first valid GPS segment |
| Wind speed = 0 | `lastWeatherWindSpeed = 0` | Output is always 0 regardless of heading; `#windSpeed` is set to 0 |
| Crosswind (90° / 270°) | $\cos(90°) = 0$ | Output is 0; no aerodynamic penalty or benefit |

---

### 🔗 Related Sections

- ⚙️ [Configuration Parameters — Headwind Speed](#️-configuration-parameters) — manual override field
- ⚙️ [Physics Engine — Resistance Energy](#️-physics-engine) — where $v_w$ is consumed
- 🌡️ [Weather Integration](#️-weather-integration) — source of `lastWeatherWindSpeed` and `lastWeatherWindDir`
- 🧭 [Heading Mode](#-heading-mode) — source of `lastHeading`

---

### ⚡️ Electricity Price

- **Input:** Numeric field (`id="elecPrice"`)
- **Default:** 0.20 €/kWh
- **Role:** Used for calculating trip cost and comparing EV expenses against ICE vehicles. This value is **saved in EV profiles** alongside vehicle weight, battery capacity, and GPS polling interval, allowing users to maintain different electricity pricing assumptions per vehicle profile.
- **Unit:** €/kWh

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

- **Battery kWh:** Numeric field with `−` / `+` stepper buttons — total usable pack energy [kWh]. The stepper calls `stepValue('batteryCapacity', ±0.5)` to increment or decrement by 0.5 kWh while respecting the field's `min`/`max` bounds.
- **SOC %:** Numeric input (0–100) with `−` / `+` stepper buttons. Each stepper call invokes `stepValue('socInput', ±1)` followed immediately by `updateBattery()` to keep the visual battery bar, the percentage label, and the range estimate in sync. The SOC percentage and the battery bar are **dynamically updated in real time** at every GPS fix by `updateBatterySoC()`: the function computes the net energy drawn (`totalConsumedWh − totalRegenWh`), derives the new SOC from the initial charge level set at trip start (`initialSoc`), writes the result back to `#socInput`, and calls `updateBattery()` to refresh both the bar fill width and the color-coded state, keeping the visual indicator always consistent with the actual energy consumption.

The `stepValue(inputId, delta)` helper respects the `min` and `max` attributes of the target input and clamps the result before writing it back, preventing out-of-range values.

---

## 🚘 EV Profiles

Trip Master includes a built-in **User Profiles** system that allows drivers to save, load, and delete named configuration snapshots. Profiles are stored in the browser's `localStorage` under the key `tripmaster_profiles` and persist indefinitely across sessions on the same device.
For further information see [POI Preference Persistence](#-poi-preference-persistence).

### 🗄️ Storage Model

Profiles are serialized as a JSON object where each key is the user-defined profile name and each value is a configuration record:

```json
{
  "My Tesla Model S": {
    "vehicleWeight": 2200,
    "gpsPolling": 5,
    "batteryKwh": 100,
    "elecPrice": 0.30,
    "is3DMode": true,
    "isHeadingUp": true,
    "isWeatherOverlayOn": false,
    "theme": "dark",
    "poiTypeEnabled": {
      "mobile_patrol": false,
      "speed_camera": true,
      "road_closure": false,
      "ev_charging": true
    }
  },
  "My Tesla Model X": {
    "vehicleWeight": 2400,
    "gpsPolling": 10,
    "batteryKwh": 100,
    "elecPrice": 0.35,
    "is3DMode": false,
    "isHeadingUp": false,
    "isWeatherOverlayOn": true,
    "theme": "light",
    "poiTypeEnabled": {
      "mobile_patrol": true,
      "speed_camera": false,
      "road_closure": true,
      "ev_charging": false
    }
  }
}
```

### 💾 Saved Parameters

Each profile snapshot captures **nine** configuration fields:

| Field | Source Element ID | Description |
|---|---|---|
| `vehicleWeight` | `vehicleWeight` | Vehicle + occupant mass [Kg] |
| `gpsPolling` | `gpsPolling` | GPS polling interval [s] |
| `batteryKwh` | `batteryCapacity` | Total usable battery capacity [kWh] |
| `elecPrice` | `elecPrice` | Electricity price for cost calculations [€/kWh] |
| `is3DMode` | `is3DMode` | Whether the 3D map view was active (`true` / `false`) |
| `isHeadingUp` | `isHeadingUp` | Whether heading-up orientation was active (`true` / `false`) |
| `isWeatherOverlayOn` | `isWeatherOverlayOn` | Whether the RainViewer precipitation radar overlay was active (`true` / `false`) |
| `theme` | `currentTheme` | Active UI theme (`"light"` or `"dark"`) |
| `poiTypeEnabled` | `poiTypeEnabled` | Snapshot of the four POI layer toggle states at save time (`Object.assign({}, poiTypeEnabled)`) |

> 💡 **Note:** Temperature efficiency and headwind speed are intentionally excluded — they represent real-time environmental conditions rather than vehicle-specific parameters.

### ⚙️ Profile Functions

| Function | Description |
|---|---|
| `getProfiles()` | Reads and parses the `localStorage` entry; returns `{}` on error or empty state |
| `saveProfiles(profiles)` | Serializes the full profiles object and writes it back to `localStorage` |
| `openProfilesModal()` | Renders the profiles list and shows the profiles modal |
| `closeProfilesModal()` | Hides the profiles modal |
| `renderProfilesList()` | Iterates all saved profiles and injects them as `profile-item` cards into the modal; shows an empty-state message when no profiles exist |
| `saveProfile()` | Reads the profile name input and all nine config fields (including `poiTypeEnabled` snapshot), merges them into the profiles object, and persists via `saveProfiles()` |
| `loadProfile(name)` | Restores all configuration fields; see [Load Behavior](#-load-behavior) for the full atomic sequence |
| `overwriteProfile(name)` | Overwrites an existing profile with the **full** current configuration — including `vehicleWeight`, `batteryKwh`, `elecPrice`, `gpsPolling`, `theme`, `is3DMode`, `isHeadingUp`, `isWeatherOverlayOn`, and the current `poiTypeEnabled` snapshot — without renaming; updates the profiles list in place. The overwrite button is styled in **yellow/warning** (`var(--warning)`) with a **sync/refresh SVG icon** (two curved arrows), positioned between the blue Load button and the red Delete button in each profile card. |
| `deleteProfile(name)` | Removes the named key from the profiles object and refreshes the list |
| `escapeHtml(str)` | Sanitizes a string for safe HTML injection by replacing `&`, `<`, `>`, `"`, and `'` with their corresponding HTML entities; used internally by `renderProfilesList()` |

### 🔄 Load Behavior

When a profile is loaded via `loadProfile()`, the UI is updated atomically:

1. `vehicleWeight` input value is set directly.
2. `batteryCapacity` input value is set, then `updateBattery()` is called to refresh the SOC bar and recompute the range estimate.
3. If the profile contains `elecPrice`, it is restored to the `elecPrice` input field; otherwise the current value is preserved.
4. The GPS polling segmented control iterates all `.segment` buttons in `#gpsPollingGroup`, removes the `active` class from all of them, and re-applies it to the button whose `data-value` attribute matches the stored `gpsPolling` value. The hidden `#gpsPolling` input is also updated to keep it in sync.
5. **POI overlay is fully reset before restoring the profile state:** `stopPoiWatchdog()` and `clearTimeout(poiMinimizeTimer)` are called, `isPoiOverlayOn` is set to `false`, all POI markers are removed from both maps via `removeAllPoiMarkers()`, `lastPoiRefreshPoint` is reset to `null`, and the POI button and panel are cleared of their `.active` / `.visible` / `.minimized` CSS classes. This ensures a clean slate before applying the profile's saved POI configuration.
6. If the profile contains an `is3DMode` boolean that differs from the current state, `toggle3DMap()` is called to switch the map view accordingly.
7. If the profile contains an `isHeadingUp` boolean that differs from the current state, `toggleHeadingMode()` is called to restore the heading orientation.
8. If the profile contains a `theme` value that differs from the current `currentTheme`, `toggleTheme()` is called to switch the UI to the saved Light/Dark mode.
9. If the profile contains an `isWeatherOverlayOn` boolean that differs from the current state, `toggleWeatherOverlay()` is called to activate or deactivate the RainViewer precipitation radar overlay accordingly.
10. **POI state is restored from the profile snapshot:** The `poiTypeEnabled` object is merged key-by-key from `p.poiTypeEnabled`, the `.poi-panel-item` CSS classes are updated to match, `savePoiPrefs()` is called to sync `localStorage`, and — if at least one POI type was enabled in the profile — `isPoiOverlayOn` is set to `true`, the POI button and panel are activated, `startPoiMinimizeTimer()` and `startPoiWatchdog()` are started, and a full POI fetch is performed asynchronously for all enabled types.
11. The modal is closed automatically.

### 🖥️ UI Entry Point

The profiles modal is accessible from the **🚘 button** in the application header. The modal contains:

- A scrollable list of saved profile cards, each showing the profile name and a compact summary (`Weight · Battery · GPS · Map mode / Heading mode · Weather overlay · enabled POI layers · Theme`), along with **Load**, **Overwrite**, and **Delete** action buttons.
- A text input field (max 40 characters) and a **💾 Save** button to persist the active configuration under a new name.

#### 🗂️ Profile Card — POI Display

In the Profiles modal, each profile card renders the enabled POI layers as labeled lines beneath the other profile metadata:

```
┌─────────────────────────────────────────────┐
│  🚗 My EV Profile                           │
│  Weight: 1850 Kg  Battery: 75 kWh           │
│  kWh Price: 0.30 €/kWh                      │
│  GPS: 5 s  Map: 🌍 / 🧭  Weather: On        │
│  POI: 🚧 Road Closures                      │  ← only enabled layers shown
│  POI: ⚡ EV Charging                        │
│  Theme: 🌙 Dark                             │
└─────────────────────────────────────────────┘
```

If **no POI layers are enabled** in a profile, the card displays `POI: **None**` instead of individual layer lines.

---

## 💾 Last Settings Auto-Save

Trip Master automatically **saves and restores the last active configuration** across page reloads using the browser's `localStorage` API. This mechanism is independent of the named [User Profiles](#-user-profiles) system and operates silently in the background — no user interaction is needed.

Unlike User Profiles (which capture named snapshots including POI state, map mode, and theme), the Last Settings Auto-Save is a **lightweight, always-on autosave** focused on the core operational parameters the driver was using when the session ended.

---

### 🗝️ Storage Key

| 🔑 Constant | 📋 Value | 📖 Purpose |
|---|---|---|
| `LAST_SETTINGS_KEY` | `'tripmaster_last_settings'` | `localStorage` key under which the current configuration snapshot is serialized as a JSON string |

```javascript
const LAST_SETTINGS_KEY = 'tripmaster_last_settings';
```

---

### 📦 Saved Parameters

Each autosave snapshot captures **ten** configuration fields:

| 🔑 Field | 🏷️ Source | 📋 Type | 📖 Description |
|---|---|---|---|
| `vehicleWeight` | `#vehicleWeight` input value | `string` | Vehicle + occupant mass [Kg] |
| `windSpeed` | `#windSpeed` input value | `string` | Headwind speed [Km/h] |
| `gpsPolling` | `#gpsPolling` hidden input value | `string` | GPS polling interval [s] |
| `batteryCapacity` | `#batteryCapacity` input value | `string` | Total usable battery capacity [kWh] |
| `currentSoc` | `#socInput` input value | `string` | State of Charge at save time [%] |
| `isHeadingUp` | `isHeadingUp` runtime variable | `boolean` | Whether heading-up map orientation was active |
| `is3DMode` | `is3DMode` runtime variable | `boolean` | Whether the 3D map view was active |
| `poiTypeEnabled` | `poiTypeEnabled` runtime object | `Object` | Shallow copy (`Object.assign`) of POI layer toggle states |
| `isWeatherOverlayOn` | `isWeatherOverlayOn` runtime variable | `boolean` | Whether the RainViewer precipitation radar overlay was active |
| `theme` | `currentTheme` runtime variable | `string` | Active UI theme at save time — `"light"` ☀️ or `"dark"` 🌙 |

> 💡 **Note:** Temperature efficiency (`η_T`) is **not** included in the autosave — it represents a real-time environmental condition and is expected to be re-set manually at each session start.

---

### ⚙️ `saveLastSettings()` — Write to Storage

```javascript
function saveLastSettings() {
    var settings = {
        vehicleWeight:      document.getElementById('vehicleWeight').value,
        windSpeed:          document.getElementById('windSpeed').value,
        gpsPolling:         document.getElementById('gpsPolling').value,
        batteryCapacity:    document.getElementById('batteryCapacity').value,
        currentSoc:         document.getElementById('socInput').value,
        isHeadingUp:        isHeadingUp,
        is3DMode:           is3DMode,
        poiTypeEnabled:     Object.assign({}, poiTypeEnabled),
        isWeatherOverlayOn: isWeatherOverlayOn,
        theme:              currentTheme
    };
    localStorage.setItem(LAST_SETTINGS_KEY, JSON.stringify(settings));
}
```

- 📸 Collects the live values from all relevant DOM inputs and runtime state variables at the moment of the call.
- 🎨 The `theme` field captures the value of `currentTheme` (`"light"` ☀️ or `"dark"` 🌙) so that the active UI appearance is seamlessly restored on the next page load.
- 🔒 The `poiTypeEnabled` object is **shallow-copied** via `Object.assign({}, poiTypeEnabled)` to prevent future mutations of the live object from affecting the stored snapshot.
- 💽 Serializes the complete settings object to a JSON string and writes it to `localStorage` under `LAST_SETTINGS_KEY`, overwriting any previous entry.

---

### ⏰ Invocation Triggers

`saveLastSettings()` is called automatically in **two distinct scenarios**:

#### 🔄 1. Periodic Autosave

When the app starts, a repeating timer is created alongside the GPS poll interval:

```javascript
autosaveInterval = setInterval(saveLastSettings, 60000);
```

| ⚙️ Property | 📋 Value |
|---|---|
| ⏱️ Timer interval | **60 000 ms** (once every 60 seconds) |
| 📦 Timer handle | `autosaveInterval` — a `number \| null` module-level variable |
| 🚦 Lifecycle | Created by `initializeSystem()` |

This ensures that even during a long trip, configuration changes made mid-journey (e.g., switching to 3D mode, toggling a POI layer, or enabling the weather overlay) are periodically captured without any user action.

#### 🛑 2. Immediate Save on Trip Stop

When the user stops a trip via `stopTracking()`, `saveLastSettings()` is called **synchronously** — immediately:

```javascript
function stopTracking() {
    if (pollInterval)      clearInterval(pollInterval);
    if (tripTimer)         clearInterval(tripTimer);
    // ...
    saveLastSettings();  // ← immediate final snapshot
}
```

This guarantees that the **final state** of all settings at the exact moment the user stops tracking is always persisted — even if less than 60 seconds have elapsed since the last periodic autosave.

---

### 🔁 Invocation Flow Diagram

```
┌──────────────────────────────────────────────────────────────────┐
│                        initializeSystem()                        │
│   autosaveInterval = setInterval(saveLastSettings, 60 000 ms)    │
│                            │                                     │
│                     every 60 seconds                             │
│                            ▼                                     │
│                   saveLastSettings()                             │
│                 └─► localStorage.setItem(LAST_SETTINGS_KEY, …)   │
├──────────────────────────────────────────────────────────────────┤
│                        stopTracking()                            │
│                            │                                     │
│                     immediately after                            │
│                            ▼                                     │
│                   saveLastSettings()                             │
│                 └─► localStorage.setItem(LAST_SETTINGS_KEY, …)   │
└──────────────────────────────────────────────────────────────────┘
```

---

### 📂 `restoreLastSettings()` — Read and Apply on Boot

On page load, `initializeSystem()` calls `restoreLastSettings()` to rehydrate all saved settings back into the UI:

```javascript
function restoreLastSettings() {
    var raw;
    try { raw = localStorage.getItem(LAST_SETTINGS_KEY); } catch(e) { return; }
    if (!raw) return;
    var s;
    try { s = JSON.parse(raw); } catch(e) { return; }
    // ... restore fields
}
```

The restore sequence applies each field conditionally — only if the field is present in the stored object — using the following atomic steps:

| 🔢 Step | 📋 Action |
|---|---|
| 1️⃣ | `vehicleWeight` input value is set directly from `s.vehicleWeight` |
| 2️⃣ | `windSpeed` input value is set directly from `s.windSpeed` |
| 3️⃣ | `batteryCapacity` input value is set; then `updateBattery()` is called to refresh the SOC bar and recompute the range estimate |
| 4️⃣ | `socInput` value is set from `s.currentSoc`; then `updateBattery()` is called immediately after |
| 5️⃣ | The GPS polling segmented control iterates all `.segment` buttons in `#gpsPollingGroup`, removes the `active` class from all, and re-applies it to the button matching `s.gpsPolling`; the hidden `#gpsPolling` input is also updated |
| 6️⃣ | 🎨 If `s.theme` is a non-empty string that differs from the current `currentTheme`, `toggleTheme()` is called to restore the saved ☀️ Light / 🌙 Dark appearance |
| 7️⃣ | If `s.isHeadingUp` is a `boolean` that differs from the current `isHeadingUp` state, `toggleHeadingMode()` is called |
| 8️⃣ | If `s.is3DMode` is a `boolean` that differs from the current `is3DMode` state, `toggle3DMap()` is called |
| 9️⃣ | If `s.isWeatherOverlayOn` is a `boolean` that differs from the current `isWeatherOverlayOn` state, `toggleWeatherOverlay()` is called |
| 🔟 | If `s.poiTypeEnabled` is an object, each key is merged into the live `poiTypeEnabled` object (only strict `boolean` values); the `.poi-panel-item` CSS classes are updated accordingly; `savePoiPrefs()` is called to keep the dedicated POI preferences storage in sync |

> ⚠️ **Note:** Steps 6–9 use **diff-based toggling**: the restore function only calls the toggle function if the stored state differs from the current default — preventing double-invocations that would result in no net change.

---

### 🔗 Integration with `initializeSystem()`

`restoreLastSettings()` is called as the **last step** of `initializeSystem()`, which runs once on page load:

```javascript
function initializeSystem() {
    setupMap();
    setupCharts();
    setupSegmentedControl();
    updateBattery();
    loadPoiPrefs();
    restoreLastSettings();  // ← applied last, after all subsystems are ready
    // ...
}
```

This ordering guarantees that all subsystems (map, charts, segmented controls, battery widget, POI panel) are fully initialized **before** the saved state is applied — preventing restore calls from targeting unready DOM elements or uninitialized map instances.

---

### 📦 State Variable

| 🔤 Variable | 📋 Type | 📖 Description |
|---|---|---|
| `autosaveInterval` | `number \| null` | Handle of the `setInterval` timer that fires `saveLastSettings` every 60 s during an active trip; `null` otherwise |

---

### 🗺️ Relationship with Other Persistence Mechanisms

Trip Master uses **three distinct persistence mechanisms** in `localStorage`, each with a different scope and purpose:

| 🔑 Storage Key | 🏷️ Mechanism | 📖 Scope | 🔄 When Written |
|---|---|---|---|
| `tripmaster_last_settings` | 💾 Last Settings Auto-Save | Operational params + transient runtime state | Every 60 s during trip + on trip stop |
| `tripmaster_profiles` | 🚘 User Profiles | Named snapshots (no `windSpeed`, no `currentSoc`) | On explicit Save / Overwrite action |
| `tripmaster_poi_prefs` | 📌 POI Preferences | POI layer toggle state only | On every POI toggle, profile load, profile overwrite |

> 💡 **Note:** The `poiTypeEnabled` object is persisted by **all three mechanisms** simultaneously (as part of `saveLastSettings`, inside User Profiles, and independently via `savePoiPrefs`). When `restoreLastSettings()` applies a POI snapshot, it explicitly calls `savePoiPrefs()` to keep `tripmaster_poi_prefs` in sync with the restored state. The `theme` 🎨 field is persisted by both the Last Settings Auto-Save and User Profiles, but is **not** tracked by the dedicated POI preferences key.

---

### 🧹 Clearing Persisted Last Settings

The autosaved settings can be cleared manually from the browser's developer tools console:

```javascript
// Clear only the last-settings autosave
localStorage.removeItem('tripmaster_last_settings');

// Clear all Trip Master persistent data
localStorage.removeItem('tripmaster_last_settings');
localStorage.removeItem('tripmaster_profiles');
localStorage.removeItem('tripmaster_poi_prefs');
```

> ⚠️ **Note:** After clearing `tripmaster_last_settings`, the app will start with its compiled-in defaults on the next page load — no vehicle weight, no wind speed override, GPS polling at 5 s, SOC at 100%, 2D map mode, north-up orientation, weather overlay off, ☀️ light theme, and all POI layers at their last `tripmaster_poi_prefs` state (which is restored independently by `loadPoiPrefs()`).

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
- 🌙 **Dark:** `liberty` style — 70% brightness, moody dark vector cartography

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
│  🔴 TRIP MASTER               [🚘][🧮] [☀️/🌙] [⭐] │
├──────────────── CONFIG GRID (4 cols) ──────────────────┤
│  Weight │ Temp Efficiency │ Headwind │ GPS Polling     │
├──────────────── STAT CARDS (8 cols) ───────────────────┤
│ Dist │ Avg Spd │ Cons │ Regen │ Alt │ Grade │ Pwr │ ⏱ │
├──────────────── RANGE ESTIMATOR ───────────────────────┤
│  [kWh ±] [SOC% ±] [═══ Battery Bar ═══] [Range] [Rem.] │
├───────────── MAP ──────────┬───── CHARTS PANEL ────────┤
│ [−][🧿][+]                 │   [🔺][🌍][⛈️][📌][↕️] │
│                            │  Elevation Profile        │
│                            │  Consumption Profile      │
│                            │  Speed Profile            │
│                            │  Energy Balance           │
│          Route Map         │  Power Breakdown          │
│                            │  Energy Flow              │
│                            │  Driving Style Analyzer   │
│                            │  Weather Panel            │
├─────────────────────── CONTROLS ───────────────────────┤
│   [▶ Start Trip]    [⏹ Stop Trip]    [↺ Reset Trip]  │
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
| 🔌 Net Energy | $E_{\text{consumed}} - E_{\text{regen}}$ (Wh) |
| 💰 Trip Cost | $E_{\text{kWh}} \times \text{elecPrice}$ (€) |
| 📊 Cost per Km | $\text{Trip Cost} / D_{\text{total}}\,\text{(Km)}$ (€/Km) |
| 💚 VS ICE Saved | $\text{ICE Cost} - \text{Trip Cost}$ (€) |
| 🚗 ICE Cost | $(D_{\text{total}} / \text{ICE Efficiency}) \times \text{ICE Fuel Price}$ (€) |
| ⛽ ICE Fuel Price | Live diesel fuel price from API or cache (€/L) |
| ⚙️ ICE Efficiency | Vehicle efficiency for ICE comparison (Km/L) |
| 📍 Total Data Points | `altChart.data.datasets[0].data.length` |

### 🏆 Efficiency Badge

The average consumption $\bar{C}$ (Wh/Km) triggers one of three badges:

| Condition | Badge |
|---|---|
| $\bar{C} < 150\ \text{Wh/Km}$ | 🏆 **Excellent Efficiency** |
| $150 \leq \bar{C} < 220\ \text{Wh/Km}$ | 👍 **Good Efficiency** |
| $\bar{C} \geq 220\ \text{Wh/Km}$ | ⚡ **High Consumption** |

### 📤 Export / Import Trip Coordinates

The Trip Summary modal includes two action buttons that allow saving and restoring the GPS route of any recorded trip. Both buttons are always visible at the bottom of the modal panel, regardless of whether a trip is currently active.

```
┌───────────────── TRIP SUMMARY MODAL ─────────────────────┐
│  📋 Trip Summary                                     [×] │
│  ─────────────────────────────────────────────────────── │
│  [summary fields and efficiency badge]                   │
│  ─────────────────────────────────────────────────────── │
│   [ ⬇ Export Trip ]          [ ⬆ Import Trip ]           │
└──────────────────────────────────────────────────────────┘
```

---

#### ⬇ Export Trip Coordinates

The **⬇ Export Trip** button calls `exportTrip()` and serializes the full route to a downloadable `.json` file. It is only functional when at least **2 GPS coordinates** have been recorded in the current session (`map3dCoords.length ≥ 2`).

##### 📄 Output File Format

The exported file is a plain JSON array of `[longitude, latitude]` pairs — one entry per recorded GPS fix — matching the GeoJSON coordinate array convention:

```json
[
  [12.4923, 41.8902],
  [12.4931, 41.8915],
  [12.4944, 41.8927],
  ...
]
```

Each element is a two-element number array: `[longitude, latitude]`, in decimal degrees (WGS 84).

##### 🏷️ Filename Convention

The file is automatically named with a timestamp derived from the current local time at the moment of export:

```
trip_coordinates_YYYYMMDD_HHmm.json
```

For example: `trip_coordinates_20250318_1435.json`.

##### ⚙️ Implementation Details

| Property | Value |
|---|---|
| Function | `exportTrip()` |
| Trigger | `onclick` on the **⬇ Export Trip** button in `#summaryModal` |
| Guard condition | Aborts with an alert if `map3dCoords.length < 2` |
| Serialization | `JSON.stringify(map3dCoords, null, 2)` — pretty-printed, 2-space indent |
| MIME type | `application/json` |
| Delivery | Programmatic anchor click with `URL.createObjectURL()` / `URL.revokeObjectURL()` |
| Source data | `map3dCoords` — the shared `[lng, lat][]` coordinate buffer used by both map instances |

---

#### ⬆ Import Trip Coordinates

The **⬆ Import Trip** button triggers a hidden `<input type="file">` element (`#importTripInput`) that accepts `.json` files. Once the user selects a file, `importTrip(event)` parses and loads it into the map.

##### 📋 Expected File Format

The imported file must be a valid JSON array of `[longitude, latitude]` pairs, identical to the format produced by the export function:

```json
[
  [longitude_1, latitude_1],
  [longitude_2, latitude_2],
  ...
]
```

Validation rules enforced at import time:

- The parsed value must be a JSON **array** (`Array.isArray(coords) === true`).
- The array must contain **at least 2 elements**.
- Each element must itself be an **array with at least 2 numeric values** (longitude, latitude).

If any condition is not met, an alert is shown (`'Invalid trip file format.'`) and the import is aborted without modifying any existing route data.

##### 🗺️ Map Behavior After Import

Once a valid file is loaded, the following actions occur automatically:

1. `map3dCoords` is replaced with the parsed coordinate array.
2. If the 2D route source (`pathLine`) is initialized, it is updated via `pathLine.setData()` to render the imported route immediately.
3. If the 3D route source (`map3dSource`) is initialized, it is updated via `map3dSource.setData()` with the same data.
4. The active map instance (`map` in 2D mode, `map3d` in 3D mode) calls `fitBounds()` with a **40 px padding** and a **600 ms animated transition**, zooming and centering the viewport to frame the entire imported route.
5. The Trip Summary modal is **automatically closed** (`display: 'none'`).

##### ⚙️ Implementation Details

| Property | Value |
|---|---|
| Function | `importTrip(event)` |
| Trigger | `onchange` on `#importTripInput` (hidden file input); activated by `onclick` on the **⬆ Import Trip** button |
| Accepted file types | `.json` (enforced via `accept=".json"` on the file input) |
| Reading method | `FileReader.readAsText()` |
| Parsing | `JSON.parse(e.target.result)` wrapped in a `try/catch`; parse errors surface as an alert with the error message |
| Map update — 2D | `pathLine.setData({ type: 'Feature', geometry: { type: 'LineString', coordinates: map3dCoords } })` |
| Map update — 3D | `map3dSource.setData({ type: 'Feature', geometry: { type: 'LineString', coordinates: map3dCoords } })` |
| Viewport fit | `activeMap.fitBounds([...], { padding: 40, duration: 600 })` — bounding box computed by reducing over all imported coordinates |
| Post-import | `#summaryModal` is hidden automatically |

> 💡 **Note:** Importing a trip replaces the current `map3dCoords` buffer entirely. Any previously recorded GPS track from an active or completed session is overwritten. The energy, speed, altitude, and consumption accumulators are **not** recalculated from the imported coordinates — they retain their current values.

---

## 📍 Start & End Markers

Whenever a trip file is successfully imported via the **⬆ Import Trip** button, Trip Master automatically places two circular endpoint markers on the map to visually identify the beginning and the end of the imported route.

### 🎨 Marker Appearance

Both markers are created by `createTripEndpointMarker(label, bgColor)`, which builds a styled `<div>` element rendered directly by MapLibre GL JS as a custom HTML marker:

```
  ┌──────────┐           ┌──────────┐
  │  🟢  S   │          │  🔴  E   │
  └──────────┘           └──────────┘
  Start of route         End of route
```

### 📌 Marker Placement

The markers are placed by `placeImportMarkers(coords)`, which receives the full imported coordinate array and derives the two anchor positions:

```javascript
const first = coords[0];               // [longitude, latitude] of the first point
const last  = coords[coords.length - 1]; // [longitude, latitude] of the last point
```

The **Start marker** (`S`) is positioned at `first`; the **End marker** (`E`) is positioned at `last`. Both are added to **both map instances** (2D and 3D) so they are always visible regardless of which map mode is currently active.

### 🔄 Lifecycle & Cleanup

Each of the four marker references (`_importStartMarker`, `_importEndMarker`, `_importStartMarker3d`, `_importEndMarker3d`) is stored on the global `window` object. Before placing new markers, `placeImportMarkers()` removes any previously existing markers:

```javascript
if (window._importStartMarker)   { window._importStartMarker.remove();   window._importStartMarker   = null; }
if (window._importEndMarker)     { window._importEndMarker.remove();     window._importEndMarker     = null; }
if (window._importStartMarker3d) { window._importStartMarker3d.remove(); window._importStartMarker3d = null; }
if (window._importEndMarker3d)   { window._importEndMarker3d.remove();   window._importEndMarker3d   = null; }
```

This guarantees that re-importing a new file always produces exactly one pair of endpoint markers, replacing the previous pair without accumulation.

### ⚙️ Implementation Details

| Property | Value |
|---|---|
| Factory function | `createTripEndpointMarker(label, bgColor)` — returns a styled `HTMLDivElement` |
| Placement function | `placeImportMarkers(coords)` — called at the end of `importTrip()` after a successful parse |
| Trigger | Automatically called on every successful `.json` file import; never called during live GPS tracking |
| 2D marker class | `maplibregl.Marker({ element: ..., anchor: 'center' }).setLngLat([lng, lat]).addTo(map)` |
| 3D marker class | `maplibregl.Marker({ element: ..., anchor: 'center' }).setLngLat([lng, lat]).addTo(map3d)` |
| Guards | Markers are only added if the respective map instance (`map` / `map3d`) is already initialized and non-null |

### 📦 State Variables

| Variable | Type | Description |
|---|---|---|
| `window._importStartMarker` | `maplibregl.Marker \| null` | Start marker on the 2D map; `null` when no trip has been imported |
| `window._importEndMarker` | `maplibregl.Marker \| null` | End marker on the 2D map; `null` when no trip has been imported |
| `window._importStartMarker3d` | `maplibregl.Marker \| null` | Start marker on the 3D map; `null` when no trip has been imported |
| `window._importEndMarker3d` | `maplibregl.Marker \| null` | End marker on the 3D map; `null` when no trip has been imported |

> 💡 **Note:** Start and End markers are placed exclusively after a file import. They are **not** drawn during a live GPS recording session, and they are **not** cleared when a new live trip is started — they persist on the map until the next file import replaces them.

---

## 🗺️ Map Modes: 2D & 3D

Trip Master provides two distinct map rendering modes that can be toggled at any time during a trip — even while recording is active. **Both modes are powered by MapLibre GL JS**, using a single WebGL-based rendering engine with OpenFreeMap vector tiles. The two modes share the same GPS coordinate stream and the same GeoJSON route data source.

### 🔄 Toggle Button

A floating **`3D` / `2D` button** is permanently overlaid in the **top-right corner** of the map panel. Clicking it switches between modes instantly:

- 🗺️ **Label `3D`** → the map is currently in **2D mode**; clicking will activate the 3D view
- 🌍 **Label `2D`** (highlighted in `--secondary` blue) → the map is currently in **3D mode**; clicking will return to the flat 2D view

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
| 🌙 Dark style | `https://tiles.openfreemap.org/styles/liberty` |
| 📐 Camera pitch | `0°` (flat top-down view) |
| 🧭 Camera bearing | `0°` (north-up) |
| ✨ Antialiasing | `true` |
| 🌍 Route layer type | `line` (GeoJSON `LineString`) — source ID `trip-path-2d` |
| 🎨 Route color | `#e21017` |
| 📏 Route line width | `5` px |
| 🔍 Initial zoom | `15` (set on first GPS fix) |
| 🧭 Map follows GPS | `map.setCenter([longitude, latitude])` on each GPS step |

The 2D map is contained in the `<div id="map">` element and initialized at page load via `setupMap()`. The route is built incrementally: each new GPS coordinate is pushed into the shared `map3dCoords` buffer and applied to the GeoJSON source via `pathLine.setData(...)`.

---

### 🌍 3D Mode — MapLibre GL + OpenFreeMap

The 3D mode reuses **MapLibre GL JS v4.7.1** with a pitched, tilted camera that gives a perspective-projected terrain view. It uses the same tile provider and the same GeoJSON route data as the 2D mode.

| 🔧 Property | 📋 Value |
|---|---|
| 🏗️ Engine | MapLibre GL JS `4.7.1` |
| 🌍 Tile provider | OpenFreeMap |
| ☀️ Light style | `https://tiles.openfreemap.org/styles/liberty` |
| 🌙 Dark style | `https://tiles.openfreemap.org/styles/liberty` |
| 📐 Camera pitch | `60°` (tilted perspective) |
| 🧭 Camera bearing | `0°` (heading-up) |
| ✨ Antialiasing | `true` (smooth WebGL rendering) |
| 🌍 Route layer type | `line` (GeoJSON `LineString`) — source ID `trip-path` |
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
| 🌙 Dark | `https://tiles.openfreemap.org/styles/liberty` | 70% brightness, detailed vector cartography |

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
| `isHeadingUp` | `boolean` | `true` while heading-up orientation is active; `false` when north-up is active |
| `lastHeading` | `number` | Most recently computed travel bearing in degrees [0–360), derived from the last two GPS coordinates |
| `positionMarker` | `maplibregl.Marker \| null` | Live GPS position marker on the 2D map; initialized at page load |
| `positionMarker3d` | `maplibregl.Marker \| null` | Live GPS position marker on the 3D map; initialized on first 3D activation |
| `isMapFullscreen` | `boolean` | `true` while the map fullscreen mode is active; `false` in normal layout |
| `isWeatherOverlayOn` | `boolean` | `true` while the RainViewer precipitation radar overlay is active; `false` when hidden |
| `weatherOverlayTimestamp` | `number \| null` | UNIX timestamp of the most recently fetched RainViewer radar frame; `null` until first overlay activation |
| `isPoiOverlayOn` | `boolean` | `true` while the POI overlay is active; `false` when hidden |
| `isPoiLoading` | `boolean` | `true` during an active POI data fetch; prevents concurrent requests |
| `lastPoiRefreshPoint` | `{ lat, lon } \| null` | GPS anchor of the last POI refresh; `null` until first overlay activation |
| `poiMarkersMap2d` | `Object` | Per-type marker arrays for the 2D map, keyed by `poiId` |
| `poiMarkersMap3d` | `Object` | Per-type marker arrays for the 3D map, keyed by `poiId` |
| `poiTypeEnabled` | `Object` | Per-type boolean flags tracking which POI layers are toggled on by the user |
| `poiMinimizeTimer` | `number \| null` | `setTimeout` handle for the POI panel auto-minimize; `null` when not running |
| `poiWatchdogTimer` | `number \| null` | `setTimeout` handle for the POI watchdog loop; `null` when stopped |
| `window._importStartMarker` | `maplibregl.Marker \| null` | Start (`S`) endpoint marker on the 2D map; set by `placeImportMarkers()` after a file import |
| `window._importEndMarker` | `maplibregl.Marker \| null` | End (`E`) endpoint marker on the 2D map; set by `placeImportMarkers()` after a file import |
| `window._importStartMarker3d` | `maplibregl.Marker \| null` | Start (`S`) endpoint marker on the 3D map; set by `placeImportMarkers()` after a file import |
| `window._importEndMarker3d` | `maplibregl.Marker \| null` | End (`E`) endpoint marker on the 3D map; set by `placeImportMarkers()` after a file import |

---

## 🔍 Map Zoom Controls

A set of three floating **zoom and re-center buttons** is overlaid in the **top-left corner** of the map panel:

```
┌─────────── MAP WRAPPER ─────────────────┐
│  ┌───┐ ┌───┐ ┌───┐                      │
│  │ − │ │ 🧿│ │ + │    (map content)     │
│  └───┘ └───┘ └───┘                      │
└─────────────────────────────────────────┘
```

| Button | Function | Description |
|---|---|---|
| `−` | `mapZoomOut()` | Decreases zoom level by 1 on the active map instance |
| `🧿` | `mapCenterOnGPS()` | Re-centers the active map on the current GPS position |
| `+` | `mapZoomIn()` | Increases zoom level by 1 on the active map instance |

All three functions resolve the currently active map as `const activeMap = is3DMode ? map3d : map` and call `activeMap.easeTo()` with a `duration: 250 ms` (zoom) or `400 ms` (center) smooth transition. `mapCenterOnGPS()` fires a fresh `navigator.geolocation.getCurrentPosition()` request with `enableHighAccuracy: true` before recentering.

The zoom group container (`#mapZoomGroup`) is automatically hidden when the map wrapper height drops below 50 px (see [Map Overlay Button Auto-Hide](#-responsive-layout-adaptations)).

---

## ↕️ Map Fullscreen Mode

Trip Master provides a **fullscreen map mode** that expands the map to fill the entire viewport, hiding all UI panels and controls except the map overlay buttons.

### 🔘 Toggle Button

A floating **`↕️` button** is permanently overlaid in the **top-right corner** of the map panel, to the right of the POI overlay button:

```
┌─────────────────────────── MAP WRAPPER ────────────────────────────────┐
│    ┌───┐  ┌───┐  ┌───┐      ┌─────┐ ┌─────┐ ┌─────┐ ┌─────┐ ┌─────┐    │
│    │ − │  │🧿 │ │ + │      │  🔺 │ │ 🌍  │ │ 📌 │ │ ⛈️  │ │  ↕ ️ │    │
│    └───┘  └───┘  └───┘      └─────┘ └─────┘ └─────┘ └─────┘ └─────┘    │
└────────────────────────────────────────────────────────────────────────┘
```

When active, the button is highlighted in `--accent-purple` (`#b39ddb`).

### ⚙️ Toggle Logic — `toggleMapFullscreen()`

| Direction | Actions |
|---|---|
| **Normal → Fullscreen** | Sets `isMapFullscreen = true` · Adds `map-fullscreen` CSS class to `<body>` · Activates button styling · Calls `map.resize()` and `map3d.resize()` after a 50 ms delay to let the DOM reflow |
| **Fullscreen → Normal** | Sets `isMapFullscreen = false` · Removes `map-fullscreen` CSS class from `<body>` · Deactivates button styling · Triggers the same resize calls |

### 🎨 Fullscreen CSS Class Effects

When `body.map-fullscreen` is active, the following elements are hidden via CSS:

- `.header` (app title bar and header buttons)
- `.config-grid` (vehicle configuration row)
- `.range-card` (battery / range estimator)
- `.grid-stats` (8 stat cards)
- `.controls` (Start / Stop / Reset buttons)
- `.charts-panel` (all charts and weather panel)

The map wrapper and its content expand to fill the remaining available space with `border-radius: 0` to eliminate rounded corners at viewport edges.

### 📦 State Variable

| Variable | Type | Description |
|---|---|---|
| `isMapFullscreen` | `boolean` | `true` while fullscreen mode is active; `false` in normal layout |

---

## 🧭 Heading Mode

Trip Master supports a **Heading-Up** orientation mode that rotates the active map so that the current travel direction always points upward — mirroring the feel of a traditional car navigation display.

### 🔘 Toggle Button

A floating **`🔺` / `🧭` button** is permanently overlaid in the **top-right corner of the map panel**, to the left of the 3D toggle:

```
┌─────────────────────────── MAP WRAPPER ────────────────────────────────┐
│    ┌───┐  ┌───┐  ┌───┐      ┌─────┐ ┌─────┐ ┌─────┐ ┌─────┐ ┌─────┐    │
│    │ − │  │🧿 │ │ + │      │  🔺 │ │ 🌍  │ │ 📌 │ │ ⛈️  │ │  ↕ ️ │    │
│    └───┘  └───┘  └───┘      └─────┘ └─────┘ └─────┘ └─────┘ └─────┘    │
└────────────────────────────────────────────────────────────────────────┘
```

| Label | State | Clicking activates |
|---|---|---|
| `🔺` | North-up is active | Heading-up mode |
| `🧭` (highlighted in `--primary` green) | Heading-up is active | North-up mode |

### ⚙️ Toggle Logic — `toggleHeadingMode()`

```javascript
function toggleHeadingMode()
```

| Direction | Actions |
|---|---|
| **North-Up → Heading-Up** | Sets `isHeadingUp = true` · Changes button label to `N` · Adds `.active` CSS class · Applies `lastHeading` as the bearing of the currently active map instance via `activeMap.easeTo({ bearing: lastHeading, duration: 400 })` |
| **Heading-Up → North-Up** | Sets `isHeadingUp = false` · Changes button label to `▲` · Removes `.active` CSS class · Resets the map bearing to `0` via `activeMap.easeTo({ bearing: 0, duration: 400 })` |

The correct active map is resolved as: `const activeMap = is3DMode ? map3d : map`.

### 📐 Heading Computation

At every valid GPS step inside `updateLocation()`, the travel bearing is recomputed from the last two entries in `map3dCoords`:

```javascript
const dLon = longitude - prev[0];
const dLat = latitude - prev[1];
lastHeading = (Math.atan2(dLon, dLat) * 180 / Math.PI + 360) % 360;
```

The resulting `lastHeading` (degrees, 0 = North, clockwise) is then passed to `map.easeTo()` / `map3d.easeTo()` as the `bearing` property when heading-up mode is active:

```javascript
const mapBearing = isHeadingUp ? lastHeading : 0;
map.easeTo({ center: [longitude, latitude], bearing: mapBearing, duration: 300 });
if (is3DMode && map3d) {
    map3d.easeTo({ center: [longitude, latitude], bearing: mapBearing, duration: 300 });
}
```

When heading-up mode is **off**, both maps always use `bearing: 0` (north-up), regardless of the vehicle's actual travel direction.

---

## 📌 POI Overlay

Trip Master provides a **Points of Interest (POI) Overlay** that places live, category-filtered markers on both the 2D and 3D maps. Data is sourced in real time from the **OpenStreetMap Overpass API** and the **Waze Live Map API** (via a CORS proxy), with no API key required for either source.

### 🔘 Toggle Button

A floating **`📌` button** is permanently overlaid in the **top-right area of the map panel**, between the Weather Overlay button and the Fullscreen button:

```
┌─────────────────────────── MAP WRAPPER ────────────────────────────────┐
│    ┌───┐  ┌───┐  ┌───┐      ┌─────┐ ┌─────┐ ┌─────┐ ┌─────┐ ┌─────┐    │
│    │ − │  │🧿 │ │ + │      │  🔺 │ │ 🌍  │ │ 📌 │ │ ⛈️  │ │  ↕ ️ │    │
│    └───┘  └───┘  └───┘      └─────┘ └─────┘ └─────┘ └─────┘ └─────┘    │
└────────────────────────────────────────────────────────────────────────┘
```

When active, the button is highlighted in `#ff9100` (orange).

Clicking `📌` also **opens or closes the POI Panel** — a compact dropdown immediately below the button — that lists all four available POI layer types with individual toggles.

### 🗂️ POI Panel

The POI Panel (`#poiPanel`) slides into view whenever the overlay is active. It contains:

- A **title row** (`POI Layers`)
- One **row per POI type**, each showing the emoji icon, a label, and a colored checkbox indicator
- A **loading label** (`#poiLoadingLabel`) that appears during fetch operations

```
┌─────────────────────────────┐
│  POI Layers                 │
│  🚧  Road Closures    [ ]  │
│  👮  Mobile Patrols   [ ]   │
│  📷  Speed Cameras    [ ]  │
│  ⚡  EV Charging      [ ]  │
│  ⌛ Fetching data…          │  ← visible only during fetch
└─────────────────────────────┘
```

Each row is individually clickable to toggle that POI layer on or off via `togglePoiType(poiId)`.

### 🏷️ POI Types

Four POI layer types are defined in the `POI_TYPES` constant array:

| ID | 🏷️ Label | Emoji | 🎨 Color | 🌐 Source | Notes |
|---|---|---|---|---|---|
| `mobile_patrol` | Mobile Patrol | 👮 | `#1565c0` | Waze Live Map | Filters `POLICE`-type alerts from the Waze georss alerts feed |
| `speed_camera` | Speed Camera | 📷 | `#c62828` | OSM Overpass | `highway=speed_camera`, `enforcement=maxspeed`, `man_made=speed_camera` |
| `road_closure` | Road Closure | 🚧 | `#ff6f00` | OSM Overpass | Barriers, jersey barriers, highway=construction, active construction ways |
| `ev_charging` | EV Charging | ⚡ | `#2e7d32` | OSM Overpass | `amenity=charging_station` nodes and ways |

### 🌐 Data Sources & API Endpoints

#### 🗺️ OpenStreetMap — Overpass API

Road Closures, Speed Cameras, and EV Charging stations are fetched from the public Overpass API:

```
POST https://overpass-api.de/api/interpreter
Content-Type: application/x-www-form-urlencoded

data=<OverpassQL query>
```

The bounding box for each query is derived from `refMap.getBounds()` and formatted as `south,west,north,east` in decimal degrees (5 decimal places).

**Road Closures query pattern:**

```
[out:json][timeout:25];(
  node["barrier"="block"](bbox);
  node["barrier"="jersey_barrier"](bbox);
  node["highway"="construction"](bbox);
  way["highway"="construction"](bbox);
  way["construction"~"."](bbox);
);out center qt;
```

**Speed Cameras query pattern:**

```
[out:json][timeout:25];(
  node["highway"="speed_camera"](bbox);
  node["enforcement"="maxspeed"](bbox);
  node["man_made"="speed_camera"](bbox);
);out center qt;
```

**EV Charging query pattern:**

```
[out:json][timeout:25];(
  node["amenity"="charging_station"](bbox);
  way["amenity"="charging_station"](bbox);
);out center qt;
```

For `way` elements, the coordinates are extracted from `el.center.lat` / `el.center.lon` (Overpass `out center` directive). For nodes, `el.lat` / `el.lon` are used directly.

#### 👮 Waze Live Map — Mobile Patrols

Mobile patrol data is fetched from the Waze georss feed, proxied through **corsproxy.io** to bypass the Waze CORS policy:

```
GET https://corsproxy.io/?<encoded Waze URL>

Waze URL: https://www.waze.com/live-map/api/georss
  ?top={north}&bottom={south}&left={west}&right={east}
  &env=row&types=alerts
```

The response is filtered to retain only alerts where `type === 'POLICE'` or `subtype` starts with `'POLICE'`. Each retained alert is mapped to `{ lat, lon, name }` using `a.location.y` / `a.location.x`.

### ⚙️ Core Functions

| 🔧 Function | 📋 Description |
|---|---|
| `togglePoiOverlay()` | Async. Toggles the overlay on/off. **On**: shows the panel, fetches all enabled POI types, stores the refresh anchor point. **Off**: hides the panel, removes all markers from both maps, resets `lastPoiRefreshPoint` to `null`. Blocked while `isPoiLoading` is `true`. |
| `togglePoiType(poiId)` | Async. Toggles an individual POI layer. If enabling, fetches points for that type and places markers on both maps. If disabling, removes markers for that type from both maps. No-ops if `isPoiOverlayOn` is `false` or `isPoiLoading` is `true`. |
| `fetchPointsForPoi(poi, refMap)` | Async router: calls `fetchWazeMobilePatrols()` for `source='waze'` types, or `fetchOsmPoi()` for `source='osm'` types. Returns a `{ lat, lon, name }[]` array. |
| `fetchOsmPoi(poi, bbox)` | Async. POSTs the POI's Overpass QL query. Throws with `e.isRateLimit = true` on HTTP 429; returns `[]` on other errors. |
| `fetchWazeMobilePatrols(bounds)` | Async. Fetches the Waze georss endpoint via corsproxy.io, filters police alerts, returns `{ lat, lon, name }[]`. Throws on rate limit (HTTP 429). |
| `placePoiMarkersOnMap(targetMap, poi, points)` | Places a `maplibregl.Marker` for each point on `targetMap`. Defers via `targetMap.once('load', …)` if the map style is not yet loaded. Each marker includes a popup with the POI type label and optional name. |
| `removePoiMarkersForType(targetMap, poiId)` | Removes and clears all markers for a specific POI type from `targetMap`. |
| `removeAllPoiMarkers(targetMap)` | Iterates `POI_TYPES` and calls `removePoiMarkersForType` for every type on `targetMap`. |
| `createPoiMarkerElement(emoji, color)` | Creates and returns a styled 28×28 px circular `HTMLDivElement` with the POI emoji, colored background, white border, and drop shadow. |
| `getPoiStore(targetMap)` | Returns `poiMarkersMap2d` or `poiMarkersMap3d` based on which map instance is passed. |
| `setPoiLoading(on, rateLimit)` | Shows/hides `#poiLoadingLabel`. When `rateLimit` is `true`, displays `⛔ POI fetching delayed!` instead of `⌛ Fetching data…`. Also disables/re-enables `#btnPoiOverlay` to prevent double-clicks during a fetch. |

### 🔄 Automatic POI Refresh While Driving

When the POI overlay is active and a trip is in progress, the overlay automatically refreshes as the vehicle moves. At each GPS fix inside `updateLocation()`, the system evaluates whether the vehicle has moved far enough from the last fetch anchor:

```
if (isPoiOverlayOn && !isPoiLoading) {
    distFromLastPoi = haversine(lastPoiRefreshPoint, currentPosition)
    if (distFromLastPoi >= POI_REFRESH_DISTANCE_M) {
        → update lastPoiRefreshPoint
        → removeAllPoiMarkers (both maps)
        → fetchPointsForPoi for each enabled type
        → placePoiMarkersOnMap on both maps
    }
}
```

| 🔧 Constant | 📋 Value | 📖 Description |
|---|---|---|
| `POI_REFRESH_DISTANCE_M` | `5000` m | Minimum vehicle displacement from the last fetch anchor to trigger a new POI fetch |

### 🏷️ Marker Popup Format

Each placed marker includes a MapLibre GL popup rendered from inline HTML:

```
┌──────────────────────────────────┐
│  🚧 Road Closure                 │
│  Via Appia Nuova (optional name) │  ← only shown if the OSM element has a name tag
└──────────────────────────────────┘
```

Popups use `JetBrains Mono` monospace font, open on marker click, and are closeable via a close button.

### ⚠️ Rate Limit Handling

Both `fetchOsmPoi` and `fetchWazeMobilePatrols` detect HTTP 429 responses and throw an error with `e.isRateLimit = true`. The calling layer (`togglePoiOverlay`, `togglePoiType`, and the GPS-driven refresh loop) catches this flag and:

1. Calls `setPoiLoading(true, true)` → displays `⛔ Server fetching delay!`
2. Schedules `setPoiLoading(false)` after a **3-second timeout** before resuming normal operation

### 📦 State Variables

| 🔤 Variable | 📋 Type | 📖 Description |
|---|---|---|
| `isPoiOverlayOn` | `boolean` | `true` while the POI overlay is active; `false` when hidden |
| `isPoiLoading` | `boolean` | `true` during an active fetch; prevents concurrent or overlapping requests |
| `lastPoiRefreshPoint` | `{ lat, lon } \| null` | GPS coordinates of the last successful POI fetch anchor; `null` until the first overlay activation |
| `poiMarkersMap2d` | `Object` | Keyed by `poiId`; each value is an array of `maplibregl.Marker` instances on the 2D map |
| `poiMarkersMap3d` | `Object` | Keyed by `poiId`; each value is an array of `maplibregl.Marker` instances on the 3D map |
| `poiTypeEnabled` | `Object` | Keyed by `poiId`; `true` if that POI layer is currently toggled on by the user |
| `POI_TYPES` | `Array` | Immutable array of four POI descriptor objects (`id`, `label`, `emoji`, `color`, `source`, `overpassQuery`) |
| `POI_REFRESH_DISTANCE_M` | `number` | `5000` — minimum displacement in metres between automatic POI refresh triggers |

---

## 🗂️ POI Panel Minimize & Expand

To avoid cluttering the map area during normal driving, the POI layer-selection panel includes an **auto-minimize** feature. After a configurable inactivity timeout, the panel collapses to a small icon; a click anywhere on the collapsed panel restores it to full size.

### ⏱️ Auto-Minimize Timer

The timer is managed by `startPoiMinimizeTimer()`. Every time the user interacts with the POI panel — opening it, toggling a layer, or having a profile loaded that activates POI — the timer is reset:

```javascript
function startPoiMinimizeTimer() {
    clearTimeout(poiMinimizeTimer);
    poiMinimizeTimer = setTimeout(function() {
        var panel = document.getElementById('poiPanel');
        if (panel && panel.classList.contains('visible')) {
            panel.classList.add('minimized');
        }
    }, 5000);
}
```

| ⚙️ Property | 📋 Value |
|---|---|
| Timeout duration | **5 000 ms** (5 seconds) of inactivity |
| Trigger condition | Panel must have the `.visible` class at the moment the timer fires |
| CSS effect | Adds `.minimized` class to `#poiPanel` — collapses the panel to a 30×30 px icon showing `🚩` |
| Timer handle | `poiMinimizeTimer` — a `number \| null` module-level variable |

The timer is **reset** (cleared and restarted) in every call to `startPoiMinimizeTimer()`, which is invoked from:

| 📍 Call Site | 🔁 When |
|---|---|
| `togglePoiOverlay()` — **On** branch | POI overlay is first activated |
| `togglePoiType(poiId)` | User clicks any POI layer row |
| `loadProfile(name)` | Profile with enabled POI layers is loaded |

The timer is **cleared without restarting** (`clearTimeout(poiMinimizeTimer)`) in:
- `stopPoiWatchdog()` / `closeProfilesModal()` / `loadProfile()` — before the panel state is reset to ensure no stale minimization fires after a full POI reset.

### 🔓 Expand on Click

When the panel is in the minimized state, a click on it calls `expandPoiPanel()`:

```javascript
function expandPoiPanel() {
    var panel = document.getElementById('poiPanel');
    if (panel && panel.classList.contains('minimized')) {
        panel.classList.remove('minimized');
        startPoiMinimizeTimer();  // restart the 5-second countdown
    }
}
```

The click listener that triggers `expandPoiPanel()` is attached once per overlay activation — inside both `togglePoiOverlay()` and `loadProfile()` — using an inline `addEventListener`:

```javascript
poiPanel.addEventListener('click', function(e) {
    if (poiPanel.classList.contains('minimized')) {
        e.stopPropagation();
        expandPoiPanel();
    }
});
```

`e.stopPropagation()` prevents the click from bubbling to the map layer and accidentally triggering a map interaction while the panel is collapsed.

### 🎨 CSS States

The `#poiPanel` element transitions through three visual states via CSS class combinations:

| 🏷️ CSS Classes | 👁️ Visual State | 📐 Dimensions |
|---|---|---|
| *(no classes)* | 🚫 Hidden — overlay is off | `display: none` |
| `.visible` | 📋 Expanded — full layer list visible | min-width: 172 px, auto height |
| `.visible .minimized` | 🚩 Collapsed — icon only | 30×30 px, content hidden, shows `🚩` via `::after` pseudo-element |

---

## 🐕 POI Watchdog System

The POI Watchdog is a **background self-healing mechanism** that monitors the POI marker state and automatically re-fetches and re-plots markers if they are detected as missing. This covers edge cases where markers fail to appear due to map style reloads, WebGL context loss, or race conditions during map mode switching.

### 🔍 Detection Logic

The watchdog uses two helper predicates:

#### `hasAnyPoiEnabled()` — Are Any POI Layers Toggled On?

```javascript
function hasAnyPoiEnabled() {
    for (var id in poiTypeEnabled) {
        if (poiTypeEnabled[id]) return true;
    }
    return false;
}
```

Returns `true` if at least one POI type has its toggle set to `true` in `poiTypeEnabled`.

#### `areSelectedPoiMarkersPlotted()` — Are All Enabled Layers Actually Visible?

```javascript
function areSelectedPoiMarkersPlotted() {
    var activeMap = is3DMode ? map3d : map;
    var store = getPoiStore(activeMap || map);
    if (!store) return true;
    var anyEnabled = false;
    for (var id in poiTypeEnabled) {
        if (poiTypeEnabled[id]) {
            anyEnabled = true;
            if (!store[id] || store[id].length === 0) return false;
        }
    }
    return !anyEnabled || true;
}
```

Inspects the marker store for the currently active map. Returns `false` if any enabled POI layer has an **empty or absent** marker array — indicating that markers should exist but don't. Returns `true` if all enabled layers have at least one marker, or if no layers are enabled.

### ⏱️ Watchdog Timer Loop

The watchdog is managed by two functions:

#### `startPoiWatchdog()`

```javascript
function startPoiWatchdog() {
    stopPoiWatchdog();
    poiWatchdogTimer = setTimeout(async function() {
        if (!isPoiOverlayOn) return;
        if (hasAnyPoiEnabled() && !areSelectedPoiMarkersPlotted()) {
            await forceReplotSelectedPoi();
            poiWatchdogTimer = setTimeout(arguments.callee, POI_WATCHDOG_EXTENDED_MS);
        } else {
            poiWatchdogTimer = setTimeout(arguments.callee, POI_WATCHDOG_INTERVAL_MS);
        }
    }, POI_WATCHDOG_INTERVAL_MS);
}
```

| ⚙️ Constant | 📋 Value | 📖 Description |
|---|---|---|
| `POI_WATCHDOG_INTERVAL_MS` | `5 000` ms | Normal polling interval — checks every 5 seconds when markers look fine |
| `POI_WATCHDOG_EXTENDED_MS` | `900 000` ms | Extended interval (15 minutes) — used after a successful force-replot to avoid hammering the API |

**Decision logic at each tick:**

```
isPoiOverlayOn?
  ├── No  → exit (watchdog stops itself)
  └── Yes → hasAnyPoiEnabled() AND !areSelectedPoiMarkersPlotted()?
              ├── Yes (markers missing) → forceReplotSelectedPoi() → reschedule at EXTENDED
              └── No  (markers present) → reschedule at INTERVAL
```

#### `stopPoiWatchdog()`

```javascript
function stopPoiWatchdog() {
    if (poiWatchdogTimer) {
        clearTimeout(poiWatchdogTimer);
        poiWatchdogTimer = null;
    }
}
```

Cancels the pending `setTimeout` and resets `poiWatchdogTimer` to `null`. Called whenever the POI overlay is turned off, a profile is loaded (before re-initializing POI state), or the app is cleaning up POI state.

### 🔧 Force Replot — `forceReplotSelectedPoi()`

When the watchdog detects missing markers, it calls `forceReplotSelectedPoi()`, which performs a full refresh cycle:

```javascript
async function forceReplotSelectedPoi() {
    if (!isPoiOverlayOn || isPoiLoading) return;
    var refMap = (is3DMode && map3d && map3d.isStyleLoaded()) ? map3d : map;
    if (!refMap || !refMap.isStyleLoaded()) return;

    setPoiLoading(true, false);
    var rateLimitHit = false;
    try {
        removeAllPoiMarkers(map);
        removeAllPoiMarkers(map3d);
        for (var i = 0; i < POI_TYPES.length; i++) {
            var poi = POI_TYPES[i];
            if (!poiTypeEnabled[poi.id]) continue;
            try {
                var points = await fetchPointsForPoi(poi, refMap);
                placePoiMarkersOnMap(map, poi, points);
                if (map3d) placePoiMarkersOnMap(map3d, poi, points);
            } catch(e) {
                if (e.isRateLimit) { rateLimitHit = true; break; }
            }
        }
        if (!rateLimitHit) {
            var center = refMap.getCenter();
            lastPoiRefreshPoint = { lat: center.lat, lon: center.lng };
        }
    } finally {
        if (rateLimitHit) {
            setPoiLoading(true, true);
            setTimeout(function() { setPoiLoading(false); }, 3000);
        } else {
            setPoiLoading(false);
        }
    }
}
```

The function:
1. 🛑 Bails out if a fetch is already in progress (`isPoiLoading`) or the overlay is off.
2. 🗑️ Clears all existing markers from both map instances via `removeAllPoiMarkers()`.
3. 🌐 Fetches fresh data for every **enabled** POI type from the appropriate API.
4. 📍 Places fresh markers on both 2D and 3D maps.
5. 🔄 Updates `lastPoiRefreshPoint` to the current map center.
6. ⚠️ On rate-limit error, displays the `⛔ POI fetching delayed!` label for 3 seconds before clearing it.

### 🚀 Start / Stop Triggers

| 📍 Action | 🔁 Effect on Watchdog |
|---|---|
| `togglePoiOverlay()` — **On** | `startPoiWatchdog()` — begins monitoring |
| `togglePoiOverlay()` — **Off** | `stopPoiWatchdog()` — stops monitoring |
| `loadProfile(name)` — **before** state reset | `stopPoiWatchdog()` — ensures clean state |
| `loadProfile(name)` — **after** state restore (if POI enabled) | `startPoiWatchdog()` — resumes monitoring with restored state |

---

## 🔁 POI Map Synchronization

When the user switches between 2D and 3D map modes while the POI overlay is active, Trip Master automatically **synchronizes the existing POI markers** from the currently active map instance to the newly activated one. This avoids a full re-fetch from the network on every map mode switch.

### ⚙️ `syncPoiMarkersToMap(sourceMap, targetMap)`

```javascript
function syncPoiMarkersToMap(sourceMap, targetMap) {
    if (!isPoiOverlayOn || !sourceMap || !targetMap) return;
    var sourceStore = getPoiStore(sourceMap);
    if (!sourceStore) return;
    POI_TYPES.forEach(function(poi) {
        if (!poiTypeEnabled[poi.id]) return;
        var sourceMarkers = sourceStore[poi.id];
        if (!sourceMarkers || sourceMarkers.length === 0) return;
        var points = sourceMarkers.map(function(m) {
            var ll = m.getLngLat();
            var popup = m.getPopup();
            var popupHtml = popup ? popup.getHTML() : '';
            var nameMatch = popupHtml.match(/<span[^>]*>([^<]*)<\/span>/);
            return { lat: ll.lat, lon: ll.lng, name: nameMatch ? nameMatch[1] : null };
        });
        removePoiMarkersForType(targetMap, poi.id);
        placePoiMarkersOnMap(targetMap, poi, points);
    });
}
```

**Behavior:**

1. 🚦 No-ops if the overlay is off, or if either map reference is null.
2. 🔍 For each **enabled** POI type, reads the existing marker positions and popup names from `sourceMap`'s marker store.
3. 🗑️ Removes any stale markers of that type from `targetMap`.
4. 📍 Re-places fresh markers on `targetMap` at the same positions, reconstructing the popup HTML from the extracted name.

This means the user sees **zero loading delay** when toggling the map mode — markers are cloned in-memory from one instance to the other rather than re-fetched from the API.

### 🔄 Call Sites

| 📍 Trigger | 🗺️ `sourceMap` | 🎯 `targetMap` |
|---|---|---|
| `toggle3DMap()` — **2D → 3D** (3D map already initialized) | `map` (2D) | `map3d` (3D) |
| `toggle3DMap()` — **3D → 2D** | `map3d` (3D) | `map` (2D) |
| `setup3DMap()` — on 3D map `load` event (first 3D activation) | `map` (2D) | `map3d` (3D) |

> 💡 **Note:** On the **first** 3D activation, `setup3DMap()` calls `syncPoiMarkersToMap(map, map3d)` inside the `map3d.on('load', ...)` handler — after the new map instance is fully ready — ensuring markers are placed on a loaded WebGL context. On **subsequent** activations, `toggle3DMap()` calls `syncPoiMarkersToMap` directly since the 3D map is already initialized.

---

## 🔀 POI Overlay Switch on Map Mode Change

In addition to synchronizing markers, when the user switches between 2D and 3D modes while the POI overlay is active, `toggle3DMap()` calls `switchPoiOverlay()` to refresh the overlay on the newly active map. This handles the case where the newly visible map may have stale or missing data due to the mode switch.

### ⚙️ `switchPoiOverlay()`

```javascript
async function switchPoiOverlay() {
    if (isPoiOverlayOn) {
        var refMap = (is3DMode && map3d && map3d.isStyleLoaded()) ? map3d : map;
        if (!refMap || !refMap.isStyleLoaded()) return;

        setPoiLoading(true, false);
        var rateLimitHit = false;
        try {
            for (var i = 0; i < POI_TYPES.length; i++) {
                var poi = POI_TYPES[i];
                if (!poiTypeEnabled[poi.id]) continue;
                try {
                    var points = await fetchPointsForPoi(poi, refMap);
                    placePoiMarkersOnMap(map, poi, points);
                    if (map3d) placePoiMarkersOnMap(map3d, poi, points);
                } catch(e) {
                    if (e.isRateLimit) { rateLimitHit = true; break; }
                }
            }
            if (!rateLimitHit) {
                var center = refMap.getCenter();
                lastPoiRefreshPoint = { lat: center.lat, lon: center.lng };
            }
        } finally {
            if (rateLimitHit) {
                setPoiLoading(true, true);
                setTimeout(function() { setPoiLoading(false); }, 3000);
            } else {
                setPoiLoading(false);
            }
        }
    }
}
```

**Key differences from `forceReplotSelectedPoi()`:**

| 🔧 Aspect | `switchPoiOverlay()` | `forceReplotSelectedPoi()` |
|---|---|---|
| 🗑️ Clears existing markers first | ❌ No — places on top of existing | ✅ Yes — full clear then replot |
| 🚦 Guards against `isPoiLoading` | ❌ No | ✅ Yes |
| 📍 Trigger | Map mode switch (`toggle3DMap`) | Watchdog detects missing markers |
| 🎯 Purpose | Ensure freshest data on mode switch | Self-heal after a display failure |

---

## 💾 POI Preference Persistence

Trip Master automatically **saves and restores** the per-layer toggle state of the POI overlay across page reloads and sessions, using the browser's `localStorage` API. No account, no server, and no cookies are required — all data lives entirely in the local browser storage of the device.

### 🗝️ Storage Key

| 🔑 Key | 📋 Storage | 📖 Purpose |
|---|---|---|
| `tripmaster_poi_prefs` | `localStorage` | Persists the `poiTypeEnabled` object — a map of each POI layer ID to its `boolean` toggle state |

### ⚙️ Core Functions

Three dedicated functions manage the full read/write lifecycle of POI preferences:

#### 📖 `getPoiPrefs()` — Read from Storage

Reads and deserializes the raw JSON string stored at `POI_PREFS_KEY`:

```javascript
function getPoiPrefs() {
    try { return JSON.parse(localStorage.getItem(POI_PREFS_KEY)) || {}; }
    catch(e) { return {}; }
}
```

- 🛡️ Wrapped in a `try/catch` — if the stored value is malformed or absent, returns a safe empty object `{}` instead of throwing.
- 📦 Returns a plain `Object` keyed by POI ID (e.g., `{ road_closure: true, ev_charging: false, ... }`).

#### 💾 `savePoiPrefs()` — Write to Storage

Serializes the live `poiTypeEnabled` object and writes it to `localStorage`:

```javascript
function savePoiPrefs() {
    localStorage.setItem(POI_PREFS_KEY, JSON.stringify(poiTypeEnabled));
}
```

- ✏️ Called automatically on every user interaction that changes a POI layer's toggle state.
- 🔄 Overwrites any previous value at the same key — always reflects the current in-memory state.

#### 📂 `loadPoiPrefs()` — Apply Stored State on Boot

Reads persisted preferences and merges them into the live `poiTypeEnabled` object, then updates the POI Panel UI to reflect the restored state:

```javascript
function loadPoiPrefs() {
    var prefs = getPoiPrefs();
    Object.keys(poiTypeEnabled).forEach(function(key) {
        if (typeof prefs[key] === 'boolean') {
            poiTypeEnabled[key] = prefs[key];
        }
    });
    Object.keys(poiTypeEnabled).forEach(function(key) {
        var item = document.querySelector('.poi-panel-item[data-poi="' + key + '"]');
        if (item) item.classList.toggle('active', poiTypeEnabled[key]);
    });
}
```

- 🔒 **Type-safe merge**: only values that are strictly `boolean` in the stored object are applied — unknown or corrupted entries are silently ignored.
- 🎨 Immediately synchronizes the `.poi-panel-item` CSS `.active` class for each POI layer, so the panel checkboxes visually match the restored state even before the user opens the POI panel.
- 🚀 Called once during `initializeSystem()` — the very first function to run after page load.

### 🔁 Persistence Lifecycle

```
┌─────────────────────────────────────────────────────────────┐
│                        PAGE LOAD                            │
│  initializeSystem()                                         │
│       └─► loadPoiPrefs()                                    │
│               ├─► getPoiPrefs()  ──► localStorage.getItem() │
│               ├─► merge into poiTypeEnabled{}               │
│               └─► update .poi-panel-item CSS classes        │
├─────────────────────────────────────────────────────────────┤
│                  USER TOGGLES A POI LAYER                   │
│  togglePoiType(poiId)                                       │
│       ├─► flip poiTypeEnabled[poiId]                        │
│       ├─► update .poi-panel-item CSS class                  │
│       └─► savePoiPrefs()  ──► localStorage.setItem()        │
├─────────────────────────────────────────────────────────────┤
│               PROFILE LOADED (loadProfile)                  │
│  loadProfile(name)                                          │
│       ├─► merge p.poiTypeEnabled into poiTypeEnabled{}      │
│       ├─► update .poi-panel-item CSS classes                │
│       └─► savePoiPrefs()  ──► localStorage.setItem()        │
└─────────────────────────────────────────────────────────────┘
```

### 💽 Stored Data Format

The value written to `localStorage` under `tripmaster_poi_prefs` is a JSON-serialized object with one boolean entry per POI layer ID:

```json
{
  "mobile_patrol": false,
  "speed_camera": true,
  "road_closure": true,
  "ev_charging": false
}
```

| 🔑 Key | 🏷️ POI Layer | ✅ `true` | ❌ `false` |
|---|---|---|---|
| `mobile_patrol` | 👮 Mobile Patrols | Layer toggled ON | Layer toggled OFF |
| `speed_camera` | 📷 Speed Cameras | Layer toggled ON | Layer toggled OFF |
| `road_closure` | 🚧 Road Closures | Layer toggled ON | Layer toggled OFF |
| `ev_charging` | ⚡ EV Charging | Layer toggled ON | Layer toggled OFF |

> 💡 **Note:** Persisted preferences record only **which layers the user had enabled**, not the live marker data itself. Markers are always re-fetched from the live APIs (Overpass / Waze) when the overlay is activated after a page reload — the saved state simply pre-checks the correct layer toggles in the POI Panel.

### ⏱️ Save Triggers

`savePoiPrefs()` is called automatically in **three distinct scenarios**, ensuring the stored state is never stale:

| 🔔 Trigger | 📋 Context | 🔧 Calling Function |
|---|---|---|
| 🖱️ User toggles an individual POI layer | POI Panel checkbox click | `togglePoiType(poiId)` |
| 📂 User loads a saved User Profile | Profile modal → load action | `loadProfile(name)` |
| 🔄 User overwrites a saved User Profile | Profile modal → overwrite action | `overwriteProfile(name)` |

### 🔗 Integration with User Profiles

POI layer toggle states are also **embedded inside User Profiles** (stored under `tripmaster_profiles`). When a profile is saved, the entire `poiTypeEnabled` snapshot is captured alongside vehicle weight, battery capacity, GPS polling interval, map mode, theme, and weather overlay state:

```javascript
profiles[name] = {
    vehicleWeight: ...,
    batteryKwh:   ...,
    gpsPolling:   ...,
    theme:        ...,
    is3DMode:     ...,
    isHeadingUp:  ...,
    isWeatherOverlayOn: ...,
    poiTypeEnabled: Object.assign({}, poiTypeEnabled)  // ← POI snapshot
};
```

When the profile is **loaded**, the POI snapshot is merged back into the live `poiTypeEnabled` object and immediately persisted to `localStorage` via `savePoiPrefs()`, so both storage locations stay in sync.

### 🧹 Clearing Persisted POI Preferences

Persisted POI preferences can be cleared manually from the browser's developer tools:

```javascript
// Clear only POI preferences
localStorage.removeItem('tripmaster_poi_prefs');

// Clear all Trip Master data (profiles + POI prefs)
localStorage.removeItem('tripmaster_profiles');
localStorage.removeItem('tripmaster_poi_prefs');
```

> ⚠️ **Note:** After clearing `tripmaster_poi_prefs`, all four POI layers will default to `false` (disabled) on the next page load, matching the compiled-in defaults of the `poiTypeEnabled` object.

---

## 🔋 Battery SOC Auto-Update

During an active trip, the **Current SoC (%)** input and the visual battery bar are **automatically updated in real time** at every GPS fix by `updateBatterySoC()`, showing consumption percentage (%), too.

### ⚙️ How It Works

```javascript
function updateBatterySoC() {
    const cap = parseFloat(document.getElementById('batteryCapacity').value) || 100;
    const netWh = totalConsumedWh - totalRegenWh;
    const newSoc = Math.min(100, Math.max(0, initialSoc - (netWh / (cap * 1000)) * 100));
    document.getElementById('socInput').value = Math.round(newSoc);
    updateBattery();
}
```

| Step | Description |
|---|---|
| 1️⃣ | **Capture initial SoC** — at trip start (`startTracking()`), the current SOC value is stored in `initialSoc` |
| 2️⃣ | **Compute net energy** — `netWh = totalConsumedWh − totalRegenWh` (energy consumed minus energy recovered) |
| 3️⃣ | **Derive new SoC** — subtract the net energy percentage from the initial SoC, clamped to [0, 100] |
| 4️⃣ | **Update UI** — writes the rounded value back to `#socInput` and calls `updateBattery()` to refresh the visual bar and range estimate |

### ✏️ Manual SOC Override with Auto-Update

The system supports **manual SOC adjustments** during an active trip. When the user manually modifies the SOC value — either by using the `−` / `+` stepper buttons or by directly typing a value — the `initialSoc` variable is automatically updated to the new value. This ensures that subsequent auto-update calculations in `updateBatterySoC()` are based on the manually set reference point rather than the original trip-start value.

```javascript
// Stepper buttons: initialSoc is updated on each +/- click
function stepValue(inputId, delta) {
    // ... existing logic ...
    if (inputId === 'socInput') {
        initialSoc = val;
    }
}

// Direct input: initialSoc is updated on every keystroke
// oninput="initialSoc = parseFloat(this.value); updateBattery()"
```

This prevents the auto-update from silently overwriting manual adjustments with the original trip-start SOC value, ensuring that user corrections are preserved throughout the trip.

### 📊 SOC Bar Color States

The battery fill bar transitions through three visual states based on the current SOC percentage:

| SOC Range | CSS Class | Gradient |
|---|---|---|
| $> 30\%$ | *(none)* | 🟢 `#00e676` → `#69f0ae` |
| $15\% < \text{SOC} \leq 30\%$ | `.warn` | 🟡 `#ffd740` → `#ffee58` |
| $\leq 15\%$ | `.critical` | 🔴 `#ff1744` → `#ff5252` |

The bar also features a **sheen overlay** (`linear-gradient(180deg, rgba(255,255,255,0.3) → transparent)`) on the top 40% for a glass-like effect, and a **positive terminal nub** on the right side (via `::after` pseudo-element).

### 🔄 Call Chain

`updateBatterySoC()` is called from `updateLocation()` at every valid GPS step (after the 5 m displacement filter), immediately after `computeRangeEstimate()` and before the POI refresh check.

---

## 🔵 Blue GPS Position Marker

A custom **blue dot marker** tracks the real-time GPS position on both the 2D and 3D maps.

### 🎨 Marker Appearance

Created by `createBlueMarkerElement()`, the marker is a 14×14 px circular `<div>` with:
- **Radial gradient** background: `#64b5f6` (light blue) at 35%/35% → `#1565c0` (dark blue)
- **White border** (2 px solid)
- **Double shadow**: outer ring (`0 0 0 2px rgba(41,182,246,0.5)`) + drop shadow (`0 2px 6px rgba(0,0,0,0.35)`)
- **`pointer-events: none`** — clicks pass through to the map

### 📍 Marker Lifecycle

| Map | Variable | Initialization |
|---|---|---|
| **2D** | `positionMarker` | Created in `map.on('load')` handler inside `setupMap()` — placed at the first GPS fix or at Rome fallback |
| **3D** | `positionMarker3d` | Created in `map3d.on('load')` handler inside `setup3DMap()` — placed at the map center on first 3D activation |

At each GPS step, both markers are repositioned via `marker.setLngLat([longitude, latitude])`.

### 🗺️ Fallback Behavior

If the Geolocation API fails or is unavailable, the marker is placed at **Rome, Italy** (41.8919, 12.5113) as a default position, and weather data is fetched for Rome coordinates.

---

## ⏱️ Trip Time Display

The **Trip Time** stat card (`#tripTimeDisplay`) shows a running wall-clock timer formatted as `HH:MM:SS`.

### ⚙️ Implementation

```javascript
tripTimer = setInterval(() => {
    tripSeconds++;
    const h = String(Math.floor(tripSeconds / 3600)).padStart(2, '0');
    const m = String(Math.floor((tripSeconds % 3600) / 60)).padStart(2, '0');
    const s = String(tripSeconds % 60).padStart(2, '0');
    document.getElementById('tripTimeDisplay').innerText = `${h}:${m}:${s}`;
}, 1000);
```

- Fires every **1 second** independently of the GPS polling interval
- Uses `padStart(2, '0')` for zero-padded formatting
- Resets to `00:00:00` when a new trip is started via `startTracking()`
- The `tripSeconds` counter is also used in the Trip Summary modal to display the total trip duration

---

## 🌙 Dark Theme Map Filter

In dark mode, both the 2D and 3D map instances receive a **CSS brightness filter**:

```css
[data-theme="dark"] #map     { filter: brightness(0.7); }
[data-theme="dark"] #map3d   { filter: brightness(0.7); }
```

This dims the OpenFreeMap `liberty` style tiles by 30%, creating a moody dark cartography effect that matches the overall dark theme without requiring a separate dark tile style. The filter is applied at the CSS level — no JavaScript map style change is needed for the dark map appearance.

---

## 🔘 Stepper Buttons

The **Battery Capacity (kWh)** and **Current SoC (%)** inputs feature **− / + stepper buttons** for quick manual adjustment without typing.

### ⚙️ `stepValue(inputId, delta)` Helper

```javascript
function stepValue(inputId, delta) {
    const input = document.getElementById(inputId);
    const min = input.min !== '' ? parseFloat(input.min) : -Infinity;
    const max = input.max !== '' ? parseFloat(input.max) : Infinity;
    let val = (parseFloat(input.value) || 0) + delta;
    val = Math.min(max, Math.max(min, val));
    input.value = val;
}
```

| Input | Step Delta | Additional Action |
|---|---|---|
| `batteryCapacity` | ±0.5 | None |
| `socInput` | ±1 | Calls `updateBattery()` immediately to sync the visual bar and range estimate |

The helper respects the `min`/`max` HTML attributes and clamps the result, preventing out-of-range values. Stepper buttons are 28×28 px with a hover lift effect (`translateY(-1px)`) and an active press effect (`translateY(0)`).

---

## ✨ Action Button Shine Effect

The **Start Trip**, **Stop Trip** and **Reset Trip** buttons feature a **sweeping shine animation** on hover:

```css
.action-btn::after {
    content: '';
    position: absolute; top: 0; left: -100%; width: 60%; height: 100%;
    background: linear-gradient(90deg, transparent, rgba(255,255,255,0.15), transparent);
    transition: left 0.4s ease;
}
.action-btn:hover:not(:disabled)::after { left: 140%; }
```

A semi-transparent white gradient sweeps across the button from left to right over 400ms. Additionally:
- **Start button** has a 3D push-down effect (`box-shadow: 0 4px 0 #00912a`) that compresses on hover
- **Stop button** has a matching red push-down effect (`box-shadow: 0 4px 0 #9b0000`)
- **Reset button** has a matching violet push-down effect (`box-shadow: 0 4px 0 #7e57c2`)
- When **active/disabled**, buttons dim to 60% opacity with a dark background and `cursor: not-allowed`

---

## 🌦️ Weather Pictogram Mapping

The `getWeatherPictogram(code)` function maps **WMO weather codes** to emoji pictograms:

| WMO Code(s) | Emoji | Condition |
|---|---|---|
| 0 | ☀️/🌙 | Clear sky |
| 1 | 🌤️/🌙☁️ | Mainly clear |
| 2 | ⛅/🌙☁️ | Partly cloudy |
| 3 | ☁️ | Overcast |
| 45 | 🌫️ | Fog |
| 48 | 🌫️ | Depositing rime fog |
| 51 | 🌦️/🌙🌧️ | Light drizzle |
| 53 | 🌦️/🌙🌧️ | Moderate drizzle |
| 55 | 🌦️/🌙🌧️ | Dense drizzle |
| 56 | ❄️💧 | Light freezing drizzle |
| 57 | ❄️💧 | Dense freezing drizzle |
| 61 | 🌧️ | Slight rain |
| 63 | 🌧️ | Moderate rain |
| 65 | 🌧️ | Heavy rain |
| 66 | ❄️🌧️ | Light freezing rain |
| 67 | ❄️🌧️ | Heavy freezing rain |
| 71 | ❄️ | Slight snow fall |
| 73 | ❄️ | Moderate snow fall |
| 75 | ❄️ | Heavy snow fall |
| 77 | ❄️ | Snow grains |
| 80 | 🌦️/🌙🌧️ | Slight rain showers |
| 81 | 🌦️/🌙🌧️ | Moderate rain showers |
| 82 | 🌧️ | Violent rain showers |
| 85 | 🌨️ | Slight snow showers |
| 86 | 🌨️ | Heavy snow showers |
| 95 | 🌩️ | Thunderstorm |
| 96 | ⛈️ | Thunderstorm with slight hail |
| 99 | ⛈️⚡ | Thunderstorm with heavy hail |
| *(other)* | N/A | Fallback for unmapped codes |

---

## 🧭 Wind Direction Display

Wind direction is converted from degrees to a **cardinal direction with triple arrows**:

```javascript
function getWindDirection(degree) {
    const directions = ['↑↑↑ N', '↗↗↗ NE', '→→→ E', '↘↘↘ SE', '↓↓↓ S', '↙↙↙ SW', '←←← W', '↖↖↖ NW'];
    return directions[Math.round(degree / 45) % 8];
}
```

The degree value is divided by 45 and rounded to the nearest octant, producing one of eight directional labels with enhanced visual arrows for quick recognition.

---

## 🖱️ Modal Click-Outside-To-Close

All three modals (Info, Summary, Profiles) support **click-outside-to-close** via a global `window.onclick` handler in `initializeSystem()`:

```javascript
window.onclick = function(event) {
    if (event.target == document.getElementById('infoModal')) toggleModal(false);
    if (event.target == document.getElementById('summaryModal')) document.getElementById('summaryModal').style.display='none';
    if (event.target == document.getElementById('profilesModal')) closeProfilesModal();
};
```

The check `event.target == modalElement` ensures only clicks on the **backdrop overlay** (not on the modal content itself) trigger dismissal.

---

## 📊 Energy Balance Chart Gradient Bars

The Energy Balance horizontal bar chart uses **directional linear gradients** for visual depth:

| Bar | Gradient Direction | Colors |
|---|---|---|
| **Consumed** (red) | Right → Left | `rgba(255,23,68,0.95)` → `rgba(200,0,40,0.7)` |
| **Recovered** (green) | Right → Left | `rgba(0,230,118,0.95)` → `rgba(0,180,90,0.7)` |

The gradients are created dynamically via `ctx.chart.ctx.createLinearGradient(ctx.chart.width, 0, 0, 0)`, flowing from the bar tip (right) toward the origin (left), giving a "fading energy" visual metaphor. Bars also feature `borderRadius: 5` and `borderSkipped: false` for rounded corners on all sides.

---

## 📐 Responsive Layout Adaptations

Trip Master includes two `ResizeObserver`-based scripts that automatically adapt the UI layout to available screen space without requiring a page reload.

### 🗺️ Map Overlay Button Auto-Hide

When the `.map-wrapper` element's height collapses below **50 px** (e.g., in very narrow viewports or when the browser collapses the map section), all six map overlay controls — the 🌍 `3D` toggle button, the 🔺 heading button, the zoom button group, the ⛈️ weather overlay button, the 📌 POI overlay button, and the ↕️ fullscreen button — are automatically hidden:

```javascript
function updateMapBtnVisibility(height) {
    var hidden = height < 50;
    toggle.style.display = hidden ? 'none' : '';
    heading.style.display = hidden ? 'none' : '';
    zoomGroup.style.display = hidden ? 'none' : '';
    fullscreen.style.display = hidden ? 'none' : '';
    weather.style.display = hidden ? 'none' : '';
    poi.style.display = hidden ? 'none' : '';
}
```

A `ResizeObserver` is attached to `.map-wrapper` on `DOMContentLoaded` and fires `updateMapBtnVisibility` on every height change, ensuring no overlay controls are rendered on an unusably small map area.

### 🔋 Battery Range Group Stacking

When the `.battery-range-group` container's width drops below **200 px**, a `.battery-stacked` CSS class is added to `.range-card`. This triggers a CSS layout switch where the battery bar and the two range sections stack vertically instead of rendering side by side, preserving readability on narrow screens:

```javascript
function updateBatteryLayout() {
    var width = batteryGroup.offsetWidth;
    if (width < 200) {
        rangeCard.classList.add('battery-stacked');
    } else {
        rangeCard.classList.remove('battery-stacked');
    }
}
```

A `ResizeObserver` on `.range-card` re-evaluates the layout breakpoint on every resize, making the battery widget fluid across all viewport sizes.

---

## 📂 Card Folding & Maximized Map View

To maximize the screen real estate dedicated to the map view without entering full-screen mode, Trip Master implements a **collapsible card system** 📁. This allows users to hide non-essential charts and panels dynamically.

### ↕️ Interaction Mechanism

- 🖱️ **Clickable Headers**: All cards in the **Charts Panel** (Elevation, Consumption, Speed, Energy Balance, Energy Flow, Driving Style, and Weather) feature interactive headers.
- 🔼 **Visual Indicators**: A dynamic arrow (`▴` for expanded, `▾` for collapsed) provides immediate feedback on the card's state.
- 📏 **Vertical Compression**: Collapsed cards are reduced to a fixed height of **32px**, hiding all internal content while keeping the title visible.

### ⚙️ Logic Implementation

The folding logic is handled by a unified CSS class and a JavaScript toggle:

```javascript
function toggleCardCollapse(header) {
    const card = header.parentElement;
    card.classList.toggle('collapsed');
    const arrow = header.querySelector('.collapse-arrow');
    if (arrow) {
        arrow.textContent = card.classList.contains('collapsed') ? '▾' : '▴';
    }
}
```

```css
.collapsed {
    height: 32px !important;
    overflow: hidden !important;
    padding-top: 0 !important;
    padding-bottom: 0 !important;
}
```

### 🔍 Focus Mode

By folding all side cards, the map area expands to fill the available width, creating a **Map-Centric Focus Mode** 🗺️ without losing the ability to quickly peek at data by unfolding a single card.

> 💡 **Note**: Primary system cards (System Configuration, Battery & Range, Trip Costs, and Trip Statistics) are excluded from the folding system to ensure critical mission data is always visible.

---

## 📦 Dependencies

All dependencies are loaded from CDN — no `npm install` required.

| Library | Version | Purpose | CDN |
|---|---|---|---|
| 🌐 MapLibre GL JS | `4.7.1` | WebGL-powered vector map engine for both 2D and 3D modes | unpkg |
| 📊 Chart.js | `latest` | All real-time charts | jsDelivr |
| 📌 chartjs-plugin-annotation | `3.0.1` | Zero-baseline annotation line on Consumption chart | jsDelivr |
| 🌦️ Open-Meteo API | — | Live weather data | Free REST API |
| 🌍 OpenFreeMap Tiles | — | Vector map styles (`liberty`) for both 2D and 3D | OpenFreeMap CDN |
| 🔤 Google Fonts (Syne) | — | UI typography | Google CDN |
| 🔤 Google Fonts (JetBrains Mono) | — | Numeric readouts | Google CDN |

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
