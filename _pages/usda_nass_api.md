---
layout: single
permalink: /projects/usda_nass_api_demo/
author_profile: true
toc: true
---

<h1 align="center"> Data Collection: <br> Accessing the USDA-NASS QuickStats API & JSON Parsing </h1>

## Goal
Define a function to quickly obtain state and county yield data for common field crops by directly hitting the USDA-NASS Quickstats API. 

## Hitting the API
USDA-NASS [Quickstats](https://quickstats.nass.usda.gov/) provides a wealth of information about the state of agriculure in the United States. For general queries, the agency provides a simple interface where users can select parameters of interest to filter the database to meet their needs and locally download a csv of the results. While convenient for one-off queries, this is inefficient from a data science perspective. Thus, an [API](https://quickstats.nass.usda.gov/api) is available for direct access to the database. The below code is an example function that allows for a data scientist to quickly obtain yield data for commodity crops at various spatial resolutions (e.g., county, district, state, etc.) for downstream use in analysis and modeling. 

### Load the Required Packages

```
import requests
from urllib.request import urlopen

import numpy as np
import pandas as pd
import janitor
import json
import geojson

import plotly.express as px
import matplotlib.pyplot as plt
import seaborn as sns
import geopandas as gpd

# Personal API key stored elsewhere for this example
from utils import usda_nass_quickstats_api_key

```

### Define the Function

```
# This product uses the NASS API but is not endorsed or certified by NASS.
def GetNassYieldData(api_key:str, crop:str, state_abv:str, agg_level:str, 
                     year:str, year_operator:str, check_row_count=False)->pd.DataFrame:
    """
    This function returns a Pandas DataFrame of USDA NASS Quickstats 
    survey data based on the provided inputs
    
    API info: https://quickstats.nass.usda.gov/api

    Args:
        api_key (str): API key obtained from the USDA at https://quickstats.nass.usda.gov/api
        crop (str): Crop of interest (e.g., corn, soybeans, cotton) \n
        state_abv (str): State postal abbreviation \n
        agg_level (str): Level of data aggregation (e.g., county, state) \n
        year (str): Anchor year to define query output\n
        year_operator (str): Define the years to be queried based on the year specified\n
            __LE= = <= \n
            __LT= = < \n
            __GT= = > \n
            __GE= = >= \n
            __LIKE= = like \n
            __NOT_LIKE= = not like \n
            __NE= = not equal \n
        check_row_count (bool): \n
            True = Print query row count \n
            False = Return query as pandas dataframe \n
    Returns:
            DataFrame: Query results (If check_row_count is False)
    """

    # Define query to obtain yield data based on function parameters
    query = f"""
        source_desc=SURVEY \
        &commodity_desc={crop.upper()} \
        &prodn_practice_desc=ALL PRODUCTION PRACTICES \
        &reference_period_desc=YEAR \
        &year{year_operator}{year} \
        &state_alpha={state_abv.upper()} \
        &agg_level_desc={agg_level.upper()} \
        &unit_desc=BU / ACRE \
        """ 
    
    # Check how many rows the define query will produce
    if check_row_count == True:

        # Set base URL for NASS API row count assessment
        base_url_get_counts = f'https://quickstats.nass.usda.gov/api/get_counts/?key={api_key}&'

        # Assemble full URL to hit API correctly
        url_counts = base_url_get_counts + query

        # Check the number of rows to be returned
        # Hit API for results
        counts_r = requests.get(url_counts)

        # Turn JSON data into a dictionary
        counts_dict = counts_r.json()

        # Print the result if the API request is successful. Otherwise, print the error dict.
        try:
            print(f"This query returns {counts_dict['count']} rows")
        except:
            print(counts_dict)

    # Run the query through the API to get the desired results
    else:
        # Set base URL for NASS API
        base_url = f'https://quickstats.nass.usda.gov/api/api_GET/?key={api_key}&'
        
        # Assemble full URL to hit API correctly
        url = base_url + query

        # Hit API for results
        r = requests.get(url)

        # Turn JSON data into a dictionary
        results_dict = r.json()

        # Convert dict to dataframe
        df = pd.DataFrame(results_dict['data']).clean_names()

        # Convert any empty strings into nan
        df = df.replace(r'^\s*$', np.nan, regex=True)

        # Assign numeric dtype to select columns
        df['year'] = df['year'].astype(int)
        df['value'] = df['value'].astype(float)

        # If the data is queried at the county-level, add the fips code
        if agg_level.upper() == 'COUNTY':

            # Remove multi-county values
            df.dropna(subset='county_ansi', inplace=True)

            df['state_fips_code'] = df['state_fips_code'].astype(str)
            df['county_ansi'] = df['county_ansi'].astype(str)
            df['fips'] = df['state_fips_code'] + df['county_ansi']

        return df
```