# DATA 512 - A1: Data Curation

## Goal
The goal of this assignment is to construct, analyze, and publish a dataset of monthly traffic on the English Wikipedia application from January 1, 2008 through August 30, 2021.

Follow the Python Notebook that can be found [here](https://github.com/smuktevi/data512hw/blob/main/data-512-a1/hcds-a1-data-curation.ipynb) to reproduce the same results of the analysis. Detailed steps on how the data was collected, transformed and visually analysed can be found in the same notebook.

## License and Sources

The source data is licensed under the [Creative Commons Attribution-ShareAlike License](https://creativecommons.org/licenses/by-sa/3.0/). 
  
The Wikimedia Foundation REST API terms of use are mentioned [here](https://www.mediawiki.org/wiki/REST_API#Terms_and_conditions).

The relevant API documentation can be found in the following links:  
* The legacy Pagecounts API ([documentation](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Legacy_Pagecounts), [endpoint](https://wikimedia.org/api/rest_v1/#!/Pagecounts_data_(legacy)/get_metrics_legacy_pagecounts_aggregate_project_access_site_granularity_start_end)) provides access to desktop and mobile traffic data from December 2007 through July 2016.  
  
* The current Pageviews API ([documentation](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Pageviews), [endpoint](https://wikimedia.org/api/rest_v1/#!/Pageviews_data/get_metrics_pageviews_aggregate_project_access_agent_granularity_start_end)) provides access to desktop, mobile web, and mobile app traffic data from July 2015 through last month.

## Data

The following is the schema for the resulting data table.  

|Column | Value/Type | 
| --- | --- |
year | YYYY 
month | MM
pagecount_all_views | num_views
pagecount_desktop_views | num_views
pagecount_mobile_views | num_views
pageview_all_views | num_views
pageview_desktop_views | num_views
pageview_mobile_views | num_views

**Data Description:**
  
* `year` : year in YYYY character string format.
* `month` : month in MM character string format.
  
Using legacy API endpoint:  
* `pagecount_all_views` : page view count from all access type.
* `pagecount_desktop_views` : page view count from desktop access type.  
* `pagecount_mobile_views` : page view count from mobile access type.
  
Using current API endpoint:
* `pageview_all_views` : page view count from all access type.
* `pageview_desktop_views` : page view count from desktop access type.
* `pageview_mobile_views` : page view count from mobile access type.  
  
## Important Notes
* The more current Pageview API allows you to filter by agent=user which ensures that we get user traffic that is not by web crawlers or spiders. This type of traffic is more valuable to us. This is not the case in the legacy Pagecount API. Therefore, the final analysis of the legacy API might include bot and web crawler traffic.
* You can see that there is about a year of overlapping data between the two APIs between 2015 and 2017.
* The current Pageview API shows less noise compared to the legacy Pagecount API which might be the indication of the legacy API not accounting for the bot and web crawler traffic.
