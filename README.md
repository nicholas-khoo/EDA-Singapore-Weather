# Study of Impact of Singapore's Historical Weather Data and Inflation Rate on Outdoor Goods Organisation's Inventory Management

### Background:
Climate change is known to affect various organisations, particularly those in the agriculatural and supply chain industry. Furthermore, extreme weather affects both supply and demand side of the economy, contributing to the rising inflation rate. 

With the advancements in technology, organisations are able to make more accurate predictions on the weather conditions. This would enable them to better plan their inventories, ensuring minimal to no disruptions in their supply chain.

### Problem Statement
The Outdoor Collectives (TOC) is an outdoor apparel shop known for their handheld electronic fans, lightweight umbrellas as well as sunblock lotions. Established since the early 2000s in Honolulu, Hawaii, TOC has since expanded it's operations to America and has set its sights on the Asean region, with Singapore being the first country for their market entry strategy.

TOC has identified that consumers are becoming increasingly reluctant to carry umbrellas, electronic fans and sunblock lotion as part of their everyday carry (EDC), reason being that these items take up additional space in their bags. As such, TOC would like to explore to setup of temoprary retail spaces around Singapore to rent their electronic fans and umbrellas as well as sell their sunblock lotions. TOC's target consumers for the organisation are Singaporeans of all ages.

TOC anticipates the demand for sunblock lotions and visors to be higher on days with more sunlight and while those for electronic fans on days with high humidity levels. Sales of umbrellas are expected to be higher on rainy days. The organisation would thus want to ensure that there is sufficient inventory throughout the year.

### Data Dictionary
The data (stored in their respective .csv files located in the data folder) were sourced from data.gov.sg and rateinflation.com.

[Data.gov.sg](https://data.gov.sg) is the Singapore government's one-stop portal to its publicly-available datasets from 70 public agencies. To date, more than 100 apps have been created using the government’s open data. </br>
[rateinflation.com](https://www.rateinflation.com) is an information and reference site, providing educational content and resources about the consumer price index and inflation. Find the latest and historical inflation rates for various countries.

___Historical weather data extracted from data.gov.sg___
1) Monthly number of rainy days from 1982 to 2022
2) Monthly total recorded rainfall in mm (millimeters) from 1982 to 2022
3) Monthly relative humidity (%) from 1982 to 2022
4) Monthly sunshine duration (hours) from 1982 to 2022

___Historical inflation rate extracted from rateinflation.com___
1) Monthly inflation rate (%) from 1982 to 2022

A brief description on the features extracted and used for analysis is shown below: </br>

|Feature|Type|Dataset|Description|
|---|---|---|---|
|month|datetime64[ns]|rainfall-monthly-number-of-rain-days|Months from from 1982 to 2022| 
|no_of_rainy_days|float64|rainfall-monthly-number-of-rain-days|No. of rainy days per month from 1982 to 2022|
|total_rainfall|float64|rainfall-monthly-total|Amount of rainfall (mm) per month from 1982 to 2022|
|mean_rh|float64|relative-humidity-monthly-mean|Humidity levels (%) per month from 1982 to 2022|
|mean_sunshine_hrs|float64|sunshine-duration-monthly-mean-daily-duration|Hours of sunshine (hours) per month from 1982 to 2022| 
|inflation|float64|singapore-historical-inflation|Inflation rate (%) per month from 1982 to 2022|

### Summary of Analysis
Singapore's historical weather data was analysed to identify periods of the year when there was a higher amount of rainfall, humidity and sunshine. The historical inflation rate data was also analysed to determine any correlations with the weather conditions.

#### Data Pre-processing
The weather dataset (rainfall-monthly-number-of-rain-days.csv, rainfall-monthly-total.csv, relative-humidity-monthly-mean.csv, sunshine-duration-monthly-mean-daily-duration.csv and sunshine-duration-monthly-mean-daily-duration.csv) was explored to determine any abnormalies (e.g. null values, inconsistent data types etc.). The data was observed to have no null values. However, it was determined that certain columns were not needed for the analysis while some dataset had more entries than others. To standardise the datasets, irrelevant column(s) and additional rows were dropped.

The inflation dataset (singapore-historical-inflation.csv) was slightly more complicated to clean as it's structure did not fit with the weather datasets. To fix this, a function was used to repivot the data to conform to the rest of the datasets. Likewise, with the weather dataset, the inflation dataset was thoroughly cleaned to prepare for the analysis.

Once both datasets were cleaned and re-formatted, they were merged into a single dataframe to commence the analysis.

#### Analysis
A correlation matrix was plotted to identify any relationships among the different categories.

The following were the key observations derived from the matrix:
1) There is a strong positive correlation between the amount of rainfall and humidity levels.
2) There is a strong position correlation between the number of rainy days and humidity levels.
3) There is a strong position correlation between the number of rainy days and the total rainfall.
- On days with more rain and less sunshine, the humidity levels were higher.

A boxplot was plotted to identify any outliers within our data. There were outliers identified in the total rainfall, humidity, hours of sunshine and inflation dataset. However, due to the nature of of the size of our data (488 rows), these outliers were not dropped.

To substantiate the correlation matrix, a pairplot was plotted to provide an overview of the distributions and relationships among the different categories. A linear trend can be observed between (1) mean_sunshine_hrs vs no_of_rainy_days, (2) mean_rh and no_of_rainy_days and (3) mean_rh vs mean_sunshine_hrs.

___mean_sunshine_hrs vs no_of_rainy_days___ </br>
As the number of rainy days decreases, the average hours of sunshine increases.</br>
___mean_rh vs no_of_rainy_days___ </br>
As the number of rainy days increases, the level of humidity increases.</br>
___mean_rh vs mean_sunshine_hrs___ </br>
As the average hours of sunshine decreases, the level of humidity increases.

To conclude the analysis, a line plot was drawn for (1) total rainfall, (2) relative humidity levels and (3) hours of sunshine over the months for the past 5 years (2018 to 2022).

Summary of the key findings from the line plots:
- High amount of rainfall can be observed from November to January (Northeast Monsoon) as well as in April and June (Southwest Monsoon).
- High amount of rainy days can be observed from November to January (Northeast Monsoon) as well as in April and June (Southwest Monsoon).
- High humidity levels are observed in months with high rainfall.
- High amount of sunshine hours can be observed from February to April and from July to August.

#### Conclusions and Recommendations
On months with more rainfall and higher levels of humidity (November to January and April to June), TOC can explore supplementing inventories for umbrellas and electronic fans.

On months with more hours of sunshine (February to April and July to August), TOC can plan for more supplies of sunblock lotions.

There is no observed high levels of humidity, rainfall or sunshine between September and October. Thus, TOC can maintain a 'neutral' level of inventory during this period.

___TOC's recommended inventory___:
|Month|Product With Expected Higher Demand|
|---|---|
|Jan| Umbrellas and electronic fans|
|Feb| Sunblock lotion|
|Mar| Sunblock lotion|
|Apr| Sunblock lotion, umbrellas and electronic fans|
|May| Umbrellas and electronic fans|
|Jun| Umbrellas and electronic fans|
|Jul| Sunblock lotion|
|Aug| Sunblock lotion|
|Sep| nil|
|Oct| nil|
|Nov| Umbrellas and electronic fans|
|Dec| Umbrellas and electronic fans|

No correlation is observed between the inflation levels and the weather data. However, taking into account the yearly increase in inflation levels, for months where there is an expected higher demand for at least two products, TOC could explore a discount campaign to drive an increase in the amount of sales.

### Areas for Improvements
1) Although no correlation was observed between historical inflation levels and weather data, with more datasets provided surrounding inflation (e.g. Consumer Price Index levels), it could influence a change in the observation.
2) Additional geographical data mapping the areas of high rainfall and sunshine including intensity levels could enable TOC to plan their inventories at a more micro level and enable the organisation to make an informed decision on the regions to setup their pop-up shops at.