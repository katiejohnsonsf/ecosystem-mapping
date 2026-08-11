# ecosystem-mapping

Network analysis and Modeling of Vegetation Classification

## data sources

California Department of Fish and Wildlife Vegetation Datasets
https://wildlife.ca.gov/Data/GIS/Vegetation-Data

IM3 Open Source Data Center Atlas (`data/im3_data_center_atlas.csv`)
https://data.msdlive.org/records/65g71-a4731 (DOI 10.57931/2550666) --
downloaded manually; the repository's own file-download API only serves a
placeholder, so there is no working scripted re-download path.

Washington DNR Natural Heritage Program (WNHP) Element Occurrences --
fetched live from the ArcGIS REST service at
gis.dnr.wa.gov/site2/rest/services/Natural_Heritage/Public_Element_Occurrences
(rare/high-quality plant community records only; USNVC Macrogroup derived
via a scientific-name crosswalk against the USNVC hierarchy table, not a
field in the source data).

LANDFIRE 2025 Existing Vegetation Type (EVT), Washington extract
(`data/wa_landfire_evt/`) -- pulled live via the LANDFIRE Product Service
v2 API (lfps.usgs.gov/api/job/submit) for Washington's bounding box at
990m resolution. Full statewide raster coverage, unlike the sparse WNHP
occurrence points; classifies every pixel by NatureServe's Ecological
System legend rather than the Division/Macrogroup/Group/Alliance/
Association ladder used elsewhere in this notebook.

## Dependencies
- Python 3.8 (project venv in `bin`/`lib`) for most of `cal_eda.ipynb`
- The Cartopy-based coverage map cell, and the Washington cells, need a
  separate `ecomap` conda environment instead (`conda create -n ecomap -c
  conda-forge python=3.11 cartopy geopandas matplotlib numpy pandas
  shapely jupyter ipykernel rasterio`): the project venv's pip-installed
  shapely bundles GEOS 3.11, while Cartopy built against Homebrew's GEOS
  3.14, and mixing the two segfaults. Run those cells' scripts with
  `ecomap`'s Python.
- When running matplotlib scripts headlessly (no display attached, e.g. in
  a background shell), call `matplotlib.use('Agg')` before importing
  `pyplot` -- otherwise `plt.show()` blocks forever waiting on a GUI event
  loop that never resolves.
