# Location Tracker

Browser-based geospatial tool for mapping retail outlets, validating field claims, and analyzing sales territory coverage.

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![Leaflet](https://img.shields.io/badge/Leaflet-199900?style=flat&logo=leaflet&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=flat)

## Overview

Location Tracker is a single-file web application with no backend dependencies. It accepts CSV data containing outlet coordinates and metadata, renders them on an interactive map, and provides cascading filters by Area, Territory, Town, and Route. All data is stored locally in IndexedDB — no server, no API keys required.

## Use Cases

### TA/DA Verification

- Visualize outlet locations per route to verify Travel Allowance and Dearness Allowance claims
- Calculate approximate route distances using nearest-neighbor path optimization
- Flag outlets with coordinates outside Bangladesh (Lat: 20–29, Lng: 86–95)

### Distributor Coverage Analysis

- Filter by Area, Territory, or Town to define distributor jurisdiction boundaries
- Identify geographic gaps in outlet coverage
- Toggle satellite and street layers for ground-level context

### Route Optimization

- Select multiple routes simultaneously to compare coverage areas
- Nearest-neighbor path drawing connects outlets in geographic order
- Route distance displayed as a real-time KPI

### Data Auditing

- Search outlets by name, code, or route across the full dataset
- Anomalous coordinates separated into a dedicated review panel
- Supports bulk validation of 50,000+ records

## Screenshot

![Location Tracker](images/locationsnap.jpg)

## CSV Format

### Required columns

| Column | Aliases | Description |
|---|---|---|
| `Outlet Latitude` | `Latitude`, `lat` | Decimal latitude |
| `Outlet Longitude` | `Longitude`, `lng` | Decimal longitude |
| `Route Name` | `route` | Sales route identifier |
| `Outlet Name` | `outletName` | Retail outlet name |

### Optional columns (auto-detected)

Additional columns are imported automatically with snake_case keys.

| Column | Purpose |
|---|---|
| `Area Name` | Top-level geographic filter |
| `Territory Name` | Mid-level geographic filter |
| `Town Name` | Town-level filter |
| `Outlet Code` | Unique identifier for search |
| `Distributor Name` | Distributor linkage |
| `Channel` | GT / MT / Pharmacy classification |

### Sample

```csv
Outlet Latitude,Outlet Longitude,Route Name,Outlet Name,Area Name,Territory Name,Town Name,Outlet Code
23.8103,90.4125,Route-Gulshan-01,Karim Store,Dhaka Metro,Dhaka North,Gulshan,OUT-0001
23.7515,90.3934,Route-Dhanmondi-03,Rahim Pharmacy,Dhaka Metro,Dhaka South,Dhanmondi,OUT-0002
22.3569,91.7832,Route-CTG-Main,Chattogram Grocery,Chittagong,CTG City,Agrabad,OUT-0003
```
