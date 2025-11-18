# Cloudless Raster Mosaic -- Satellite Tile Merging Pipeline

This project delivers a **complete, production-ready pipeline** for
generating a **cloudless, georeferenced satellite mosaic** from multiple
raster tiles.\
The workflow ensures **consistent CRS, spatial resolution, cloud
masking, efficient mosaicing**, and **quality-checked outputs**,
optimized for Google Colab / Kaggle environments.

## ⭐ Key Capabilities

-   Automated dataset download & extraction\
-   Metadata introspection for each input tile\
-   Reprojection + resampling to a unified CRS\
-   Cloud detection using brightness, saturation & reflectance
    thresholds\
-   Morphological cleaning for mask refinement\
-   RAM-efficient mosaic generation using GDAL VRT\
-   Preview generation (PNG + 8-bit GeoTIFF)\
-   Export of metadata CSV + validation report

## 📦 Libraries & Tools

### System / GDAL

-   gdal-bin\
-   libgdal-dev

### Python Libraries

-   rasterio, rioxarray\
-   geopandas\
-   numpy\
-   matplotlib\
-   Pillow (PIL)\
-   rasterstats\
-   scipy\
-   tqdm\
-   subprocess

## 🚀 Execution Workflow

### 1️⃣ Install Dependencies

``` bash
!apt-get update -y && apt-get install -y gdal-bin libgdal-dev
!pip install rasterio rioxarray geopandas matplotlib pillow numpy rasterstats tqdm
```

### 2️⃣ Download & Extract Dataset

Dataset:\
`https://objectstore.e2enetworks.net/btechtasksampledata/data.zip`

Extracts to:

    /content/raster_mosaic_task/

### 3️⃣ Scan & Validate Input Tiles

-   Identifies all `.tif/.tiff` files\
-   Reads CRS, bounds, pixel resolution\
-   Shows RGB preview

### 4️⃣ Standardize Tiles (CRS + Resolution)

All tiles converted to:

-   CRS: EPSG:3857\
-   Resolution: 1.21 m\
-   Datatype: uint8

Output: `standardized_tiles/`

### 5️⃣ Cloud Masking

Cloud detection using:

-   Brightness threshold\
-   Saturation threshold\
-   High reflectance\
-   Morphological opening/closing

Cloud pixels → NoData (0).\
Output: `cloudmasked_tiles/`

### 6️⃣ RAM-Safe Mosaic (GDAL VRT)

-   `gdalbuildvrt`\
-   `gdal_translate`

Final output: `cloudless_mosaic.tif`

### 7️⃣ Preview Outputs

-   `cloudless_mosaic_preview.png`\
-   `cloudless_mosaic_8bit.tif`

### 8️⃣ Metadata & Validation Reports

-   `tiles_metadata.csv`\
-   `mosaic_report.txt`

## ✅ Final Output Summary

    cloudless_mosaic.tif
    cloudless_mosaic_preview.png
    cloudless_mosaic_8bit.tif
    tiles_metadata.csv
    mosaic_report.txt
