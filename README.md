# Trip Master: High-Performance EV Energy Dashboard 🚗⚡

**Trip Master** is a real-time tracking application designed specifically for electric vehicle (EV) enthusiasts and sustainable mobility analysis. Built as a Progressive Web App (PWA), it transforms raw GPS data into actionable energy insights, providing a live "physics-engine" view of your trip's efficiency.

---

## 🌟 Features

* **Real-Time Physics Simulation**: Estimates energy consumption ($Wh/km$) based on vehicle weight, altitude changes, and environmental factors.
* **Real-time Geolocation Tracking**: Live mapping using Leaflet.js and providing a configurable GPS polling interval.
* **Dynamic UI**: Includes a live Leaflet map and three synchronized Chart.js dashboards for Altitude, Consumption, and Energy Balance.
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
* **PWA Ready**: Features a manifest and mobile-optimized viewport for use as a standalone "Web App" on mobile devices.
* **Responsive & Dark Mode**: Optimized for mobile use with a toggleable Dark/Light UI.

---

## 🧮 Calculation Logic & Physics Engine

The core of Trip Master is its ability to estimate energy usage without a direct OBDII connection. It uses the following logic to derive consumption:

### 1. Distance & Slope
The system calculates the distance between two GPS coordinates using the **Haversine formula** to determine the shortest distance over the earth's surface. 
Distance is validated against a 5-meter movement threshold to filter out GPS "jitter" during stops.

### 2. The Energy Formula
For every recorded step, the energy consumption ($Wh$) is calculated using a simplified physics model:

$$E_{step} = \frac{(R_{base} \cdot d_{km}) + E_{pot}}{Efficiency_{temp}}$$

**Where:**
* **Base Resistance ($R_{base}$)**: A derived constant accounting for rolling resistance and aerodynamic drag, adjusted by user-inputted headwind and vehicle weight. The formula used is roughly `(120 + (wind * 0.8) + (weight * 0.012))`.
* **Potential Energy ($E_{pot}$)**: Calculated as $\frac{m \cdot g \cdot \Delta h}{3600}$ to convert Joules to Watt-hours, where $m$ is weight and $\Delta h$ is the change in altitude.
* **Regenerative Braking**: If $E_{step}$ is negative (downhill), the system applies a **70% recuperation efficiency** factor to the potential energy gained, adding it to the "Brake Regen" total.

---

## ⚠️ Known Limitations & Assumptions

To maintain a lightweight, client-side architecture, the following assumptions are made:

* **Aerodynamic Drag**: The model uses a simplified linear scaling for wind resistance rather than a full quadratic drag equation. This is optimized for typical urban and suburban speeds.
* **Constant Efficiency**: The "Temp Efficiency" selection applies a global multiplier to the base resistance to simulate battery internal resistance and HVAC load, but it does not vary dynamically during the trip.
* **GPS Altitude**: The accuracy of "Grade" and "Potential Energy" calculations is highly dependent on the device's GPS altimeter, which can be less precise than barometric sensors.
* **Regen Fixed Rate**: Regenerative braking is capped at a 70% return rate and assumes the battery is not at 100% State of Charge (where regen would be limited).

*Disclaimer: This tool provides estimates based on physics models and GPS data; actual vehicle telemetry may vary.*

---

## 🛠️ Technical Stack

* **Frontend**: HTML5, CSS3 (Custom properties for theming).
* **Mapping**: [Leaflet.js](https://leafletjs.com/) with CartoDB Voyager tiles.
* **Data Visualization**: [Chart.js](https://www.chartjs.org/).
* **Calculations**: Vanilla JavaScript implementation of the Haversine formula and kinetic energy physics.
* **PWA**: Service Worker integration for offline readiness and "Add to Home Screen" support.

---

## 🛠 Installation & Usage

1.  **Clone the repository**:
    ```bash
    git clone [https://github.com/gianfrancopiazzolla/Trip-Master.git](https://github.com/gianfrancopiazzolla/Trip-Master.git)
    ```
2.  **Deployment**:
    Since this is a client-side application, you can simply open `index.html` in any modern browser. For PWA features (Service Workers), it is recommended to serve it via HTTPS or a local server.
3.  **Configuration**: Input your specific **Vehicle Weight**, current **Ambient Temperature**, **Headwind** and **GPS Polling**.
4.  **Usage**:
    * Grant Location Permissions when prompted.
    * Press **Start Trip** to begin recording data.

---

## 📱 Mobile Installation

Trip Master is designed to feel like a native app.
* **iOS**: Open in Safari -> Share -> "Add to Home Screen".
* **Android**: Open in Chrome -> Settings -> "Install App".

---

## 📄 License

This project is distributed under the **MIT License**. Feel free to use, modify, and share.

**Author**: Gianfranco Piazzolla  

---

**Developed for the sustainable mobility community.** If you find this tool helpful, please leave a star! 😉

---
