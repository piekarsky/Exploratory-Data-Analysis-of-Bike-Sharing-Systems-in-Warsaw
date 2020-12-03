# Analysis-And-Visualization-For-Bike-Sharing-Systems-In-Warsaw


<p style="font-size:30px"><b>1. Project description </b></p>

Jupyter Notebook contains data analysis and visualization of the bike-sharing system in Warsaw. The project uses over 4,100 JSON files, saved every 10 minutes, containing station data and lists of bikes located at each bike station in Warsaw.
The project uses archival meteorological data collected by the Institute of Meteorology and Water Management - available at https://danepubliczne.imgw.pl/datastore.

Main information about data:
- 4,184 JSON files, saved every 10 minutes between 03/04/2018 - 04/04/2018
- 1 JSON file contains information on an average of 355 bicycle stations in Warsaw
<hr>


2. Description of dataset
An overview of the most important attributes included in this set used in the analysis and visualization is presented below:

- uid - identifier of a bike station
- bikes - the number of bikes at a station
- bike_racks - the number of racks at a station
- free_racks - the number of free positions at a station
- bike_numbers - numbers of individual bikes pinned at a given station
- lat, lng - coordinates (longitude and latitude) of a bike station

<hr>





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

