#### **Smart Cities: the use of sensors to help tackle the Urban Heat Island effect**
##### A Data-Science-for-Smart-Cities project carried out with Python | October 24, 2017 

---


#### Problem Statement: the Urban Heat Island Effect (UHI)

<img src="/images/Atlanta_thermal.jpg" width="380" height="280"> 


The image above was collected in May 1997 by NASA ([source](https://commons.wikimedia.org/w/index.php?curid=6026139)) 
to show the distribution of temperatures in downtown Atlanta. The majority of the white areas happen to be located on roofs, and 
a significant contribution is given by the streets (in red). This phenomenon, known as [Urban Heat Island effect](https://en.wikipedia.org/wiki/Urban_heat_island), is all but new, having first been observed in the early 19th Century. It indicates an increase in temperatures around the city core with respect to the rural areas surrounding it, and it is caused by the introduction of dark surfaces - [asphalt](https://en.wikipedia.org/wiki/Asphalt), mainly - that absorb the incident solar radiation. This leads to an increase in temperature on the surface of dark objects, which in turn produces a spike in the thermal radiation they emit back into the air. 
Rooftops and roads are particularly good heat absorpters, due to the presence of [asphaltene](https://en.wikipedia.org/wiki/Asphaltene). 

<img src="/images/asphalt.jpg" width="300" height="240"> 

A look into the typical values of [thermal conductivity](https://en.wikipedia.org/wiki/Thermal_conductivity) quantifies the extent to which concrete and asphalt are serious contributors, their contribution being amplified by the dense spatial presence of roads and rooftops.

<table class="tg">
  <tr>
    <th class="tg-baqh" colspan="2">Thermal Conductivity [W/(m K)]</th>
  </tr>
  <tr>
    <th class="tg-baqh">Material</th>
    <th class="tg-baqh">Value</th>
  </tr>
  <tr>
    <td class="tg-baqh">Asphalt</td>
    <td class="tg-baqh">0.75</td>
  </tr>
  <tr>
    <td class="tg-baqh">Bricks</td>
    <td class="tg-baqh">0.47</td>
  </tr>
  <tr>
    <td class="tg-baqh">Concrete, medium</td>
    <td class="tg-baqh">0.4 - 0.7</td>
  </tr>
  <tr>
    <td class="tg-baqh">Concrete, dense</td>
    <td class="tg-baqh">1.0 - 1.8</td>
  </tr>
  <tr>
    <td class="tg-baqh">Soil with organic matter</td>
    <td class="tg-baqh">0.15 - 2.0</td>
  </tr>
  <tr>
    <td class="tg-baqh">Wood</td>
    <td class="tg-baqh">0.07 - 0.17</td>
  </tr>
</table>


As pointed out by the [NASA Earth Observatory](https://earthobservatory.nasa.gov/Features/UrbanRain/urbanrain2.php), the UHI effect triggers a negative climatic effect. Urban landscapes may experience temperatures between 3.5°C and 4.5°C higher than the surrounding landscapes, resulting in warmer and unstable layers of air that can hold more moisture. [Research has demonstrated that this increases the frequency of more extreme rainfall events in the summer](https://www.atmos-chem-phys.net/17/5439/2017/acp-17-5439-2017.pdf) in the Northern Hemisphere. As a result, the risk of floods may increase.

#### The Los Angeles solution

<img src="/images/LA.jpg" width="380" height="280"> 

The Mayor of Los Angeles has recently committed to painting some of the city streets in a light shade of grey (pictured above, courtesy of the [Bureau of Street Services](https://bss.lacity.org)) in an attempt to cut the UHI effect. As reported by the [press](http://www.digitaljournal.com/news/environment/los-angeles-paining-streets-white-to-combat-urban-warming/article/502092), the ambition is to decrease urban temperatures by as much as 1.67°C over the next two decades. The plan is to use a specific coating that, in a pilot experiment, has led to a decrease in road surface temperature of 4.5°C. Apparently, this solution could potentially offset the projected increase reported by NASA and exceed the ambition of the Bureau of Street Services.
However, the financial side of things is not equally promising, as the cost of the specific coating to be used is estimated to be around [$40,000 per mile](http://www.mercurynews.com/2017/05/22/cool-pavement-to-cut-urban-street-heat-gets-first-california-tryout-in-canoga-park/). Moreover, the Bureau of Street Services is responsible for maintaining [6,500 miles of streets and 800 miles of alleys](https://www.google.co.uk/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=0ahUKEwj-3M7NrpPXAhXQaVAKHYBgCI4QFggqMAE&url=http%3A%2F%2Fbss.lacity.org%2Fstate_streets%2Fstateofthestreets.htm&usg=AOvVaw3aIaOEQBr27krhVrplNCSV), accounting for the largest street system in the United States at the municipal level. Having to allocate $260 million to coat the streets (while neglecting the alleys) is probably haunting the dreams of city officials. The answer may lie in a **decision-making tool to identify areas to prioritise, allowing to create a strategic investment plan**.

#### How Big Data from Smart Infrastructures can enable Smart Decisions

<img src="/images/sensors.jpg" width="300" height="280"> 

Manufacturers and suppliers of sensors have already started supplying devices ([picture above](https://www.campbellsci.eu/road-surface-sensors)) that can measure **road surface temperatures** at very short intervals of time. These datasets are an ideal component of open datasets that cities could make available.
This project was carried out using the open data made available by the [City of Seattle Open Data Portal](https://data.seattle.gov/Transportation/Road-Weather-Information-Stations/egc4-d24i), which records data for 10 bridges and road intersections (pictured below) every minute. Ideally, sensors should be placed at each intersection and on each bridge. However, the cost of installing dense networks and the lack of awareness are probably the reasons why extended datasets are rather difficult to find.

<img src="/images/Sensor_locations.png" width="610" height="360"> 

##### Taking advantage of Python

This project takes advantage of the Python programming language and its packages dedicated to Big Data Analytics. The City of Seattle road surface temperatures come in a *.csv* file of 2.26GB and span the 03/03/2014 to 24/10/2017 period, with over 700,000 measurements. To avoid memory issues, the script associated with this project loads the file as an [high-performance, very large data frame](http://dask.pydata.org/en/latest/dataframe.html) and queries it. On average, the hottest month in Seattle is August, and as such, all data outside this window are dropped to save memory. A quick look at the average temperature values for 1-minute intervals reveals the sine wave trends for August 2016:

<img src="/images/timeseries.png" width="720" height="880"> 


<table class="tg">
  <tr>
    <th class="tg-baqh" colspan="2">Average Peak Time of Road Surface Temperature</th>
  </tr>
  <tr>
    <th class="tg-baqh">Bridge</th>
    <th class="tg-baqh">Time</th>
  </tr>
  <tr>
    <td class="tg-baqh">35th Avenue SW - SW Myrtle Street</td>
    <td class="tg-baqh">17:35</td>
  </tr>
  <tr>
    <td class="tg-baqh">Alaskan Way Viaduct - King Street</td>
    <td class="tg-baqh">15:55</td>
  </tr>
  <tr>
    <td class="tg-baqh">Albro Place Airport Way</td>
    <td class="tg-baqh">15:55</td>
  </tr>
  <tr>
    <td class="tg-baqh">Aurora Bridge</td>
    <td class="tg-baqh">15:21</td>
  </tr>
  <tr>
    <td class="tg-baqh">Harbor Avenue Upper North Bridge</td>
    <td class="tg-baqh">16:08</td>
  </tr>
  <tr>
    <td class="tg-baqh">Jose Rizal Bridge North</td>
    <td class="tg-baqh">16:10</td>
  </tr>
  <tr>
    <td class="tg-baqh">Magnolia Bridge</td>
    <td class="tg-baqh">15:51</td>
  </tr>
  <tr>
    <td class="tg-baqh">NE 45th Street Viaduct</td>
    <td class="tg-baqh">15:54</td>
  </tr>
  <tr>
    <td class="tg-baqh">Roosevelt Way - NE 80th Street</td>
    <td class="tg-baqh">14:05</td>
  </tr>
  <tr>
    <td class="tg-baqh">Spokane Swing Bridge</td>
    <td class="tg-baqh">16:10</td>
  </tr>
</table>

Except for the 35th Avenue SW - SW Myrtle Street location, which is not a bridge but an intersection, all average peak times are between 2:05PM and 4:10PM, with a group of values gathered around 3:55PM. This concentration does not occur in a specific area of the city, and the different peak times may be a result of shadowing buildings. As a representative case, the 3:50PM-4:10PM interval is considered as the *de facto* average peak time given its recurrence. Depending on the case, specific times may be chosen, especially if the study targets a specific sensor or group of sensors. The maximum average road surface temperature for the month of August 2016 in the 3:50PM-4:10PM time frame is shown below.

<table class="tg">
  <tr>
    <th class="tg-baqh" colspan="2">Maximum Average Road Surface Temperature [°C]</th>
  </tr>
  <tr>
    <th class="tg-baqh">Bridge</th>
    <th class="tg-baqh">Value</th>
  </tr>
  <tr>
    <td class="tg-baqh">35th Avenue SW - SW Myrtle Street</td>
    <td class="tg-baqh">25.34</td>
  </tr>
  <tr>
    <td class="tg-baqh">Alaskan Way Viaduct - King Street</td>
    <td class="tg-baqh">33.94</td>
  </tr>
  <tr>
    <td class="tg-baqh">Albro Place Airport Way</td>
    <td class="tg-baqh">38.35</td>
  </tr>
  <tr>
    <td class="tg-baqh">Aurora Bridge</td>
    <td class="tg-baqh">29.17</td>
  </tr>
  <tr>
    <td class="tg-baqh">Harbor Avenue Upper North Bridge</td>
    <td class="tg-baqh">35.32</td>
  </tr>
  <tr>
    <td class="tg-baqh">Jose Rizal Bridge North</td>
    <td class="tg-baqh">36.77</td>
  </tr>
  <tr>
    <td class="tg-baqh">Magnolia Bridge</td>
    <td class="tg-baqh">35.77</td>
  </tr>
  <tr>
    <td class="tg-baqh">NE 45th Street Viaduct</td>
    <td class="tg-baqh">35.19</td>
  </tr>
  <tr>
    <td class="tg-baqh">Roosevelt Way - NE 80th Street</td>
    <td class="tg-baqh">31.71</td>
  </tr>
  <tr>
    <td class="tg-baqh">Spokane Swing Bridge</td>
    <td class="tg-baqh">36.15</td>
  </tr>
</table>

These temperatures are much lower than those recorded for Los Angeles, although the average number of sunny days in Seattle is only 46.47% of what Los Angeles typically experiences. The different latitudes should be accounted for as well. 

#### Interactive plotting
The interactive package [Folium](http://folium.readthedocs.io/en/latest/index.html) is an elegant way to create an interactive plot of the maximum average road surface temperatures using the City of Seattle base map. This map would come with a much finer resolution if a denser network of sensors was available. Also, a densely populated map could help visualize how these temperatures are distributed across the city, to improve the effectiveness of decision-making. However, given the coarse resolution of the available datasets, this project aims at showing what could be produced if larger data were available. The image below shows the spatial distribution of road surface temperatures in the 10 locations available. Its interactive nature is best appreciated by looking at the <a href="/Files/2017-10-24-Sensors-for-Smart-Cities.ipynb" target="_blank">source Jupyter script</a>, where it is possible to zoom in, click, and read the details of each bridge.

<img src="/images/Heatmap.png" width="520" height="340"> 

#### Conclusion

In the context of a strategic investment plan, this short project allows to identify the bridges that should be coated first based on a (coarse) network of road surface temperature sensors. The 10 bridges included in this pilot study certainly are a non significant sample: amounting to an overall length of 5.1 miles, they are a negligible portion of the over 3,900 miles of paved roads that compose the Seattle's urban texture. In this limited sample, there does not seem to be any particular spatial bias. The Albro Place Airport Way bridge stands out as a remarkable contributor relative to other locations, whereas the 35th Avenue SW - SW Myrtle Street junction is on the other side of the spectrum, and it would be ignored by the investment plan. 
Again, if a denser network was available, the [Seattle City Council](https://www.seattle.gov/council/) could select a fraction of the roads that emit the most heat. This would be possible because a denser network could produce measurements at short distances, resembling a grid. The purchase and installation of sensors is only the early stage of a costly process, which burden could probably be lightened by the use of a [fleet of drones equipped with thermal cameras](https://www.dslrpros.com/thermal-drones.html?gclid=Cj0KCQjwm9vPBRCQARIsABAIQYfOtOT23jMkPh_kgD1aR-Gl8-p3puJ2M_yqdADlrBelh29Kt4XOBX0aAnkzEALw_wcB). 
Whatever the cost, however, it seems that the era of [Digital Transformation and IoT](https://www.ice.org.uk/news-and-insight/the-civil-engineer/july-2017/has-digitals-impact-civil-engineering-really-hit) that is fastly approaching the world of Civil Engineering asks for a radical change in perspective, wise investment plans, and *does not take no for an answer*.

---
<a href="/Files/2017-10-24-Sensors-for-Smart-Cities.ipynb" target="_blank">Project script available here</a>

