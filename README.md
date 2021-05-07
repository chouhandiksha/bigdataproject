


# Visualizing the Mobility Gradient Over Time and in Relation to Poverty



**Students:** Justin Snider, Anchit Srivastava, and Diksha Chouhan

**Professor:** Juliana Freire

**TAs:** Rupesh Bagwe and Christina Ye

**Paper:** [paper.pdf](paper.pdf)

**Slideshow:** [slides.pdf](slides.pdf)




## Abstract

We compared the mobility patterns of people in Chicago, New York City and Los Angeles metropolitan area in 2020 as they respond to the COVID-19 pandemic. Then, within each city, we compared the mobility patterns of census block groups with different levels of poverty. Using the SafeGraph Social Distancing Data mobile phone metadata, generated from mobile phone records, we were able to observe daily behaviors such as full-time work, part-time work and full-time stay at home behavior. The daily statistics are provided for each Census Block Group (CBG). The data we use to find the population size of each CBG, the number of people in poverty in each CBG and calculate the percentage of the population in poverty is the American Community Survey (2016) 5-year estimate available from SafeGraph. We compare the mobility of Census Block Groups with high and low percentages of individuals in poverty. We visualize and explain who has been able to effectively decrease their mobility. Understanding who has not been able to decrease their mobility can help us understand who is most at risk and who is most in need of assistance to reduce their exposure to COVID-19. [5]

You can read the full paper [here](paper.pdf).




## README Table of Contents

  * [Abstract](#abstract)
  * [Introduction](#introduction)
  * [Related Work](#related-work)
  * [Findings](#findings)
    + [Stay at Home Behavior](#stay-at-home-behavior)
    + [Full-time and Part-time Work Behavior](#full-time-and-part-time-work-behavior)
    + [Data Reliability](#data-reliability)
  * [Computational Reproducibility Instructions](#computational-reproducibility-instructions)
    + [Step 1 // Get the Data](#step-1----get-the-data)
    + [Step 2 // Extract the Needed Rows And Columns](#step-2----extract-the-needed-rows-and-columns)
    + [Step 3 // Data Cleaning and Quality Verification](#step-3----data-cleaning-and-quality-verification)
  * [Notebooks](#notebooks)
      - [New York Times COVID-19 Data // Extraction and Cleaning:](#new-york-times-covid-19-data----extraction-and-cleaning-)
      - [SafeGraph Census Data // Extraction and Cleaning:](#safegraph-census-data----extraction-and-cleaning-)
      - [SafeGraph Social Distancing Dataset // Extraction (Using Pandas):](#safegraph-social-distancing-dataset----extraction--using-pandas--)
      - [SafeGraph Social Distancing Dataset // Extraction (Using Spark):](#safegraph-social-distancing-dataset----extraction--using-spark--)
      - [SafeGraph Social Distancing Dataset // Cleaning:](#safegraph-social-distancing-dataset----cleaning-)
      - [SafeGraph Social Distancing Dataset // Analysis:](#safegraph-social-distancing-dataset----analysis-)
  * [Data Sources](#data-sources)
  * [Data Acquisition](#data-acquisition)
    + [New York Times COVID-19 Data](#new-york-times-covid-19-data)
    + [SafeGraph Social Distancing Metrics](#safegraph-social-distancing-metrics)
    + [SafeGraph Census Block Group Data](#safegraph-census-block-group-data)
  * [Data Extraction](#data-extraction)
    + [New York Times COVID-19 Data](#new-york-times-covid-19-data-1)
    + [SafeGraph Census Block Group Data](#safegraph-census-block-group-data-1)
    + [SafeGraph Social Distancing Metrics](#safegraph-social-distancing-metrics-1)
  * [Data Cleaning](#data-cleaning)
    + [New York Times COVID-19 Data](#new-york-times-covid-19-data-2)
    + [SafeGraph Census Block Group Data](#safegraph-census-block-group-data-2)
      - [Chicago Metropolitan Area Demographic Data](#chicago-metropolitan-area-demographic-data)
      - [Los Angeles Metropolitan Area Demographic Data](#los-angeles-metropolitan-area-demographic-data)
      - [New York Metropolitan Area Demographic Data](#new-york-metropolitan-area-demographic-data)
    + [SafeGraph Social Distancing Metrics](#safegraph-social-distancing-metrics-2)
      - [Chicago Metropolitan Area Social Distancing](#chicago-metropolitan-area-social-distancing)
      - [Los Angeles Metropolitan Area Social Distancing](#los-angeles-metropolitan-area-social-distancing)
      - [New York Metropolitan Area Social Distancing](#new-york-metropolitan-area-social-distancing)
  * [Citations and Bibliographies](#citations-and-bibliographies)



## Introduction

Many recent papers, including "Mobility network models of COVID-19 explain inequities and inform reopening" [1] and "Coronavirus infections and deaths by poverty status: The effects of social distancing" [2] have established an essential link between mobility and COVID-19 infection rates and deaths. We study the daily change in mobility of the general population during 2019 and 2020 in the three most populous cities in the US: New York, Los Angeles and Chicago. Using the SafeGraph Social Distancing Metrics data\cite{safegraph_social}, we analyze mobility at the resolution of the census block group level. We use attributes such as the number of devices that remain at home, the count of devices with full-time work behavior, the median distance traveled by devices and other vital actions relevant to mobility. We then visualize each city’s mobility using graphs and maps produced with the GeoJSON file provided by SafeGraph of the Census Blocks. 

We compare the mobility of census blocks with the largest and smallest percentage of people in poverty based on the Census American Survey data provided by SafeGraph [3]. Our objective is to better understand and visualize to what degree different groups have adopted limited mobility to mitigate the documented threat of COVID-19 exposure created by higher mobility. 

All code used to extract, clean, integrate and visualize the data is available on the project Github repository https://github.com/chouhandiksha/bigdataproject. All the steps used for acquiring, extracting, integrating and cleaning the data used for the project are described in sections 3 through 6. 



## Related Work

In the \textit{Nature} article "Mobility network models of COVID-19 explain inequities and inform reopening"\cite{Chang2021} Chang et al. produce a model that predicts the number of anticipated SARS-CoV-2 infections. The model takes as an input mobility data derived from mobile phone data. The model tracks the predicted number of susceptible, exposed, infectious and removed (SEIR) people anticipated to be in the population. The model is able to predict real case trajectories on held out data. The model correctly predicts higher infection rates among disadvantaged racial and socioeconomic groups solely as the result of differences in mobility. 

Several months have passed since the publication of this article. All the 2020 data is now available from SafeGraph. There is now an opportunity to evaluate visualize the relationships between mobility, income, race and the impact of COVID-19 in our communities.\cite{Reeves_RV_Rothwell_J_2020}

"Coronavirus infections and deaths by poverty status: The effects of social distancing"\cite{jung_manley_shrestha_2021} have shown the highest initial number of cases are in both the wealthiest and poorest countries. However, there is a great difference between the wealthy and poor countries when stay at home policies are put in place. The wealthiest countries have been able to show much greater reductions in mobility. As a result the wealthiest countries are able to curb the infection rates more effectively than poorer countries.



## Findings

During our study includes identical analysis on the cities of New York, Los Angeles and Chicago. Starting in March of 2020 much of the population in Chicago, New York City and Los Angeles metropolitan area drastically changed their mobility patterns.  Using the SafeGraph Social Distancing data we visualize the scale of the change in population mobility through analysis of the amount of people staying at home, leaving home for full-time work and leaving home for part-time work. We compare the ability of the three cities to adopt new mobility patterns revealing both similarities and differences. 

Comparisons are also made between the mobility patterns of census block groups with the highest and lowest levels of poverty in all three cities. We find areas with low levels of poverty reduce their mobility much more than those areas with high poverty. Specifically vulnerable populations in census block groups where 80% to 100% of the population are living in poverty are less able to reduce their mobility by staying at home and working from home. The majority of the population exhibit a rapid change in behavior to stay at home in March and April of 2020. However, for the poorest census block groups the response tends to be slower, less drastic, less lasting, or all three.

One of the most notable findings we observed was New York stands out from Chicago and Los Angeles at all stages of analysis. The disparity between the richest and poorest groups is seen to be the most prolonged and continuous in New York [8]. It is also clearly visible that the mobility between the two groups are distinct from each other throughout the year. As soon as the stay at home orders are imposed, the two lines that show our mobility parameters including completely home, full-time and part-time work begin to separate. For the entire 2020, we see that this disparity continues.  This finding is also presented and talked about in a studies published in the International Journal of Population Research. [9] 



### Stay at Home Behavior


In all three cities the fully at home percentage of the population starts below the 2019 mean. However, in mid-march the percentage increases drastically with the trend continuing into April where all three cities peak.

The stay at home percentage reaches an extreme peak during April. New York has the highest peak at about 55 percent of individuals staying at home. Los Angeles just barely touches 50 percent and Chicago peaks below 50 percent.

We get an even clearer picture of the change of behavior when we look at the 2020 stay at home percentage deviation from the 2019 mean. We can see both New York and LA were able to change their behavior to a much greater extent than Chicago. Specifically, New York and LA increase their stay at home percentage by about 25% from mid-March to mid-April. Chicago on the other hand exhibits an increase close to 20% and is not able to keep the stay at home percentage above the 2019 mean through the summer. New York and LA maintain slightly elevated numbers.

There are also consistent trends when it comes to the relationship between poverty and the fully at home percentage. When we group census block groups by the percentage of the population in poverty we find areas with highest levels of poverty, 90%-100%, have the lowest fully at home percentages in all three cities.

The mobility disparity between the wealthy and the poor is often most pronounced in March and April of 2020, which is a trend we see in all three cities. In areas with high poverty less people stay fully at home to reduce their exposure.

We see in all three cities that areas with 90%-100% of the population below the poverty line approximately 5% less of the population do not stay at home.  A subtle trend that we see is that the wealthiest and poorest CBGs stay home the least on average in 2020. A larger percentage of those in the middle of the spectrum stayed home reducing their exposure. This surprising pattern is in parallel to the findings of Jung et al.[2] who found COVID infection rates to be the highest in the wealthiest and poorest countries. 

We plotted the map of Chicago, LA and New York for each day of 2020. The color of the CBG is set by the 2020 stay at home percentage deviation from the 2019 mean. A deep red represents over a 12% or more drop in the number of people at home from the 2019 mean. A deep blue represents an 11% or larger increase from the 2019 mean. 2020 up through the month of March starts out primarily red with a lot of activity. A relatively large percentage of people are out and not at home, especially during the weekdays. In all three cities we see a clear shift in behavior the days of March 14th, 15th and 16th. Monday, March 16th marked the first weekday we see a large number of people staying at home from work. Then, throughout the second half of March we see the majority of all three cities transition to a deep blue as many people stay at home. However, in all three cities you can still see deep red CBGs that are not staying at home.



#### Chicago

In Chicago, we see that the wealthiest people stayed at home significantly more than the poorest people for the entire period from March to June. In Chicago the values for the wealthy and the poor areas both begin to increase at the same time. The two lines sometimes track closely together. The CBGs with the greatest levels of poverty have a substantially larger percentage of the population not staying at home when compared with the CBGs having the lowest levels of poverty. From March 17 the two lines deviate. We commonly see 10% less of the population at home and sometimes up to 20%. Despite the mobility disparity, the wealthiest and poorest areas fully at home percentage values tend to track more closely than in the other cities, usually within about 5%. Part of the reason the groups track closely together is Chicago does not increase the stay at home percentage as much as New York and Los Angeles. The Chicago mean daily fully at home percentage peaks below 50%. We tracked down the dates of the major announcements related to lock downs in Chicago in 2020, and analyzed their effect in the people's mobility.[11]



#### Los Angeles

In the Los Angeles at fully at home percentages we see a large mobility disparity between the behavior of the areas with the highest and lowest levels of poverty. Areas with low poverty rapidly changed their behavior in March and April increasing the fully at home percentage of the population by almost 30%. However, we do not see the areas with low poverty making a substantial change in behavior for over a month and a half. The delay in changed behavior may have contributed substantially to the increased exposure of the poor to possible infection. In no other cities do we see such a slow response. While the wealthiest areas reach a peak stay at home percentage, the poorest have about 20% more of their population not staying fully at home. However, in May they is a rapid increase in the number of people in poor areas staying home that allows the two groups to predominantly converge on similar values.

In Los Angeles, the Governor imposed stay at home restrictions on March 19 but we already see an existing gap in mobility between the areas with the highest and lowest poverty levels. The gap remains the same throughout March and further in summer. During the second half of 2020, we see that the gap between the two groups minimizes but by the end of the year, it is evident from the visualisation that the difference in the mobility increases again. 



#### New York

The poorest areas in New York also have a delayed response, but the delay is shorter than we see in Los Angeles. The poorest areas took an additional 2 week to match the response of the rich when individuals began to stay home in March in New York. However, the poorest areas daily fully at home percentage stays 5% to 15% below the wealthiest for most of 2020. The mobility disparity is clear. In neither of the other two cities do we see such a sustained difference between the two groups. 

In New York, there is a significant drop in the stay-at-home percentage in the CBGs with the poorest population from March 9. The areas with the richest population on the other hand continuously increased their stay at home percentage and the gap between the two groups remained throughout the year. Following the month of March, the CBGs with the wealthiest population maintained their stay at home over 25% in March- April and above 15% later during summer. The CBGs with the poorest population show many irregularities in their behavior. We see that they stayed at home during the weekends but often during the weekdays they do not stay at home despite the lockdown impositions becoming stricter with time [7].



### Full-time and Part-time Work Behavior

The wealthiest areas in all three cities decrease the amount of the population commuting to full-time and part-time in mid-March. Then, they all maintain the low mobility throughout the rest of the year with only a slight gradual increase. The poorest areas in all three cities did not change their behavior in such a complete and consistent way. In all three cities the poor often leave home to go to work in larger numbers than those in more wealthy areas. 



#### Chicago

In Chicago, we see an inversion of the work behavior of the those with the greatest levels of poverty and those with the least. We see the behavior of the wealthy and the poor tracking more closely together than in New York and Los Angeles. 



#### Los Angeles

Unlike Chicago and New York, in Los Angeles the areas with the highest levels of poverty do not show a drastic decrease in full-time work in March and April. In fact the poorest areas show an increase in full-time work during all of 2020, including March and April. During the same period the wealthiest areas are steeply decreasing their commuting to work behavior. Even the average commuting to work behavior in all cities, including LA, shows a steep decline during this period. The poor areas in Los Angeles are initially low, often around 2%-3%, which may explain the lack of downward change. Perhaps the wealthy avoiding in-person work and many in poor areas not having work contributed to the increasing at-work numbers we see in Los Angeles through 2020. 

The part-time work behavior the poorest areas does decline in March. However, the magnitude of the change is small in comparison with the radically changing behavior of the wealthy. Furthermore, the poorest areas are back to high percentages of at-work patterns of behavior by August of 2020. 

The lack of rapid change in the fully at home home percentage among those living in poor areas is partly explained by the lack of substantial change in part-time work behavior and the increase in at-work behavior. We see a steep increase in the number of fully at home people at the end of April. At the same time full-time work is increasing steeply and part-time work is relatively stable. April is when the first round of stimulus checks went out, which may have been a major contributing factor to allow the increased at home percentage. Especially since full-time work is increasing at the same time. 



#### New York

In New York, wealthy people went out for full-time work more than the poor people, but this trend inverts sharply during March. Furthermore, we see that during subsequent months, there are some time periods when rich people go out more than the poor. However, these time periods are very rare and it is mostly poor people who couldn't avoid going out for work. In fact, there are big peaks in the trends for poor people on some weekdays. This directly implies that while rich people were able to continue their jobs from home, poor people do not have the luxury to do the same. A similar observation can be made for the part-time work behavior. Both the groups increase their participation in the part-time work increases during weekdays and decreases during weekends, but until December it is mostly poor people that go out of home for part-time. Only until December, we see both the groups leaving homes for their respective jobs. 



### Sampling Bias

We divided the average number of devices by the population size in each census block group, which was multiplied by a 100 to get the percentage of the population included in the SafeGraph Social Distancing in each census block group. We found in Chicago and Los Angeles the areas with the least poverty have a larger sample percentage than those with more poverty. In New York the sample percentage is smaller for the areas with the highest poverty. 



## Conclusions


New York was most able to reduce their fully at home percentage peaking at 55%, followed by Los Angeles peaking around 50%. Chicago's population shows the least amount of change in their fully at home percentage peaking below 50%. Chicago has the most unified response, both the wealthiest and the poorest census block groups often stay with 5% of each other throughout 2020.

New York shows the most consistent mobility disparity where the poorest areas have a fully at home percentage 5% to 15% below the wealthiest areas for most of 2020. In New York the disparity is also apparent in the working patterns. The areas with the most poverty have full-time and part-time that often rises 5% to 10% above the wealthier areas. The wealthier areas on the other hand had a very stable low value with none of the erratic increase seen with the poor. 

The disparity between the areas with high and low poverty plays out differently in Los Angeles. While the wealthy immediately and drastically change their stay at home behavior in mid-March the poorest areas do not see a substantial increase for a full month and a half. Only in May did the poorer areas begin to change their behavior and stay at home in larger numbers. In Los Angeles we see another surprising event. The areas with high poverty actually increase their at-work behavior throughout most of the year, peaking after a 4% increase in September. The striking increase in mobility above the baseline moves counter to the behavior in Chicago and New York. Also, the increase in mobility moves counter to the wealthy areas in Los Angeles, which reduce their at-work behavior starting in March and lasting through the rest of 2020.

Out of all three cities Chicago had the largest mean percentage of the population included in the sample when compared with Los Angeles and New York.

We found a bias in the percentage of the population sampled in the SafeGraph Social Distancing data relative to the amount of poverty in the census block group. In all three cities higher areas with higher poverty had a lower percentage of the population included in the sample. In Chicago and Los Angeles areas with the least poverty, 0% to 20% of the population in poverty, had the largest percentage of the population of the included. All areas with higher poverty, 20% to 100% of the population in poverty, the percentage of the population included in the sample is lower. In New York the areas with 80% to 100% of the population in poverty have a lower percentage of the population included in the sample than all other areas. We should be careful about the assumptions we make when using data such as cell phone data. It is possible for some groups to be overrepresented and other to be left out all together. 

The SafeGraph data is of high quality. As a result, our comprehensive data quality study found no major issues. The Census Block Group data was unique, all the values were found to fall within the expected range and there were no null values.

The datasets are huge and require a lot of computational time. The data extraction process can be run on a modest machine, but very slowly. Especially the very large SafeGraph Social Distancing dataset, which can take two hours to extract the data for just one city. However, after the extraction process loading data for one year of one city into memory only takes 15 minutes. Once in memory exploration and analysis can be performed quickly. 

Using Google Colab with Google Drive the data can be extracted from the raw data set. However, occasionally the Google API call limit is reached. The issue only occurred when extracting the very large SafeGraph Social Distancing dataset. When the API limit is reached we found that closing all notebooks and waiting 24 hours allowed us to finish running the extraction notebooks. 

The semantics of working with the Census data is not very intuitive. You must understand the FIPS code system, which is the primary method used for encoding the geological entities throughout the United States. The ACS columns naming system is not intuitive. In addition, the column descriptions in the documentation are not always easily understood either. Fortunately, the ACS documentation is very rigorous and there are many resources online to provide additional instruction on how to work with Census data. In addition, once you figure out the semantics and structure of the data there is very little cleaning to do because the quality of data is very good.

We anticipated a spike in the number of individuals staying at home starting in March due to many factors, including the issuing of stay at home orders. Inversely, we expected to see the number of people exhibiting part-time and full-time work behavior decline in March. We visualized the mean percentage values for each of these three attributes for each of the three cities in our study. The line graphs conform to our expectations, which gives us confidence in the data. In comparison, the line graphs of 2019 show gradual change



## Figures

We see an unmistakable increase in the percentage of individuals staying at home in March of 2020. The average for all three city moves spikes up approximatly 20% in all three cities from the begining to the end of March. A drastic change in the number of people leaving home for full-time and part-time work occurs at the same time. 



<table style="background-color:#FFFFFF !important">
<tr>
<th colspan="3">2020 Rolling 10 Day Average</th>
</tr>
<tr style="background-color:#FFFFFF !important">
	<td><img src="media/findings/baseline/homework/ny.png"></td>
  <td><img src="media/findings/baseline/homework/la.png"></td>
  <td><img src="media/findings/baseline/homework/ch.png"></td>
</tr>
<tr >
	<td><b>New York City</b></td>
  <td><b>Los Angeles</b></td>
  <td><b>Chicago</b></td>
</tr>
</table>



<table>
<tr>
<th colspan="3">2020 Rolling 10 Day Average 
  Stay At Home Percentage Deviation from 2019 Mean</th>
</tr>
<tr style="background-color:#FFFFFF">
	<td><img src="media/findings/baseline/stayathome/ny.png"></td>
  <td><img src="media/findings/baseline/stayathome/la.png"></td>
  <td><img src="media/findings/baseline/stayathome/ch.png"></td>
</tr>
  <tr>
	<td><b>New York City</b></td>
  <td><b>Los Angeles</b></td>
  <td><b>Chicago</b></td>
</tr>
</table>



<table>
<tr>
<th colspan="3">Mean percentage staying home grouped by percentage of the population below the poverty line</th>
</tr>
<tr style="background-color:#FFFFFF">
	<td><img src="media/findings/subgroups/phome/ny.png"><img src="media/findings/subgroups/phome/ny-all.png"></td>
  <td><img src="media/findings/subgroups/phome/la.png"><img src="media/findings/subgroups/phome/la-all.png"></td>
  <td><img src="media/findings/subgroups/phome/ch.png"><img src="media/findings/subgroups/phome/ch-all.png"></td>
</tr>
  <tr>
	<td><b>New York City</b></td>
  <td><b>Los Angeles</b></td>
  <td><b>Chicago</b></td>
</tr>
</table>



<table>
<tr>
<th> Comparison of mobility between the wealthiest and poorest groups for 2020-Completely Home Percentage </th>
</tr>
<tr style="background-color:#FFFFFF">
<td>
    <div>
    	<b>Chicago</b>
    </div>
    <div>
     <img src="media/findings/baseline/time/home/ch/ch_time_wealthy_poor_yearly.png" style="display:block; margin-left: auto; margin-right: auto;">
    </div>
 </td>
 </tr>
 <tr style="background-color:#FFFFFF">
<td >
    <div>
    	<b>New York</b>
    </div>
    <div>
     <img src="media/findings/baseline/time/home/ny/ny_time_wealthy_poor_yearly.png" style="display:block; margin-left: auto; margin-right: auto;">
    </div>
 </td>
 </tr>
 <tr style="background-color:#FFFFFF">
<td >
    <div>
    	<b>Los Angeles</b>
    </div>
    <div>
     <img src="media/findings/baseline/time/home/la/la_time_wealthy_poor_yearly.png" style="display:block; margin-left: auto; margin-right: auto;">
    </div>
 </td>
 </tr>
 </table>
 




<table>
<tr>
<th> Comparison of mobility between the wealthiest and poorest groups for 2020 - Full Time Work Percentage</th>
</tr>
<tr style="background-color:#FFFFFF">
<td>
    <div>
    	<b>Chicago</b>
    </div>
    <div>
     <img src="media/findings/fullYearVisualisations/CHfulltimework.png" style="display:block; margin-left: auto; margin-right: auto;">
    </div>
 </td>
 </tr>
 <tr style="background-color:#FFFFFF">
<td >
    <div>
    	<b>New York</b>
    </div>
    <div>
     <img src="media/findings/fullYearVisualisations/NYfulltimework.png" style="display:block; margin-left: auto; margin-right: auto;">
    </div>
 </td>
 </tr>
 <tr style="background-color:#FFFFFF">
<td >
    <div>
    	<b>Los Angeles</b>
    </div>
    <div>
     <img src="media/findings/fullYearVisualisations/LAfulltimework.png" style="display:block; margin-left: auto; margin-right: auto;">
    </div>
 </td>
 </tr>
 </table>

<table>
<tr>
<th> Comparison of mobility between the wealthiest and poorest groups for 2020 - Part Time Work Percentage</th>
</tr>
<tr style="background-color:#FFFFFF">
<td>
    <div>
    	<b>Chicago</b>
    </div>
    <div>
     <img src="media/findings/fullYearVisualisations/CHparttimework.png" style="display:block; margin-left: auto; margin-right: auto;">
    </div>
 </td>
 </tr>
 <tr style="background-color:#FFFFFF">
<td >
    <div>
    	<b>New York</b>
    </div>
    <div>
     <img src="media/findings/fullYearVisualisations/NYparttimework.png" style="display:block; margin-left: auto; margin-right: auto;">
    </div>
 </td>
 </tr>
 <tr style="background-color:#FFFFFF">
<td >
    <div>
    	<b>Los Angeles</b>
    </div>
    <div>
     <img src="media/findings/fullYearVisualisations/LAparttimework.png" style="display:block; margin-left: auto; margin-right: auto;">
    </div>
 </td>
 </tr>
 </table>




#### Chicago

During the month of March we can see the majority of Census Group Blocks go from a below average number of people at home, signified by a dark red, to many more people than average staying at home, signified by a dark blue.



<table>
<tr>
<th colspan="7"><div>
  Chicago Timeline
  </div></th>
</tr>
<tr>
<td colspan="7">First Week of March 2020</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/baseline/time/home/ch/2020-03-01.png"></td>
<td><img src="media/findings/baseline/time/home/ch/2020-03-02.png"></td>
<td><img src="media/findings/baseline/time/home/ch/2020-03-03.png"></td>
<td><img src="media/findings/baseline/time/home/ch/2020-03-04.png"></td>
<td><img src="media/findings/baseline/time/home/ch/2020-03-05.png"></td>
<td><img src="media/findings/baseline/time/home/ch/2020-03-06.png"></td>
<td><img src="media/findings/baseline/time/home/ch/2020-03-07.png"></td>
</tr>
<tr>
<td colspan="7">Second Week of March 2020</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/baseline/time/home/ch/2020-03-08.png"></td>
<td><img src="media/findings/baseline/time/home/ch/2020-03-09.png"></td>
<td><img src="media/findings/baseline/time/home/ch/2020-03-10.png"></td>
<td><img src="media/findings/baseline/time/home/ch/2020-03-11.png"></td>
<td><img src="media/findings/baseline/time/home/ch/2020-03-12.png"></td>
<td><img src="media/findings/baseline/time/home/ch/2020-03-13.png"></td>
<td><img src="media/findings/baseline/time/home/ch/2020-03-14.png"></td>
</tr>
<tr>
<td colspan="7">Third Week of March 2020</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/baseline/time/home/ch/2020-03-15.png"></td>
<td><img src="media/findings/baseline/time/home/ch/2020-03-16.png"></td>
<td><img src="media/findings/baseline/time/home/ch/2020-03-17.png"></td>
<td><img src="media/findings/baseline/time/home/ch/2020-03-18.png"></td>
<td><img src="media/findings/baseline/time/home/ch/2020-03-19.png"></td>
<td><img src="media/findings/baseline/time/home/ch/2020-03-20.png"></td>
<td><img src="media/findings/baseline/time/home/ch/2020-03-21.png"></td>
</tr>
<tr>
<td colspan="7">Fourth Week of March 2020</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/baseline/time/home/ch/2020-03-22.png"></td>
<td><img src="media/findings/baseline/time/home/ch/2020-03-23.png"></td>
<td><img src="media/findings/baseline/time/home/ch/2020-03-24.png"></td>
<td><img src="media/findings/baseline/time/home/ch/2020-03-25.png"></td>
<td><img src="media/findings/baseline/time/home/ch/2020-03-26.png"></td>
<td><img src="media/findings/baseline/time/home/ch/2020-03-27.png"></td>
<td><img src="media/findings/baseline/time/home/ch/2020-03-28.png"></td>
</tr>
<tr>
<td colspan="7" style="background-color:#FFFFFF">
  <div>
    2020 stay at home percentage deviation from the 2019 mean
  </div>
<img src="media/findings/baseline/time/home/ch-key.png">
</td>
</tr>
</table>


<table>
<tr><th colspan='2'>Chicago // Mondays in March, 2020</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/baseline/time/home/ch/2020-03-02.png"></td>
<td><img src="media/findings/baseline/time/home/ch/2020-03-09.png"></td>
</tr>
<tr>
<td><b>2020-03-02</b></td>
<td><b>2020-03-09</b></td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/baseline/time/home/ch/2020-03-16.png"></td>
<td><img src="media/findings/baseline/time/home/ch/2020-03-23.png"></td>
</tr>
<tr>
<td><b>2020-03-16</b></td>
<td><b>2020-03-23</b></td>
</tr>
<tr>
<td colspan="7" style="background-color:#FFFFFF">
  <div>
    2020 stay at home percentage deviation from the 2019 mean
  </div>
<img src="media/findings/baseline/time/home/ch-key.png">
</td>
</tr>
</table>




<table>
<tr>
<th>Chicago Timeline</th>
</tr>
  <tr>
	<td>
    <div>
    <b>Thursday, March 12, 2020</b>
      <ul>
      <li>Governor Pritzker issues order to shutdown all  public events with over 1,000 people in Illinois.</li>
      </ul>
    </div>
  </td>
</tr>
<tr>
	<td>
    <div>
    <b>Tuesday, Mar 17, 2020</b>
      <ul>
      <li>Governor Pritzker order to close Bars and Restaurants to dine in service takes effect.</li>
      <li>Primary election is held despite the onset of the pandemic.</li>
      <li>Mayor Lightfoot announces school closure.</li>
      </ul>
    </div>
  </td>
</tr>
<tr>
	<td>
    <div>
    <b>Friday, Mar 20, 2020</b>
      <ul>
      <li>Governor Pritzker issues stay at home order fro entire state of Illinois.</li>
      </ul>
    </div>
  </td>
</tr>
</table>




<table>
<tr>
<th>Comparison of mobility between the wealthiest and poorest groups for 2020 for specific timelines (Chicago)
</th>
</tr>
<tr>
<td> Completely Home Percentage-March
</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/CH_comp_home_March.png"></img>
</td>
</tr>
<tr>
<td> Completely Home Percentage-April</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/CH_comp_home_April.png"></img></td>
</tr>
<tr>
<td> Completely Home Percentage-June</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/CH_comp_home_June.png"></img></td>
</tr>
<tr>
<td> Completely Home Percentage-September</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/CH_comp_home_September.png"></img></td>
</tr>
<tr>
<td> Full Time Work Percentage-March</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/CH_full_time_March.png"></img></td>
</tr>
<tr>
<td> Full Time Work Percentage-April</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/CH_full_time_April.png"></img></td>
</tr>
<tr>
<td> Full Time Work Percentage-June</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/CH_full_time_June.png"></img></td>
</tr>
<tr>
<td> Full Time Work Percentage-September</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/CH_full_time_September.png"></img></td>
</tr>
<tr>
<td> Part Time Work Percentage-March</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/CH_part_time_March.png"></img></td>
</tr>
<tr>
<td> Part Time Work Percentage-April</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/CH_part_time_April.png"></img></td>
</tr>
<tr>
<td> Part Time Work Percentage-June</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/CH_part_time_June.png"></img></td>
</tr>
<tr>
<td> Part Time Work Percentage-September</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/CH_part_time_September.png"></img></td>
</tr>
</table>

#### New York Metro Area



<table>
<tr>
<th colspan="7">New York City Timeline</th>
</tr>
<tr>
<td colspan="7">First Week of March 2020</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/baseline/time/home/ny/2020-03-01.png"></td>
<td><img src="media/findings/baseline/time/home/ny/2020-03-02.png"></td>
<td><img src="media/findings/baseline/time/home/ny/2020-03-03.png"></td>
<td><img src="media/findings/baseline/time/home/ny/2020-03-04.png"></td>
<td><img src="media/findings/baseline/time/home/ny/2020-03-05.png"></td>
<td><img src="media/findings/baseline/time/home/ny/2020-03-06.png"></td>
<td><img src="media/findings/baseline/time/home/ny/2020-03-07.png"></td>
</tr>
<tr>
<td colspan="7">Second Week of March 2020</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/baseline/time/home/ny/2020-03-08.png"></td>
<td><img src="media/findings/baseline/time/home/ny/2020-03-09.png"></td>
<td><img src="media/findings/baseline/time/home/ny/2020-03-10.png"></td>
<td><img src="media/findings/baseline/time/home/ny/2020-03-11.png"></td>
<td><img src="media/findings/baseline/time/home/ny/2020-03-12.png"></td>
<td><img src="media/findings/baseline/time/home/ny/2020-03-13.png"></td>
<td><img src="media/findings/baseline/time/home/ny/2020-03-14.png"></td>
</tr>
<tr>
<td colspan="7">Third Week of March 2020</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/baseline/time/home/ny/2020-03-15.png"></td>
<td><img src="media/findings/baseline/time/home/ny/2020-03-16.png"></td>
<td><img src="media/findings/baseline/time/home/ny/2020-03-17.png"></td>
<td><img src="media/findings/baseline/time/home/ny/2020-03-18.png"></td>
<td><img src="media/findings/baseline/time/home/ny/2020-03-19.png"></td>
<td><img src="media/findings/baseline/time/home/ny/2020-03-20.png"></td>
<td><img src="media/findings/baseline/time/home/ny/2020-03-21.png"></td>
</tr>
<tr>
<td colspan="7">Fourth Week of March 2020</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/baseline/time/home/ny/2020-03-22.png"></td>
<td><img src="media/findings/baseline/time/home/ny/2020-03-23.png"></td>
<td><img src="media/findings/baseline/time/home/ny/2020-03-24.png"></td>
<td><img src="media/findings/baseline/time/home/ny/2020-03-25.png"></td>
<td><img src="media/findings/baseline/time/home/ny/2020-03-26.png"></td>
<td><img src="media/findings/baseline/time/home/ny/2020-03-27.png"></td>
<td><img src="media/findings/baseline/time/home/ny/2020-03-28.png"></td>
</tr>
<tr>
<td colspan="7" style="background-color:#FFFFFF">
  <div>
    2020 stay at home percentage deviation from the 2019 mean
  </div>
<img src="media/findings/baseline/time/home/ny-key.png">
</td>
</tr>
</table>



<table>
<tr><th colspan='2'>New York City // Mondays in March, 2020</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/baseline/time/home/ny/2020-03-02.png"></td>
<td><img src="media/findings/baseline/time/home/ny/2020-03-09.png"></td>
</tr>
<tr>
<td><b>2020-03-02</b></td>
<td><b>2020-03-09</b></td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/baseline/time/home/ny/2020-03-16.png"></td>
<td><img src="media/findings/baseline/time/home/ny/2020-03-23.png"></td>
</tr>
<tr>
<td><b>2020-03-16</b></td>
<td><b>2020-03-23</b></td>
</tr>
<tr>
<td colspan="7" style="background-color:#FFFFFF">
  <div>
    2020 stay at home percentage deviation from the 2019 mean
  </div>
<img src="media/findings/baseline/time/home/ny-key.png">
</td>
</tr>
</table>



<table>
<tr>
<th >New York Timeline</th>
</tr>
<tr>
	<td>
    <div>
    <b>Friday, March 6, 2020</b>
      <ul>
      <li>Typical pre-shutdown busy weekday with a large percentage of the population not at home.</li>
      </ul>
    </div>
  </td>
  </tr>
  <tr>
	<td>
    <div>
    <b>Friday, March 7, 2020</b>
      <ul>
      <li>Governor Cuomo declares a state of emergency.</li>
      </ul>
    </div>
  </td>
  </tr>
  <tr>
	<td>
    <div>
    <b>Saturday, March 8, 2020</b>
      <ul>
      <li>NYC issues guidlines to avoid densely packed busses, subways, and trains.</li>
      </ul>
    </div>
  </td>
</tr>
<tr>
	<td>
    <div>
    <b>Saturday, March 14, 2020</b>
      <ul>
      <li>First documented two COVID deaths in NYS.</li>
      </ul>
    </div>
  </td>
  </tr>
  <tr>
	<td>
    <div>
    <b>Sunday, March 15, 2020</b>
      <ul>
      <li>CDC recommends no gatherings of 50+ in the United States.</li>
      </ul>
    </div>
  </td>
</tr>
<tr>
	<td>
    <div>
    <b>Monday, March 16, 2020</b>
      <ul>
      <li>NYC public schools are closed.</li>
      </ul>
    </div>
  </td>
  </tr>
  <tr>
	<td>
    <div>
    <b>Tuesday, March 17, 2020</b>
      <ul>
      <li>NYC bars and restaurants are allowed delivery only.</li>
      </ul>
    </div>
  </td>
  </tr>
  <tr>
	<td>
    <div>
    <b>Sunday, March 22, 2020</b>
      <ul>
      <li>NYS pause probram begins. All non-essentail workers are ordered to stay home.</li>
      </ul>
    </div>
  </td>
</tr>
</table>





<table>
<tr>
<th>Comparison of mobility between the wealthiest and poorest groups for 2020 for specific timelines (New York)
</th>
</tr>
<tr>
<td> Completely Home Percentage-March
</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/NY_comp_home_March.png"></img>
</td>
</tr>
<tr>
<td> Completely Home Percentage-April</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/NY_comp_home_April.png"></img></td>
</tr>
<tr>
<td> Completely Home Percentage-July</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/NY_comp_home_July.png"></img></td>
</tr>
<tr>
<td> Completely Home Percentage-October</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/NY_comp_home_October.png"></img></td>
</tr>
<tr>
<td> Full Time Work Percentage-March</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/NY_full_time_March.png"></img></td>
</tr>
<tr>
<td> Full Time Work Percentage-April</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/NY_full_time_April.png"></img></td>
</tr>
<tr>
<td> Full Time Work Percentage-July</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/NY_full_time_July.png"></img></td>
</tr>
<tr>
<td> Full Time Work Percentage-October</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/NY_full_time_October.png"></img></td>
</tr>
<tr>
<td> Part Time Work Percentage-March</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/NY_part_time_March.png"></img></td>
</tr>
<tr>
<td> Part Time Work Percentage-April</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/NY_part_time_April.png"></img></td>
</tr>
<tr>
<td> Part Time Work Percentage-July</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/NY_part_time_July.png"></img></td>
</tr>
<tr>
<td> Part Time Work Percentage-October</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/NY_part_time_October.png"></img></td>
</tr>
</table>

#### Los Angeles

<table>
<tr>
<th colspan="7">Los Angeles Metro Area Timeline</th>
</tr>
<tr>
<td colspan="7">First Week of March 2020</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/baseline/time/home/la/2020-03-01.png"></td>
<td><img src="media/findings/baseline/time/home/la/2020-03-02.png"></td>
<td><img src="media/findings/baseline/time/home/la/2020-03-03.png"></td>
<td><img src="media/findings/baseline/time/home/la/2020-03-04.png"></td>
<td><img src="media/findings/baseline/time/home/la/2020-03-05.png"></td>
<td><img src="media/findings/baseline/time/home/la/2020-03-06.png"></td>
<td><img src="media/findings/baseline/time/home/la/2020-03-07.png"></td>
</tr>
<tr>
<td colspan="7">Second Week of March 2020</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/baseline/time/home/la/2020-03-08.png"></td>
<td><img src="media/findings/baseline/time/home/la/2020-03-09.png"></td>
<td><img src="media/findings/baseline/time/home/la/2020-03-10.png"></td>
<td><img src="media/findings/baseline/time/home/la/2020-03-11.png"></td>
<td><img src="media/findings/baseline/time/home/la/2020-03-12.png"></td>
<td><img src="media/findings/baseline/time/home/la/2020-03-13.png"></td>
<td><img src="media/findings/baseline/time/home/la/2020-03-14.png"></td>
</tr>
<tr>
<td colspan="7">Third Week of March 2020</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/baseline/time/home/la/2020-03-15.png"></td>
<td><img src="media/findings/baseline/time/home/la/2020-03-16.png"></td>
<td><img src="media/findings/baseline/time/home/la/2020-03-17.png"></td>
<td><img src="media/findings/baseline/time/home/la/2020-03-18.png"></td>
<td><img src="media/findings/baseline/time/home/la/2020-03-19.png"></td>
<td><img src="media/findings/baseline/time/home/la/2020-03-20.png"></td>
<td><img src="media/findings/baseline/time/home/la/2020-03-21.png"></td>
</tr>
<tr>
<td colspan="7">Fourth Week of March 2020</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/baseline/time/home/la/2020-03-22.png"></td>
<td><img src="media/findings/baseline/time/home/la/2020-03-23.png"></td>
<td><img src="media/findings/baseline/time/home/la/2020-03-24.png"></td>
<td><img src="media/findings/baseline/time/home/la/2020-03-25.png"></td>
<td><img src="media/findings/baseline/time/home/la/2020-03-26.png"></td>
<td><img src="media/findings/baseline/time/home/la/2020-03-27.png"></td>
<td><img src="media/findings/baseline/time/home/la/2020-03-28.png"></td>
</tr>
<tr>
<td colspan="7" style="background-color:#FFFFFF">
  <div>
    2020 stay at home percentage deviation from the 2019 mean
  </div>
<img src="media/findings/baseline/time/home/la-key.png">
</td>
</tr>
</table>



<table>
<tr><th colspan='2'>Los Angeles Metro Area // Mondays in March, 2020</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/baseline/time/home/la/2020-03-02.png"></td>
<td><img src="media/findings/baseline/time/home/la/2020-03-09.png"></td>
</tr>
<tr>
<td><b>2020-03-02</b></td>
<td><b>2020-03-09</b></td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/baseline/time/home/la/2020-03-16.png"></td>
<td><img src="media/findings/baseline/time/home/la/2020-03-23.png"></td>
</tr>
<tr>
<td><b>2020-03-16</b></td>
<td><b>2020-03-23</b></td>
</tr>
<tr>
<td colspan="7" style="background-color:#FFFFFF">
  <div>
    2020 stay at home percentage deviation from the 2019 mean
  </div>
<img src="media/findings/baseline/time/home/la-key.png">
</td>
</tr>
</table>


<table>
<tr>
<th>Los Angeles Timeline</th>
</tr>
<tr>
	<td>
    <div>
    <b>Wednesday, March 11, 2020</b>
      <ul>
      <li>First person to die of the coronavirus in Los Angeles County is reported.</li>
      </ul>
    </div>
  </td>
</tr>
<tr>
	<td>
    <div>
    <b>Monday, March 16, 2020</b>
      <ul>
      <li>LA county orders the closure of bars, gyms, and entertainment centers. Restaurants are restricted to just take-out or delivery service..</li>
      <li>LAUSD schools close.</li>
      </ul>
    </div>
  </td>
</tr>
<tr>
	<td>
    <div>
    <b>Thursday, March 19, 2020</b>
      <ul>
      <li>California Governor Gavin Newsome issues a statewide stay at home order.</li>
      </ul>
    </div>
  </td>
</tr>
<tr>
	<td>
    <div>
    <b>Friday, March 20, 2020</b>
      <ul>
      <li>Mayor Eric Garcetti issues a safer at home health order stopping non-essential activities outside of residences in response to COVID-19.</li>
      </ul>
    </div>
  </td>
</tr>
<tr>
	<td>
    <div>
    <b>Sunday, March 22, 2020</b>
      <ul>
      <li>President Donald Trump declares a major distaster in California and approves federal funds for the state to fight coronavirus.</li>
      <li>The National Guard deployed in California.</li>
      </ul>
    </div>
  </td>
</tr>
</table>

<table>
<tr>
<th>Comparison of mobility between the wealthiest and poorest groups for 2020 for specific timelines (Los Angeles)
</th>
</tr>
<tr>
<td> Completely Home Percentage-March
</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/LA_comp_home_March.png"></img>
</td>
</tr>
<tr>
<td> Completely Home Percentage-August</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/LA_comp_home_August.png"></img></td>
</tr>
<tr>
<td> Completely Home Percentage-October</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/LA_comp_home_October.png"></img></td>
</tr>
<tr>
<td> Completely Home Percentage-December</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/LA_comp_home_December.png"></img></td>
</tr>
<tr>
<td> Full Time Work Percentage-March</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/LA_full_time_March.png"></img></td>
</tr>
<tr>
<td> Full Time Work Percentage-August</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/LA_full_time_August.png"></img></td>
</tr>
<tr>
<td> Full Time Work Percentage-October</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/LA_full_time_October.png"></img></td>
</tr>
<tr>
<td> Full Time Work Percentage-December</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/LA_full_time_December.png"></img></td>
</tr>
<tr>
<td> Part Time Work Percentage-March</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/LA_part_time_March.png"></img></td>
</tr>
<tr>
<td> Part Time Work Percentage-August</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/LA_part_time_August.png"></img></td>
</tr>
<tr>
<td> Part Time Work Percentage-October</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/LA_part_time_October.png"></img></td>
</tr>
<tr>
<td> Part Time Work Percentage-December</td>
</tr>
<tr style="background-color:#FFFFFF">
<td><img src="media/findings/subgroups/groups/LA_part_time_December.png"></img></td>
</tr>
</table>



### Data Reliability



<table>
  <tr style="background-color:#FFFFFF"><th colspan='3'>Mean percentage of the population included in the sample</th></tr>
  <tr style="background-color:#FFFFFF">
    <td><img src="media/findings/bias/sample/pov/ch.png"></td>
  	<td><img src="media/findings/bias/sample/pov/la.png"></td>
  	<td><img src="media/findings/bias/sample/pov/ny.png"></td>
  </tr>
  <tr style="background-color:#FFFFFF">
    <td><img src="media/findings/bias/sample/pov/ch-all.png"></td>
  	<td><img src="media/findings/bias/sample/pov/la-all.png"></td>
  	<td><img src="media/findings/bias/sample/pov/ny-all.png"></td>
  </tr>
  <tr style="background-color:#FFFFFF">
    <td><b>Chicago</b></td>
  	<td><b>Los Angeles Metro Area</b></td>
  	<td><b>New York Metro Area</b></td>
  </tr>
</table>


## Computational Reproducibility Instructions

### Step 1 // Get the Data

In this repository we provide computational reproducibility for our findings. Detailed instructions on how to secure the same raw input data are provided below in the [Data Sources](#data-sources) and [Data Acquisition](#data-acquisition) sections. We have also prepared a shared private Google Drive to be used by the research team, TAs, and professor Freire. Please reach out to the research team if you do not have the login credentials. While all data used is available for academic researchers to use, the SafeGraph data requires an agreement that we do not make the data public ourselves.  



### Step 2 // Extract the Needed Rows And Columns

The SafeGraph and NYTimes COVID data includes information on counties outside the 3 metropolitan areas of New York, Los Angeles, and Chicago. So the first step is to extract just the rows for our three cities. Also, we needed to select just the relevant subset of columns from each dataset. Detailed instructions on the process are provided in the [Data Extraction](#data-extraction) section below. 

We also provide jupyter notebooks for each step of the extraction process, allowing complete computational reproducibility. The NYTimes COVID data extraction notebook is [here](####new-york-times-covid-19-data-//-extraction-and-cleaning:). The SafeGraph Census data extraction notebooks are [here](####safegraph-census-data-//-extraction-and-cleaning:). The SafeGraph Social Distancing data extraction notebooks are [here](####safegraph-social-distancing-dataset-//-extraction:). 

A word of warning, both Google Colab and Google Drive enforce API call quotas. If you receive an OS IO error you have likely reached your quota on API calls. In our testing we have always found closing all notebooks and letting 24 hours pass was sufficient to reset the Google Drive and Google Colab API quotas. Once the API quotas are reset we have always been able to run the notebooks successfully. Alternatively, you can download the data and code to run on your own machine. All code has been tested on a MacBook Pro with a 2.6 GHz Quad-Core Intel Core i7 with 16 GB of memory.



### Step 3 // Data Cleaning and Quality Verification

Once you have extracted the needed data we are ready to verifiy the data is clean. Fortunately the data sources we are using are of a high quality. So in our case the data cleaning process if more of a data quality verification process. You can read about all the data verification steps we cary out in the [Data Cleaning](##data-cleaning) section below. 

For simplicity sake, the NYTimes COVID cleaning steps are in a single notebook with the extraction steps [here](####new-york-times-covid-19-data-//-extraction-and-cleaning:). Also, for simplicity the SafeGraph Census data cleaning notebooks are also combined with the extraction notebooks [here](####safegraph-census-data-//-extraction-and-cleaning:). 

Finally, you can find all of the SafeGraph Social Distancing notebooks [here](####safegraph-social-distancing-dataset-//-cleaning:). The SafeGraph Social Distancing set cleaning notebooks are not combined with the cleaning notebooks due to the large size of the dataset. So be sure to run the SafeGraph Social Distancing extraction notebooks from the above step 2 first. The SafeGraph Social Distancing Cleaning notebooks are broken up by city and year. 


## Notebooks

There are a series of notebooks used to extract, clean and visualize the data. The notebooks are organized by the dataset, city, and year.  Click on the Colab badge to open the notebook directly in Google Colab. Below each badge is the Github link where you can download the notebook file. The notebooks need to be run in the order listed here. Each notebook depends on the files output by many of the previous notebooks. 

#### New York Times COVID-19 Data // Extraction and Cleaning:
  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20and%20Clean%20Times%20COVID-19%20Data.ipynb) [Extract and Clean Times COVID-19 Data.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20and%20Clean%20Times%20COVID-19%20Data.ipynb) 
#### SafeGraph Census Data // Extraction and Cleaning:
  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20and%20Clean%20Chicago%20Census%20Data.ipynb) [Extract and Clean Chicago Census Data.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20and%20Clean%20Chicago%20Census%20Data.ipynb) 
  
  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20and%20Clean%20LA%20Census%20Data.ipynb) [Extract and Clean LA Census Data.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20and%20Clean%20LA%20Census%20Data.ipynb) 
  
  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20and%20Clean%20New%20York%20Census%20Data.ipynb) [Extract and Clean New York Census Data.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20and%20Clean%20New%20York%20Census%20Data.ipynb)  
#### SafeGraph Social Distancing Dataset // Extraction (Using Pandas):
  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20Chicago%20from%20Social%20Distancing.ipynb) [Extract Chicago from Social Distancing.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20Chicago%20from%20Social%20Distancing.ipynb) 
  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20LA%20from%20Social%20Distancing.ipynb) [Extract LA from Social Distancing.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20LA%20from%20Social%20Distancing.ipynb) 
  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20New%20York%20from%20Social%20Distancing.ipynb) [Extract New York from Social Distancing.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20New%20York%20from%20Social%20Distancing.ipynb) 
#### SafeGraph Social Distancing Dataset // Extraction (Using Spark):
  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20Chicago%20from%20Social%20Distancing%20Spark.ipynb) [Extract Chicago from Social Distancing Spark.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20Chicago%20from%20Social%20Distancing%20Spark.ipynb) 
  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20LA%20from%20Social%20Distancing%20Spark.ipynb) [Extract LA from Social Distancing Spark.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20LA%20from%20Social%20Distancing%20Spark.ipynb) 
* [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20New%20York%20from%20Social%20Distancing%20Spark.ipynb) [Extract New York from Social Distancing Spark.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20New%20York%20from%20Social%20Distancing%20Spark.ipynb) 

#### SafeGraph Social Distancing Dataset // Cleaning:
  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Clean%20CH%202019%20Social%20Distancing%20Dataset.ipynb) [Clean CH 2019 Social Distancing Dataset.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Clean%20CH%202019%20Social%20Distancing%20Dataset.ipynb) 
  
  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Clean%20CH%202020%20Social%20Distancing%20Dataset.ipynb) [Clean CH 2020 Social Distancing Dataset.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Clean%20CH%202020%20Social%20Distancing%20Dataset.ipynb) 
  
  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Clean%20LA%202019%20Social%20Distancing%20Dataset.ipynb) [Clean LA 2019 Social Distancing Dataset.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Clean%20LA%202019%20Social%20Distancing%20Dataset.ipynb)  
  
  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Clean%20LA%202020%20Social%20Distancing%20Dataset.ipynb) [Clean LA 2020 Social Distancing Dataset.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Clean%20LA%202020%20Social%20Distancing%20Dataset.ipynb) 
  
  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Clean%20NY%202019%20Social%20Distancing%20Dataset.ipynb) [Clean NY 2019 Social Distancing Dataset.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Clean%20NY%202019%20Social%20Distancing%20Dataset.ipynb) 
  
  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Clean%20NY%202020%20Social%20Distancing%20Dataset.ipynb) [Clean NY 2020 Social Distancing Dataset.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Clean%20NY%202020%20Social%20Distancing%20Dataset.ipynb) 

#### SafeGraph Social Distancing Dataset // Analysis:

  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20CH%20Population%20Density.ipynb) [Analysis CH Population Density.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20CH%20Population%20Density.ipynb) 

  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20LA%20Population%20Density.ipynb) [Analysis LA Population Density.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20LA%20Population%20Density.ipynb) 

  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20NY%20Population%20Density.ipynb) [Analysis NY Population Density.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20NY%20Population%20Density.ipynb) 


  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20CH%20Get%202019%20Social%20Distancing%20Stats.ipynb) [Analysis CH Get 2019 Social Distancing Stats.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20CH%20Get%202019%20Social%20Distancing%20Stats.ipynb) 

  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20LA%20Get%202019%20Social%20Distancing%20Stats.ipynb) [Analysis LA Get 2019 Social Distancing Stats.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20LA%20Get%202019%20Social%20Distancing%20Stats.ipynb) 

  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20NY%20Get%202019%20Social%20Distancing%20Stats.ipynb) [Analysis NY Get 2019 Social Distancing Stats.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20NY%20Get%202019%20Social%20Distancing%20Stats.ipynb) 

  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20CH%20Compare%202019%20with%202020%20Social%20Distancing%20Dataset.ipynb) [Analysis CH Compare 2019 with 2020 Social Distancing Dataset.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20CH%20Compare%202019%20with%202020%20Social%20Distancing%20Dataset.ipynb) 

  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20NY%20Compare%202019%20with%202020%20Social%20Distancing%20Dataset.ipynb) [Analysis NY Compare 2019 with 2020 Social Distancing Dataset.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20NY%20Compare%202019%20with%202020%20Social%20Distancing%20Dataset.ipynb) 

  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20LA%20Compare%202019%20with%202020%20Social%20Distancing%20Dataset.ipynb) [Analysis LA Compare 2019 with 2020 Social Distancing Dataset.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20LA%20Compare%202019%20with%202020%20Social%20Distancing%20Dataset.ipynb) 

  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20CH%20poverty%20and%20mobility.ipynb) [Analysis CH poverty and mobility.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20CH%20poverty%20and%20mobility.ipynb) 

  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20LA%20poverty%20and%20mobility.ipynb) [Analysis LA poverty and mobility.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20LA%20poverty%20and%20mobility.ipynb) 

  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20NY%20poverty%20and%20mobility.ipynb) [Analysis NY poverty and mobility.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20NY%20poverty%20and%20mobility.ipynb) 
  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/colab/notebooks/temporal-analysis/completely_home/analyse_CH_mobility_poverty_2020.ipynb) [ Analyse CH Compare Completely Home Percentage For Wealthiest And Poorest.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Analyse%20CH%20Compare%20Completely%20Home%20Percentage%20For%20Wealthiest%20And%20Poorest.ipynb) 
  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Analyse%20CH%20Compare%20Full%20Time%20Work%20Percentage%20For%20Wealthiest%20And%20Poorest.ipynb
) [ Analyse CH Compare Full Time Work Percentage For Wealthiest And Poorest.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Analyse%20CH%20Compare%20Full%20Time%20Work%20Percentage%20For%20Wealthiest%20And%20Poorest.ipynb) 
* [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Analyse%20CH%20Compare%20Full%20Time%20Work%20Percentage%20For%20Wealthiest%20And%20Poorest.ipynb) [ Analyse CH Compare Part Time Work Percentage For Wealthiest And Poorest.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Analyse%20CH%20Compare%20Part%20Time%20Work%20Percentage%20For%20Wealthiest%20And%20Poorest.ipynb) 
* [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Analyse%20LA%20Compare%20Completely%20Home%20Percentage%20For%20Wealthiest%20And%20Poorest.ipynb) [ Analyse LA Compare Completely Home Percentage For Wealthiest And Poorest.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Analyse%20LA%20Compare%20Completely%20Home%20Percentage%20For%20Wealthiest%20And%20Poorest.ipynb) 
* [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Analyse%20LA%20Compare%20Full%20Time%20Work%20Percentage%20For%20Wealthiest%20And%20Poorest.ipynb) [ Analyse LA Compare Full Time Work Percentage For Wealthiest And Poorest.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Analyse%20LA%20Compare%20Full%20Time%20Work%20Percentage%20For%20Wealthiest%20And%20Poorest.ipynb) 
* [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Analyse%20LA%20Compare%20Part%20Time%20Work%20Percentage%20For%20Wealthiest%20And%20Poorest.ipynb) [ Analyse LA Compare Part Time Work Percentage For Wealthiest And Poorest.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Analyse%20LA%20Compare%20Part%20Time%20Work%20Percentage%20For%20Wealthiest%20And%20Poorest.ipynb) 
* [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Analyse%20NY%20Compare%20Completely%20Home%20Percentage%20For%20Wealthiest%20And%20Poorest.ipynb
) [ Analyse NY Compare Completely Home Percentage For Wealthiest And Poorest.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20CH%20Compare%202019%20with%202020%20Social%20Distancing%20Dataset.ipynb) 

* [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Analyse%20NY%20Compare%20Full%20Time%20Work%20Percentage%20For%20Wealthiest%20And%20Poorest.ipynb) [ Analyse NY Compare Full Time Work Percentage For Wealthiest And Poorest.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Analyse%20NY%20Compare%20Full%20Time%20Work%20Percentage%20For%20Wealthiest%20And%20Poorest.ipynb) 
*  [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Analyse%20NY%20Compare%20Part%20Time%20Work%20Percentage%20For%20Wealthiest%20And%20Poorest.ipynb
) [ Analyse NY Compare Part Time Work Percentage For Wealthiest And Poorest.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Analyse%20NY%20Compare%20Part%20Time%20Work%20Percentage%20For%20Wealthiest%20And%20Poorest.ipynb) 
*  [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20CH%20Sampling%20Bias.ipynb
) [Analysis CH Sampling Bias.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20CH%20Sampling%20Bias.ipynb) 
*  [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20LA%20Sampling%20Bias.ipynb
) [Analysis LA Sampling Bias.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20LA%20Sampling%20Bias.ipynb) 
*  [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20NY%20Sampling%20Bias.ipynb
) [Analysis NY Sampling Bias.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Analysis%20NY%20Sampling%20Bias.ipynb) 










## Data Sources



We propose to use the SafeGraph COVID-19 Response Social Distancing Metrics[4], The SafeGraph Demographic American Survey Census Data[3], and The New York Times COVID-19 Data. [5] We have verified all three datasets are available to researchers, secured access to, and downloaded the datasets.

The SafeGraph COVID-19 Response Social Distancing Metrics [4] schema can be viewed online at https://docs.safegraph.com/docs. The dataset is organized by Census Block and includes mobility statistics generated from cell phone data such as median distance travel from home, completely at-home device count, full-time work behavior, and many more mobility aggregate statistics.  

The SafeGraph Demographic American Survey Census [3] schema can be viewed online at https://docs.safegraph.com/docs/open-census-data. The dataset is organized by Census Block and contains demographic information, including statistics about race, household income, and poverty. 

The New York Times COVID-19 Data [5] can be accessed online at https://github.com/nytimes/covid-19-data. The dataset contains reported daily COVID cases and deaths organized at the Country, State, and county levels. 



## Data Acquisition



### New York Times COVID-19 Data

**Description:** The New York Times COVID-19 Data can be accessed online at https://github.com/nytimes/covid-19-data. The dataset contains reported daily COVID cases and deaths organized at the Country, State, and county levels. 

**Data Source:** https://github.com/nytimes/covid-19-data

**Data Schema:** https://github.com/nytimes/covid-19-data

The New York Times COVID-19 data can easily be downloaded directly from the Github repository at https://github.com/nytimes/covid-19-data. We are using the us-counties.csv file for county level daily case and death counts. The CSV file was about 46 MB, a manageable size. 



### SafeGraph Social Distancing Metrics

**Description:** Due to the COVID-19 pandemic, people are currently engaging in social distancing. In order to understand what is actually occurring at a census block group level, SafeGraph is offering a temporary Social Distancing Metrics product. The SafeGraph COVID-19 Response Social Distancing Metrics schema can be viewed online at https://docs.safegraph.com/docs. The dataset is organized by Census Block and includes mobility statistics generated from cell phone data such as median distance travel from home, completely at-home device count, full-time work behavior, and many more mobility aggregate statistics.

**Social Distancing Metrics Data Source:** https://www.safegraph.com/covid-19-data-consortium 

**Social Distancing Metrics Data Schema:** https://docs.safegraph.com/docs  

**Includes:** COVID-19 Response Social Distancing MetricsDates: January 1, 2019, to present

**Attributes:** 

* Number of devices 
* Median distance travelled from home
* Completely home device count
* Median home-dwelling time
* Part-time work behavior
* Full-time work behavior
* Destinations (POI visited)
* [many more...](https://docs.safegraph.com/docs )

The SafeGraph Social Distancing Metrics file size was 81 GB at the time of our download. The file includes daily aggregate data for each CBG for all of 2019, 2020, and the beginning of 2021. 

The SafeGraph Census Block Group Data was 10 GB. The file includes the American Community Survey (2016) 5-year estimate on the Census Block Group level. 

**Steps to Download the Data:**

- **Step 1:** Create an account at https://www.safegraph.com/covid-19-data-consortium. Those with academic NYU email address can register for free.
- **Step 2:** Follow the instructions and sign the legal document received in the email mentioning we should not release the data to the public and use it only for research/project purposes. 
- **Step 3:** Open the links provided for the various datasets mentioned above including the Social Distancing Metrics and Census Block Group Data.
- **Step 4:** Download and Install AWS CLI using this link:	https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html
- **Step 5:** Click the “Reveal Access Key” button present on the SafeGraph data screen. 
- **Step 6:** Complete the setup displayed on the screen after revealing the access key.
- **Step 7:** Go back to the dataset page and select the menu option “CLI”.
- **Step 8:** Run the command with the local directory to complete the downloading process.



### SafeGraph Census Block Group Data

**Census Data Source:** https://www.safegraph.com/open-census-dataData 

**Census Data Schema:** https://docs.safegraph.com/docs/open-census-data 

**Census Data Guide:** https://www.safegraph.com/blog/beginners-guide-to-census 

**Description:** The SafeGraph Demographic American Survey Census Data schema can be viewed online at https://docs.safegraph.com/docs/open-census-data. The dataset is organized by Census Block and contains demographic information including statistics about race, household income, and poverty. 

**Includes:** 

* All demographic data from the American Community Survey (2016) 5-year estimate on the Census Block Group level. 
* All census block group boundaries formatted as a GeoJSON file.

**Steps to Download the Data:** Same as the SafeGraph Social Distancing Metrics above. 



## Data Extraction

A FIPS code is a number that uniquely identify a specific geographic area. Each Census Block Group (CBG) is represented by a 12 digit FIPS code. The first two digits of a FIPS code represents the state. The next three digits represent the county. Then, six digits give the Census Tract. Our final digit is the block group. Knowing the FIPS codes for the counties in a given metropolitan area allows us to extract the rows we need and leave the other behind. 



### New York Times COVID-19 Data
* [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20and%20Clean%20Times%20COVID-19%20Data.ipynb) [Extract and Clean Times COVID-19 Data.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20and%20Clean%20Times%20COVID-19%20Data.ipynb) 

The New York Times COVID-19 file us-counties.csv has a FIPS column. After loading the file into a dataframe using Pandas we filter out just the rows with FIPS matching the counties in the metro areas. The result allowed us to get all the relevant row for the counties of Los Angeles and Chicago. 

Filtering for the New York FIPS counties returned no rows. Upon investigation we discovered ironically the New York Times does not maintain county level information for the counties of New York City. They just group all 5 counties of New York City together. Filtering for New York City in the county name column we were able to secure the city level cases and deaths for New York City.  



### SafeGraph Census Block Group Data
* [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20and%20Clean%20Chicago%20Census%20Data.ipynb) [Extract and Clean Chicago Census Data.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20and%20Clean%20Chicago%20Census%20Data.ipynb) 

* [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20and%20Clean%20LA%20Census%20Data.ipynb) [Extract and Clean LA Census Data.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20and%20Clean%20LA%20Census%20Data.ipynb) 

* [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20and%20Clean%20New%20York%20Census%20Data.ipynb) [Extract and Clean New York Census Data.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20and%20Clean%20New%20York%20Census%20Data.ipynb)  

SafeGraph provides a download of the 2016 American Community Survey (ACS) 5-year estimate on the Census Block Group level. We where able to filter out just the counties of the New York, Los Angeles, and Chicago Metro areas from the dataset one CSV file at a time using the FIPS code. We simply filter out CBGs where the first five digits of the CBG FIPS code matches a county from one of our 3 metro areas. Each row includes a Census Block Group that the row attributes describe. There are so many attributes in the ACS that the data is broken up into separate CSV files. The name of the file tells you want attributes are included in the file. Inside each file there is one row for each CBG. 

**We have extracted the following columns for all CBG in the three metro areas:** 

**Column B01003e1:** the total estimate population

**Column B02001e2:** the white only estimated population

**Column C17002e1:** the total population for whom poverty status is determined

**Column C17002e2:** the population for whom the ratio of income to poverty level in the past 12 month is under 0.5 from the population for whom poverty status is determined

**Column C17002e3:** the population for whom the ratio of income to poverty level in the past 12 months is between 0.5 to 0.99 inclusive from the population for whom poverty status is determined

To better make comparisons between CBGs we calculated the white only and poverty percentages for each CBG from the given population values. The CBG white only percentage is calculated using the standard formula ![eq](https://latex.codecogs.com/svg.latex?%5Cfrac%7Bw%7D%7Bt%7D%5Ccdot%20100) where ![eq](https://latex.codecogs.com/svg.latex?w) is the white only population and ![eq](https://latex.codecogs.com/svg.latex?t) is the total population. The CBG percentage in poverty is calculated by ![eq](https://latex.codecogs.com/svg.latex?%5Cfrac%7Ba&plus;b%7D%7Bd%7D%20%5Ccdot%20100) where ![eq](https://latex.codecogs.com/svg.latex?%28a&plus;b%29) is the total population with income below the poverty level and ![eq](https://latex.codecogs.com/svg.latex?d) is the total population for whom the poverty status is determined.


### SafeGraph Social Distancing Metrics
  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20Chicago%20from%20Social%20Distancing.ipynb) [Extract Chicago from Social Distancing.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20Chicago%20from%20Social%20Distancing.ipynb) 
  
  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20LA%20from%20Social%20Distancing.ipynb) [Extract LA from Social Distancing.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20LA%20from%20Social%20Distancing.ipynb) 
  
  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20New%20York%20from%20Social%20Distancing.ipynb) [Extract New York from Social Distancing.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20New%20York%20from%20Social%20Distancing.ipynb) 

  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20Chicago%20from%20Social%20Distancing%20Spark.ipynb) [Extract Chicago from Social Distancing Spark.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20Chicago%20from%20Social%20Distancing%20Spark.ipynb) 

  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20LA%20from%20Social%20Distancing%20Spark.ipynb) [Extract LA from Social Distancing Spark.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20LA%20from%20Social%20Distancing%20Spark.ipynb) 

* [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20New%20York%20from%20Social%20Distancing%20Spark.ipynb) [Extract New York from Social Distancing Spark.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20New%20York%20from%20Social%20Distancing%20Spark.ipynb) 

The SafeGraph Social Distancing Metrics data is downloaded from AWS S3 storage to a local directory. The file structure provides the labels for the many separate gzip csv files. The folder structure pattern is: **YYYY/MM/DD.gz**. For instance, we have 12 folders representing each month i.e. from 01 to 12 in the “2019” folder, and in each of the folders a zipped file representing each day of the month were present. This was massive data that took us a significant amount of time to download.

There is one file for each day of 2019 and 2020. There are also daily files for the first few months of 2021. The data set is still being updated every day with about a 1 week lag time between when data is captured and when it is added to the data set. 

We looped through all the files in the data set reading them into memory and keeping just the CBG rows from the 3 metro areas using the FIPS code column. For convenience once selected we save the filtered rows for each day to a csv file. Our new files follow a different format. The name of the file gives the year, month, and date by using the format **YYY-MM-DD-social-distancing.csv** and are all stored in a single directory for the entire year. For analysis we just read any needed daily data into memory by looping through the new filtered data files. 

In addition to filtering the metro area rows, we have calculated several critical percentage values: the percentage of devices exhibiting part-time work behavior, percentage of devices exhibiting full-time work behavior, and percentage of devices exhibiting completely home status. Each of these percentages was taken using ![eq](https://latex.codecogs.com/svg.latex?%5Cfrac%7Bb%7D%7Bd%7D%20%5Ccdot%20100) where ![eq](https://latex.codecogs.com/svg.latex?b) is the population exhibiting the behavior in the CBG and ![eq](https://latex.codecogs.com/svg.latex?d) is the total number of devices in the CBG.

Finally, for each of these three percentages we have also calculated the normalized value by using ![eq](https://latex.codecogs.com/svg.latex?%5Cfrac%7Bv-%5Cmu%7D%7B%5Csigma%7D) where ![eq](https://latex.codecogs.com/svg.latex?v) is the value to normalize, ![eq](https://latex.codecogs.com/svg.latex?%5Cmu) is the mean, and ![eq](https://latex.codecogs.com/svg.latex?%5Csigma) is the standard deviation.

## Data Cleaning



### New York Times COVID-19 Data
  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20and%20Clean%20Times%20COVID-19%20Data.ipynb) [Extract and Clean Times COVID-19 Data.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20and%20Clean%20Times%20COVID-19%20Data.ipynb) 

**In order to clean the data we have used Python, Pandas, and OpenRefine to take the following steps:**

* Verify the dates fall between January 24th, 2020 and March 18th, 2021 using Pandas min and max function.
* We have verified the extracted rows only include the desired rows from the 3 metro areas using Pandas.
* We have verified all unique date and CBG combos have only one row by comparing the total number of rows to the number of unique combos. We found the count matches for all extracted data.
* Verify the cases and deaths are integer values as expected using the Pandas min and max function. 
* We have verified there are no empty, Null or NaN values in the extracted data we are using. 



### SafeGraph Census Block Group Data
  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20and%20Clean%20Chicago%20Census%20Data.ipynb) [Extract and Clean Chicago Census Data.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20and%20Clean%20Chicago%20Census%20Data.ipynb) 
  
  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20and%20Clean%20LA%20Census%20Data.ipynb) [Extract and Clean LA Census Data.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20and%20Clean%20LA%20Census%20Data.ipynb) 
  
  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20and%20Clean%20New%20York%20Census%20Data.ipynb) [Extract and Clean New York Census Data.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Extract%20and%20Clean%20New%20York%20Census%20Data.ipynb)  

**In order to clean the ACS data we have used Python, Pandas, and OpenRefine to take the following steps:**

* We have checked that each CBG is unique and is not duplicated.
* We have checked to make sure all percentages fall within the valid range from zero to a hundred using the Pandas min and max function.
* We have produced histograms for each attribute to verify the shape of the data and range of values are valid. 
* We have visualized the CBG values on maps to give an intuition into the contents of the data and look for outliers.
* Using Pandas `.isna` function we verified there are no empty, NaN, or Null entries in any of the Social Distancing CSV files.



<table>
<tr>
<th colspan="3">Census Block Group Population Density</th>
</tr>
<tr style="background-color:#FFFFFF">
	<td><img src="media/findings/baseline/density/ny.png"></td>
  <td><img src="media/findings/baseline/density/la.png"></td>
  <td><img src="media/findings/baseline/density/ch.png"></td>
</tr>
  <tr>
	<td><b>New York City</b></td>
  <td><b>Los Angeles</b></td>
  <td><b>Chicago</b></td>
</tr>
</table>




#### Chicago Metropolitan Area Demographic Data

![Figures-chicago](https://github.com/chouhandiksha/bigdataproject/raw/main/media/dem/Figures-chicago.png)

#### Los Angeles Metropolitan Area Demographic Data

![Figures-LA](https://github.com/chouhandiksha/bigdataproject/raw/main/media/dem/Figures-LA.png)

#### New York Metropolitan Area Demographic Data

![Figures-NY](https://github.com/chouhandiksha/bigdataproject/raw/main/media/dem/Figures-NY.png)


### SafeGraph Social Distancing Metrics
  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Clean%20CH%202019%20Social%20Distancing%20Dataset.ipynb) [Clean CH 2019 Social Distancing Dataset.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Clean%20CH%202019%20Social%20Distancing%20Dataset.ipynb) 
  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Clean%20CH%202020%20Social%20Distancing%20Dataset.ipynb) [Clean CH 2020 Social Distancing Dataset.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Clean%20CH%202020%20Social%20Distancing%20Dataset.ipynb) 
  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Clean%20LA%202019%20Social%20Distancing%20Dataset.ipynb) [Clean LA 2019 Social Distancing Dataset.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Clean%20LA%202019%20Social%20Distancing%20Dataset.ipynb)  
  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Clean%20LA%202020%20Social%20Distancing%20Dataset.ipynb) [Clean LA 2020 Social Distancing Dataset.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Clean%20LA%202020%20Social%20Distancing%20Dataset.ipynb) 
  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Clean%20NY%202019%20Social%20Distancing%20Dataset.ipynb) [Clean NY 2019 Social Distancing Dataset.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Clean%20NY%202019%20Social%20Distancing%20Dataset.ipynb) 
  * [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chouhandiksha/bigdataproject/blob/main/notebooks/Clean%20NY%202020%20Social%20Distancing%20Dataset.ipynb) [Clean NY 2020 Social Distancing Dataset.ipynb](https://github.com/chouhandiksha/bigdataproject/blob/main/notebooks/Clean%20NY%202020%20Social%20Distancing%20Dataset.ipynb) 

**In order to clean Social Distancing data we have used Python, Pandas, and OpenRefine to take the following steps:**

* OpenRefine we have checked for duplicate CBG on a subset of the hundreds of csv files. We found no duplicates in any files we checked.
* Using Pandas we checked the minimum and maximum date values to ensure all the dates fall within the expected time frame. We found no values outside the expected time frame for all Social Distancing CSV files.
* Using the Pandas max and min function we checked that all the percentage values fall within the expected range for all percentage columns. We found no values outside the expected range for all Social Distancing CSV files. 
* Using the Pandas max and min function we checked that all integer data types fall within the expected range, which includes no negative values. We found no values outside the expected range for all Social Distancing CSV files.
* Using Pandas `.isna` function we verified there are no empty, NaN, or Null entries in any of the Social Distancing CSV files.
* For each city we visualized the mean daily and mean monthly values for all three percentage values **percentage\_completely\_home**, **percentage\_part\_time\_work**, and **percentage\_full\_time\_work** in both 2019 and 2020. All three cities show an increase in completely home individuals during 2020. There is also a visible decrease in part-time and full-time work behaviour in 2020. Given the documented decrease in mobility during 2020 these are the trends we expect to see. 



#### Chicago Metropolitan Area Social Distancing

![ch-monthly-2019](https://github.com/chouhandiksha/bigdataproject/raw/main/media/social-dist/ch-monthly-2019.png)

![ch-monthly-2020](https://github.com/chouhandiksha/bigdataproject/raw/main/media/social-dist/ch-monthly-2020.png)



#### Los Angeles Metropolitan Area Social Distancing

![la-monthly-2019](https://github.com/chouhandiksha/bigdataproject/raw/main/media/social-dist/la-monthly-2019.png)

![la-monthly-2020](https://github.com/chouhandiksha/bigdataproject/raw/main/media/social-dist/la-monthly-2020.png)



#### New York Metropolitan Area Social Distancing

![ny-monthly-2019](https://github.com/chouhandiksha/bigdataproject/raw/main/media/social-dist/ny-monthly-2019.png)

![ny-monthly-2020](https://github.com/chouhandiksha/bigdataproject/raw/main/media/social-dist/ny-monthly-2020.png)



## Citations and Bibliographies


Chang2021
[1] Serina Chang, Emma Pierson, Pang Wei Koh, Jaline Gerardin, Beth Redbird, David
Grusky, and Jure Leskovec. 2021. Mobility network models of COVID-19 explain
inequities and inform reopening. Nature 589, 7840 (01 Jan 2021), 82–87. https://doi.org/10.1038/s41586-020-2923-3

jung_manley_shrestha_2021
[2] Juergen Jung, James Manley, and Vinish Shrestha. 2021. Coronavirus infections
and deaths by poverty status: The effects of social distancing. Journal of Economic
Behavior & Organization 182 (2021), 311–330. https://doi.org/10.1016/j.jebo.2020.12.019

safegraph_acs
[3] SafeGraph. 2016. Census Block Group Data. https://docs.safegraph.com/docs/open-census-data (All data from 2016 American Community Survey by Census
Block Group).

safegraph_social
[4] SafeGraph. 2021. Social Distancing Metrics. https://docs.safegraph.com/docs/social-distancing-metrics

nyt_covid_19
[5] The New York Times. 2021. Coronavirus (COVID-19) Data in the United States.
https://github.com/nytimes/covid-19-data

nytimees_stayathome_richpoor
[6] Denise Lu Jennifer Valentino-DeVries and Gabriel J.X. Dance. 2020. Location Data Says It All: Staying at Home During Coronavirus Is a Luxury. [https://www.nytimes.com/interactive/2020/04/03/us/coronavirus-stay-home-rich-poor.html](https://www.nytimes.com/interactive/2020/04/03/us/coronavirus-stay-home-rich-poor.html)

ny_timeline_events
[7] Alexandra Kerr. 2021. A Historical Timeline of COVID-19 in New York City. https://www.investopedia.com/historical-timeline-of-covid-19-in-new-york-city-5071986

income_inequality_threatens
[8] Bijan Kimiagar and Jack Mullan. 2020. Opinion: NYC’s Growing Income Inequal-
ity Threatens Pandemic Recovery. https://citylimits.org/2020/10/06/opinion-nycs-growing-income-inequality-threatens-pandemic-recovery/

contrast_poverty_cities
[9] Robert G. Mogull. 2011. A Contrast of U.S. Metropolitan Demographic Poverty: Chicago, Los Angeles, and New York. https://www.hindawi.com/journals/ijpr/2011/860684

Reeves_RV_Rothwell_J_2020
[10] RichardV.ReevesandJonathanRothwell.2020.ClassandCOVID:HowtheLess
Affluent face Double Risks. https://www.brookings.edu/blog/up-front/2020/03/27/class-and-covid-how-the-less-affluent-face-double-risks

chicago_timeline_outbreak
[11] TRIBUNE STAFF WITH NEWS SERVICES. 2020. 6 months of COVID-19: Time-
line of the outbreak and how politics, sports, entertainment and the economy changed. https://www.chicagotribune.com/coronavirus/ct-viz-coronavirus-timeline-20200507-uvrzs32nljabrpn6vkzq7m2fpq-story.html






