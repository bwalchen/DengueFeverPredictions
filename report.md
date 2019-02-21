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



## ___ Notes: to talk about

Year
Vegetations
Min air


Does San Juans not have data pre 2000s or did Dengue not exist there then

"Aedes aegyptibites primarily during the day. This species is most active for approximately two hours after sunrise and several hours before sunset,but it can bite at night in well lit areas" ([source](https://www.cdc.gov/dengue/resources/30jan2012/aegyptifactsheet.pdf)).

We found that the variable `reanalysis_tdtr_k`, that is daytime (diurnal) temperature range, has the second highest absolute correlation probability (-27%) for total cases of Dengue fever.
