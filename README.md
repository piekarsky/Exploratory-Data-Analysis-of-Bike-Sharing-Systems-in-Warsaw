# Exploratory Data Analysis of Bike Sharing Systems in Warsaw

## Table of Contents

+ [Overview](#overview)
+ [About the dataset ](#about_the_dataset)
+ [Preparing data for analysis](#preparing_data_for_analysis)
    + [Data preprocessing](#data_preprocessing)
    + [Checking for missing values](#checking_for_missing_values)
	+ [Checking outliers](#checking_outliers)
+ [Exploratory data analysis](#exploratory_data_analysis)
	+ [Interactive grouping of bike stations using the Folium library](#interactive_grouping_of_bike_stations)
	+ [Analysis of the popularity of bike routes](#analysis_of_the_popularity_of_bike_routes)
	+ [Exploration of patterns of bike routes using clustering algorithm](#exploration_of_patterns_of_bike_routes)
	+ [Analysis of the length of bike rentals](#analysis_of_the_length_of_bike_rentals)
	+ [Analysis of bike rentals](#analysis_of_bike_rentals)
	+ [Popularity analysis of bike stations](#popularity_analysis_of_bike_stations)



## Overview <a name = "overview"></a>

Exploratory analysis on the dataset which contains historical time series data of public bike sharing systems in Warsaw. This dataset was built with information of 4100 JSON files, saved every 10 minutes containing data about each bike station (i.e.: number of bikes at the station, number of racks, number of free racks) in Warsaw. This project explores patterns of bike routes using clustering algorithm and shows among other things the relationship between the number of bike rentals and the weather or day of the week. The [following notebook](https://github.com/piekarsky/Exploratory-Data-Analysis-of-Bike-Sharing-Systems-in-Warsaw/blob/master/source.ipynb) contains all stages from preparing data (cleaning, checking outliers) to creating analysis, visualization and discovering patterns in dataset.  

</br>

## About the dataset <a name = "about_the_dataset"></a>

Main information about the data:
- 4184 JSON files, saved every 10 minutes between 03/04/2018 - 04/04/2018
- 1 JSON file contains information about 355 bike stations in Warsaw on average

The most important attributes included in this dataset used in the analysis and visualization:
- <b>uid</b> - the ID of the bike station
- <b>bikes</b> - the number of bikes at the station
- <b>bike_racks</b> - the number of racks at the station
- <b>free_racks</b> - the number of free positions at the station
- <b>bike_numbers</b> - numbers of bikes docked at the station
- <b>lat</b>, <b>lng</b> - the coordinates (longitude and latitude) of the bike station


</br>

## Preparing data for analysis <a name = "preparing_data_for_analysis"></a>

### Data preprocessing <a name = "data_preprocessing"></a>

After loading and preprocessing data (removing redundant columns, changing data types and dividing the JSON file name into year, month, day, hour, minutes), the basic dataframe was extended, among others the values ​​of temperatures and the amount of rainfall in particular time intervals. The analyzed, grouped dataframe is presented below. The columns: <b>day_of_the_week</b>, <b>city_code</b>, <b>date_normalize</b> were created for analysis purposes.
</br>
The analyzed dataframe with multiple indexes is shown below:
</br>
<img width="800" height="350" src = figures/fig_1.png/>


The first part of the notebook contains the analysis  and visualization of bike routes (based on the numbers of bikes attached to each bike station in a given period of time). This collection contains <b>19 783 745</b> observations.
The second part of the notebook contains the analysis of bike rentals. This collection contains <b>1 472 021</b> observations.


### Checking for missing values <a name = "checking_for_missing_values"></a>

The data analysis began with checking whether the entire data set at each station contains enough information about the number of bikes in a given time period. As seen below, missing values ​​were noted for 29 stations (a maximum of 4184 could be recorded because that's how many JSON files were used in the dataset).
<img width="400" height="350" src = figures/fig_2.png/>
<br>


For the stations:

- <b>Czerniakowska - Gagarina</b>
- <b>Marszałkowska - al. Solidarności</b>
- <b>Wołoska - Odyńca</b>
- <b>al. Jana Pawła II - Grzybowska</b>

The number of missing information on the number of bikes at stations has been replaced with values from previous time intervals, as they do not constitute a large share in the entire dataset. 
The rest of the stations from the dataframe above were removed from the analysis due to the large amount of missing information
e.g. for the Fieldorf - Bukowski station 1092 NaN / 4184 = 26%


#### Checking outliers <a name = "checking_outliers"></a>

The occurrence of outliers for particular days was checked using a box plot. It shows that one station on <b> March 14</b> and <b>March 25</b> recorded a much larger number of bike rentals compared to all other stations on that day.
<img width="600" height="650" src = figures/fig_3.png/>


Due to the large variety of locations of bike stations and the fact that they can be very popular in the event of major sports or music events, these values do not have to mean a data collection error. The popularity of the station was assessed on the basis of the median, which is not sensitive to outliers, so extreme points were not removed.


</br>
Using the box-plot, it is also possible to evaluate the occurrence of outliers at particular hours of each day based on the sum of bikes rented from all stations. The chart shows that one day at 2 a.m. and 7 a.m. there was a much greater number of rentals, and these values ​​in such hours over five times higher than their median are certainly unrealistic.
<img width="700" height="420" src = figures/fig_4.png/>



Analyzing the data in terms of the largest number of bikes rented from all time periods, it can be seen that for many stations on <b>March 27</b> at <b>2:30</b> and <b>March 14 </b>at <b>7:00 </b>there were above-average numbers of bikes rented. 

In view of the above, the data on the number of bikes at stations from <b>2018-03-27 02:30</b>, <b>2018-03-27 02:40 </b>and <b>2018-03-14 07:00 </b>have been deleted.
After adding up the number of bikes rented at all stations throughout the dataset period, it can be seen that there are stations from which no bike has left in the considered time. These stations, in the context of the popularity rating, were not taken into account and were removed from the dataset.
<img width="750" height="400" src = figures/fig_5.png/>



## Exploratory data analysis <a name = "exploratory_data_analysis"></a>

### Interactive grouping of bike stations using the Folium library <a name = "interactive_grouping_of_bike_stations"></a>

The analysis and visualization of this data uses the Folium library, thanks to which it was created a map containing interactive markers that automatically group the number of stations on the map. Tags are grouped with locations if they are close enough to each other.

The picture below shows the map of Warsaw with the location of <b>380</b> bike stations using interactive grouping.

<img width="600" height="350" src = figures/fig_6.png/>

<br>
On this map there are names of  stations along with the number of bike stands there. This is visible after zooming in on the map and hovering the cursor over the selected marker.

<img width="600" height="350" src = figures/fig_7.png/>




### Analysis of the popularity of bike routes <a name = "analysis_of_the_popularity_of_bike_routes"></a>

The main dataset was transformed into a dataset containing information on bike numbers at stations to analyze popular bike routes.
The analyzed set, containing information about the numbers of bikes that are docked at the station in a given time interval, constitutes <b>19 783 745</b> observations. In the analyzed period, information on <b> 5249</b> bikes was recorded.
The analyzed dataframe is presented below. </br>
<img width="550" height="300" src = figures/fig_8.png/>

By using the Folium library, the most popular routes can also be shown. Those that were counted at least 50 times over the analyzed period are presented on the map below.
<img width="550" height="500" src = figures/fig_9.png/>


### Exploration of patterns of bike routes using clustering algorithm <a name = "exploration_of_patterns_of_bike_routes"></a>

Routes can be represented as a graph. Such a graph with distinguished clusters is presented below (the <b>Louvain algorithm</b> which is a hierarchical clustering algorithm was used as the clustering method).
<img width="620" height="600" src = figures/fig_10.png/>

The composition of three exemplary clusters is presented below.
<img width="600" height="210" src = figures/fig_11.png/>


The vast majority of stations in a particular cluster are stations located in one region, so it can be concluded that people most often move between stations located in close proximity to each other.
This relationship can also be seen on the heatmap below. </br>
<img width="540" height="500" src = figures/fig_12.png/>


It shows that most people cycle between stations not far from each other (stations with similar ID numbers).


The table below presents the most popular bike routes (the count column indicates the number of bike trips from station A to station B in a given period).
<br>
<img width="450" height="220" src = figures/fig_13.png/>


The picture below shows the map of Warsaw with the 15 most popular bike routes marked.
<img width="400" height="450" src = figures/fig_14.png/>

The most popular routes can also be presented as a graph.
<img width="500" height="450" src = figures/fig_15.png/>

The fragment of the map of Warsaw illustrates the most popular bike route  <b>Stefana Banacha - UW <—> al. Niepodległości - Batory </b> is presented below.</br>
<img width="550" height="280" src = figures/fig_16.png/>



### Analysis of the length of bike rentals <a name = "analysis_of_the_length_of_bike_rentals"></a>

The histogram below illustrates how long bikes are typically rented. Unfortunately, due to the low dynamics of data (data was collected every 10 minutes), this histogram is burdened with a large error and a trip that lasted e.g. 12 minutes can be recorded in the same way as a 28 minutes drive. For example, a bike that was rented at 2:39 and returned at 2:51 was qualified as a 30 minutes ride, as well as a bike rented at 2:31 and returned at 2:59. The 30 minutes bar does not have to specify such a bike rental time and with more dynamic data it could be a 20 minutes value. The issue of the length of renting a bike is quite important because the first 20 minutes of bike rental are free. </br>
<img width="500" height="300" src = figures/fig_17.png/>


### Analysis of bike rentals <a name = "analysis_of_bike_rentals"></a>
 
The notebook includes many charts, among others
correlation between the number of bike rentals and temperature or day of the week. <br>
The chart below shows the relationship between the number of bike rentals and temperature.
<img width="550" height="300" src = figures/fig_18.png/>



This relationship can also be seen in the scatter plot of number of bike rentals depending on temperature.
<img width="550" height="300" src = figures/fig_19.png/>
<br>

With regard to number of bikes rented per hour on each days, it is as follows:
<img width="550" height="300" src = figures/fig_20.png/>
<br>


The table of correlation values ​​between the number of bikes rented and temperature or total rainfall during the day is presented below. </br>
<img width="250" height="100" src = figures/fig_21.png/>

The Pearson correlation coefficient between the number of bikes rented and the temperature is <b>0.67</b>, which indicates a significant correlation between these variables. Pearson's correlation coefficient between the number of bikes rented and the sum of rainfall is <b>-0.41</b> (negative correlation), which shows a moderate correlation.


The graph below shows the number of bike rentals depending on the hour on each day of the week. </br>
<img width="600" height="300" src = figures/fig_22.png/>

The table below presents a detailed average number of bikes rented at specific hours of each day of the week.
<img width="450" height="520" src = figures/fig_23.png/>


Looking at the graph and table above, it can be seen that the largest number of bike rentals is recorded on working days in the <b>afternoon</b>, i.e. <b>4 - 5 p.m.</b>, and higher than usual rental values ​​are also visible in the <b>morning 7 - 8 a.m.</b>. Therefore, it can be concluded that city bikes are a popular means of transport when commuting to or returning from work, school, or they are used to transport to the subway station. The graph shows that city bikes are also popular on weekends. Great interest can be seen in the afternoon (especially on <b>Sundays</b>).

### Popularity analysis of bike stations <a name = "popularity_analysis_of_bike_stations"></a>

The most popular bike stations in Warsaw (with the largest median of bike rentals during the day) are the following stations: <b>Al. Niepodległości - Batory</b>, <b>Stefan Banach - UW</b> and <b>Rondo Jazdy Polskiej</b>. The dataframe of the 10 bike stations with the highest median of bike rentals is presented below. </br>
<img width="450" height="300" src = figures/fig_24.png/>
