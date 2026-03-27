# 📍 Location Tracker — Retail Outlet Mapping & Sales Territory Intelligence

> A lightweight, browser-based geospatial tool for mapping retail outlets, optimizing sales routes, validating TA/DA claims, and defining distributor coverage areas — built for FMCG field operations in Bangladesh.

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![Leaflet](https://img.shields.io/badge/Leaflet-199900?style=flat&logo=leaflet&logoColor=white)
![TailwindCSS](https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=flat&logo=tailwindcss&logoColor=white)
![IndexedDB](https://img.shields.io/badge/Storage-IndexedDB-blue?style=flat)
![License](https://img.shields.io/badge/License-MIT-green?style=flat)

---

## 🧭 Overview

**Location Tracker** is a zero-backend, single-file web application that enables sales teams, distributors, and field managers to:

- **Upload CSV data** containing outlet coordinates and metadata
- **Visualize thousands of retail outlets** on an interactive map
- **Filter by Area → Territory → Town → Route** with cascading dropdowns
- **Identify data anomalies** (coordinates outside Bangladesh boundaries)
- **Calculate approximate route distances** using nearest-neighbor path optimization
- **Store everything locally** in the browser via IndexedDB — no server, no API keys, no cost

---

## 🎯 Use Cases

### 1. 🧾 TA/DA Mapping & Verification

Field sales representatives submit Travel Allowance (TA) and Dearness Allowance (DA) claims based on routes visited. This tool helps managers:

- **Verify claimed routes** by visualizing actual outlet locations on a map
- **Cross-check route distances** — the app calculates approximate km covered per route
- **Detect ghost outlets** — coordinates falling outside Bangladesh (Lat: 20–29, Lng: 86–95) are flagged automatically
- **Compare planned vs actual** coverage by filtering specific routes and territories

> **Example:** A Territory Manager claims 45 km travel for "Route-Mirpur-12". Upload the outlet master, filter to that route, and instantly see the mapped distance and outlet spread.

---

### 2. 🏭 Distributor Area Mapping & Coverage Analysis

When onboarding new distributors or evaluating existing ones:

- **Define coverage boundaries** — filter by Area/Territory/Town to see which outlets fall under a distributor's jurisdiction
- **Identify white spaces** — spot geographic gaps where no outlets exist but market potential is present
- **Plan redistribution** — when splitting or merging distributor territories, visualize outlet density to make data-driven decisions
- **Satellite & street view** — toggle map layers to understand real ground-level geography (urban density, road access, etc.)

> **Example:** Filtering "Dhaka North → Uttara → Town-A" shows 87 outlets clustered near the main road, but zero coverage 2 km east — a potential expansion zone.

---

### 3. 📊 Sales Route Optimization

- **Multi-route selection** — select multiple routes simultaneously to compare coverage areas
- **Nearest-neighbor path drawing** — the app connects outlets in geographic order (not data order), giving a realistic travel path
- **Route distance KPI** — see total kilometers per filtered view to balance workload across Sales Officers

---

### 4. 🔍 Outlet Data Auditing

- **Search by outlet name, code, or route** — instantly locate any outlet across the entire database
- **Anomaly detection panel** — outlets with invalid GPS coordinates are separated into a dedicated horizontal-scroll panel with lat/lng details
- **Bulk data validation** — upload 50,000+ records and let the app separate valid from invalid automatically

---

### 5. 🗺️ Territory Review & Beat Planning

- **Cascading filters** replicate the real hierarchy: `Area → Territory → Town → Route`
- **Auto-zoom** — the map automatically adjusts to show all outlets in the current filter selection
- **KPI cards** — total outlet count and route distance update in real-time as filters change

---

## 🖼️ Screenshots

| Map View with Route Lines | Filter Panel | Anomaly Detection |
|:---:|:---:|:---:|
| *Outlets connected by nearest-neighbor path* | *Cascading Area → Route filters* | *Invalid coordinates flagged* |

> Replace the above with actual screenshots of your deployed application.

---

## 📂 CSV Format

The application expects a CSV file with **at minimum** these columns:

| Column Name | Aliases Accepted | Required | Description |
|---|---|---|---|
| `Outlet Latitude` | `Latitude`, `lat` | ✅ | Decimal latitude (e.g., `23.8103`) |
| `Outlet Longitude` | `Longitude`, `lng` | ✅ | Decimal longitude (e.g., `90.4125`) |
| `Route Name` | `route` | ✅ | Sales route identifier |
| `Outlet Name` | `outletName` | ✅ | Name of the retail outlet |

### Optional columns (auto-detected):

Any additional columns in your CSV are automatically imported with snake_case keys. Common useful columns:

| Column | Use Case |
|---|---|
| `Area Name` | Top-level geographic filter |
| `Territory Name` | Mid-level geographic filter |
| `Town Name` | Town-level filter |
| `Outlet Code` | Unique outlet identifier for search |
| `Distributor Name` | Link outlets to distributors |
| `Channel` | GT / MT / Pharmacy classification |
| `Last Visit Date` | Recency tracking |

### Sample CSV

```csv
Outlet Latitude,Outlet Longitude,Route Name,Outlet Name,Area Name,Territory Name,Town Name,Outlet Code
23.8103,90.4125,Route-Gulshan-01,Karim Store,Dhaka Metro,Dhaka North,Gulshan,OUT-0001
23.7515,90.3934,Route-Dhanmondi-03,Rahim Pharmacy,Dhaka Metro,Dhaka South,Dhanmondi,OUT-0002
22.3569,91.7832,Route-CTG-Main,Chattogram Grocery,Chittagong,CTG City,Agrabad,OUT-0003
24.3636,88.6241,Route-Rajshahi-01,Rajshahi Mart,Rajshahi,Rajshahi Sadar,Boalia,OUT-0004
