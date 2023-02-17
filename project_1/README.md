![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 1: Exploring climate data of Singapore


### Problem Statement


It was reported in 2013 that more accidents occur on days of thunderstorms. Traffic accidents cause road congestion and Traffic Police and Civil Defence resources need to be deployed to help ease this. By using climate information on rainfall and traffic accident statistics, this project aims to help Traffic Police and Civil Defence better facilitate manpower and resource allocation throughout the year by identifying trends between traffic accidents and weather.

---

### Datasets	


##### Weather related Datasets[](http://localhost:8888/notebooks/Documents/GA/my_materials/project_1/code/starter-code.ipynb#Weather-related-Datasets)

rainfall-monthly-total.csv: Monthly total rain recorded in mm(millimeters) from 1982 to 2022.

rainfall-monthly-number-of-rain-days.csv: Monthly number of rain days from 1982 to 2022. A day is considered to have “rained” if the total rainfall for that day is 0.2mm or more.

sunshine-duration-monthly-mean-daily-duration.csv: The monthly mean sunshine hours in a day recorded at the Changi Climate Station from 1982 to 2022.

rainfall-monthly-highest-daily-total.csv: The highest daily total rainfall for the month recorded at the Changi Climate Station recorded in mm(millimeters) from 1982 to 2022.

All above datasets provided in data folder for Project 1 obtained from  [data.gov.sg](http://localhost:8888/notebooks/Documents/GA/my_materials/project_1/code/data.gov.sg)

##### Traffic Accident related Datasets[](http://localhost:8888/notebooks/Documents/GA/my_materials/project_1/code/starter-code.ipynb#Traffic-Accident-related-Datasets)

traffic_accident_statistics.csv: Traffic accident data reflected as accidents per month between 2008 to 2021 to include both accidents resulting in fatalities, and caused injury.

Traffic accident dataset obtained from  [https://www.police.gov.sg/-/media/1F7F9460FD8F48928B6DEFE096414975.ashx](https://www.police.gov.sg/-/media/1F7F9460FD8F48928B6DEFE096414975.ashx), table 1a and converted into a csv file.

---

### Outside Research


I have quoted the title of an article cited below, (1), in my problem statement as it quite aptly summed up the problem. I also google searched for relavent data to be used for my project. I have taken the traffic accident data from the cited source below, (2), specifically table 1a which comprises of data that reflects accidents per month between 2008 to 2021 to include both accidents resulting in fatalities, and caused injury as this would affect how Civil Defence resources are deployed.

The further along the project I got, it became clear that I may have to recommend an expansion on the data required of this project to properly aid in truly efficient resource allocation. I then took some experiences from the US (3) and how weather may affect road conditions there to see what other statistics can be recommended for an improved version of this study.

1.  [https://www.straitstimes.com/singapore/more-road-accidents-on-days-of-thunderstorms](https://www.straitstimes.com/singapore/more-road-accidents-on-days-of-thunderstorms)  (reported in 2013)

2.  [https://www.police.gov.sg/-/media/1F7F9460FD8F48928B6DEFE096414975.ashx](https://www.police.gov.sg/-/media/1F7F9460FD8F48928B6DEFE096414975.ashx)  (published statistics from SPF 2021)
    
3.  [https://ops.fhwa.dot.gov/weather/q1_roadimpact.htm](https://ops.fhwa.dot.gov/weather/q1_roadimpact.htm)

---

### Process Overview

#### Data Import & Cleaning

1. The weather datasets were imported and merged checked for data type and missing values.
2. They were then merged and cleaned to form a dataframe with the desired information displayed such that it was easier for me to later on use the columns for visualization.
3. Traffic accident dataset was then imported and went through the same cleaning process as the weather datasets.
4. Traffic accident dataset was then manipulated to match the merged weather dataframe so that it would be easy to merge.
5. Weather and traffic accident data was then merged only to only fit the years 2008 to 2021 for easy comparison later on, and also because traffic data was only available for the aforementioned years.

#### Exploratory Data Analysis
##### Steps Taken
1. Calculation of mean, median and standard deviations of all the relevant data was done.
2. Minimum and maximum values were taken for years at intervals to see if there was any emerging patterns that could be discovered.
3. Box plots for all columns were done to determine if there were outliers worth noting in the data.
4. Another dataframe was created using the original to display the data as a sum in years as opposed to months was created to explore a more macro view to see if there were any patterns to be found.
5. Usage of .corr() to find if there were any correlations worth noting for both monthly and yearly dataframes. 

##### Initial Findings
1. There were no significant patterns or correlations when matching each metric with Traffic Accident statistics from the EDA done. 
2. It was noted that there were significantly more outliers for Accident Statistics as compared to the rest of the weather data which warrants further investigation.
3. It was noted that 2020 and 2021 were covid lockdown years which significantly reduced the total number of accidents in those 2 years. (perhaps road usage data should be used to compare next to weather data and accident statistics to form a more robust study)

#### Visualization of Data
1. Heatmap was used to find correlation between accidents and weather data for both months and years.
Findings: No strong and significant correlations were observed, however, it was noted that the highest possible correlations, although not very significant, came from the maximum rainfall recorded in a day (I made an assumption that this would mean intensity of rainfall on that given day), and the mean number of hours of sunshine per day in a month, which suggests visibility on roads is a factor to consider.

2. Histograms were plot to find the distribution of all the data and color coded for the rest of the visualization process. 
Findings: Most of the weather statistics are relatively normally distributed and their means and medians are also all very close to each other. Possible outliers were noticed and warrant further investigation to check for special occurrences outside of seasonal phenomenon. 
The traffic accident distribution is skewed to the left but could be more pronounced because of the inclusion of numbers between 2020 and 2021 (covid lockdown)

3. Boxplots were also plot and color coded as above for all data.
Findings: These further reinforced the findings I made when looking through the histograms in terms of distribution and the presence of outliers in the traffic data, total rainfall monthly, and the maximum rainfall recorded in a day for the month.

4. Scatter plots were plot for traffic accidents versus all the other weather data to see if other patterns emerged and were color coded as above.
Findings: After plotting the scatter plots of all the different weather variables versus the number of accidents recorded, no clear trends stand out. This could be an indicator that on it's own, weather does not significantly affect the number of traffic accidents.

5. Line graphs were also plot and color coded for the traffic data and all the weather data.
Findings: The line graphs seem to reaffirm what we concluded above in the scatter plots. That the weather data as it is, does not show any meaningful correlation or trends when compared with accident statistics.

---

### Conclusions and Recommendations


Conclusion: Given the lack of a correlation or clear pattern when comparing weather statistics against traffic accident data, we can conclude that weather on its own is not a significant reason for traffic accidents in Singapore. 

Recommendations: For now, I would recommend maintaining the status quo in terms of resource allocation during months with high rainfall numbers. I would also recommend that we explore using the following data, together with weather data when determining how to properly allocate manpower and resources.

1. Obtain weather data from other parts of Singapore and compare them to the corresponding accident statistics in that area.
2. Due to the drastic fall in accidents in 2020 and 2021, I would suggest looking at the correlation between road usage and traffic accidents.
3. A quick Google search online will yield many articles suggesting that visibility is a factor in the number of accidents (citations number 3). I would suggest obtaining weather data specifically looking at months with stormy weather and intense rainfall against traffic accident statistics.

Based on the outliers found in traffic accident data distribution due to the inclusion of 2020 and 2021 statistics, I would recommend that instead of allocating additional resources to Traffic Police and Civil Defence during the rainy season, resources should be directed to reducing road usage in general in order to bring down the number traffic accidents.

---

### Data Dictionary
|Feature|Type|Dataset|Description|
|---|---|---|---|
|total_rainfall|float|rainfall-monthly-total.csv| Monthly total rain recorded in mm(millimeters) from 1982 to 2022.| 
|maximum_rainfall_in_a_day|float|rainfall-monthly-highest-daily-total.csv|The highest daily total rainfall for the month recorded at the Changi Climate Station recorded in mm(millimeters) from 1982 to 2022.| 
|no_of_rainy_days|integer|rainfall-monthly-number-of-rain-days.csv|Monthly number of rain days from 1982 to 2022. A day is considered to have “rained” if the total rainfall for that day is 0.2mm or more.| 
|mean_sunshine_hrs|float|sunshine-duration-monthly-mean-daily-duration.csv|The monthly mean sunshine hours in a day recorded at the Changi Climate Station from 1982 to 2022.| 
|num_of_accidents|integer|traffic_accident_statistics.csv|Traffic accident data reflected as accidents per month between 2008 to 2021 to include both accidents resulting in fatalities, and caused injury.|

---

### Citations

1. https://www.straitstimes.com/singapore/more-road-accidents-on-days-of-thunderstorms (reported in 2013)

2. https://www.police.gov.sg/-/media/1F7F9460FD8F48928B6DEFE096414975.ashx (published statistics from SPF 2021)

3. https://ops.fhwa.dot.gov/weather/q1_roadimpact.htm 