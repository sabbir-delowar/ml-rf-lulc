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
├── results/           # PNG maps and visual outputs
├── notebooks/           # Jupyter notebooks
│   ├── 1-gee-download.ipynb
│   ├── 2-load-composite.ipynb
│   ├── 3-prepare-worldcover-map.ipynb
│   ├── 4-prepare-training-data.ipynb
│   ├── 5-train-model.ipynb
│   ├── 6-model-deploy.ipynb
│   ├── 7-clip-and-visualize-lulc.ipynb
├── study-area/        # Barishal shapefile and boundary files
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

### Run the pipeline step-by-step: open in JupyterLab/Notebook and run cells top to bottom

- **Download Sentinel-2 composites** using the GEE API: `notebooks/1-gee-download.ipynb`
- **Load and prepare composites**: `notebooks/2-load-composite.ipynb`
- **Prepare and align WorldCover map**: `notebooks/3-prepare-worldcover-map.ipynb`
- **Prepare training data**: `notebooks/4-prepare-training-data.ipynb`
- **Train the Random Forest model**: `notebooks/5-train-model.ipynb`
- **Deploy model and predict LULC**: `notebooks/6-model-deploy.ipynb`
- **Clip prediction and visualize LULC maps**: `notebooks/7-clip-and-visualize-lulc.ipynb`


---

## Output

- Clipped GeoTIFF LULC maps (`results/`)
- Color-coded PNG visualizations (`results/`)

---

## Notes

- Large GeoTIFF files are **excluded from the repo** due to GitHub limits; download or generate using scripts.
- Future work includes automating the entire pipeline and expanding to other regions.

---

## License

MIT License