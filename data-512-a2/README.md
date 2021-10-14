# A2: Bias in Data

## Goal
The goal of this assignment is to explore the concept of bias through data on Wikipedia articles - specifically, articles on political figures from a variety of countries.

Follow the Python Notebook that can be found [here](https://github.com/smuktevi/data512hw/blob/main/data-512-a2/hcds-a2-bias.ipynb) to reproduce the same results of the analysis. Detailed steps on how the data was collected, transformed and visually analysed can be found in the same notebook.

## Sources

This repository uses two data sources.

* The Wikipedia politicians by country dataset can be found on [Figshare](https://figshare.com/articles/dataset/Untitled_Item/5513449). Download and unzip it to extract the data file, which is called `page_data.csv`.

`Note:` In the case of page_data.csv, the dataset contains some page names that start with the string "Template:". These pages are not Wikipedia articles.

* The population data is available in CSV format as `WPDS_2020_data.csv`. This dataset is drawn from the world population data sheet published by the [Population Reference Bureau](https://www.prb.org/international/indicator/population/table/).

`Notes:` Similarly, `WPDS_2020_data.csv` contains some rows that provide cumulative regional population counts, rather than country-level counts. These rows are distinguished by having ALL CAPS values in the 'Geography' field (e.g. AFRICA, OCEANIA). These rows won't match the country values in `page_data.csv`, but you will want to retain them (either in the original file, or a separate file) so that you can report coverage and quality by region in the analysis section.
