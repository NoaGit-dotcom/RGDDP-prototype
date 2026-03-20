# RGDDP-prototype
Gender Data Resource Discovery Hackathon
# Developer: Noa ndacyayisenga

# 🌍 Rwanda Gender Data Discovery Portal (RGDDP)

<div align="center">

![Version](https://img.shields.io/badge/version-1.2-brightgreen)
![Platform](https://img.shields.io/badge/platform-Google%20Earth%20Engine-4285F4)
![Language](https://img.shields.io/badge/language-JavaScript-F7DF1E)
![License](https://img.shields.io/badge/license-MIT-green)
![Status](https://img.shields.io/badge/status-Hackathon%20Prototype-orange)
![GIZ](https://img.shields.io/badge/program-GIZ%20%2F%20FAST-1A6B3C)

**A cloud-native geospatial web application that makes Rwanda's gender data visible, accessible, and actionable.**
🌐 Published Application:
👉https://noahamza64.users.earthengine.app/view/rwanda-gender-data-discovery-portal


*GIZ / FAST Program — Gender Data Resource Discovery Hackathon · 19–20 March 2026*

[🎯 Objective](#-project-objective) · [👤 User Personas](#-user-personas) · [🔄 Key Workflows](#-key-workflows) · [🚀 Setup Steps](#-setup-steps) · [✨ Features](#-features) · [🗂 Architecture](#-architecture) · [📡 Data Sources](#-data-sources) · [🔬 Methodology](#-gvi-methodology) · [🛠 Customisation](#-customisation) · [⚠ Limitations](#-limitations) · [🗺 Next Steps](#-next-steps)

---

</div>

---

## 🎯 Project Objective

Across Rwanda, critical gender-focused information exists in abundance — but it is **scattered, hard to find, and impossible to navigate without specialist tools**. Datasets from NISR, MIGEPROF, UNFPA, UN Women, REB, RLMUA, Rwanda National Police, and academic institutions sit in incompatible formats across dozens of portals with no unified discovery layer.

The **Rwanda Gender Data Discovery Portal (RGDDP)** was built to solve this with four interlocking objectives:

**① Make gender data findable.** The Data Catalogue aggregates 8 institutional sources with full provenance metadata, access status, and file format information — answering "what data exists, who holds it, and how do I get it?" in under one minute from any browser.

**② Make gender data spatially visible.** Seven gender indicators are rendered as interactive choropleth maps across all 30 Rwanda districts, fused with satellite imagery (Sentinel-2, Landsat 8, VIIRS Night-Time Lights, SRTM Elevation) to reveal spatial patterns invisible to tabular analysis.

**③ Produce a composite vulnerability score.** The Gender Vulnerability Index (GVI) combines six normalised indicators into a single 0-to-1 score per district, giving policymakers and funders a defensible, methodologically transparent ranking for resource allocation decisions.

**④ Turn data into advocacy action.** The district inspector, trend charts, Gap Finder module, and GeoTIFF export give CSO officers, journalists, and researchers publication-ready evidence in under 15 minutes — without any GIS training.

> **Zero infrastructure cost.** No server. No licence. No installation. Runs entirely in the browser on Google Earth Engine's cloud and publishes as a public App with a single click.

---

## 👤 User Personas

RGDDP was designed around four distinct user types, each with different needs and different levels of technical expertise. Every feature in the application maps back to at least one of these personas.

---

### Persona 1 — The CSO Programme Officer

**Who:** A programme officer at a Rwandan women's rights organisation (e.g. Haguruka, ActionAid Rwanda, CARE Rwanda). Based in Kigali or a regional town. Works in programme design, monitoring, and fundraising. Has no GIS training. Uses Excel, Word, and PowerPoint daily.

**Pain point:** Needs district-specific gender evidence for funding proposals but spends 3–5 working days contacting multiple ministries, receiving data in incompatible formats, and attempting to manually synthesise statistics.

**How RGDDP helps:**
- Opens the app → clicks a target district → reads a full 6-indicator district profile in 10 seconds
- Uses the Gap Finder to identify data-poor districts and uses this as an advocacy argument for new data investment
- Exports a GeoTIFF map for embedding in a donor proposal — no GIS software needed
- Checks data access status (Public vs Restricted) in the catalogue before deciding which evidence to cite

**Success metric:** Generates a district evidence brief in under 15 minutes instead of 3–5 days.

---

### Persona 2 — The Policy Researcher

**Who:** An academic or think-tank researcher at the University of Rwanda, INES-Ruhengeri, or an international organisation. Has statistical skills. Familiar with Excel and possibly SPSS or R. Limited GIS experience.

**Pain point:** Wants to identify research gaps and spatial patterns in Rwanda's gender data landscape but has no way to see coverage of existing datasets across districts, or to visualise multi-dimensional vulnerability spatially.

**How RGDDP helps:**
- Uses the Data Catalogue to map which institutions hold which datasets and identify districts with fewer than 3 sources (HIGH GAP)
- Switches between indicator layers to explore spatial correlations (e.g. NDVI vs GBV, night-time lights vs enrolment)
- Downloads the GVI GeoTIFF as a starting point for deeper analysis in R or ArcGIS
- Uses the correlation insights panel as leads for new research hypotheses

**Success metric:** Identifies the 5 most under-documented districts in Rwanda in under 5 minutes.

---

### Persona 3 — The Data Journalist

**Who:** A journalist at The New Times Rwanda, KT Press, or an international outlet covering Rwanda. Has strong narrative skills. No GIS experience. Works under deadline pressure.

**Pain point:** Wants to write a data-driven story about gender inequality in Rwanda but cannot build maps, does not know where to find district-level statistics, and cannot verify which data is publicly citable.

**How RGDDP helps:**
- Views the GVI choropleth map to immediately see which provinces and districts show the most acute vulnerability
- Clicks specific districts to get quotable indicator values with units
- Uses the Data Catalogue's access status badges to confirm what is publicly citable without a formal request
- Embeds a screenshot of the interactive map directly in an online article

**Success metric:** Produces a data-driven gender story with district-specific evidence without contacting a single government ministry.

---

### Persona 4 — The District Policymaker

**Who:** A District Executive Secretary, gender focal person, or sector coordinator in one of Rwanda's 30 districts. Has administrative authority over local resource allocation. Limited quantitative analysis experience. Works primarily on mobile.

**Pain point:** Knows gender inequality is a problem in their district but has no unified view of how their district compares to others nationally, or which specific dimension (GBV, education, land, health) is most acute.

**How RGDDP helps:**
- Opens the app on a smartphone browser — no installation required
- Sees immediately where their district sits on the GVI colour spectrum relative to all 30 districts
- Clicks their own district to read all six indicator values and vulnerability classification
- Uses the district comparison chart to present evidence at a budget planning meeting

**Success metric:** Arrives at a budget planning meeting with a one-page district gender profile generated in 2 minutes, with no specialist support.

---

## 🔄 Key Workflows

These are the five primary end-to-end user journeys the application supports.

---

### Workflow 1 — Explore Gender Vulnerability Across Rwanda

**User:** Any persona | **Time:** ~3 minutes | **Tab:** Explore

```
Open app → GVI choropleth loads automatically over 30 districts
    ↓
Use indicator dropdown to switch between 7 gender layers
    ↓
Select a satellite context layer (optional) for environmental correlation
    ↓
Use opacity slider to fade between choropleth and satellite imagery
    ↓
Read the dynamic legend (bottom-left) for value interpretation
    ↓
Observe spatial patterns — which districts are most vulnerable
```

**Outcome:** A visual understanding of Rwanda's gender vulnerability landscape in under 3 minutes, without reading a single report.

---

### Workflow 2 — Inspect a Specific District

**User:** CSO Officer, Journalist, Policymaker | **Time:** ~1 minute | **Tab:** Explore

```
Click any point on the map within Rwanda
    ↓
Loading label shows "⏳ Identifying district..." (1–2 second GEE query)
    ↓
Gold marker appears at click location
    ↓
District Inspector panel fills with:
  · District name and province
  · GVI score + vulnerability level (LOW / MODERATE / HIGH)
  · All 6 indicator values with units
  · Institution, last updated date, data gap status
    ↓
Trend chart appears — 2002 → 2012 → 2022 trajectory
    ↓
Press ✕ Clear to reset and inspect a different district
```

**Outcome:** A complete district gender profile in under 60 seconds. The exact clicked district is always returned via real spatial join (v1.1 fix).

---

### Workflow 3 — Discover Data Sources and Gaps

**User:** Researcher, CSO Officer | **Time:** ~4 minutes | **Tab:** Data Catalogue

```
Click the Data Catalogue tab
    ↓
Browse 8 institution cards:
  · Read dataset title, topic tags, format, access status
  · Note: green badge = Public/Open · amber = Restricted (MOU required)
  · Copy GEE Asset path for production data integration
    ↓
Scroll to Gap Finder → click "🔍 Activate Gap Finder Layer"
    ↓
Map switches to data coverage layer:
  · Red   = HIGH GAP  (1–2 sources)
  · Amber = MODERATE  (3–4 sources)
  · Green = COVERED   (5–8 sources)
    ↓
Identify data-poor districts for research investment advocacy
```

**Outcome:** Complete picture of Rwanda's gender data ecosystem — what exists, who holds it, and where the gaps are.

---

### Workflow 4 — Generate a National Analysis Summary

**User:** Researcher, Policymaker | **Time:** ~2 minutes | **Tab:** Analysis

```
Click the Analysis tab
    ↓
Read national KPI cards (30 districts, 8 institutions, averages)
    ↓
Read vulnerability rankings — top 3 most / least vulnerable districts
    ↓
Read 4 satellite-gender correlation insights
    ↓
Click "📈 Generate District GVI Chart"
    ↓
Click "⬇ Export GVI to Google Drive"
    ↓
Check GEE Tasks tab → Run export → GeoTIFF saved to Drive
```

**Outcome:** National vulnerability overview with publication-ready chart and GeoTIFF raster.

---

### Workflow 5 — Prepare a Funding Proposal Evidence Brief

**User:** CSO Officer | **Time:** ~15 minutes | **Multiple tabs**

```
[1] Workflow 1: Identify target district on GVI map (3 min)
    ↓
[2] Workflow 2: Click target district → read full indicator profile (1 min)
    ↓
[3] Workflow 3: Data Catalogue → check access status → activate Gap Finder (4 min)
    ↓
[4] Return to Explore → select Night-Time Lights → use opacity slider
    to visualise infrastructure–GBV spatial correlation (2 min)
    ↓
[5] Workflow 4: Analysis tab → generate bar chart → export GVI GeoTIFF (2 min)
    ↓
[6] Open GeoTIFF in ArcGIS/QGIS → add labels → export map image (3 min)
    ↓
[7] Insert map + district statistics into funding proposal document
```

**Outcome:** A fully evidenced, spatially grounded funding proposal section in 15 minutes — without contacting a single institution.

---

## 🚀 Setup Steps

### Prerequisites

- A Google account (free)
- Google Earth Engine access — sign up free at [signup.earthengine.google.com](https://signup.earthengine.google.com). Approval typically takes 1–3 days for non-commercial use.

### Step 1 — Open the GEE Code Editor

Navigate to [code.earthengine.google.com](https://code.earthengine.google.com) and sign in.

### Step 2 — Paste the Script

Copy the entire contents of `RGDDP_GEE_App_v1_2.js` and paste into the Code Editor's central text panel.

### Step 3 — Run

Click the **▶ Run** button. The app loads in under 3 seconds. The GVI choropleth appears over Rwanda's 30 districts automatically.

### Step 4 — Verify Successful Load

Check the **Console** panel (bottom of Code Editor) for:
```
✅ RGDDP v1.2 loaded — spatial click fix + Clear button.
📌 Click any district → inspector shows correct data.
   Click "✕ Clear" button to reset the inspector and remove the map marker.
   Publishing: Apps → Manage Apps → New App.
```

### Step 5 — Publish as a Public App (optional)

```
Top menu → Apps → Manage Apps → New App
→ Name: "RGDDP Rwanda"
→ Source: Script in repository
→ Click Publish → copy the generated public URL
```

### Step 6 — Test Before Any Demo

Test the click handler on at least three districts before presenting:

| Test | Expected Result |
|---|---|
| Click Gasabo area (Kigali) | Inspector shows "Gasabo" or Kigali district |
| Click Kirehe area (Eastern) | Inspector shows Eastern Province district |
| Click Rubavu area (Western) | Inspector shows Western Province district |
| Click outside Rwanda | Loading label shows "Outside Rwanda boundaries" |
| Press ✕ Clear | Marker disappears, inspector resets to placeholder |

---

## ✨ Features

### 🗺 Explore Tab — Interactive Gender Data Map

| Feature | Description |
|---|---|
| **7 Gender Indicator Layers** | GVI, GBV Incidence, Girls' Enrolment, Female Land Ownership, Maternal Mortality, Women in Leadership, Data Coverage |
| **4 Satellite Context Layers** | Sentinel-2 True Colour, Landsat 8 NDVI, VIIRS Night-Time Lights, SRTM Elevation |
| **Opacity Slider** | Fade between gender choropleth and satellite background |
| **District Inspector** | Click any location → real spatial query → correct district profile |
| **Clear Button (v1.2)** | Reset inspector, remove marker, return to blank state in one click |
| **Trend Chart** | 3-point time-series chart (2002 → 2012 → 2022) per clicked district |
| **Dynamic Legend** | Colour bar that updates automatically with every layer change |

### 📂 Data Catalogue Tab

| Feature | Description |
|---|---|
| **8 Institution Cards** | NISR, MIGEPROF, UNFPA, UN Women, REB, RLMUA, Rwanda National Police, University of Rwanda |
| **Access Status Badges** | Green = Public/Open · Amber = Restricted (MOU required) |
| **GEE Asset Paths** | Exact upload paths for connecting real data |
| **Gap Finder Button** | Activates data coverage choropleth — red = fewer than 3 sources |

### 📊 Analysis Tab

| Feature | Description |
|---|---|
| **National KPI Cards** | 30 districts, 8 institutions, average GBV rate, average girls' enrolment |
| **Vulnerability Rankings** | Top 3 most and least vulnerable districts auto-identified |
| **Correlation Insights** | 4 satellite-gender spatial relationships |
| **District GVI Chart** | On-demand bar chart for all 30 districts |
| **GeoTIFF Export** | GVI raster at 1km resolution exported to Google Drive |

---

## 🗂 Architecture

### Script Structure

```
RGDDP_GEE_App_v1_2.js  (1,296 lines)
│
├── DATA LAYER
│   ├── §0  Global Config & Colour Palette
│   ├── §1  Spatially Joined District Data      ← FAO GAUL polygons + gender join
│   ├── §2  Satellite Imagery Layers
│   └── §3  Choropleth Image Painter
│
├── UI LAYER
│   ├── §4  UI Initialisation
│   ├── §5  Style Helpers
│   ├── §6  App State & Layer Registry
│   ├── §7  Left Side Panel
│   ├── §8  Explore Tab (incl. Clear button)
│   ├── §9  Data Catalogue Tab
│   ├── §10 Analysis Tab
│   ├── §11 About Tab
│   ├── §14 Dynamic Legend
│   └── §15 Info Banner
│
└── INTERACTION LAYER
    ├── §12 Map Click Handler + clearInspector()
    ├── §13 Map Layer Management
    ├── §16 Tab Switching Logic
    ├── §17 Split Panel Layout
    └── §18 Startup & Initialisation
```

### Technology Stack

| Component | Technology | Purpose |
|---|---|---|
| Cloud GIS Engine | Google Earth Engine (JavaScript API) | Spatial analysis, tile rendering, satellite processing |
| App Hosting | Earth Engine Apps (ee.ui framework) | Instant public URL, zero DevOps |
| Satellite Data | Sentinel-2, Landsat 8, SRTM, VIIRS | Environmental and infrastructure context layers |
| Admin Boundaries | FAO GAUL 2015 Level-2 | Rwanda's 30 district polygons for spatial join |
| Charts | GEE ui.Chart API | Server-side bar and line chart rendering |
| Export | GEE Export.image.toDrive | GeoTIFF to Google Drive |

---

## 📡 Data Sources

### Gender Indicator Datasets

| Institution | Dataset | Status | GEE Asset |
|---|---|---|---|
| **NISR** | Rwanda Census 2022 — Gender Tables | 🟢 Public | `users/rgddp/nisr_census_2022` |
| **MIGEPROF** | GBV Incidence Report 2018–2024 | 🟡 Restricted | `users/rgddp/migeprof_gbv` |
| **UNFPA** | Maternal Mortality Survey 2020 | 🟢 Public | `users/rgddp/unfpa_matmort` |
| **REB** | Girls' Enrolment 2022/23 | 🟢 Public | `users/rgddp/reb_enrolment` |
| **RLMUA** | Female Land Title Ownership 2023 | 🟢 Public | `users/rgddp/rlmua_land` |
| **UN Women** | Women in Leadership 2022 | 🟢 Public | `users/rgddp/unwomen_leader` |
| **Rwanda National Police** | Isange Centre Case Data | 🟡 Restricted | `users/rgddp/rnp_isange` |
| **University of Rwanda** | Gender Empowerment Dataset 2021 | 🟢 Open | `users/rgddp/ur_gender_econ` |

### Satellite Datasets (GEE Public Catalogue — Free, No Upload Required)

| Dataset | GEE Collection ID | Resolution |
|---|---|---|
| Sentinel-2 Surface Reflectance | `COPERNICUS/S2_SR_HARMONIZED` | 10m |
| Landsat 8 Collection 2 | `LANDSAT/LC08/C02/T1_L2` | 30m |
| SRTM Elevation | `USGS/SRTMGL1_003` | 30m |
| VIIRS Night-Time Lights | `NOAA/VIIRS/DNB/MONTHLY_V1/VCMCFG` | 500m |
| WorldPop Population | `WorldPop/GP/100m/pop` | 100m |
| FAO GAUL Boundaries | `FAO/GAUL/2015/level2` | Vector |

---

## 🔬 GVI Methodology

```
GVI = GBV Rate × 0.25  +  Girls Enrolment × 0.20  +  Female Land × 0.20
    + Maternal Mort × 0.20  +  Female Leaders × 0.10  +  NTL Proxy × 0.05
```

Each indicator is min-max normalised to [0, 1]. Indicators where high values mean good outcomes (enrolment, land, leadership, lights) are inverted. **Higher GVI = more vulnerable.**

| Indicator | Weight | Min | Max | Unit |
|---|---|---|---|---|
| GBV Incidence Rate | 25% | 80 | 420 | per 100,000 |
| Girls' Secondary Enrolment | 20% | 42 | 94 | % |
| Female Land Ownership | 20% | 12 | 51 | % |
| Maternal Mortality Ratio | 20% | 150 | 560 | per 100,000 live births |
| Women in Leadership | 10% | 38 | 72 | % |
| Night-Time Lights Proxy | 5% | 0.02 | 0.85 | 0–1 normalised |

---

## 🛠 Customisation

### Connecting Real Data
```javascript
// Section 1 — replace synthetic block with:
var districtFC = ee.FeatureCollection('users/YOUR_USERNAME/rwanda_districts_2024');
// Required properties: district, province, gbv_rate, girls_enrol, fem_land,
// mat_mort, fem_leader, data_sources, gvi, gap_status, institution, last_updated
```

### Adding a New Indicator (3 steps)
```javascript
// 1. Section 3 — create raster
var myImage = paintIndicator(districtFC, 'my_property');

// 2. Section 6 — add to LAYERS registry
myindicator: { label:'My Indicator', image:myImage,
  vis:{ min:0, max:100, palette:['#FF0000','#00FF00'] },
  unit:'%', icon:'📊', desc:'Description.' },

// 3. Section 8 — add key to genderLayerKeys array
var genderLayerKeys = ['gvi','gbv','enrol','land','matmort','leader','gap','myindicator'];
```

### Adjusting GVI Weights
```javascript
// Section 1 — weights must always sum to 1.00
var gvi = nGBV*0.25 + nEnrol*0.20 + nLand*0.20
        + nMat*0.20 + nLeader*0.10 + nNTL*0.05;
```

---

## ⚠ Limitations

### Data Limitations

**Synthetic data in this prototype.** All district indicator values are generated mathematically within realistic Rwanda ranges. Do not cite RGDDP's district numbers as factual statistics until real institutional datasets are connected.

**GBV under-reporting is severe.** Rwanda's 2020 DHS estimates only ~24% of GBV incidents are formally reported. District GBV rates represent reported cases only — true incidence may be 3–4 times higher. Low reported rates can indicate weak reporting infrastructure rather than genuinely better conditions.

**District name matching is required.** The spatial join matches gender attributes to GAUL polygons by `ADM2_NAME`. If your real dataset uses different spellings, the join silently produces null values. Always normalise district names to exact GAUL spelling before upload.

**DHS 2014–15 data is outdated.** The household survey data analysed during research was from 2014–15. Use the 2019–20 DHS for any production deployment.

**Restricted datasets require MOUs.** MIGEPROF and Rwanda National Police data require formal data-sharing agreements before integration into a public-facing application.

### Technical Limitations

**GEE evaluate() is asynchronous.** The click handler takes 1–3 seconds to return results via server-side spatial query. Wait for the inspector to populate before clicking again.

**GEE ui framework is CSS-limited.** `rgba()` colours, `transparent`, `letterSpacing`, `textTransform`, `display: flex`, and gradients are not supported and will throw `Invalid style property` errors.

**Satellite layers may be slow at high zoom.** Sentinel-2 and Landsat tile rendering at zoom level 12+ can take 5–15 seconds — this is a GEE server-side constraint, not a code bug.

**No offline capability.** Internet connection required at all times.

**Export requires manual task execution.** The GeoTIFF export button submits a task — the user must click "Run" in the GEE Tasks panel before the file appears in Google Drive.

**Trend charts use synthetic time-series.** The 2002–2012–2022 trend is calculated by scaling current values backwards using assumed growth rates — not actual historical district data.

**Mobile layout not optimised.** The 320px fixed sidebar can be cramped on small-screen smartphones.

---

## 🗺 Next Steps

### Immediate (Week 0–2)
- [ ] Submit repository to GIZ/FAST with all four documentation files
- [ ] Present live demo — 19-20 March 2026, GIZ Digital Technical Center
- [ ] Publish as permanent public Earth Engine App with stable URL
- [ ] Register on GEE Community Apps gallery

### Phase 1 — Real Data Integration (Weeks 1–4)
- [ ] Sign data-sharing MOUs with NISR, MIGEPROF, UNFPA, REB, RLMUA
- [ ] Process and upload real district datasets to GEE Assets
- [ ] Replace `syntheticValue()` with real FeatureCollection joins
- [ ] Update GVI min/max ranges to match real data distributions
- [ ] Validate spatial join — confirm all 30 district names match GAUL

### Phase 2 — Platform Enhancement (Weeks 4–8)
- [ ] Sentinel-2 time-series animation (land use change 2018–2023)
- [ ] Sector-level granularity (416 sectors below district)
- [ ] Automated Python (geemap) ETL pipeline for quarterly data refresh
- [ ] Click-to-download district CSV from inspector panel
- [ ] Mobile-responsive layout — sidebar collapses to bottom sheet
- [ ] Real historical time-series data for trend chart

### Phase 3 — Advanced Spatial Analysis (Weeks 6–10)
- [ ] Kernel density estimation — GBV hotspot mapping at sub-district level
- [ ] Isange One Stop Centre accessibility analysis (distance-to-facility)
- [ ] GVI v2 — 10 indicators with peer-reviewed weighting
- [ ] Multi-year GVI animated raster time-lapse
- [ ] ML-based vulnerability prediction using `ee.Classifier`

### Phase 4 — Capacity Building & Sustainability (Weeks 10–12)
- [ ] 2-day GEE training workshop for Rwanda CSO partners in Kigali
- [ ] User guide in English, French, and Kinyarwanda
- [ ] YouTube video tutorial series
- [ ] Submit to GEE Community Scripts library for global replication
- [ ] Press release and public launch with NISR / MIGEPROF co-branding

---

## ⚙ GEE-Specific Technical Notes

### Supported Colour Format
```javascript
color: '#1A6B3C'          // ✅ 6-digit hex only
color: 'transparent'      // ❌ not supported
color: 'rgba(255,255,255,0.8)'  // ❌ not supported
```

### Unsupported Style Properties
```javascript
// ❌ will throw "Invalid style property" in GEE ui styles:
letterSpacing · textTransform · lineHeight · display: 'flex'
```

### Layer Stack Order
```
Top    →  District Outline  (green 1px, 60% opacity)
Middle →  Gender Choropleth (85% opacity, slider-controlled)
Bottom →  Satellite Layer   (75% opacity, optional)
```

### Lazy Evaluation
GEE registers all `ee.ImageCollection` operations as a computation graph executed only when the map requests tiles — this is why the app loads in under 3 seconds despite referencing petabytes of satellite data.

---

## 📁 Repository Structure

```
RGDDP/
├── RGDDP_GEE_App_v1_2.js                    ← Main application script
├── README.md                                 ← This file
├── docs/
│   ├── 01_Architecture_Logic_Note.docx
│   ├── 02_Data_Usage_Provenance_Note.docx
│   ├── 03_Demo_Script_Slides.docx
│   └── 04_Policy_Advocacy_Scenario.docx
└── data/
    └── dhs_gender_district_full.csv          ← DHS 2014-15 district gender summary
```

---

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/sector-level-data`
3. Make changes in `RGDDP_GEE_App_v1_2.js`
4. Test in GEE Code Editor — click 5+ districts, test Clear button, test all 7 indicator layers
5. Document new sections following the `// ══ SECTION N ══` style
6. Submit a pull request with a clear description of what changed and why

---

## 📜 License

```
MIT License — Copyright (c) 2026 GIS & Remote Sensing Engineer — GIZ/FAST Program

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software to deal in the Software without restriction, including the
rights to use, copy, modify, merge, publish, distribute, sublicense, and/or
sell copies of the Software, subject to the above copyright notice appearing
in all copies.
```

---

## 🙏 Acknowledgements

| Organisation | Contribution |
|---|---|
| **GIZ / FAST Program** | Hackathon host, problem definition, mentorship, and prize |
| **Google Earth Engine** | Cloud geospatial platform, satellite data catalogue, App hosting |
| **NISR** | Rwanda census and DHS gender statistics |
| **MIGEPROF** | GBV data framework and National Gender Policy monitoring |
| **UNFPA Rwanda** | Maternal health indicator methodology |
| **FAO** | GAUL level-2 administrative boundary dataset |
| **NOAA** | VIIRS night-time lights satellite data |
| **USGS** | Landsat 8 and SRTM elevation data |
| **ESA / Copernicus** | Sentinel-2 surface reflectance satellite imagery |

---

## 📞 Contact

**Project:** Rwanda Gender Data Discovery Portal (RGDDP) v1.2
**Program:** GIZ / FAST — Gender Data Resource Discovery Hackathon
**Event:** 19–20 March 2026 · GIZ Digital Technical Center, Kigali, Rwanda
**Prize Ceremony:** 23 March 2026
**Registration:** [https://forms.gle/cXbprfqrQJCkjrWs9](https://forms.gle/cXbprfqrQJCkjrWs9)

---

<div align="center">

*"Where satellites meet statistics, advocacy becomes undeniable."*

**Built with ❤ for gender equity in Rwanda · March 2026**

</div>
*"Where satellites meet statistics, advocacy becomes undeniable."*

**Built with ❤ for gender equity in Rwanda · March 2026**

</div>
