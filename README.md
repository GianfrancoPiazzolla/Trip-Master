# ⚡ Trip Master

> **High-performance, real-time EV trip tracking and energy analysis dashboard**

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![PWA](https://img.shields.io/badge/PWA-Ready-blueviolet)](https://web.dev/progressive-web-apps/)
[![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![Leaflet](https://img.shields.io/badge/Leaflet-199900?logo=leaflet&logoColor=white)](https://leafletjs.com/)
[![Chart.js](https://img.shields.io/badge/Chart.js-FF6384?logo=chartdotjs&logoColor=white)](https://www.chartjs.org/)

---

**Trip Master** is a lightweight, zero-dependency, single-file web application designed for **electric vehicle (EV) drivers**. It provides real-time GPS-based trip tracking, physics-accurate energy consumption modelling, live weather integration, and interactive charts — all running entirely in the browser with no backend required.

---

## ✨ Features

### 🗺️ Live GPS Tracking & Map
- Uses the browser's **Geolocation API** with `enableHighAccuracy: true` for precise positioning.
- Renders an interactive map powered by **Leaflet.js** with **CartoDB Voyager** tiles (high-saturation visual style).
- Draws the driven route as a **live red polyline** that updates in real time.
- The map automatically **pans to follow** the current position as the trip progresses.
- Falls back to a default **Rome, Italy** center view if geolocation is unavailable.
- In **dark mode**, the map tile filter is adjusted (`brightness + contrast + saturation`) for comfortable night use.

---

### ⚙️ Trip Configuration Panel
Four configurable parameters available before and during a trip:

| Parameter | Description |
|---|---|
| 🏋️ **Vehicle Weight (Kg)** | Numeric input (default: 2200 kg). Used in physics calculations for rolling resistance and gravitational potential energy. |
| 🌡️ **Thermal Efficiency (%@°C)** | Segmented control selecting battery efficiency based on ambient temperature: **100%** at 20°C, **85%** at 10°C, **70%** at 0°C, **55%** at -10°C. Color-coded green → yellow → orange → red. |
| 💨 **Headwind (Km/h)** | Numeric input for wind resistance, factored into the aerodynamic drag component. |
| 📡 **GPS Polling (s)** | Segmented control for the GPS sampling interval: **1s, 5s (default), 10s, 30s, 60s**. |

> 💡 On app load, the **thermal efficiency preset is automatically selected** based on the current ambient temperature fetched from the weather API.

---

### 📊 Real-Time Statistics Dashboard
Six stat cards updated live during the trip:

| Stat | Unit | Accent |
|---|---|---|
| 📍 **Trip Distance** | Km | Blue |
| 🚗 **Average Speed** | Km/h | Blue |
| ⚡ **Run Consumption** | Wh/Km | Red |
| 🏔️ **Route Altitude** | m | Yellow |
| 📐 **Route Grade** | % | Yellow |
| 🔋 **Brake Regen** | Wh | Green |

---

### 🧠 Physics Engine

#### 📏 Distance — Haversine Formula

The distance between two consecutive GPS coordinates is computed using the **Haversine formula**, which gives the great-circle distance over a spherical Earth of radius $R = 6{,}371{,}000\ \text{m}$:

$$a = \sin^2\!\left(\frac{\Delta\varphi}{2}\right) + \cos\varphi_1 \cdot \cos\varphi_2 \cdot \sin^2\!\left(\frac{\Delta\lambda}{2}\right)$$

$$d = 2R\,\arctan2\!\left(\sqrt{a},\,\sqrt{1-a}\right)$$

where $\varphi$ is latitude and $\lambda$ is longitude, both in radians.

> 🚫 GPS readings with $d \leq 5\ \text{m}$ are **discarded** to suppress positioning noise.

---

#### ⚡ Energy Consumption per Step

For each accepted GPS step of distance $d\ [\text{km}]$, the total energy expenditure is:

$$E_{\text{step}} = \underbrace{R_{\text{base}} \cdot d}_{\text{resistive losses}} + \underbrace{\dfrac{m\,g\,\Delta h}{3600}}_{\text{potential energy}} \qquad [\text{Wh}]$$

where the **base resistance** $R_{\text{base}}$ is:

$$R_{\text{base}} = \frac{120 + 0.8\,v_w + 0.012\,m}{\eta} \qquad \left[\frac{\text{Wh}}{\text{km}}\right]$$

| Symbol | Quantity | Unit |
|---|---|---|
| $m$ | Vehicle mass | kg |
| $g$ | Gravitational acceleration $(9.81)$ | m/s² |
| $\Delta h$ | Altitude change between two GPS points | m |
| $v_w$ | Headwind speed | km/h |
| $\eta$ | Thermal efficiency factor | dimensionless $\in (0,\,1]$ |
| $d$ | Step distance | km |

---

#### 🔋 Regenerative Braking Model

When $E_{\text{step}} < 0$ (downhill or deceleration), energy is **not consumed** but partially recovered at a recovery efficiency of **70%**:

$$E_{\text{step}} < 0 \;\Longrightarrow\; \begin{cases} E_{\text{regen}} \mathrel{+}= \left|E_{\text{step}}\right| \cdot 0.70 \\ E_{\text{consumed}} \mathrel{+}= 0 \end{cases}$$

When $E_{\text{step}} \geq 0$:

$$E_{\text{step}} \geq 0 \;\Longrightarrow\; \begin{cases} E_{\text{consumed}} \mathrel{+}= E_{\text{step}} \\ E_{\text{regen}} \mathrel{+}= 0 \end{cases}$$

The **instantaneous specific consumption** reported in the dashboard is:

$$c_{\text{inst}} = \left\lfloor \frac{E_{\text{step}}}{d} \right\rfloor \qquad \left[\frac{\text{Wh}}{\text{km}}\right]$$

---

#### 📐 Road Grade

The road gradient between two consecutive GPS points is expressed as a percentage:

$$G = \frac{\Delta h}{d_{\text{m}}} \times 100 \qquad [\%]$$

where $d_{\text{m}}$ is the step distance in **metres**.

---

#### 🚗 Average Speed

The average speed over the entire trip is:

$$\bar{v} = \frac{D_{\text{total}}\ [\text{km}]}{\Delta t\ [\text{h}]} \qquad \left[\frac{\text{km}}{\text{h}}\right]$$

where $\Delta t$ is the elapsed time since **Start Trip** was pressed.

---

### 🌡️ Thermal Efficiency Presets

The factor $\eta$ is automatically selected from the current ambient temperature at startup:

| Temperature Range | $\eta$ | Label | Color |
|---|---|---|---|
| $T \geq 20\ °\text{C}$ | $1.00$ | 100% @ 20°C | 🟢 Green |
| $10 \leq T < 20\ °\text{C}$ | $0.85$ | 85% @ 10°C | 🟡 Yellow |
| $0 \leq T < 10\ °\text{C}$ | $0.70$ | 70% @ 0°C | 🟠 Orange |
| $T < 0\ °\text{C}$ | $0.55$ | 55% @ −10°C | 🔴 Red |

---

### 📈 Live Charts (Chart.js)

Four chart panels displayed side by side (2×2 on tablet, stacked on mobile):

| Chart | Type | X-Axis | Description |
|---|---|---|---|
| 🏔️ **Altitude Profile** | Line (filled) | Distance (Km) | Elevation in metres over distance traveled. Orange line. |
| ⚡ **Consumption Profile** | Line (filled) | Distance (Km) | $c_{\text{inst}}\ [\text{Wh/km}]$ over distance. Red line. |
| 🔋 **Energy Balance** | Bar (grouped) | Trip Total | $E_{\text{consumed}}$ (red) vs $E_{\text{regen}}$ (green). |
| 🌤️ **Weather Condition** | Custom widget | — | Live weather panel. |

All charts use `update('none')` for maximum rendering performance. Axis colours adapt dynamically to the active theme.

---

### 🌦️ Live Weather Integration
- Powered by the **Open-Meteo API** (free, no API key required).
- Fetched automatically at **app startup** based on current GPS position.
- **Refreshed every 2 km** of distance traveled during a trip.
- The weather panel displays:
  - 🌡️ Current temperature (°C)
  - ⬇️ Min / Max daily temperature (°C)
  - 💧 Relative humidity (%)
  - 💨 Wind speed (Km/h)
  - 🧭 Wind direction — 8-point compass with arrow glyphs (N ↑, NE ↗, E →, …)
  - 🔵 Surface pressure (hPa)
  - 🌈 Weather pictogram — emoji icon mapped from WMO weather code
- Each value is **colour-coded** on update: 🟢 green if increased, 🔴 red if decreased vs. the previous reading.

---

### 🎮 Trip Controls
- ▶️ **Start Trip** — Begins GPS polling at the configured interval, records `startTime`, disables itself, enables Stop.
- ⏹️ **Stop Trip** — Clears the polling interval, re-enables Start. All accumulated data is preserved for review.

---

### 🌗 Light / Dark Theme
- Toggle button in the header (🌙 / ☀️).
- Full CSS variable-based theming: backgrounds, cards, inputs, borders, labels, and modal overlays.
- Dark mode uses pure black (`#000000`) for OLED-friendly display.
- Map tile filter and chart axis colours update dynamically on toggle.

---

### 📱 Progressive Web App (PWA)
- Includes a **Web App Manifest** (`manifest.json`) for home-screen installability on Android and iOS.
- Registers a **Service Worker** (`sw.js`) for offline caching capability.
- Apple-specific meta tags for full-screen display and status bar styling.
- Requests a **Screen Wake Lock** (`navigator.wakeLock`) on startup to keep the screen on during navigation.

---

### 📐 Responsive Layout

| Breakpoint | Layout |
|---|---|
| > 1100 px | 4-column chart grid |
| 800–1100 px | 2-column chart grid |
| < 800 px | Single-column, scrollable; 250px fixed map; 3-column stat grid |

---

## 🛠️ Tech Stack

| Technology | Role |
|---|---|
| 🌐 **HTML5 / CSS3 / Vanilla JS** | Core application — no build step, no framework |
| 🗺️ **Leaflet.js v1.9.4** | Interactive map rendering |
| 📊 **Chart.js** | Real-time charts |
| 🌦️ **Open-Meteo API** | Free weather data (no API key needed) |
| 📡 **Browser Geolocation API** | GPS positioning |
| 📱 **Service Worker + Manifest** | PWA support |
| 🔒 **Screen Wake Lock API** | Keeps screen active during trips |

---

## 🚀 Getting Started

### Option 1 — Open directly in browser
```bash
git clone https://github.com/gianfrancopiazzolla/Trip-Master.git
cd Trip-Master
open index.html
```

> ⚠️ For GPS and Service Worker to function correctly, the app must be served over **HTTPS** or `localhost`.

### Option 2 — Local development server
```bash
# Python
python3 -m http.server 8080

# Node.js
npx serve .
```
Then open `http://localhost:8080`.

### Option 3 — Static deployment
Upload all files to any static host (GitHub Pages, Netlify, Vercel). No server-side processing required.

---

## 📁 File Structure

```
Trip-Master/
├── index.html          # 🧠 Main application (self-contained)
├── manifest.json       # 📱 PWA manifest
├── sw.js               # ⚙️  Service Worker
├── favicon.ico         # 🔖 Browser tab icon
└── icon-192x192.png    # 📲 PWA home screen icon
```

---

## 📄 License

Distributed under the **MIT License**. Feel free to use, modify, and share.

---

## 👤 Author

**Gianfranco Piazzolla**
- 🐙 GitHub: [@gianfrancopiazzolla](https://github.com/gianfrancopiazzolla)

---

> _Developed for the sustainable mobility community. If you find this tool helpful, please leave a ⭐ on GitHub!_
