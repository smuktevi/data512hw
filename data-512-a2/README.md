# A2: Bias in Data

## Goal
The goal of this assignment is to explore the concept of bias through data on Wikipedia articles - specifically, articles on political figures from a variety of countries.

Follow the Python Notebook that can be found [here](https://github.com/smuktevi/data512hw/blob/main/data-512-a2/hcds-a2-bias.ipynb) to reproduce the same results of the analysis. Detailed steps on how the data was collected, transformed and visually analysed can be found in the same notebook.

## License and Sources

This repository uses the MIT license.  
  
This repository uses two data sources.

* The Wikipedia politicians by country dataset can be found on [Figshare](https://figshare.com/articles/dataset/Untitled_Item/5513449). Download and unzip it to extract the data file, which is called `page_data.csv`.

`Note:` In the case of page_data.csv, the dataset contains some page names that start with the string "Template:". These pages are not Wikipedia articles.

* The population data is available in CSV format as `WPDS_2020_data.csv`. This dataset is drawn from the world population data sheet published by the [Population Reference Bureau](https://www.prb.org/international/indicator/population/table/).

`Notes:` Similarly, `WPDS_2020_data.csv` contains some rows that provide cumulative regional population counts, rather than country-level counts. These rows are distinguished by having ALL CAPS values in the 'Geography' field (e.g. AFRICA, OCEANIA). These rows won't match the country values in `page_data.csv`, but you will want to retain them (either in the original file, or a separate file) so that you can report coverage and quality by region in the analysis section.

## Article Quality

Used a machine learning system called ORES to obtain article quality. The article quality estimates are, from best to worst:

FA - Featured article
GA - Good article
B - B-class article
C - C-class article
Start - Start-class article
Stub - Stub-class article

You can obtain these values by using ORES REST API endpoint. 

`Note:` 
* Review the [ORES REST documentation](https://ores.wikimedia.org/v3/#!/scoring/get_v3_scores_context_revid_model). It expects a revision ID, which is the third column in the Wikipedia dataset, a model, which is "articlequality", and context which is "enwiki".  
* It's possible that you will be unable to get a score for a particular article. You can find the list of articles which did not retrieve scores in my case in `page_data_not_found.csv` and the ones that did get a score in `page_data_filtered_final.csv`.
* I used saved intermediate data after using the API as it takes a while to run the API call. The data can be found for both population and articles in `country_pop_data.csv` and `page_data_filtered_final.csv` respectively.

## Resulting Data

You can find my outputs in the `data_result` folder.
  
Merge the wikipedia data and population data together. Both have fields containing country names for just that purpose. After merging the data, you'll invariably run into entries which cannot be merged. Either the population dataset does not have an entry for the equivalent Wikipedia country, or vise versa.  
  
Please remove any rows that do not have matching data, and output them to a CSV file called: `wp_wpds_countries-no_match.csv`
Consolidate the remaining data into a **final** single CSV file called: `wp_wpds_politicians_by_country.csv`.

|Column | Value/Type | 
| --- | --- |
country |	Country of the article
article_name |	Name of the article
revision_id |	Revision ID of the article
article_quality_est. |	Article quality predicted by ORES
population |	Population of the country
  
  
## Reflections

In this study, I expected to see a large difference in articles per person depending upon the size and regional languages spoken in a specific country. While processing the data, there were instances where we introduce bias into the analysis such as some articles not returning valid ORES scores. It's can be easily true that the remaining sample can not be fully generalizable. The results we get can not easily be correlated with each other because of the varying results based on the different metrics that we use. 

Some hypotheses I that I thought about included trying to factor in the biases we can see depending on the country's popoulation size and languages spoken. I also tried to think that politicians that are more "internet famous" might have more quality. The anslysis confirms that it is tough to specify any one metric to assess qualitative measures without having a list of prioritized attributes.

* What biases did you expect to find in the data (before you started working with it), and why?

This being the English Wikipedia highly skews the data distribution as there could be more articles written in regional languages for popular politicians in a specific sub-region. Smaller countries will have less population generally compared to much bigger ones. Hence, the number of politicians and fame might be scaled down for these countries. This is also a bias in the data and politicians from smaller countries will have less exposure worldwide and might not have the best quality of articles.

* What (potential) sources of bias did you discover in the course of your data processing and analysis?

Similar to my initial thought on being biased due to using only English Wikipedia and not other languages, Does the machine learning algorithm used here (ORES) also cater to this bias? We should be weary of assessing quality on biased data and ensure that machine learning does not "overfit" on certain kinds of data. Another note on population not being a good metric here to assess based on proportion of articles on famous politicians. This is because different countries have vastly varying densities of the world population and countries like China might be severly biased against due to its large population with our current metrics.

* What might your results suggest about (English) Wikipedia as a data source?

This data source might not be the best judge the effective quality of articles on politicians for certain countries. As expected, due to the biases I've stated in previously, we can see it reflect in the results. For example, the region of North America seems to have the best quality of articles but this could be mainly due to the English language bias and also the large population. Whereas, using the total counts directly we can see that Oceania is at the top which begs to ask the question of whether we are using the right measure in this case and requires further research.
