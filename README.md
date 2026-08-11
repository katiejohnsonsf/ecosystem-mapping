# ecosystem-mapping

Network analysis and Modeling of Vegetation Classification

## data sources

California Department of Fish and Wildlife Vegetation Datasets
https://wildlife.ca.gov/Data/GIS/Vegetation-Data

## Dependencies
- Python 3.8 (project venv in `bin`/`lib`) for most of `cal_eda.ipynb`
- The Cartopy-based coverage map cell needs a separate `ecomap` conda
  environment instead (`conda create -n ecomap -c conda-forge python=3.11
  cartopy geopandas matplotlib numpy pandas shapely jupyter ipykernel`):
  the project venv's pip-installed shapely bundles GEOS 3.11, while Cartopy
  built against Homebrew's GEOS 3.14, and mixing the two segfaults. Run
  that cell's script with `ecomap`'s Python.
