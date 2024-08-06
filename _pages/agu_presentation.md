---
layout: collection
author_profile: true
---

<h1 align="center"> Field-Scale Greenhouse Gas <br> Emissions Modeling </h1>


[Presented at the 2023 American Geophysical Union Annual Meeting](https://agu.confex.com/agu/fm23/meetingapp.cgi/Paper/1395322)



<p align="center">
    <a href="/images/agu_2023/agu_2023_title_slide.jpg">
        <kbd>
            <img src="/images/agu_2023/agu_2023_title_slide.jpg">
        </kbd>
    </a>
</p>



## Abstract 
As many of the largest consumer packaged goods brands publicly commit to reducing their environmental footprints, the demand for reliable methods to quantify scope 3 greenhouse gas (GHG) emissions from commodity grain production is rapidly increasing. Indigo Ag is pioneering methods to estimate annual GHG emissions at continental-scale for corn, wheat, and other field crops. By training machine learning models on large datasets of fused publicly available resources (e.g., multi-temporal remote sensing imagery from Harmonized Landsat-Sentinel, USDA survey responses, etc.) and private, field-level management data collected directly from growers, total GHG emissions from individual field cultivation cycles can be predicted on auto-delineated field boundaries across large portions of the U.S. and flexibly aggregated to meet stakeholder needs. While on a field-by-field basis the presented methods may not be as accurate as a traditional life cycle impact assessment or biogeochemical model run, the approach allows for rapid, cost-efficient, regional-scale assessment with zero on-site data collection requirements.

This advancement will allow for the agricultural community to better understand how spatiotemporal factors (e.g., weather, soil) combine with field management to influence regional emissions on an annual basis, pinpoint where intervention-type emissions reduction programs may have the largest return on investment, and target areas where further data collection and innovation are required. Here, we present methods for arriving at field-level GHG predictions with associated uncertainty metrics and highlight some general trends in field cropping emissions for sample counties of the United States followed by a brief discussion of where we see potential for future collaboration moving forward.

## Highlights

### Field-Level Emissions

The modeling system first predicted annual greenhouse gas emissions at the field-level. While interesting, the individual predictions themselves are likely not the most accurate given the coarse resolution of data available via satellite for any given field. However, these predictions serve as the foundation for meaningful interpretation of trends at scale and provide flexibility to aggregate information based on business needs and not according to arbitrary political boundaries (e.g., counties, states).

<p align="center">
    <a href="/images/agu_2023/agu_2023_field_emissions.png">
        <kbd>
            <img src="/images/agu_2023/agu_2023_field_emissions.png">
        </kbd>
    </a>
</p>

### Grain Elevator Assessment

For example, emissions distributions are presented here for fields within a 30 mile radius of three grain elevator facilities. Each curve is comprised of hundreds to thousands of individual field-level observations, and we can see that the emissions estimate can vary substantially by field. 

In 2021, regardless of location emissions are relatively similar, but in 2022 they diverge. Given the local population of fields in this example, it may be that if given the option, a client may wish to work with facility A first, before sourcing from B and then C. 


<p align="center">
    <a href="/images/agu_2023/agu_2023_facility_emissions.png">
        <kbd>
            <img src="/images/agu_2023/agu_2023_facility_emissions.png">
        </kbd>
    </a>
</p>

### Regional Trends

It is helpful to assess general emissions trends on larger scales as well to understand if grain sourcing decisions should be redirected and/or if intervention programs can be put in place to reduce GHG emissions in higher emitting areas.

<p align="center">
    <a href="/images/agu_2023/agu_2023_il.png">
        <kbd>
            <img src="/images/agu_2023/agu_2023_il.png">
        </kbd>
    </a>
</p>

Looking at the state of Illinois, the maximum return to N fertilizer [recommendation system](https://www.cornnratecalc.org/) (left) breaks the state into three distinct management regions. On average, the system tends to recommend higher nitrogen application rates in the south relative to the north. For example, for corn following soybeans in a year with a 10:1 Corn:N price ratio, 178 lbs N per acre are recommended in the north versus 200 lbs N per acre in the south.

This is partially due to the fact that soil organic carbon stocks (seen in the second tile) are generally higher in the north relative to the south. Typically, agronomists assume 10-20 lbs N per percent organic matter per year are provide to crops through normal soil carbon turnover. 

Additionally, corn yields are typically higher in the north due to generally more productive soil and weather conditions. In 2022, yields in the northeastern portion of the state were slightly depressed due to severe drought conditions during silking/anthesis.

<p align="center">
    <a href="/images/agu_2023/agu_2023_drought_map.png">
        <kbd>
            <img src="/images/agu_2023/agu_2023_drought_map.png">
        </kbd>
    </a>
</p>

These factors of lower nitrogen application rates, higher yields, and others often combine to result in lower emissions on a per bushel basis in the north vs. the south as is predicted by the models.




