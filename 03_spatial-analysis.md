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

# Lab 03 - Fundamental Spatial Analysis

**Author**: Kenneth Wong (kennethwong12.netlify.app)

**Last Edited**: 2021-10-25

---

## Setup

```python
!pip3 install geopandas matplotlib contextily folium
```

```python
import geopandas as gpd
import contextily as ctx # for basemaps
from matplotlib import pyplot as plt
```

---

## About the dataset

The dataset used here is the **Recycling Organisations and Collection Points** from the Geodata Store, with preview available in https://geodata.gov.hk/gs/datasets?c=8ce3a677-ae10-4a5e-91d3-6eacbeef70ec

[API reference](https://geodata.gov.hk/gs/geodataQueryAPI?uuid=8379b096-2c23-4dfb-9e4c-5c60d4683b8f) of the dataset is also available.

## Import data

```python
COLLECTION_PT_URL = "https://geodata.gov.hk/gs/api/v1.0.0/geoDataQuery?q=%7Bv%3A%221%2E0%2E0%22%2Cid%3A8379b096-2c23-4dfb-9e4c-5c60d4683b8f%2Clang%3A%22ENG%22%7D"

collection_pt = gpd.read_file(COLLECTION_PT_URL)
```

## Explore data

```python
collection_pt.head()
```

```python
# find all unique values of district
collection_pt['District'].unique()
```

It is better to map them out.

```python
collection_pt.plot(figsize = (15,15), alpha = 0.6, column = 'District', legend = True)
```

## Fundemental Spatial Analysis

### Filtering data

> What if I only want the collection point within Kwun Tong District?

```python
collection_pt_KT = collection_pt[collection_pt['District'] == 'KWUN TONG']
```

```python
collection_pt_KT.plot()
```


### Compute area within a distance from objects (Buffer)

>  What are the area *within 200 m straight line distance* from the points?

```python
collection_pt_KT_buffer = collection_pt_KT.to_crs(2326).buffer(200)
```

```python
collection_pt_KT_buffer.plot()
```

```python
collection_pt_KT_buffer.plot(color = 'green', markersize = 5, alpha = 0.25)
```


### Create static map

Map it out again...

```python
basemap = collection_pt_KT.to_crs(2326).plot(figsize = (15,15), alpha = 0.6, column = 'District', legend = True)

buffer_map = collection_pt_KT_buffer.plot(ax = basemap, color = 'green', markersize = 5, alpha = 0.25)

ctx.add_basemap(buffer_map, crs = collection_pt_KT_buffer.crs, source = ctx.providers.CartoDB.Positron)
```

---

## Create Interactive Maps

**[folium](https://github.com/python-visualization/folium)** is a Python library for interactive mapping based on **leaflet.js**.

```python
import folium
```

### Create a basic interactive web-map

Let’s first see how we can do a simple interactive web-map without any data on it. We just visualize OpenStreetMap on a specific location of the a world.

First thing that we need to do is to create [a Map instance](https://python-visualization.github.io/folium/modules.html#folium.folium.Map)

```python
# Create a Map instance
m = folium.Map(location = [22.37, 114.12], zoom_start = 11, control_scale = True)

```

The first parameter `location` takes a pair of lat, lon values as list as an input which will determine where the map will be positioned when user opens up the map. `zoom_start` -parameter adjusts the default zoom-level for the map (the higher the number the closer the zoom is). `control_scale` defines if map should have a scalebar or not.

Let’s see what our map looks like:

```python
m
```

### Adding layers to the map

The spatial data we just imported needs to be converted to the format where folium understand. (Think of it as converting a video file from `.mov` to `.mp4` such that the video player could play with it)

Now we have our data stored as **GeoJSON** format, which basically contains the data as text in a similar way that it would be written in the `.geojson` -file.

```python
collection_pt_KT_gjson = folium.features.GeoJson(collection_pt_KT, name = "KT_Collection_Pt")
```

Add it to the map

```python
# Add points to the map instance
collection_pt_KT_gjson.add_to(m)

m
```

Same for the buffer

```python
collection_pt_KT_buffer_gjson = folium.features.GeoJson(collection_pt_KT_buffer, name = "KT_Collection_Buffer")
```

Add it to map also

```python
collection_pt_KT_buffer_gjson.add_to(m)

m
```

---

Consult the official documentation of the **[folium](https://python-visualization.github.io/folium/)** package if you would like to add additional customisation to the interactive map. Some common customisation includes:

- Changing the symbol (marker) of the point
- Changing the fill and border colour of the buffer circles
- Changing the basemap
- Adding popup to show details of the points when user clicks on the data
