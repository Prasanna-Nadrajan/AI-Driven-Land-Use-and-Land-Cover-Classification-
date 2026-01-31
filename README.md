# 🌍 AI-Driven Land Use and Land Cover Classification  
**Project Code:** P3  

## 📌 Project Title  
**AI-Driven Land Use and Land Cover Mapping using Supervised Machine Learning Algorithms**

---

## 🎯 Objective  
To generate an accurate **Land Use and Land Cover (LULC)** map by applying **supervised Machine Learning (ML)** algorithms on multispectral satellite imagery.  
This project leverages **AI-based classification techniques** to automate land cover mapping and enhance spatial interpretation for geospatial analysis.

---

## 🗺️ Study Area  
The study area is defined using an **Area of Interest (AOI)** shapefile.

### Boundary Shapefile Sources  
- GADM: https://gadm.org  
- DIVA-GIS: https://www.diva-gis.org/gdata  

---

## 🛰️ Data Used  

### Satellite Imagery  

#### Sentinel-2 MSI (10 m spatial resolution)  
**Required Bands:**  
- Band 2 – Blue  
- Band 3 – Green  
- Band 4 – Red  
- Band 8 – Near Infrared (NIR)  

#### Landsat-8 OLI (30 m spatial resolution)  
**Required Bands:**  
- Band 2 – Blue  
- Band 3 – Green  
- Band 4 – Red  
- Band 5 – Near Infrared (NIR)  

---

## 📂 Ancillary Data  
- Area of Interest (AOI) shapefile  
- Google Earth imagery for visual interpretation and validation  

---

## 🌐 Data Sources  
- **USGS Earth Explorer:** https://earthexplorer.usgs.gov/  
- **Copernicus Open Access Hub:** https://scihub.copernicus.eu/  

---

## 🛠️ Software & Tools  
- **QGIS** – Supervised classification, spatial analysis, and map layout  
- **Google Earth Engine (GEE)** – Cloud-based AI classification  
- **Google Earth Pro** – Reference data and visual validation  

---

## 📐 Reference / Validation Data  
- Google Earth Pro: https://www.google.com/earth/versions/#earth-pro  
- Administrative boundaries from:  
  - https://gadm.org/  
  - https://www.diva-gis.org/gdata  

---

## 🔬 Methodology  

### 🧠 QGIS-Based Workflow (AI-Assisted Supervised Classification)

1. Download cloud-free or minimal-cloud satellite imagery.
2. Load required spectral bands into QGIS.
3. Clip raster bands to AOI using:  
   **Raster → Extraction → Clip Raster by Mask Layer**
4. Stack bands into a multiband raster using:
   - Build Virtual Raster (VRT) **or**
   - Merge tool
5. Define LULC classes:
   - Water Bodies  
   - Vegetation / Forest  
   - Agriculture  
   - Built-up / Urban  
   - Barren / Open Land
6. Collect training samples using polygon or point digitization.
7. Train a supervised ML classifier (Random Forest / SVM).
8. Execute classification to generate LULC raster.
9. Apply post-classification refinement (majority filter, noise removal).
10. Convert raster to vector using:  
    **Raster → Conversion → Polygonize**
11. Calculate class-wise area statistics using Field Calculator:  
    ```text
    area($geometry) / 1,000,000
    ```
    *(Area in square kilometers)*
12. Design a professional GIS map layout with legend, scale bar, north arrow, and data sources.

---

### ☁️ Google Earth Engine (GEE) Workflow (AI-Enabled Classification)

1. Define AOI by uploading shapefile or drawing geometry.
2. Load Sentinel-2 Surface Reflectance imagery:
   ```javascript
   var image = ee.ImageCollection("COPERNICUS/S2_SR")
     .filterBounds(aoi)
     .filterDate('2023-11-01', '2023-11-30')
     .filter(ee.Filter.lt('CLOUDY_PIXEL_PERCENTAGE', 10))
     .median();
