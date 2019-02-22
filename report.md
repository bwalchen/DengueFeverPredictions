## Problem Overview

**Dengue Fever** is also known as breakbone fever and dandy fever It is a single-stranded RNA virus caused by Mosquitoes of the genus Aedes. These mosquitoes are most often found in **urban** areas as they like to harvest in man made products such as tires, flowerpots, and buckets. They were brought into Northern America and Europe by Asian products. It should be noted that they are capable of surviving subfreezing temperatures, allowing them to spread to cooler climates. There are four types of Dengue viruses which results in an acute infectious disease with **symptoms** of a high fever, joint pain, and muscle pain. The first signs of dengue includes fever, headache, joint pain, and rashes.

This disease is spread through the **female mosquito** bite and often occurs in tropical areas. A mosquito becomes infected when it drinks the blood of a person who is already infected with dengue. The mosquito can transmit the virus after one week of being infected. Dengue can’t be spread from person-to-person; however, infected humans can travel and potentially spread dengue to other countries. Other than providing a patient with pain medications and fluid, there is no specific **treatment** for dengue. A dengue vaccine is being developed and one has been approved for use in Mexico and Brazil.

**Goal**: Predict weekly reported dengue fever cases in San Juan, Puerto Rico, and Iquitos Perú based on environmental variables.
The format for the post-analysis submission file is simply the `city, year, weekofyear, total_cases`

**Dengue dataset**: Data collected by U.S. Federal Government agencies
- Centers for Disease Control and Prevention
- DoD Naval Medical Research 
- Armed Forces Health Surveillance Center
- National Oceanic and Atmospheric Administration

**Pertinent variables**:
Dengue fever is known to be related to climate and humidity:
* `station_diur_temp_rng_c` – Diurnal temperature range
* `reanalysis_relative_humidity_percent` – Mean relative humidity

#### Citations
* https://www.drivendata.org/competitions/44/dengai-predicting-disease-spread/ 
* https://www.health.ny.gov/diseases/communicable/dengue_fever/fact_sheet.htm 
* http://www.muxetv.com/2019/01/08/medical-centric-what-is-dengue/



## Data Preparation

We see that lacking values were filled with `NaN`. Initially we considered dropping all rows that contain any nulls. After some consideration we realized that we would be losing a lot of data if we did so. Our strategy will be to make a temporary data frame for each model we use. Each of these will drop rows with nulls **only** if the variable being used for that row is a null.

Added a new variable `new_avg_temp_c` to the data frame that averages both `station_avg_temp_c` and `reanalysis_avg_temp_k`.



## Data Explortation

________________ --------------

## Statistical Modeling

**Chosen Statistical Approach**
We are choosing to use **forward selection** as our statistical approach by using the code provided in [this link](https://planspace.org/20150423-forward_selection_with_statsmodels/) with total Dengue cases as our dependent variable. 


**What is forward selection**
At a high level forward selection is the idea of starting with an empty model and slowly adding on whatever variable will make our model best until a variable make the model worse or until we are out of variables.

In a more detailed explanation,  forward selection is a type of _stepwise regression_ that outputs the best independent variables to use in a model.

It’s construction  begins with a base intercept, we test the potential given independent variables that may be relevant, and add the one that best improves our model. This process is repeated until the variables offered only decreased the r-squared value or until there are no more variables available.


**Why forward selection**
To avoid overfitting, we’ll use forward selection to determine the top variables while allowing us the flexibility of scaling our model past this dataset

Looking at the correlations from our exploratory analysis, we found that multiple variables stood between 0.20 and 0.30 correlation probability in relation to total cases of Dengue. With so many variables at high correlation probabilities we found that forward selection would do a good job of picking up the ones that best support a model. We understand that this method tends to be over fitting. In our situation we would prefer this in comparison to the under fitting backwards selection as we would be basing our aggressive fit on real data. Additionally with the support of our background research we are confident that we could remove variables from the selection output that we believe will negatively impact the mode






## Model Variables

After running the forward selection function with total cases of dengue as the dependent variable, our resulting model looks like:

``` 

total_cases ~ 
week_start_date + station_diur_temp_rng_c + station_avg_temp_c + 
reanalysis_max_air_temp_k + reanalysis_sat_precip_amt_mm + 
reanalysis_precip_amt_kg_per_m2 + reanalysis_specific_humidity_g_per_kg + 
reanalysis_dew_point_temp_k + reanalysis_min_air_temp_k + city + 1 

```


### Variable overview

#### Dependent Variable
**total_cases** is the dependent variable that we are trying to predict based off of the independent, environmental variables.

#### **Date**
As seen in our exploratory visualization on the relationship between the week of the year and the total cases of dengue, the total cases fluctuate depending on the week number and thus, the season. With the idea that mosquitoes prefer warmer weather, changes in the **week_start_date** is directly related to changes in the temperature and how mosquitos behave.

#### **Temperature-related variables**
These variables include:
station_diur_temp_rng_c 
station_avg_temp_c 
reanalysis_max_air_temp_k 
reanalysis_min_air_temp_k 

According to our background research on dengue fever, the disease often occurs in tropical areas where it is warm. As the air temperatures and daytime temperatures increases and mosquitoes become more active, the total_cases will increase as well.

#### **Humidity-related variables**

As described in our background research, mosquitoes tend to live and spawn near water. According to the Museum of Climate Controls ([source](http://www.musecc.com/how-are-temperature-and-relative-humidity-related)), temperature and humidity are closely related. Throughout our data exploration and online research we have found that there is a strong relationship between tropical climates and cases of dengue fever. It is no surprise that humidity variables were returns by the forward selection as the greater the temperature the more moisture the air can hold. Tropical climates tend to have higher temperatures and our data exploration so far has shown that high temperatures throughout the day are related to dengue cases.As the humidity and precipitation increases and mosquitoes become more active, the total_cases will increase as well.

These variables include:
reanalysis_sat_precip_amt_mm 
reanalysis_precip_amt_kg_per_m2 
reanalysis_specific_humidity_g_per_kg 
reanalysis_dew_point_temp_k 

 

#### **Location**
The dataset included two cities  - San Juan, Puerto Rico and Iquitos, Perú. San Juan is surrounded by water and has higher observed temperatures, whereas Iquitos is located relatively more inland. Though Iquitos near a river but with lower observed temperatures. Depending on the geographical location of a **city**, relative to any surrounding bodies of water and temperature, mosquitoes are more likely to thrive in warmer cities near water.


## ___ Notes: to talk about

Year
Vegetations
Min air


Does San Juans not have data pre 2000s or did Dengue not exist there then

"Aedes aegyptibites primarily during the day. This species is most active for approximately two hours after sunrise and several hours before sunset,but it can bite at night in well lit areas" ([source](https://www.cdc.gov/dengue/resources/30jan2012/aegyptifactsheet.pdf)).

We found that the variable `reanalysis_tdtr_k`, that is daytime (diurnal) temperature range, has the second highest absolute correlation probability (-27%) for total cases of Dengue fever.


[Forward selection explained.](https://www.statisticshowto.datasciencecentral.com/forward-selection/)
