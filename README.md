# Trip Master 🚗⚡

**Trip Master** is a high-performance, real-time Electric Vehicle (EV) trip tracking and energy analysis dashboard. Built as a Progressive Web App (PWA), it leverages geolocation and physics-based modeling to provide drivers with instantaneous consumption data, regenerative braking analytics, and terrain mapping.

---

## 🌟 Key Features

* **Real-time Geolocation Tracking**: Live mapping using Leaflet.js with a dedicated "Tesla-inspired" aesthetic.
* **Dynamic Physics Engine**: Calculates energy consumption ($Wh/km$) by accounting for:
    * **Vehicle Mass**: User-configurable weight impacts.
    * **Thermal Efficiency**: Adjusts battery performance based on ambient temperature.
    * **Aerodynamics**: Factors in headwind speeds.
    * **Potential Energy**: Real-time altitude and grade (slope) integration.
* **Energy Recovery Monitoring**: Tracks total regenerative braking gains ($Wh$) during descents.
* **Interactive Analytics**: Three-tier chart system powered by Chart.js:
    * **Altitude Profile**: Visualize the terrain elevation.
    * **Instantaneous Consumption**: Real-time efficiency tracking.
    * **Energy Balance**: Comparative bar chart of energy consumed vs. energy recovered.
* **Responsive & Dark Mode**: Optimized for mobile use with a toggleable Dark/Light UI.

---

## 🧬 The Physics Model

The application calculates consumption using a simplified resistance model within the `calculatePhysics` function:

$$Consumption \approx \frac{BaseResistance + WindResistance + WeightResistance}{Efficiency} + \Delta PotentialEnergy$$

When the resulting energy is negative (e.g., during a steep descent), the system applies a **70% recuperation efficiency** factor to calculate the regenerative braking gain.

---

## 🛠️ Technical Stack

* **Frontend**: HTML5, CSS3 (Custom properties for theming).
* **Mapping**: [Leaflet.js](https://leafletjs.com/) with CartoDB Voyager tiles.
* **Data Visualization**: [Chart.js](https://www.chartjs.org/).
* **Calculations**: Vanilla JavaScript implementation of the Haversine formula and kinetic energy physics.
* **PWA**: Service Worker integration for offline readiness and "Add to Home Screen" support.

---

## 🚀 Getting Started

1.  **Clone the repository**:
    ```bash
    git clone [https://github.com/yourusername/trip-master.git](https://github.com/yourusername/trip-master.git)
    ```
2.  **Deployment**:
    Since this is a client-side application, you can simply open `index.html` in any modern browser. For PWA features (Service Workers), it is recommended to serve it via HTTPS or a local server.
3.  **Usage**:
    * Enter your vehicle's parameters (Weight, Temperature, Wind).
    * Grant Location Permissions when prompted.
    * Press **Start Trip** to begin recording data.

---

## 📱 Mobile Installation

Trip Master is designed to feel like a native app.
* **iOS**: Open in Safari -> Share -> "Add to Home Screen".
* **Android**: Open in Chrome -> Settings -> "Install App".

---

**Developed for EV Enthusiasts.** *Disclaimer: This tool provides estimates based on physics models and GPS data; actual vehicle telemetry may vary.*

---
