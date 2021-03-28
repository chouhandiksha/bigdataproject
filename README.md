# Visualizing the Mobility Gradient Across Different Demographic Groups



## Introduction





## Related Work



## Data Sources



## Data Acquisition



### New York Times COVID-19 Data



### SafeGraph Social Distancing Metrics and Census Block Group Data



## Data Extraction















# ARCHIVE





## Project Description

Many recent papers, including [Mobility network models of COVID-19, explain inequities and inform reopening](https://www.nature.com/articles/s41586-020-2923-3.epdf?sharing_token=c2VoryoYtQWd97ZdgEeRENRgN0jAjWel9jnR3ZoTv0P4QCkIKJMffNLo7c2z6ZZTYnGvAvX3fI35Ev4XiT4qy_Aw6981p_PWN2cUGQp-Db0e94Jx4cKJQKn89MbI01LV-5MeKLdkAFZjD7pS4mC45svhw8DcXn1DInTY6nWUQ50%3D) and [*Coronavirus infections and deaths by poverty status: The effects of social distancing*](https://pubmed.ncbi.nlm.nih.gov/33362321/) have established an essential link between mobility and COVID-19 infection rates and deaths. 

We propose to study the daily change in mobility of the general population from January 1st through May 31st from 2020 in the three most populated cities in the US: New York, Los Angeles, and Chicago. Using the [SafeGraph COVID-19](https://www.safegraph.com/covid-19-data-consortium) dataset, we will generate a mobility index with a resolution of the census blocks. We will use attributes such as the number of devices that remain at home, the count of devices with full-time work behavior, the median distance traveled by devices, and other vital actions relevant to mobility. We will then visualize each city’s mobility based on the mobility index using graphs and maps produced with the GeoJSON file provided by SafeGraph of the Census Blocks. 

We will compare with visualizations the mobility index of census blocks with the largest and smallest percentage of people in poverty based on the Census American Survey data provided by SafeGraph. Also, we will compare with visualizations the mobility index of census blocks with the largest and smallest percentage of minority residents based on the Census American Survey data provided by SafeGraph. Our objective is to better understand and visualize to what degree different groups have been able to adopt limited mobility to mitigate the [documented](https://www.nature.com/articles/s41586-020-2923-3.epdf?sharing_token=c2VoryoYtQWd97ZdgEeRENRgN0jAjWel9jnR3ZoTv0P4QCkIKJMffNLo7c2z6ZZTYnGvAvX3fI35Ev4XiT4qy_Aw6981p_PWN2cUGQp-Db0e94Jx4cKJQKn89MbI01LV-5MeKLdkAFZjD7pS4mC45svhw8DcXn1DInTY6nWUQ50%3D) threat of COVID-19 exposure created by higher mobility. 



## Datasets

We propose to use the SafeGraph COVID-19 Response Social Distancing Metrics, The SafeGraph Demographic American Survey Census Data, and The New York Times COVID-19 Data. We have verified all three datasets are available to researchers, secured access to, and downloaded the datasets.

### SafeGraph Social Distancing Data

**Desription:** Due to the COVID-19 pandemic, people are currently engaging in social distancing. In order to understand what is actually occurring at a census block group level, SafeGraph is offering a temporary Social Distancing Metrics product.
The SafeGraph COVID-19 Response Social Distancing Metrics schema can be viewed online at https://docs.safegraph.com/docs. The dataset is organized by Census Block and includes mobility statistics generated from cell phone data such as median distance travel from home, completely at-home device count, full-time work behavior, and many more mobility aggregate statistics. 

**Data Source:** https://www.safegraph.com/covid-19-data-consortium Data Schema: https://docs.safegraph.com/docs  Data: https://docs.safegraph.com/docs/social-distancing-metrics

**Includes:** COVID-19 Response Social Distancing MetricsDates: January 1, 2019, to present

**Attributes:** 

* Number of devices 
* Median distance traveled from home
* Completely home device count
* Median home-dwelling time
* Part-time work behavior
* Full-time work behavior
* Destinations (POI visited)
* many more...

### SafeGraph Demographic Census Data

**Description:** The SafeGraph Demographic American Survey Census Data schema can be viewed online at https://docs.safegraph.com/docs/open-census-data. The dataset is organized by Census Block and contains demographic information including statistics about race, household income, and poverty. 

**Data Source:** https://www.safegraph.com/open-census-dataData Schema: https://docs.safegraph.com/docs/open-census-data 

**Data Guide:** https://www.safegraph.com/blog/beginners-guide-to-census 

**Includes:** 

* All demographic data from the American Community Survey (2016) 5-year estimate on the Census Block Group level. 
* All census block group boundaries formatted as a GeoJSON file.

### New York Times COVID-19 Data

**Description:** 

The New York Times COVID-19 Data can be accessed online at https://github.com/nytimes/covid-19-data. The dataset contains reported daily COVID cases and deaths organized at the Country, State, and county levels. 

**Data Source:** https://github.com/nytimes/covid-19-data

