# Weather Data and Changing Climates

Hello! This is a repository housing data, analysis, and images of weather information obtained from open online sources.  This was originally created in service of a DSI group project for General Assembly in April of 2021. <!-- the weather was beautiful -->

Contributors
-
    - Chang, Trevor
    - Reagin, Stephen
    - Steele, Nicholas

# Problem Statement and Introduction

**Can we use weather data to determine its decade of origin?**

Weather data is a rich domain with many characteristics that make prediction difficult, and other characteristics which reveal an underlying structure. The important characteristics for our investigation include:
- There exist very many data sources keeping excellent records for decades
- Measurements can be noisy with high variance
- Weather forecasting for a region (a city, say) is notoriously hard to predict with precision
- There are continuous changes by hour and location
- We can extrapolate from reliable patterns (e.g. daily and seasonal changes based on Earth's relative position with the Sun)
- Baseline changes tend to occur gradually

The *climate change hypothesis* in its most basic form supposes that Earth's climate changes over time. Thus, climate outputs (like weather) may differ in some time periods versus others. 

This hypothesis is quite obviously true in certain contexts: 
- Daily weather changes are often forecast a week ahead (probabilistically, e.g. 40% chance of rain)
- Summer months tend to warmer than Winter months; while Spring and Autumn are rather mild
- 'Little ice ages' can last 300 - 500 years, and longer ice ages or warming periods can last for many thousands of years

The typical context of a climate change discussion involves medium-long timescales, on the order of decades or centuries.  And such discussions can imply that, IF the climate is changing over time, THEN it was somehow different in the past than today. The natural follow-up question is, do certain time periods have characteristic weather patterns that are distinguishable from decade to decade?

Said another way: **if we know the weather patterns over a given time period, can we reliably determine which time period was recorded?**

Our assumption is, with enough well-recorded data over long time stretches, we can build models to find patterns of changing signal and figure out "when" we are.  To carry this experiment out we collected weather data from multiple sources, building classification models to see if there are distinguishable changes from decade to decade

##### Please note that we did not investigate any potential *explanatory causes* for changing climate conditions over time.

# Datasets

### NOAA

[NOAA API](https://www.ncdc.noaa.gov/cdo-web/webservices/v2):
- GHCN-Daily: Global Historical Climatology Network + Daily
- Stations: 118,486 weather stations all around the world
- Date range: 1763 - Now
- Values Provided: 137 variables

Among those 1181,486 stations located all around the world, 1676 stations provide all variables we want. 

These 1676 stations are located in 29 countries and most of them are located in US and Canada.

We randomly selected one station from each of those countries. Then make the request to get all the data we want from 1979 to 1999.

#### NOAA Local Climatological Data (LCD)
For the cities below, data was grabbed manually from the [NOAA LCD website:](https://www.ncdc.noaa.gov/cdo-web/datatools/lcd) <br>
Atlanta, GA -- data from 1945 - 2020, gap in 1972 - 1973 <br>
Cincinnati, KY -- data from 1948 - 2020, gap in 1966 - 1973 <br>
Houston, TX -- data from 1948 - 2020, gap in 1966 - 1973 <br>
NewYork, NY -- data from 1948 - 2020, gap in 1966 - 1973 <br>


### Assorted Datasets

Delhi, 1997 - 2016 https://www.kaggle.com/mahirkukreja/delhi-weather-data <br>
Brazil (**not in repo**), 2000 - 2016 https://www.kaggle.com/PROPPG-PPG/hourly-weather-surface-brazil-southeast-region <br>
Madrid, 1997 - 2015 https://www.kaggle.com/juliansimon/weather_madrid_lemd_1997_2015.csv <br>
Bangladesh, 1901 - 2015 https://www.kaggle.com/yakinrubaiat/bangladesh-weather-dataset <br>


### data.world datasets

West Australia, 1944 - 2016 https://data.world/damian-arntzen/west-aus-weather-1944-2016 <br>
Canada (*needs lots of cleaning!!*), 1917 - 2017: https://data.world/pegarciadotcom/canada-monthly-weather-data-1917-2017-dataloversbrazil <br>
UK ECN (environmental change network), (**not in repo**) 1993(?) - 2012 https://data.world/datagov-uk/2fc75b92-a71c-4f87-acc3-f1e5a2803c85 <br>
US Weather Outliers (**not in repo**), 1964 - 2013 https://data.world/carlvlewis/u-s-weather-outliers-1964 <br>
US Daily Climate Normals (**not in repo**), 1981 - 2010 https://data.world/us-noaa-gov/f9a2a75d-8454-4274-9ed3-a3a3f9f095a1 <br>
Kenneth Curtis analyses, 1820 - 2015: https://data.world/kacurtis/global-and-city-yearly-average-temperatures-1750-2015 <br>
Hanford Station Data, 1946 - 2017: https://data.world/homerhanumat/hanford-station-data <br>


# E.D.A.
Our exploratory analysis of the various weather datasets took the longest portion of time. Raw data files for weather come in a variety of shapes, sizes, and features. Some of the common weather variables we wanted to use include:
- Datetime
    - Sometimes by the hour, sometimes only as a daily or monthly measurement
- Temperature
    - Min, Max, Avg, hourly, et cetera
    - *WetBulb* temp differs from *DryBulb* temp differs from *DewPoint* temp
- Precipitation
    - Rainfall, snow depth, et cetera
- Windspeed and wind direction

Efforts were made to ensure unit consistency, converting (*e.g.*) length measurements from imperial to standard or (*e.g.*) temperatures from Fahrenheit to Kelvins.

*Missing data* was a consistent challenge for most datasets; sometimes days or months or even whole years have been skipped or lost in the original dataset. There's typically very few ways to infer these missing values and so they are more often dropped entirely. 

We can also make certain approximations, e.g. creating an 'average' temperature by calculating (Max + Min) / 2. This method would not hold up to a line-by-line scrutiny against the true average, but it can be a useful replacement for some calculations. In those cases we assume the differences are likely small enough to be ignored.

> EDA also uncovered summary findings such as rising temperatures over decades, which is a common theme across datasets as well

|Average Temperature (K) by Decade|
|Decade|Houston, TX|Laguardia, NY|Atlanta, GA|
|----|-------|------|------|
|1950| 293.74|285.80|285.42|
|1960| 293.40|285.24|284.72|
|1970| 293.22|285.36|284.65|
|1980| 293.57|285.59|285.10|
|1990| 294.20|286.36|285.42|
|2000| 294.41|286.27|285.60|
|2010| 294.77|286.74|286.06|


# Modeling Predictions by Decade

We decided to classify the data based on **Decade**, such that any data collected from 1950 - 1959 would be classified under *the 1950s* and so on.  We then trained models to associate certain weather patterns with certain decades, and ran test data attempting to classify it by decade.

Specifically, we built Logistic Regression and Random Forest classification models for the NOAA city dataset, and we built Neural Net classification models for the Canada dataset (we also ran NOAA API data through this Canada model just for monkey testing). 

### NOAA Hourly Data Classification
The NOAA models used weather data that was collected at hourly intervals, with each city having roughly 600,000 observations each. The LogisticRegression() and RandomForest() models used the default parameters. Below is a table showing the accuracy scores. 

| City          | Log.Regression      | RandomForest     |
|---------------|---------------------|------------------|
|Atlanta, GA    | train score: 0.404  |train score: 1.000|
|               | test score:  0.405  |test score: 0.813 |
|Cincinnati, OH | train score: 0.313  |train score: 1.000|    
|               | test score:  0.312  |test score: 0.794 |
|Queens, NY     | train score: 0.326  |train score: 1.000|
|               | test score:  0.326  |test score: 0.796 |
|Houston, TX    | train score: 0.230  |train score: 0.999|
|               | test score:  0.230  |test score: 0.837 |
|Cities combined| train score: 0.424  |train score: 0.999|
|               | test score:  0.423  |test score: 0.809 |

The baseline expectation was something like 15% - 20% accuracy through random guessing.  As seen above, the models performed quite above baseline in most cases. The training and testing scores for Logistic Regression are very similar to one another, whereas the Random Forest model tended to overfit (even if the test accuracy was significantly higher, this overfitting reduces our confidence in the predictive capability of this model). The important takeaway: our standard Logistic Regression model predicted the Decade of given weather data quite above the baseline expectation with very little customization.

### Canada Station Data Classification
The other model was a Neural Net based on the dataset for weather in Canada. This included over 850,000 observations, and the model was trained to predict which of 11 decades the data came from.  The Neural Net has 3 hidden layers with 512 nodes each, and was made with a batch size of 256 and 30 epochs. The training accuracy was 48% and the test accuracy was 42%. The baseline for the Canadian dataset was similarly 15%. 

After the Canada neural net model was made, we also tested NOAA API data from around the world in the model. Locations such as American Samoa, Germany, and Puerto Rico were used, all of which can be expected to have very different climates than Canada at least some of the time (indeed, we even expect weather in some parts of Canada to be very different from other parts of Canada). But we tested this approach to see if the effect of a changing climate could be detected with data from around the globe. This neural net model, trained on Canada and now predicting data sourced from all over the globe, was able to predict the global data with 38% accuracy. This is very close to the test accuracy of the model on its original Canada data. This leads us to advance the idea that, whatever climate effects are happening on the country-wide level are also happening on a global scale too. 


# Conclusion 

The data analysis shows that tempatures are rising decade over decade. Adding the predictive power of our clasiification models over local, country, and global levels, all the above suggests the climate is changing from decade over decade. The limit of our models serve to give us insight that the climate is having a measurable change across decades, although we did not investigate any explanatory causes.  

Further explorations might include analyzing which factors are most correlated with these change, potential causal influences, and the downstream effects of these changes. For example, flood insurance premiums near coastline may require reassessment if a warming Earth implies higher ocean levels (due to both thermal expansion of water, and possibly increased melted ice). Due to the limit of scope of this project we were not able to answer these questions. But our results from our data analysis and modeling suggest these are worthwhile ventures.
