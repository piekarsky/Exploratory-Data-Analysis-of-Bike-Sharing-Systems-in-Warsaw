# Analysis-And-Visualization-For-Bike-Sharing-Systems-In-Warsaw


<h2><b>1. Project description </b></p></h2>

Jupyter Notebook contains data analysis and visualization of the bike-sharing system in Warsaw. The project uses over 4,100 JSON files, saved every 10 minutes, containing station data and lists of bikes located at each bike station in Warsaw.
The project uses archival meteorological data collected by the Institute of Meteorology and Water Management - available at https://danepubliczne.imgw.pl/datastore.

Main information about data:
- 4,184 JSON files, saved every 10 minutes between 03/04/2018 - 04/04/2018
- 1 JSON file contains information on an average of 355 bicycle stations in Warsaw


<h2><b>2. Description of dataset </b></p></h2>

An overview of the most important attributes included in this set used in the analysis and visualization is presented below:

- <b>uid</b> - identifier of a bike station
- <b>bikes</b> - the number of bikes at a station
- <b>bike_racks</b> - the number of racks at a station
- <b>free_racks</b> - the number of free positions at a station
- <b>bike_numbers</b> - numbers of individual bikes pinned at a given station
- <b>lat</b>, <b>lng</b> - coordinates (longitude and latitude) of a bike station




<h2><b>3. Preparing data for analysis </b></h2>
<h3><b>3.1. Data preprocessing </b></h3>


After reading and data preprocessing (removing unnecessary columns, changing data types and breaking down the JSON file name into year, month, day, hour, minutes), the basic data frame was extended, among others o the values ​​of temperatures and amount of rainfall in individual time intervals. Meteorological data along with the codes of stations or parameters of phenomenon were downloaded from the website of the Institute of Meteorology and Water Management available at  https://danepubliczne.imgw.pl/datastore.
The analyzed, grouped data frame is presented in the photo below. The <b>day_of_week</b>, <b>city_code</b>, <b>date_normalize</b> columns were created for the purpose of data analysis.
</br>
The analyzed dataframe with multiple indexes is shown below
</br>
<img width="800" height="350" src = img/dataframe.png/>


The first part of the notebook contains an analysis  and visualization of bike routes - on the basis of information about the bike numbers that are pinned to the station in a given time interval. This collection contains <b>19 783 745</b> observations.
The second part of the notebook contains an analysis of bicycle stations and is based on the basic dimension of the collection. This dimension comprises <b>1 472 021</b> observations and <b>13</b> variables. 


<h3><b>3.2. Checking for missing data </b></h3>
The data analysis began with checking whether the entire data set at each station contains enough information about the number of bikes in a given time period. As seen below, missing values ​​were noted for 29 stations (these values ​​could be recorded up to 4184, because that many JSON files constituted the dataset).
<img width="350" height="600" src = img/table1.png/>
<br>


For the stations:
<b>Czerniakowska - Gagarina</b>,
<b>Marszałkowska - al. Solidarności</b>,
<b>Wołoska-Odyńca</b>,
<b>al. Jana Pawła II - Grzybowska</b>
The number of missing information on the number of bikes at stations has been replaced with values from previous time intervals, as they do not constitute a large share in the entire data set.

The rest of the stations from the list above were removed from the analysis due to the large amount of missing information
e.g. for the Fieldorf - Bukowski stations 1092 NaN / 4184 = 26%

<h3><b>3.3. Checking outliers </b></h3>

The occurrence of outliers for particular days was checked using a box plot. It shows that one station on March 14 and March 25 recorded a much larger number of bike rentals compared to all other stations on that day.
<img width="650" height="650" src = img/box-plot1.png/>




On the chart above, it can be seen that one station on March 14 and March 25 recorded a much larger number of bike rentals compared to all other stations on that day.

Due to the large variety of locations of bicycle stations and the fact that they can be very popular in the event of major sports or music events, these values do not have to mean a data collection error. The popularity of the station was assessed on the basis of the median, which is not sensitive to outliers, so extreme points were not removed

</br>
Using the box-plot, it is also possible to evaluate the occurrence of outliers at particular hours of each day based on the sum of bikes rented from all stations. The chart shows that one day at 2 a.m. and 7 a.m. there was a much greater number of rentals, and these values ​​in such hours over five times higher than their median are certainly unrealistic.
<img width="600" height="450" src = img/box-plot1.png/>







The analysis and visualization of this data uses the folium library, thanks to which it was created a map containing interactive markers that automatically group the number of stations on the map. Tags are grouped with locations if they are close enough to each other.



The picture below shows the map of Warsaw with the location of 380 bike stations using interactive grouping

<img width="600" height="350" src = img/warsaw_map.png/>

<br>
On this map there are names of individual stations along with the number of bike stands there. This is visible when you zoom in on the map and hover the cursor over the selected marker.

<img width="600" height="350" src = img/folium.png/>

<br>
Thanks to the use of the Folium library, we can also present popular bike routes. Those that were counted at least 50 times over the analyzed period are presented on the map below.
<img width="600" height="500" src = img/popular_routes.png/>

<hr>

The notebook includes many charts, among others
correlation between the number of bike rentals and the air temperature or depending on the hour on individual days of the week. <br>
The chart below shows the correlation between the number of bike rentals and the air temperature.
<img width="600" height="300" src = img/chart1.png/>
<br>

And the chart below showing the correlation air temperature or depending on the hour on individual days of the week.
<img width="600" height="300" src = img/chart2.png/>

