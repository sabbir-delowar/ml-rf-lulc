# ml-rf-lulc

## Land Use / Land Cover (LULC) Classification for Barishal, Bangladesh

This repository contains code and data for performing supervised LULC classification using Sentinel-2 satellite imagery and Random Forest machine learning. The project leverages Google Earth Engine (GEE) for image collection and processing, combined with local Python workflows for training, prediction, and visualization.

---

## Project Overview

- Use **GEE API** to create cloud-free Sentinel-2 composites clipped to Barishal district boundary.
- Calculate spectral indices: **NDVI**, **NDBI**, **NDWI**.
- Prepare training data using the ESA WorldCover 2021 dataset, reprojected and aligned to Sentinel-2 composites.
- Train a Random Forest classifier to map five simplified LULC classes:
  - Built-up
  - Cropland
  - Vegetation (trees, shrubs, grass)
  - Water
  - Wetland
- Generate and clip LULC predictions to the study area.
- Visualize results as GeoTIFF and PNG with clear legend and masking of NoData pixels.

---

## Repository Structure

```
ml-rf-lulc/
├── data/
│   ├── raw/           # Raw data downloads and composites
│   ├── interim/       # Processed intermediate files (e.g. aligned WorldCover)
│   ├── processed/     # Final clipped and cleaned rasters
├── results/           # PNG maps and visual outputs
├── scripts/           # Modular Python scripts for each pipeline step
│   ├── 1-gee-download.py
│   ├── 2-load-composite.py
│   ├── 3-prepare-worldcover-map.py
│   ├── 4-prepare-training-data.py
│   ├── 5-train-model.py
│   ├── 6-model-deploy.py
│   ├── 7-clip-and-visualize-lulc.py
├── study-area/        # Barishal shapefile and boundary files
├── notebooks/         # Jupyter notebooks for exploration and prototyping
├── .gitignore
└── README.md
```

---

## Getting Started

### Prerequisites

- Python 3.8+
- Google Earth Engine Python API (`earthengine-api`)
- Rasterio, GeoPandas, NumPy, Matplotlib
- Git for version control

### Setup

1. Clone this repository:

```bash
git clone https://github.com/sabbir-delowar/ml-rf-lulc.git
cd ml-rf-lulc
```

2. Install dependencies (preferably in a virtual environment):

```bash
pip install -r requirements.txt
```

3. Authenticate Earth Engine (only once):

```bash
earthengine authenticate
```

---

## Usage

### Run the pipeline step-by-step:

- **Download Sentinel-2 composites** using the GEE API: `scripts/1-gee-download.py`
- **Load and prepare composites**: `scripts/2-load-composite.py`
- **Prepare and align WorldCover map**: `scripts/3-prepare-worldcover-map.py`
- **Prepare training data**: `scripts/4-prepare-training-data.py`
- **Train the Random Forest model**: `scripts/5-train-model.py`
- **Deploy model and predict LULC**: `scripts/6-model-deploy.py`
- **Clip prediction and visualize LULC maps**: `scripts/7-clip-and-visualize-lulc.py`

*Note:* See notebooks for detailed exploration and prototyping.

---

## Output

- Clipped GeoTIFF LULC maps (`data/processed/`)
- Color-coded PNG visualizations (`results/`)

---

## Notes

- Large GeoTIFF files are **excluded from the repo** due to GitHub limits; download or generate using scripts.
- NoData areas outside the study area are masked and shown as white/transparent.
- Future work includes automating the entire pipeline and expanding to other regions.

---

## License

MIT License