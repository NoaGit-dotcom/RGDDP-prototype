# RGDDP-prototype
Gender Data Resource Discovery Hackathon
# 🌍 Rwanda Gender Data Discovery Portal (RGDDP)

<div align="center">

![Version](https://img.shields.io/badge/version-1.0-brightgreen)
![Platform](https://img.shields.io/badge/platform-Google%20Earth%20Engine-4285F4)
![Language](https://img.shields.io/badge/language-JavaScript-F7DF1E)
![License](https://img.shields.io/badge/license-MIT-green)
![Status](https://img.shields.io/badge/status-Hackathon%20Prototype-orange)
![GIZ](https://img.shields.io/badge/program-GIZ%20%2F%20FAST-1A6B3C)

**A cloud-native geospatial web application that makes Rwanda's gender data visible, accessible, and actionable.**

*GIZ / FAST Program — Gender Data Resource Discovery Hackathon · 19–20 March 2026*

[🚀 Quick Start](#-quick-start) · [✨ Features](#-features) · [🗂 Architecture](#-architecture) · [📡 Data Sources](#-data-sources) · [🔬 Methodology](#-gvi-methodology) · [🛠 Customisation](#-customisation) · [🗺 Roadmap](#-roadmap)

---

</div>

## 📌 Overview

Across Rwanda, critical gender-focused information exists in abundance — but it is **scattered, hard to find, and difficult to navigate**. Datasets from NISR, MIGEPROF, UNFPA, UN Women, REB, RLMUA, Rwanda National Police, and academic institutions sit in incompatible formats across dozens of portals, with no unified discovery layer.

**RGDDP** solves this by providing a single, browser-based geospatial platform built entirely on **Google Earth Engine (JavaScript API)** that:

- 🗺 **Maps** gender indicators across all 30 Rwanda districts in real-time choropleth layers
- 🔍 **Discovers** which districts are data-poor using the Gap Finder module
- 📡 **Fuses** gender statistics with satellite imagery (Sentinel-2, Landsat 8, VIIRS, SRTM)
- 📊 **Analyses** spatial vulnerability patterns via the composite Gender Vulnerability Index (GVI)
- 📂 **Catalogues** 8 gender dataset sources with full provenance metadata
- ⬇ **Exports** GeoTIFF rasters and CSV data directly to Google Drive

> **Zero infrastructure cost.** No server. No licence. No installation. Runs entirely in the browser and publishes as a public Earth Engine App with a single click.

---

## ✨ Features

### 🗺 Explore Tab — Interactive Gender Data Map
| Feature | Description |
|---|---|
| **7 Gender Indicator Layers** | GVI, GBV Incidence, Girls' Enrolment, Female Land Ownership, Maternal Mortality, Women in Leadership, Data Coverage |
| **4 Satellite Context Layers** | Sentinel-2 True Colour, Landsat 8 NDVI, VIIRS Night-Time Lights, SRTM Elevation |
| **Opacity Slider** | Fade between gender choropleth and satellite background to explore spatial correlations |
| **District Inspector** | Click any location → instant district data card with all 6 indicator values |
| **Trend Chart** | 3-point time-series chart (2002 → 2012 → 2022) for girls' enrolment, land ownership, and female leadership |
| **Dynamic Legend** | Colour bar that updates automatically with every layer change |

### 📂 Data Catalogue Tab — Gender Data Resource Discovery
| Feature | Description |
|---|---|
| **8 Institution Cards** | NISR, MIGEPROF, UNFPA, UN Women, REB, RLMUA, Rwanda National Police, University of Rwanda |
| **Full Provenance Metadata** | Dataset name, topic tags, district coverage, file format, year, access status |
| **GEE Asset Paths** | Exact upload paths for connecting real data |
| **Gap Finder Button** | One click activates the data coverage layer showing data-poor districts in red |

### 📊 Analysis Tab — Spatial Intelligence
| Feature | Description |
|---|---|
| **National KPI Cards** | 30 districts, 8 institutions, average GBV rate, average girls' enrolment |
| **Vulnerability Rankings** | Top 3 most and least vulnerable districts identified automatically |
| **Correlation Insights** | Satellite-gender data spatial relationships (NTL ↔ enrolment, NDVI ↔ GBV, etc.) |
| **District GVI Chart** | On-demand bar chart across all 30 districts |
| **GeoTIFF Export** | Export GVI raster at 1km resolution to Google Drive |

### ℹ About Tab
Mission statement, GVI methodology with exact weights, satellite data justification, data source attribution, and hackathon event details.

---

## 🚀 Quick Start

### Prerequisites
- A Google account
- Access to [Google Earth Engine](https://code.earthengine.google.com) (free — sign up at [signup.earthengine.google.com](https://signup.earthengine.google.com))

### Run in 3 Steps

```
1. Open  →  https://code.earthengine.google.com
2. Paste →  Copy the entire RGDDP_GEE_App.js file into the Code Editor
3. Run   →  Click the ▶ Run button
```

The app loads in under 3 seconds. The Gender Vulnerability Index choropleth appears automatically over Rwanda's 30 districts.

### Publish as a Public App

```
Apps → Manage Apps → New App → Configure → Publish
```

This generates a public URL anyone can open in a browser — no GEE account required for viewers.

### Verify Successful Load

Check the **Console** panel (bottom of the Code Editor) for:
```
✅ RGDDP App loaded successfully.
📌 Instructions:
   1. Use the left panel to switch indicators and satellite layers.
   2. Click anywhere on the map to inspect district data.
   3. Switch tabs: Explore | Data Catalogue | Analysis | About
   4. Click "Apps" → "New App" to publish as a public Earth Engine App.
```

---

## 🗂 Architecture

### Script Structure

The application is a single JavaScript file (`RGDDP_GEE_App.js`) organised into **18 clearly labelled sections**:

```
RGDDP_GEE_App.js  (1,531 lines)
│
├── DATA LAYER
│   ├── §0  Global Config & Colour Palette      ← CFG object, 6 map palettes
│   ├── §1  Simulated District Data             ← 30 districts × 8 indicators, GVI formula
│   ├── §2  Satellite Imagery Layers            ← Sentinel-2, Landsat 8, SRTM, VIIRS, WorldPop
│   └── §3  Choropleth Image Painter            ← Vector → Raster conversion for map rendering
│
├── UI LAYER
│   ├── §4  UI Initialisation                   ← Map object, hybrid basemap, control visibility
│   ├── §5  Style Helpers                       ← S object (design system) + 6 factory functions
│   ├── §6  App State & Layer Registry          ← STATE object, LAYERS catalogue (11 layers)
│   ├── §7  Left Side Panel                     ← Header, nav tabs, scrollable content area
│   ├── §8  Explore Tab                         ← Dropdowns, opacity slider, inspector, chart panel
│   ├── §9  Data Catalogue Tab                  ← 8 dataset cards, Gap Finder button
│   ├── §10 Analysis Tab                        ← KPI cards, correlations, chart, export
│   ├── §11 About Tab                           ← Mission, methodology, attribution
│   ├── §14 Dynamic Legend                      ← Floating colour bar, bottom-left of map
│   └── §15 Info Banner                         ← Floating label, top-right of map
│
└── INTERACTION LAYER
    ├── §12 Map Click Handler                   ← District inspector + trend chart trigger
    ├── §13 Map Layer Management                ← updateMapLayer(), updateSatelliteLayer()
    ├── §16 Tab Switching Logic                 ← switchTab(), button highlight updates
    ├── §17 Split Panel Layout                  ← Final assembly → ui.root.add(splitPanel)
    └── §18 Startup & Initialisation            ← Default layer load, boundary draw, console log
```

### Technology Stack

| Component | Technology | Purpose |
|---|---|---|
| Cloud GIS Engine | Google Earth Engine (JavaScript API) | All spatial analysis, server-side rendering, satellite processing |
| Web App Hosting | Earth Engine Apps (`ee.ui` framework) | Instant public URL — zero DevOps |
| Satellite Imagery | Sentinel-2, Landsat 8, SRTM, VIIRS | Environmental and infrastructure context layers |
| Gender Data | GEE FeatureCollection Assets | District-level gender indicator attributes |
| Charts | GEE `ui.Chart` API | In-app interactive bar and line charts |
| Export | GEE `Export.image.toDrive` | GeoTIFF download to Google Drive |
| Boundaries | FAO GAUL 2015 Level-1 | Rwanda district polygon boundaries |

### App Layout

```
┌─────────────────────┬──────────────────────────────────────────┐
│   LEFT PANEL        │                                          │
│   320px wide        │         INTERACTIVE MAP                  │
│                     │         (Google Hybrid Satellite)        │
│  ┌───────────────┐  │                                          │
│  │  🌍 RGDDP    │  │   ┌─────────────────────────────────┐   │
│  │  Header       │  │   │ 🌍 RGDDP · Rwanda Gender Data  │   │
│  └───────────────┘  │   │ Discovery · Click map to inspect│   │
│  [🗺][📂][📊][ℹ]   │   └─────────────────────────────────┘   │
│  ───────────────    │                                          │
│                     │         Choropleth Layer                 │
│  Active Tab Content │         (GVI / GBV / Enrolment…)        │
│  (Explore shown)    │                                          │
│                     │         District Boundary Outline        │
│  ▸ SELECT INDICATOR │                                          │
│  [Gender Dropdown]  │         Satellite Layer (optional)       │
│  [Satellite Dropdown│                                          │
│                     │   ┌──────────────────────┐              │
│  ▸ LAYER OPACITY    │   │ 🔴 Gender Vulnerability│              │
│  [════════════]     │   │ ████████░░░░░░░░░░░░  │              │
│                     │   │ Low / 0   High / 1    │              │
│  ▸ DISTRICT INSPECTOR   └──────────────────────┘              │
│  [Click map…]       │                                          │
└─────────────────────┴──────────────────────────────────────────┘
```

---

## 📡 Data Sources

### Gender Indicator Datasets

| Institution | Dataset | Districts | Format | Status | GEE Asset Path |
|---|---|---|---|---|---|
| **NISR** | Rwanda Population & Housing Census 2022 — Gender Tables | All 30 | CSV / PDF | 🟢 Public | `users/rgddp/nisr_census_2022` |
| **MIGEPROF** | GBV Incidence Report by District 2018–2024 | All 30 | Excel / PDF | 🟡 Restricted | `users/rgddp/migeprof_gbv` |
| **UNFPA** | Maternal Mortality Survey Rwanda 2020 | All 30 | PDF / SPSS | 🟢 Public | `users/rgddp/unfpa_matmort` |
| **REB** | Girls' School Enrolment by District & Level 2022/23 | All 30 | Excel | 🟢 Public | `users/rgddp/reb_enrolment` |
| **RLMUA** | Female Land Title Ownership by Sector 2023 | All 30 | Shapefile / CSV | 🟢 Public | `users/rgddp/rlmua_land` |
| **UN Women** | Women in Leadership Positions — Rwanda 2022 | All 30 | Excel / PDF | 🟢 Public | `users/rgddp/unwomen_leader` |
| **Rwanda National Police** | Isange One Stop Centre Locations & Case Data | 22 | CSV point data | 🟡 Restricted | `users/rgddp/rnp_isange` |
| **University of Rwanda** | Gender & Economic Empowerment Research Dataset 2021 | 12 | CSV / R data | 🟢 Open | `users/rgddp/ur_gender_econ` |

### Satellite Datasets (GEE Public Catalogue — No Upload Required)

| Dataset | GEE Collection ID | Temporal Filter | Use in App |
|---|---|---|---|
| Sentinel-2 Surface Reflectance | `COPERNICUS/S2_SR_HARMONIZED` | 2023, cloud < 15% | True colour visual context |
| Landsat 8 Collection 2 | `LANDSAT/LC08/C02/T1_L2` | 2023, cloud < 20% | NDVI vegetation proxy |
| SRTM Digital Elevation Model | `USGS/SRTMGL1_003` | Static (2000) | Terrain & accessibility |
| VIIRS Night-Time Lights | `NOAA/VIIRS/DNB/MONTHLY_V1/VCMCFG` | 2023 monthly median | Electrification proxy |
| WorldPop Population | `WorldPop/GP/100m/pop` | 2020 | Population density |
| FAO GAUL Boundaries | `FAO/GAUL/2015/level1` | Static | Rwanda district polygons |

---

## 🔬 GVI Methodology

The **Gender Vulnerability Index (GVI)** is a composite score from 0 (least vulnerable) to 1 (most vulnerable), computed from six normalised indicators:

```
GVI = (GBV Rate      × 0.25)
    + (Girls Enrolment× 0.20)   ← inverted: high enrolment = low vulnerability
    + (Female Land    × 0.20)   ← inverted: high ownership  = low vulnerability
    + (Maternal Mort  × 0.20)
    + (Female Leaders × 0.10)   ← inverted: high leadership = low vulnerability
    + (NTL Proxy      × 0.05)   ← inverted: high lights     = low vulnerability
```

### Normalisation

Each indicator is scaled to [0, 1] using min-max normalisation. Indicators where a high value represents a **negative** outcome (GBV rate, maternal mortality) are used directly. Indicators where a high value represents a **positive** outcome (enrolment, land ownership, leadership, night-time lights) are **inverted** (1 − normalised value) so that the GVI always reads: higher score = more vulnerable.

### Weight Rationale

| Indicator | Weight | Justification |
|---|---|---|
| GBV Incidence Rate | 25% | Most direct measure of gender-based harm |
| Girls' Secondary Enrolment | 20% | Structural predictor of lifetime gender outcomes |
| Female Land Ownership | 20% | Economic security and legal empowerment |
| Maternal Mortality Ratio | 20% | Direct measure of health system gender equity |
| Women in Leadership | 10% | Structural change indicator, slower to respond |
| Night-Time Lights (proxy) | 5% | Infrastructure context, not direct gender harm |

### Data Range References (Rwanda DHS / NISR)

| Indicator | Min | Max | Unit |
|---|---|---|---|
| GBV Incidence Rate | 80 | 420 | per 100,000 population |
| Girls' Secondary Enrolment | 42 | 94 | % enrolled |
| Female Land Ownership | 12 | 51 | % of titles held by women |
| Maternal Mortality Ratio | 150 | 560 | per 100,000 live births |
| Women in Leadership | 38 | 72 | % female representation |

---

## 🛠 Customisation

### Connecting Real Data

Replace the simulated data in **Section 1** with your GEE Asset:

```javascript
// BEFORE (prototype)
var districtData = ee.FeatureCollection(featureList);

// AFTER (production)
var districtData = ee.FeatureCollection(
  'users/YOUR_USERNAME/rwanda_districts_gender_2024'
);
```

Your asset must contain these **exact property names**:

```javascript
{
  district     : 'Gasabo',          // string — district name
  province     : 'Kigali',          // string — province name
  gbv_rate     : 245.3,             // number — per 100,000
  girls_enrol  : 78.5,              // number — percentage
  fem_land     : 34.2,              // number — percentage
  mat_mort     : 287.0,             // number — per 100,000 live births
  fem_leader   : 58.4,              // number — percentage
  data_sources : 5,                 // integer — count of datasets
  gvi          : 0.43,              // number — 0 to 1
  gap_status   : 'COVERED',         // string — 'HIGH GAP'|'MODERATE'|'COVERED'
  institution  : 'NISR / MIGEPROF', // string — source institution(s)
  last_updated : '2024-Q4'          // string — last data update
}
```

### Uploading Data to GEE

```bash
# CSV with district name column → GEE Asset
earthengine upload table \
  --asset_id users/YOUR_USERNAME/rwanda_districts_gender_2024 \
  rwanda_gender_2024.csv

# Shapefile → GEE Asset
earthengine upload table \
  --asset_id users/YOUR_USERNAME/rwanda_districts_gender_2024 \
  rwanda_gender_districts.shp
```

Or use the **Assets tab** in the GEE Code Editor: Assets → New → Table upload.

### Changing the Colour Theme

All colours are defined in **Section 0** (`CFG` object). Change one variable to update every element that uses it:

```javascript
var CFG = {
  clrPrimary : '#1A6B3C',  // ← change this to rebrand the entire app
  clrBg      : '#0D1B12',  // ← map and panel background
  clrLight   : '#4CAF7D',  // ← highlights, section headers, legend titles
  // ...
};
```

### Adjusting GVI Weights

In **Section 1**, find the GVI formula and update the weights (they must sum to 1.0):

```javascript
var gvi = nGBV    * 0.25  // ← adjust weights here
        + nEnrol  * 0.20
        + nLand   * 0.20
        + nMat    * 0.20
        + nLeader * 0.10
        + nNTL    * 0.05;
//          total = 1.00  ← must always sum to 1.00
```

### Adding a New Indicator Layer

Three steps:

**Step 1** — Create the raster image in Section 3:
```javascript
var myNewImage = paintIndicator(districtData, 'my_property');
```

**Step 2** — Add an entry to the `LAYERS` object in Section 6:
```javascript
myindicator: {
  label : 'My New Indicator',
  image : myNewImage,
  vis   : { min:0, max:100, palette:['#FF0000','#00FF00'] },
  unit  : 'percentage',
  icon  : '📊',
  desc  : 'Description of what this indicator measures.'
},
```

**Step 3** — Add the key to the `genderLayerKeys` array in Section 8:
```javascript
var genderLayerKeys = ['gvi','gbv','enrol','land','matmort','leader','gap','myindicator'];
```

That is all — the dropdown, legend, info box, and map all update automatically.

### Updating the Data Catalogue

Add a new entry to the `CATALOGUE` array in **Section 9**:

```javascript
{
  id         : 'cat9',
  institution: 'Ministry of Health',
  name       : 'Rwanda Health Facility Census 2024 — Gender Data',
  topics     : ['Health','GBV'],
  districts  : 'All 30',
  format     : 'Excel / CSV',
  year       : '2024',
  status     : 'Public',
  url        : 'https://www.moh.gov.rw',
  geeAsset   : 'users/rgddp/moh_health_gender_2024'
},
```

---

## 📁 Project Structure

```
RGDDP/
├── RGDDP_GEE_App.js          ← Main application script (paste into GEE Code Editor)
├── README.md                 ← This file
├── docs/
│   ├── RGDDP_Proposal.docx   ← Full project proposal (GEE version)
│   └── Script_Explanation.docx ← Detailed section-by-section technical explanation
└── data/
    └── sample/
        └── rwanda_districts_sample.csv  ← Sample CSV showing required property schema
```

---

## 🗺 Roadmap

### Hackathon Prototype (v1.0) — Current
- [x] 30-district GVI choropleth map
- [x] 7 gender indicator layers
- [x] 4 satellite context layers
- [x] Data catalogue with 8 institutions
- [x] District click inspector with trend chart
- [x] Gap Finder module
- [x] GeoTIFF export to Google Drive
- [x] Dynamic legend and info banner
- [x] Published as public Earth Engine App

### Phase 1 — Real Data Integration (Weeks 1–4)
- [ ] Data-sharing MOUs with NISR, MIGEPROF, UNFPA, REB, RLMUA
- [ ] Upload real district-level datasets as GEE Assets
- [ ] Replace `syntheticValue()` generator with real FeatureCollection
- [ ] Validate GVI scores against known district rankings

### Phase 2 — Platform Enhancement (Weeks 4–8)
- [ ] Sentinel-2 time-series animation (land use change 2018–2023)
- [ ] Sector-level granularity (below district, 416 sectors)
- [ ] Automated Python (geemap) ETL pipeline for quarterly data refresh
- [ ] Click-to-download district data as CSV from inspector panel
- [ ] Mobile-responsive layout optimisation

### Phase 3 — Advanced Analysis (Weeks 6–10)
- [ ] Kernel density estimation for GBV hotspot mapping
- [ ] GVI v2 with 10 indicators and peer-reviewed weighting
- [ ] Accessibility analysis — distance to Isange One Stop Centres
- [ ] ML-based vulnerability prediction using `ee.Classifier`
- [ ] Multi-year GVI trend raster (animated time-lapse)

### Phase 4 — Capacity Building & Launch (Weeks 10–12)
- [ ] 2-day GEE training workshop for CSO partners in Kigali
- [ ] User guide in English, French, and Kinyarwanda
- [ ] Video tutorial series (YouTube)
- [ ] Submit to GEE Community Scripts library for global visibility
- [ ] Press release and public launch event

---

## ⚙ GEE-Specific Technical Notes

### Supported Colour Format
GEE's `ui` framework only accepts **6-digit hex colour strings**. The following formats will throw errors and must not be used:

```javascript
// ✅ SUPPORTED
color: '#1A6B3C'
color: '#FFFFFF'

// ❌ NOT SUPPORTED — will throw "Invalid style property" error
color: 'transparent'
color: 'rgba(255, 255, 255, 0.8)'
color: 'green'
```

### Supported Style Properties
GEE's `ui.Label` and `ui.Panel` support a subset of CSS. The following properties are **not supported** and will throw errors:

```javascript
// ❌ NOT SUPPORTED in GEE ui styles
letterSpacing: '1px'
textTransform: 'uppercase'
lineHeight: '1.5'
display: 'flex'        // use ui.Panel.Layout.flow() instead
```

### Layer Stack Order
Layers are stacked in the order they are added. The app manages three layers explicitly:

```
Top     →  District Outline  (districtOutline, green, 60% opacity)
Middle  →  Gender Choropleth (GVI / GBV / Enrolment…, 85% opacity)
Bottom  →  Satellite Layer   (Sentinel-2 / NDVI / NTL / DEM, 75% opacity)
```

Always use `map.layers().add(layer, 0)` to insert at the bottom, and `map.layers().add(layer)` without index to add at the top.

### Lazy Evaluation
GEE does not compute satellite images when the script runs. All `ee.ImageCollection` operations (filtering, selecting, reducing) are registered as a computation graph that only executes when the map requests tiles at a specific zoom level and bounding box. This is why the app loads in under 3 seconds despite referencing petabytes of satellite data.

---

## 🤝 Contributing

This project was built for the GIZ/FAST Gender Data Resource Discovery Hackathon. Contributions that extend the platform toward production deployment are welcome.

### How to Contribute

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/sector-level-data`
3. Make your changes in `RGDDP_GEE_App.js`
4. Test thoroughly in the GEE Code Editor
5. Document new sections following the existing `// ══ SECTION N ══` comment style
6. Submit a pull request with a clear description of what changed and why

### Reporting Issues

If you encounter a GEE-specific error, include:
- The exact error message from the GEE Code Editor console
- The line number and the code block it appears in
- Your GEE Code Editor browser and OS version

---

## 📜 License

```
MIT License

Copyright (c) 2026 GIS & Remote Sensing Engineer — GIZ/FAST Program

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.
```

---

## 🙏 Acknowledgements

| Organisation | Contribution |
|---|---|
| **GIZ / FAST Program** | Hackathon host, problem definition, mentorship, and prize |
| **Google Earth Engine** | Cloud geospatial platform, satellite data catalogue, and App hosting |
| **NISR** | Rwanda census and gender statistics reference data |
| **MIGEPROF** | Gender-based violence data framework and policy context |
| **UNFPA Rwanda** | Maternal health indicator methodology |
| **FAO** | GAUL administrative boundary dataset |
| **NOAA** | VIIRS night-time lights satellite data |
| **USGS** | Landsat 8 and SRTM elevation data |
| **ESA / Copernicus** | Sentinel-2 satellite imagery |

---

## 📞 Contact

**Project:** Rwanda Gender Data Discovery Portal (RGDDP)
**Hackathon:** GIZ / FAST Program — Gender Data Resource Discovery
**Event:** 19–20 March 2026 · GIZ Digital Technical Center, Kigali, Rwanda
**Prize Ceremony:** 23 March 2026

**Registration:** [https://forms.gle/cXbprfqrQJCkjrWs9](https://forms.gle/cXbprfqrQJCkjrWs9)

---

<div align="center">

*"Where satellites meet statistics, advocacy becomes undeniable."*

**Built with ❤ for gender equity in Rwanda · March 2026**

</div>
