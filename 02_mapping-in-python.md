---
jupyter:
  jupytext:
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.1'
      jupytext_version: 1.1.0
  kernelspec:
    display_name: Python 3
    language: python
    name: python3
---

# Lab 02 - Mapping in Python

**Author**: Kenneth Wong (khwongk12@gmail.com)

**Last Edited**: TODO

---

## Setup


```python
!pip3 install geopandas contextily shapely matplotlib
```

```python
import geopandas as gpd
import contextily as ctx # for basemaps
from shapely.geometry import Point, LineString, Polygon
from matplotlib import pyplot as plt
```

---

## Spatial Data

Intrinsically, there are 3 vector data types: **point**, line and **polygon**.

![Types of vector objects](https://datacarpentry.org/organization-geospatial/fig/dc-spatial-vector/pnt_line_poly.png)

- **Points:** Each point is defined by a single x, y coordinate. There can be many points in a vector point file. Examples of point data include: sampling locations, the location of individual trees, or the location of survey plots.
- **Lines:** Lines are composed of many (at least 2) points that are connected. For instance, a road or a stream may be represented by a line. This line is composed of a series of segments, each “bend” in the road or stream represents a vertex that has defined x, y location.
- **Polygons:** A polygon consists of 3 or more vertices that are connected and closed. The outlines of survey plot boundaries, lakes, oceans, and states or countries are often represented by polygons.

Read more: https://datacarpentry.org/organization-geospatial/02-intro-vector-data/

---

## Import spatial data to Jupyter Notebook

### Getting spatial data from web

For this notebook, we are using data in *Shapefile* format representing distributions of specific beautifully colored fish species called Damselfish and the country borders of Europe.

We're going to use the `wget` terminal command to download a file from a url. We then use `unzip` to unzip the archive into a folder of the same name. The `-o` option is used to overwrite the folder if it already exists We then us `ls` to see the contents of the folder.

```python
!wget https://github.com/Automating-GIS-processes/FEC/raw/master/data/DAMSELFISH.zip -O fish_data.zip
!unzip -o fish_data.zip -d fish_data
!ls fish_data
```

### Introduction to Geopandas

**Geopandas** (http://geopandas.org/) makes it possible to work with geospatial data in Python in a relatively easy way. Geopandas combines the capabilities of the data analysis library [**pandas**](https://pandas.pydata.org/pandas-docs/stable/) with other packages like [**shapely**](https://shapely.readthedocs.io/en/stable/manual.html) and [**fiona**](https://fiona.readthedocs.io/en/latest/manual.html) for managing spatial data.

Read more about **Geopandas**: https://automating-gis-processes.github.io/site/master/notebooks/L2/geopandas-basics.html

Typically reading the data into Python is the first step of the analysis pipeline. In GIS, there exists various dataformats such as [Shapefile](https://en.wikipedia.org/wiki/Shapefile), [GeoJSON](https://en.wikipedia.org/wiki/GeoJSON), [KML](https://en.wikipedia.org/wiki/Keyhole_Markup_Language), and [GPKG](https://en.wikipedia.org/wiki/GeoPackage) that are probably the most common vector data formats. **Geopandas** is capable of reading data from all of these formats (plus many more). Reading spatial data can be done easily with geopandas using `gpd.read_file()` -function:

```python
# path to shapefile
filepath = "fish_data/DAMSELFISH_distributions.shp"

# Read file using gpd.read_file()
data = gpd.read_file(filepath)
```

### Quick view of data


```python
#look at top entries - looks like a pandas dataframe
data.head()
```

```python
data.columns
```

Note that the data are in (lon, lat) ordering --- this is because the convention is (x, y) for computers, but (lat, lon) for coordinates. This is a frequent cause of error.

```python
data['geometry']
```

```python
# geopandas adds useful attributes to the geodataframe, such as the ability to get bounds
# of all the geometry data
data.bounds
```

```python
# similary, we can get attributes such as boundary
data.boundary
```

---

