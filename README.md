**Background**

The learning goals were defined in a way to align some aspects related to data science that I would like to develop during the course, and the technical needs of the group project. Setting realistic goals is also among the criteria, considering that the course lasts for only three weeks. The link to the individual plan can be accessed on this link: https://github.com/hudson-passos/DSSE-Individual-Portfolio/blob/main/01.%20Introduction.ipynb.

Initially, the group chose the topic related to air quality, and we would like the study area to be located in Europe, as there is an abundant amount of data and ease of language. In the first researches, we noticed that Poland has very high air pollution levels and this motivated us to seek to better understand the causes and consequences of this case. The project was titled: "Investigating Causes and Impacts of Air Pollution in Poland" and we divided it into three objectives: <br>
1. "Analyze the contribution of sources of Nitrogen Oxides (NOx) to the air pollution in Poland in 2019". 
2. "Investigate the relationship between traffic and emissions using machine learning and predict the emission in 2023".
3. "Investigate the relationship of annual average concentration of PM 2.5 and rate of death caused by respiratory diseases".
   
After the definition of the objectives, we assigned the group members responsible for developing these tasks: the first objective was assigned to Qin Xu (Olive) and I; the second was under Dong Liang; and the third was with Pamungkas Intam and Sabrina Ramadwiriani.

The needs of the first objective were well aligned with what I had defined in my learning goals:

1. Geospatial analysis in GeoPandas: We did all the geospatial analyses using Pandas and GeoPandas. This learning goal was challenging, especially in terms of generating subplots of multiple GeoPandas objects. However, it was surprising how similar GeoPandas is to Pandas and this made this tool much more familiar than I imagined. Fortunately, all the operations and analyses that I would do with some of the GIS applications, with which I am more familiar, I was able to perform with Pandas/GeoPandas.

2. Combining information: We were able to combine data from different sources into integrated dataframes. This task was less challenging than the previous one, but more laborious. I still can't make these codes cleaner and more compact. I can do repeated operations with the application of "functions", but I still have difficulty using "classes".

3. Github: We were able to create our repository on Github and make it our main means of sharing codes. Despite the fact that there are other more specific applications of github that we still do not know (e.g. "version control"), this experience was crucial to introduce us to this resource once and for all. Our Github repository can be found at: https://github.com/hudson-passos/DSSE.

<br>

**Data sources:**

- Administrative boundaries: 
  - Source: GIS.Box 
  - Product: boundaries from Poland, voivodeships (provinces), counties and municipalities 
  - Type: shapefile 
  - Spatial distribution: 
  - Link: https://gis-support.pl/baza-wiedzy-2/dane-do-pobrania/granice-administracyjne/
  
- Air pollution: 
  - Source: Inspekcja Ochrony Środowiska 
  - Product: emissions of NOx air pollution (kg) 
  - Type: csv 
  - Spatial distribution: points (air quality measuremente stations) 
  - Link: https://powietrze.gios.gov.pl/pjp/archives 

- Traffic: 
  - Source: Statistics Poland 
  - Product: emissions of NOx air pollution (tonnes) 
  - Type: csv 
  - Spatial distribution: provinces 
  - Link: https://transtat.stat.gov.pl/ 

- Industry: 
  - Source: European Environment Agency  
  - Product: industrial emissions of NOx (kg) 
  - Type: csv 
  - Spatial distribution: points 
  - Link: https://www.eea.europa.eu/en/datahub/datahubitem-view/9405f714-8015-4b5b-a63c-280b82861b3d


The spreadsheet with a detailed description of all the datasets used in the project can be accessed at the link: https://github.com/hudson-passos/DSSE/raw/main/Report%20and%20Presentation/Data%20Availability.xlsx
<br>
<br>

**Methodology**

The methodology consists of extracting information related to pollution, emissions of pollutants from industrial and traffic sectors, and inserting them into the polygons of their respective provinces. The idea is using this information to identify the contribution to the air pollution through data analysis and, additionally, applying the feature importance analysis to compare the results.

To achieve all of this, we had to complete a series of steps:

- Search and download the datasets, and understand the data and how the information is organized in it;
- Clean the data with information without coordinates, not a number and inconsistent values;
- Prepare the data by applying filters to obtain subsets with part of the specific data that we wanted to use (e.g., country Poland, pollutant NOx, etc.);
- Combine the data into an integrated dataframe, where first we relate the dataframe of air quality measurement stations, with their coordinates, and the dataframe with the emissions and the name of the measurement stations. Then, we concatenate the data of industrial emissions, traffic, and air pollution;
- Prepare the maps and bar charts for data analysis;
- Prepare the integrated dataframe for machine learning:
  - Standardization
  - Split into training and test data
  - Run the grid search to get the best hyperparameters
  - Run the XGBoost model
  - Evaluate the model (cross-validation)
  - Features importance analysis
<br>

**Details about the implementation**

The entire implementation can be accessed in full through the link: 
https://github.com/hudson-passos/DSSE-Individual-Portfolio/blob/main/Objective%201_Analyze_the_contribution_of_sources_of_Nitrogen_Oxides_(NOx)_to_the_air_pollution_in_Poland_in_2019.ipynb

<br>

**Results**

The energy sector emerged as the primary source of NOx emissions in the generated graphs, especially in the provinces of Slaskie, Lodzkie, and Mazowieckie. In second place, emissions from motor vehicle traffic (urban buses, lorries, and road tractors) are present in all provinces, with the highest level in the province of Mazowieckie, which contains the city of Warsaw, the capital and largest city of Poland. In third place comes the mining industry, which, despite emitting little in comparison to the first two polluting agents, has a relatively extensive presence in the Polish territory. The rest have scattered, localized, and low contributions. 

One factor that stands out is the absence of NOx emissions from intensive livestock. A quick search of the data showed that in 2019, the fractions recorded for the entire livestock and aquaculture industry were 80% NH3, 10% CH4, 4% N2O, and 4% PM10. Therefore, the vast majority of nitrogen gas emissions are expelled in the form of ammonia.

The feature importance analysis produced a slightly different outcome. The NOx emissions from the energy sector is the feature that contributes most to the final prediction of NOx air pollution (score 32). In second place of importance comes the chemical industry, with 20 score. In third, mineral industry, with 10 score. The remaining features do not offer significant contribution to the final prediction.

It is important to note that not necessarily the factors that are responsible for large emissions of pollutants are the ones that contribute the most to the prediction. In this case, there was a coincidence with the energy sector, which is indeed a major polluter. However, the same cannot be said of the chemical industry, which seems to contribute precisely because it has an inverse correlation. Where there is a presence of enormous emissions, there is an absence of the chemical industry in the data; and the lower the total emissions of the provinces, the presence (although modest) of emissions from this industry is noted.

<br>

**Conclusions on the results**

The results show that the most appropriate methodology for obtaining insights into the sources with the highest contribution to air pollution was the direct data analysis through visualization features in graphs and maps.

Our initial conception that feature importance analysis could identify the most important sources for air pollution did not prove to be an appropriate methodology for this purpose. The difference is that feature importance is focused on identifying the best features exclusively for air pollution prediction, without causal relationship, only in terms of correlation. The chemical industry, for example, contributes very little to air pollution in Poland, and yet it was the second feature with the highest importance for prediction, because where there are regions with huge NOx emissions, this industry is absent. This pattern was noticed during training and became crucial for the model to correctly predict NOx air pollution concentration.

We can draw this conclusion with regard to both methods, because we used the same pollutants, with the same units of measurement for the explanatory variables. However, perhaps feature importance would be more useful if we were using explanatory data that cannot be directly compared, such as the number of vehicles per year in a given province.

<br>

**Conclusions on the accomplishment of the goals**

As for the learning goals, I think they were all met successfully. It was also a great satisfaction to be able to work on areas of knowledge that we were interested in. For example, I will use spatial analysis with GeoPandas more often throughout the course and my career. Similarly, I found that Github, which I always thought had a somewhat unintuitive interface, is an excellent tool for sharing code and even text.












