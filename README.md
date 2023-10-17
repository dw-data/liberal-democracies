# How European democracies evolved

Data analysis and visualization: [Gianna-Carina Grün](https://twitter.com/giannagruen), [Kira Schacht](https://twitter.com/daten_drang)

Research and writing: [Gianna-Carina Grün](https://twitter.com/giannagruen)

You can read the story in [English](https://dw.com/a-67110321) and [German](https://dw.com/a-67103631)

# Data Sources

The visualisations in this story are based on two different datasources. The *map* and the *timeseries* are based on the dataset provided by the **V-Dem Institute** of the University of Gothenburg.
The last update was published in March 2023 and includes data up until/including 2022 and can be downloaded [here](https://v-dem.net/data/the-v-dem-dataset/) (due to filesize limitations it is not incorporated into this directory directly). 
For this analysis, the dataset `V-Dem-CY-Core_csv_v13.csv` was used, downloaded from the page from the section "Country-Year: V-Dem Core". For further details, see the section on Analysis and Visualization below.

The survey data is based on the [**Eurobarometer**](https://europa.eu/eurobarometer/screen/home), a survey series regularly commissioned by the European Union since the 1970s to find out about EU citizens' social and political views, as well as attitudes towards the EU and its policies. It usually includes around 1000 respondents per EU member states. For this analysis, we are using data from the [Eurobarometer 98.2
(2023)](https://search.gesis.org/research_data/ZA7953), done in early 2023 and published in the [gesis data catalogue](https://www.gesis.org/en/eurobarometer-data-service/home) of the German Leibniz Institute for the Social Sciences. We analyze question
`sd18a - DEMOCRACY SATISFACTION - COUNTRY`, phrased as: *"On the whole, are you very
satisfied, fairly satisfied, not very satisfied or not at all satisfied
with the way democracy works in (OUR COUNTRY)?"*

# Analysis and visualization

*Timeseries and Map* 

All the analysis and visualization steps can be seen in the accompanying [jupyter notebook](https://github.com/dw-data/liberal-democracies/blob/main/V-Dem-Analysis/Vdem-Analysis.ipynb). 

- First, the dataframe was reduced to only include data covering the years from 2000 to 2022.
- For the map, the values in the column `v2x_libdem` were used for the year 2022. Details on the indicator can be found in [V-Dem's codebook](https://v-dem.net/documents/24/codebook_v13.pdf), p. 45.
- For the timeseries, two indicators were used. The indicator/column `v2x_libdem` was used for the y-values corresponding to each year and the `v2x_regime` indicator, classifying each country into a category - liberal democracy, electoral democracy, electoral autocracy or closed autocracy -, was used to color each year's dot.

The quantitative analysis was further corroborated with the qualitative [Democracy Report 2023, published by V-Dem](https://v-dem.net/documents/29/V-dem_democracyreport2023_lowres.pdf).

*Survey*

The R code for this analysis can be found in the folder `Eurobarometer-Analysis`.

- Load dataset and filter to include only country codes and answer codes to question `sd18a`.
- Summarize individual responses to calculate number and share of respondents by country and answer.
- Append answer labels and country
names.
- Save results by country to file, calculate overall satisfaction levels.
