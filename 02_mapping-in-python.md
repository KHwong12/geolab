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


