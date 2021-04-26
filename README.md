# Weather Data and Changing Climates

Hello! This is a repository housing data, analysis, and images of weather information obtained from open online sources.  This was originally created in service of a DSI group project for General Assembly in April of 2021. <!-- the weather was beautiful -->

Contributors
-
    - Chang, Trevor
    - Reagin, Stephen
    - Steele, Nicholas
# Problem Statement

**Can we use weather data to determine its decade of origin?**
Weather data is a rich domain and has many characteristics that make prediction difficult, with other characteristics that show an underlying structure. The important characteristics for our investigation include:
- Very many data sources keeping excellent records for decades
- Noisy measurements with high variance
- Notoriously hard to predict with precision
- Continuous changes by hour and location
- Follows reliable patterns (e.g. daily, seasonal)
- Baseline changes occur gradually
The *climate change hypothesis* in its most basic form supposes that Earth's climate changes over time. Thus, climate outputs (like weather) may differ in some time periods versus others. This hypothesis is quite obviously true in certain contexts: 
- Daily weather changes are often forecast a week ahead (probabilistically, e.g. 40% chance of rain)
- Summer months tend to warmer than Winter months; while Spring and Autumn are rather mild
- 'Little ice ages' can last 300 - 500 years, and longer ice ages or warming periods can last for many thousands of years
The typical context of a climate change discussion involves medium-long timescales, on the order of decades or centuries.  And such discussions can imply that, IF the climate is changing over time, THEN it was somehow different in the past than today. The natural follow-up question is, do certain time periods have characteristic weather patterns that are distinguishable from decade to decade?
Said another way: **if we know the weather patterns over a given time period, can we reliably determine which time period it was recorded?**
Our assumption is, with enough well-recorded data over long time stretches, we can build models to find patterns of changing signal and figure out "when" we are.  To carry this experiment out we collected weather data from multiple sources, building classification models to see if there are distinguishable changes from decade to decade
##### Please note that we did not investigate any potential *explanatory causes* for changing climate conditions over time.

# Datasets

## NOAA

[NOAA API](https://www.ncdc.noaa.gov/cdo-web/webservices/v2):
- GHCN-Daily: Global Historical Climatology Network + Daily
- Stations: 118,486 weather stations all around the world
- Date range: 1763 - Now
- Values Provided: 137 variables
Among those 1181,486 stations located all around the world, 1676 stations provide all variables we want. 
These 1676 stations are located in 29 countries and most of them are located in US and Canada.
We randomly selected one station from each of those countries. Then make the request to get all the data we want from 1979 to 1999.

For the cities below, data was grabbed manually from the NOAA LCD website: https://www.ncdc.noaa.gov/cdo-web/datatools/lcd <br>
Atlanta, GA -- data from 1945 - 2020, gap in 1972 - 1973 <br>
Cincinnati, KY -- data from 1948 - 2020, gap in 1966 - 1973 <br>
Houston, TX -- data from 1948 - 2020, gap in 1966 - 1973 <br>
NewYork, NY -- data from 1948 - 2020, gap in 1966 - 1973 <br>
### Assorted Datasets
Delhi, 1997 - 2016 https://www.kaggle.com/mahirkukreja/delhi-weather-data <br>
Brazil (**not in repo**), 2000 - 2016 https://www.kaggle.com/PROPPG-PPG/hourly-weather-surface-brazil-southeast-region <br>
Madrid, 1997 - 2015 https://www.kaggle.com/juliansimon/weather_madrid_lemd_1997_2015.csv <br>
Bangladesh, 1901 - 2015 https://www.kaggle.com/yakinrubaiat/bangladesh-weather-dataset <br>
## data.world datasets
West Australia, 1944 - 2016 https://data.world/damian-arntzen/west-aus-weather-1944-2016 <br>
Canada (*needs lots of cleaning!!*), 1917 - 2017: https://data.world/pegarciadotcom/canada-monthly-weather-data-1917-2017-dataloversbrazil <br>
UK ECN (environmental change network), (**not in repo**) 1993(?) - 2012 https://data.world/datagov-uk/2fc75b92-a71c-4f87-acc3-f1e5a2803c85 <br>
US Weather Outliers (**not in repo**), 1964 - 2013 https://data.world/carlvlewis/u-s-weather-outliers-1964 <br>
US Daily Climate Normals (**not in repo**), 1981 - 2010 https://data.world/us-noaa-gov/f9a2a75d-8454-4274-9ed3-a3a3f9f095a1 <br>
Kenneth Curtis analyses, 1820 - 2015: https://data.world/kacurtis/global-and-city-yearly-average-temperatures-1750-2015 <br>
Hanford Station Data, 1946 - 2017: https://data.world/homerhanumat/hanford-station-data <br>
# Workflow
    -how we grabed data
    -cleaning data
    -EDA
    -modeling
    
# Conclution 
