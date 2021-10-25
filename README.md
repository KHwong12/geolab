# Geolab - Intro to Python for spatial data

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/KHwong12/geolab)


This repo is a set of notebooks I prepare for the workshop **Introduction to Python language and Google Colab for spatial data visualization and analysis**, a Professional Geospatial Workshop organised by the Geospatial Lab of Hong Kong (see the [poster](https://csdigeolab.gov.hk/en/upcoming-events/professional-geospatial-talk-1015-1022) of the workshop for details).

This workshop aims to let attendances without prior knowledge in coding grasp a taste of Python. Therefore, not much theoretical knowledges are covered. The rundown workshop is organised in a way for attendances to **make maps immediately**. In that way, their motivation could stay high (they could see the product, easily) when need to learn less-fun aspects of spatial data afterwards.

The notebooks (tentatively) covers the following:

- A (very) quick intro to Python
- Using **Google Colab** for Jupyter Notebooks
- Create static maps with **matplotlib** and **contextily**
- Create interactive, dynamic maps with **folium**

---

## How to open and use the notebook

1. In Google Colab, Click **File -> Open notebook** 
2. Click the **GitHub** tab
3. Enter `https://github.com/KHwong12/geolab` for the URL and click Enter
4. Choose the notebook you would like to open

Or, click the Open in Colab badge [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/KHwong12/geolab) on top of this document.

### If the approach above doesn't work

Sometimes, Google Colab requires users to have a GitHub account in order to view the jupyter notebooks, regardless of repository's visibility.

You may need to download this folder to your local computer, then upload and open it in Google Colab.

1. On this Webpage on GitHub, click on the **Code** green button
2. Click **Download ZIP**
3. Unzip the file in your local computer
4. Click **File -> Open notebook** 
5. Click on the **Upload** tab in the pop up window
6. Select the notebook you would like to view and drag it to the **Upload File** area
7. Google Colab should redirect you to a new webpage with the new notebook opened

---

## About the notebooks

The notebooks are written in Markdown, then converted to Jupyter Notebook using the **[jupytext](https://github.com/mwouts/jupytext)** plugin of Jupyter with the following command.

```
jupytext --to notebook THEMDNOTEBOOK.md
```

## References

The open source and open science culture helped me countless number of times to prepare the materials. In particular, part of the notebooks in this workshop are inspired by the following sources:

- The *Geo-python* course (https://geo-python-site.readthedocs.io/en/latest/index.html) by University of Helsinki
- *Data 8: The Foundations of Data Science* (https://github.com/data-8/materials-x19) by UC Berkeley
- BWSI Remote Sensing course (https://github.com/bwsi-hadr)
- *CP255 Urban Informatics and Visualization* by UC Berkeley
