---
layout: single
permalink: /projects/usda_nass_api_demo/
author_profile: true
toc: true
---

<h1 align="center"> Data Collection: <br> Accessing the USDA-NASS QuickStats API & JSON Parsing </h1>

## Goal
Define a function to quickly obtain state and county yield data for common field crops by directly hitting the USDA-NASS Quickstats API. 

## Overview
USDA-NASS [Quickstats](https://quickstats.nass.usda.gov/) provides a wealth of information about the state of agriculure in the United States. For general queries, the agency provides a simple interface where users can select parameters of interest to filter the database to meet their needs and locally download a csv of the results. While convenient for one-off queries, this is inefficient from a data science perspective. Thus, an [API](https://quickstats.nass.usda.gov/api) is available for direct access to the database. This notebook contains an example function that allows for a data scientist to quickly obtain yield data for commodity crops at various spatial resolutions (e.g., county, district, state, etc.) for downstream use in analysis and modeling. 

## Example Uses