---
# the default layout is 'page'
icon: fas fa-info-circle
order: 4
title: ClimateGenerator
---

🌍 **ClimateGenerator** is an interactive tool for downloading, combining, and converting climate data from the **German Weather Service (DWD)** into simulation-ready formats.  
It enables engineers, researchers, and planners to generate consistent weather files for building performance simulations and environmental modeling.

![Climate Generator](/assets/img/screenshot-climategenerator.png)

---

## 🔍 What It Does

- 🛰️ **Accesses Measurement Data**  
  Retrieves hourly measurement data (temperature, humidity, solar radiation, wind, precipitation, etc.) from the official **DWD FTP server**.

- 🧩 **Interactive Data Selection**  
  Choose time periods, measurement stations, and relevant variables through a user-friendly interface or configuration file.

- 🗃️ **Combines Multiple Data Sources**  
  Merges data from different stations (e.g. temperature from one, radiation from another) into a coherent dataset for simulation.

- 🔄 **Converts to Simulation Formats**  
  Generates standard weather file formats such as:
  - **EPW (EnergyPlus Weather File)**
  - **C6B (VICUS/DELPHIN format)**
  - **TSV (Tab-separated values, CSV with Tabs - easy to open in LibreCalc, MS Excel)**

---

## 🛠️ Applications

The generated files can be directly used in:
- **SIM-VICUS** – Dynamic urban district simulation tool
- **DELPHIN** – Coupled heat and moisture simulation tool
- **EnergyPlus / OpenStudio** – Building energy simulation
- Any other simulation software supporting EPW or CSV-based climate input

---

## 📂 Data Sources

All data is based on high-quality measurements from the **Deutscher Wetterdienst (DWD)**:
- Synoptic stations (climate reference)
- Radiation stations (solar components)
- Precipitation and wind data

Access is via the [DWD Open Data FTP](https://opendata.dwd.de/climate_environment/CDC/), which is publicly available.

---

## 🚧 Project Goals

- ✅ Provide a transparent and reproducible way to generate simulation-ready climate files
- ✅ Enable combinations of multiple DWD stations based on proximity or data quality

---

## Download

[⬇️ Download for Windows 64 Bit v1.6.0]({{ site.url }}/assets/installer/ClimateGenerator_1.6.0_win64.exe)
[🐧 Download for Linux 64 Bit v1.6.0]({{ site.url }}/assets/installer/ClimateGenerator_1.6.0_linux.7z)
