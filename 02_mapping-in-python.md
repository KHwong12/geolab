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

<a href=\"https://colab.research.google.com/github/KHwong12/geolab" target=\"_parent\"><img src=\"https://colab.research.google.com/assets/colab-badge.svg\" alt=\"Open In Colab\"/></a>

**Author**: Kenneth Wong (khwongk12@gmail.com)

**Last Edited**: TODO

---

## Setup


```
!pip3 install geopandas contextily shapely matplotlib
```

```python
import geopandas as gpd
import contextily as ctx # for basemaps
from shapely.geometry import Point, LineString, Polygon
from matplotlib import pyplot as plt
```

---



