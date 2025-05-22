---
title: Python Project Cookie Cutter
date: 2025-04-27
description  : "Building a cookie cutter to use on personal python projects."
tags: ["Python"]
hex: "#FECF49"
image : "wip.jpg"
imageart: ""
imageartcapt: ""
---



# Building a cookie cutter 🍪

This project

{{< figure dclass="card-image card-image-blog p-0" fclass="blog-front-image" iclass="img-fluid rounded img-border" src="wip.jpg" alt="Rivers Kasai and Sankuru and buffer around the rivers." caption="Figure 1 - Rivers Kasai and Sankuru (Left). Buffer around the rivers (Right)." >}}

{{< customtable caption="Table 1 - Length of the rivers Kasai, Sankuru and total length of both combined.">}}

| River          | River Length | Unit |
|----------------|--------------|------|
| River Kasai    | 1926         | km   |
| River Sankuru  | 1280         | km   |
| Total length   | 3206         | km   |
{{< /customtable >}}

## Village dataset

After evaluating datasets from various sources and validating them with satellite images, I selected the dataset compiled by the **National Geospatial Intelligence Agency** (NGA) for its completeness and accuracy, featuring 5277 villages in the 50 km buffer zone.

[Download the data][download_village_dataset]

## Population dataset

To estimate the population, I utilized both a well-established dataset and a newer product available at the time of analysis. These datasets are the **Global Human Settlement Layer** (GHSL) published by the **EU Commission, Joint Research Center** and the **Facebook - High-Resolution Population Density Maps** from the Humanitarian Data Exchange platform.

[Facebook- Download the data][facebook_data]
[GHSL - Download the data][ghsl_data]

## Methods and results

The data processing and analysis was carried out using **R Studio** and **QGIS**.Below is a list of the libraries used:

```python
library(sf)
library(dplyr)
library(tidyr) 
library(tmap) 
library(raster)
library(rgdal) 
```

{{gitlabicon href="<https://github.com/marcopizzolato-mp/drc-villages">}}>

From a technical standpoint, allocating population figures to settlement point geometries required resampling the Facebook population raster to match the GHSL raster, which has a resolution of 2x2 km. The allocation of population figures to individual settlements carries a small degree of approximation at the micro-level; for example, if two or more points fall within a 2 km x 2 km square, the population count is evenly distributed among them.

Comparing the two population datasets shows that the GHSL dataset generally estimates higher populations around the Kasai River and lower populations around the Sankuru River. The discrepancy increases further from the rivers into the mainland. However, the overall population figures from both datasets are relatively consistent, with a divergence of only 5.4%.

##### Total Villages Analysis

{{< customtable caption="Table 2 - Population figures for all villages.">}}

| Description       | Village Count  | Population GHSL   | Population FB   | Diff % GHSL-FB |
|-------------------|----------------|-------------------|-----------------|----------------|
| Total villages    | 5,277          | 4,895,775         | 4,631,871       | +5.4%          |
{{< /customtable >}}

##### Villages within 20 km

{{< customtable caption="Table 3 - Population figures for villages within 0 km buffer.">}}

| Description             | Village Count   | Population GHSL   | Population FB   | Diff % GHSL-FB |
|-------------------------|-----------------|-------------------|-----------------|----------------|
| General                 | 2,475           | 2,668,299         | 2,549,717       | +4.4%          |
| Near Sankuru            |   806           | 1,110,766         | 1,165,728       | -4.9%          |
| Near Kasai              | 1,669           | 1,557,533         | 1,383,989       | +11.1%         |
{{< /customtable >}}

##### Villages within 50 km

{{< customtable caption="Table 4 - Population figures for villages within 50 km buffer.">}}

| Description             | Village Count  | Population GHSL   | Population FB   | Diff % GHSL-FB |
|-------------------------|----------------|-------------------|-----------------|----------------|
| General                 | 2,802          | 2,227,476         | 2,082,154       | +6.5%          |
| Near Sankuru            | 1,044          | 715,225           | 839,952         | -17.4%         |
| Near Kasai              | 1,758          | 1,512,251         | 1,242,202       | +17.9%         |
{{< /customtable >}}

**Additional Notes**

- **GHSL**: Represents data from the Global Human Settlement Layer, which provides detailed global population data.
- **FB**: Stands for data derived from Facebook's high-resolution population datasets, used for humanitarian and research purposes.
- Percent differences are calculated based on the discrepancy between GHSL and FB data, highlighting potential variances in data collection methods or actual changes in population.

## R Shiny Web Application

To facilitate the visual exploration of the dataset, I created and deployed a **fully responsive and dynamic** R-Shiny Web Application named **Shiny Afrique**. This application allows users to retrieve information for each village on-click, and to filter villages by distance from the river or by name. Additionally, it dynamically calculates and displays statistics based on the villages visible on the map. These statistics include an histogram depicting the number of villages relative to their distance from the rivers and a table displaying the total population and the average population per village for the current selection.

[Open the Web App][shinyafrique-app]
{{< figure dclass="card-image card-image-blog p-0" fclass="blog-front-image" iclass="img-fluid img-border"
src="shinyapp_layout_min.jpg"
alt="View of the Shiny Afrique landing page."
caption="Figure 2 - View of the Web Application landing page."
link="<https://marcopizzo.shinyapps.io/ShinyAfrique/>" >}}

[download_village_dataset]:"http://geonames.nga.mil/gns/html/namefiles.html"
[ghsl_data]:"https://ghsl.jrc.ec.europa.eu/datasets.php"
[facebook_data]:"https://data.humdata.org/dataset/highresolutionpopulationdensitymaps"
[shinyafrique-app]:"https://marcopizzo.shinyapps.io/ShinyAfrique/"

<!-- Images by Marco Pizzolato -->