---
title: Cholera Response DRC
date: 2021-02-16
description  : "Extracting villages location and population estimates to support WASH activity in Democratic Republic of Congo"
tags: ["WASH","HumanitarianResponse","GIS","Maps"]
image : "cholera_frontpage_16x9.jpg"
imageart: "village_river_min.jpg"
imageartcapt: "Village along the river, Bor, South Sudan."
---



# Fighting Cholera in Democratic Republic of Congo

This project began after a call from a friend of mine deployed in the Democratic Republic of Congo (DRC). She reported that cholera outbreaks were ongoing in many villages along the Kasai and Sankuru rivers. Her organization planned to launch a comprehensive Water Sanitation and Hygiene (WASH) campaign targeting all settlements within a 20 km radius and monitoring those between 30 and 50 km from these rivers. They lacked a reliable list of villages with population estimates, and she asked if I could assist by examining available datasets.



"I'll see what I can do," I said. After some days of intensive work, I provided a list of **over 5000** villages located within 20 to 50 km of the two rivers, complete with population estimates from two different datasets and an **interactive R Shiny Web Application** to navigate the results 

## Area of interest
The area of interest is extensive, covering more than 3000 km of river length and an area of approximately 100,000 km<sup>2</sup> within the 20 km buffer and 250,000 km<sup>2</sup> within the 50 km buffer.


{{< figure dclass="card-image card-image-blog p-0" fclass="blog-front-image" iclass="img-fluid rounded img-border" src="drc_layout_min.jpg" alt="Rivers Kasai and Sankuru and buffer around the rivers." caption="Figure 1 - Rivers Kasai and Sankuru (Left). Buffer around the rivers (Right)." >}}


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

```
library(sf)
library(dplyr)
library(tidyr) 
library(tmap) 
library(raster)
library(rgdal) 
```
{{< gitlabicon href="https://github.com/marcopizzolato-mp/drc-villages">}}

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
link="https://marcopizzo.shinyapps.io/ShinyAfrique/" >}}



    
[download_village_dataset]:"http://geonames.nga.mil/gns/html/namefiles.html"
[ghsl_data]:"https://ghsl.jrc.ec.europa.eu/datasets.php"
[facebook_data]:"https://data.humdata.org/dataset/highresolutionpopulationdensitymaps"
[shinyafrique-app]:"https://marcopizzo.shinyapps.io/ShinyAfrique/"

<!-- Images by Marco Pizzolato -->