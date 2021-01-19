# Exploratory-Data-Analysis-of-Bike-Sharing-Systems-in-Warsaw


<h2><b>1. Synopsis </b></p></h2>

Exploratory analysis on the dataset which contains historical time series data of public bike sharing systems in Warsaw. Project explores patterns of bike routes using clustering algorithm and shows the relationship between the bike rentals and the explanatory variables like weather or the day of the week. . The project uses over 4,100 JSON files, saved every 10 minutes, containing station data and lists of bikes located at each bike station in Warsaw.
The project uses archival meteorological data collected by the Institute of Meteorology and Water Management - available at https://danepubliczne.imgw.pl/datastore. Project in Python with usage of Jupyter Notebook and ML libraries(e.g Numpy, Pandas, Matplotlib)


</br>

<h2><b>2. Description of the dataset </b></p></h2>


Main information about data:
- 4,184 JSON files, saved every 10 minutes between 03/04/2018 - 04/04/2018
- 1 JSON file contains information on an average of 355 bicycle stations in Warsaw

An overview of the most important attributes included in this set used in the analysis and visualization is presented below:

- <b>uid</b> - identifier of a bike station
- <b>bikes</b> - the number of bikes at a station
- <b>bike_racks</b> - the number of racks at a station
- <b>free_racks</b> - the number of free positions at a station
- <b>bike_numbers</b> - numbers of individual bikes pinned at a given station
- <b>lat</b>, <b>lng</b> - coordinates (longitude and latitude) of a bike station


</br>

<h2><b>3. Preparing data for analysis </b></h2>
<h3><b>3.1. Data preprocessing </b></h3>


After reading and data preprocessing (removing unnecessary columns, changing data types and breaking down the JSON file name into year, month, day, hour, minutes), the basic data frame was extended, among others o the values ​​of temperatures and amount of rainfall in individual time intervals. Meteorological data along with the codes of stations or parameters of phenomenon were downloaded from the website of the Institute of Meteorology and Water Management available at  https://danepubliczne.imgw.pl/datastore.
The analyzed, grouped data frame is presented in the photo below. The <b>day_of_week</b>, <b>city_code</b>, <b>date_normalize</b> columns were created for the purpose of data analysis.
</br>
The analyzed dataframe with multiple indexes is shown below
</br>
<img width="800" height="350" src = img/dataframe.png/>


The first part of the notebook contains an analysis  and visualization of bike routes - on the basis of information about the bike numbers that are pinned to the station in a given time interval. This collection contains <b>19 783 745</b> observations.
The second part of the notebook contains an analysis of bike stations and is based on the basic dimension of the collection. This dimension comprises <b>1 472 021</b> observations and <b>13</b> variables. 


<h3><b>3.2. Checking for missing values </b></h3>
The data analysis began with checking whether the entire data set at each station contains enough information about the number of bikes in a given time period. As seen below, missing values ​​were noted for 29 stations (these values ​​could be recorded up to 4184, because that many JSON files constituted the dataset).
<img width="400" height="350" src = img/table1.png/>
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
<img width="600" height="650" src = img/box-plot1.png/>




On the chart above, it can be seen that one station on March 14 and March 25 recorded a much larger number of bike rentals compared to all other stations on that day.

Due to the large variety of locations of bike stations and the fact that they can be very popular in the event of major sports or music events, these values do not have to mean a data collection error. The popularity of the station was assessed on the basis of the median, which is not sensitive to outliers, so extreme points were not removed


</br>
Using the box-plot, it is also possible to evaluate the occurrence of outliers at particular hours of each day based on the sum of bikes rented from all stations. The chart shows that one day at 2 a.m. and 7 a.m. there was a much greater number of rentals, and these values ​​in such hours over five times higher than their median are certainly unrealistic.
<img width="700" height="420" src = img/box-plot2.png/>



Analyzing the data in terms of the largest number of bikes rented from all time periods, it can be seen that for many stations on <b>March 27</b> at <b>2:30</b> and <b>March 14 </b>at <b>7:00 </b>there were above-average numbers of bikes rented. 

In view of the above, the data on the number of bikes at stations from <b>2018-03-27 02:30</b>, <b>2018-03-27 02:40 </b>and <b>2018-03-14 07:00 </b>have been deleted.
After adding up the number of bikes rented at all stations throughout the dataset period, it can be seen that there are stations from which no bike has left in the considered time. These stations, in the context of the popularity rating, were not taken into account and were removed from the dataset.
<img width="700" height="400" src = img/dataframe2.png/>



<h2><b>4. Exploratory data analysis </b></h2>

<h3><b>4.1. Interactive grouping of bikes stations using the Folium library </b></h3>


The analysis and visualization of this data uses the folium library, thanks to which it was created a map containing interactive markers that automatically group the number of stations on the map. Tags are grouped with locations if they are close enough to each other.

The picture below shows the map of Warsaw with the location of <b>380</b> bike stations using interactive grouping

<img width="600" height="350" src = img/warsaw_map.png/>

<br>
On this map there are names of individual stations along with the number of bike stands there. This is visible when you zoom in on the map and hover the cursor over the selected marker.

<img width="600" height="350" src = img/folium.png/>




<h3><b>4.2. Analysis of the popularity of bike routes </b></h3>
The main dataset was transformed into a dataset containing information on bike numbers at stations to analyze popular bike routes.
The analyzed set, containing information about the numbers of bikes that are pinned to the station in a given time interval, constitutes <b>19 783 745</b> observations. In the analyzed period, information on <b> 249</b> bikes was recorded.
The picture of the analyzed dataframe is presented below </br>
<img width="550" height="300" src = img/dataframe3.png/>

Thanks to the use of the Folium library, we can also present popular bike routes. Those that were counted at least 50 times over the analyzed period are presented on the map below.
<img width="550" height="500" src = img/popular_routes.png/>


<h3><b>4.3.  Exploration of patterns of bike routes using clustering algorithm </b></h3>
Routes can be represented as a graph. Such a graph with distinguished clusters is presented below (the <b>Louvain algorithm</b>, which is a hierarchical clustering algorithm, was used as the clustering method).
<img width="620" height="600" src = img/graph.png/>

the composition of three exemplary clusters is presented below.
<img width="600" height="210" src = img/cluster.png/>


The vast majority of stations in a particular cluster are stations located in one region, so it can be concluded that people most often move between stations located in close proximity to each other.
This relationship can also be seen on the heatmap below. </br>
<img width="540" height="500" src = img/heatmap.png/>


It shows that it is between the neighboring stations - stations with similar ID numbers that are most frequently used.

The table below presents the most popular bike routes (the count column indicates the number of bikes that traveled from station A to station B in a given period).
<img width="450" height="220" src = img/10pop_routes.png/>


The picture below shows a map of Warsaw with the 15 most popular bike routes marked.
<img width="400" height="450" src = img/pop_routes_marked.png/>

The most popular routes can also be presented as a graph.
<img width="500" height="450" src = img/graph2.png/>

Below is a fragment of the map of Warsaw showing the most popular bike route - <b>Stefan Banach - UW <—> al. Niepodległości - Batory </b></br>
<img width="550" height="280" src = img/the_most_pop_route.png/>



<h3><b>4.4.  Analysis of the length of bike rentals </b></h3>
The image below shows a histogram that shows how long bikes are typically rented. Unfortunately, due to the low dynamics of data (data collected every 10 minutes), this histogram is burdened with a large error and a trip that lasted e.g. 12 minutes can be recorded in the same way as a 28-minute drive. For example, a bike that was rented at 2:39 PM and returned at 2:51 PM will be considered as a 30-minute ride, as well as a bike rented at 2:31 PM and returned at 2:59 PM. The 30-minute bar does not have to specify such a bike rental time and with more dynamic data it could be a 20-minute value. The issue of the length of renting a bike is quite important because the first 20 minutes are free.
<img width="500" height="300" src = img/hist_of_length_of_bike_rentals_.png/>



<br>
<h3><b>4.5.  Visualization of bike sharing data as a time series </b></h3>
The notebook includes many charts, among others
correlation between the number of bike rentals and the air temperature or depending on the hour on individual days of the week. <br>
The chart below shows the correlation between the number of bike rentals and the air temperature.
<img width="600" height="300" src = img/chart1.png/>
<br>


The table of correlation values ​​between the number of bikes rented and the value of the air temperature or the sum of rainfall during the day is presented below. </br>
<img width="250" height="100" src = img/corr_table.png/>

The correlation coefficient (in this case Pearson) between the number of bikes rented and the temperature value is <b>0.67 </b>, which indicates a significant correlation between these variables. The correlation coefficient between the number of bikes rented and the sum of rainfall is <b>-0.41</b> (negative correlation), which shows a moderate correlation.


And the chart below showing the correlation air temperature or depending on the hour on individual days of the week. </br>
<img width="600" height="300" src = img/graph3.png/>

The table below presents a detailed average number of bikes rented at specific hours of each day of the week.
<img width="350" height="520" src = img/table2.png/>


Looking at the chart and tables above, it can be seen that the most bike rentals are recorded on working days in the <b>afternoon</b>, i.e. <b>4 pm - 5 pm</b>, and greater rental values ​​than usual are also visible in the <b>mornings 7 - 8 a.m.</b>. It can therefore be concluded that city bikes They are a popular means of transport for commuting or returning from work, school, or to transport to the metro station. The graph shows that city bikes are also popular on <b>weekends</b>. There is a lot of interest in the afternoon hours (especially on <b>Sundays</b>).

<h3><b>4.6. Analysis of popularity of bike stations </b></h3>
The most popular bike stations in Warsaw (with the largest median of rentals during the day) are the following stations: <b>Al. Niepodległości - Batory</b>, <b>Stefan Banach - UW</b> and <b>Rondo Jazdy Polskiej</b>. The list of the 10 bike stations with the highest median is presented below.
<img width="450" height="300" src = img/the_most_popular_bike_stations.png/>
