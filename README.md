# California-Infectious-Diseases-Analysis
## Overview
This project aims to analyse and generate insight into the infectious disease cases reported by California residents between 2001-2022. To achieve this, it uses the Python libraries of pandas, numpy, matplotlib and seaborn. Additionally, to have a clear object, five questions were defined beforehand:

### Project Questions:
* What are the most common diseases in terms of rate (between 2001-2022)?
* What is the trend of mean rates of diseases by year?
* What are the trends of each disease (top 10) over the years?
* How is the distribution of incidence of diseases (top 10) by gender?
* What is the distribution of diseases by county (top 20) and year?

## Dataset & Methods

---
### Dataset
The dataset was taken from the official website of [Data.gov](https://catalog.data.gov/dataset/infectious-diseases-by-disease-county-year-and-sex-6e856). It was published and is still regularly maintained by the California Department of Public Health. As of this writing, the specific version of data (last updated on 30 March 2024) is used. The general structure of the dataset is as follows:
* **Disease**: The name of the disease
* **County**: The county where a given resident was residing at during the report of a disease
* **Year**: The year when a specific disease was reported
* **Sex**: The sex of the patient (Male, Female)
* **Cases**: The number of patients reported to have a certain disease
* **Population**: The numbers of population which are given both for each sex and as total in terms of county and the respective year.
* **Rate**: The rate of disease per 100,000 population.
* **Lower_95__CI**: The lower bound of 95% confidence interval
* **Upper_95__CI**: The upper bound of 95% confidence interval
---
---
### Methods & Steps
Below are the general steps taken for the data analysis. A few example codes are given to have an idea of what has been done. To look at the full codes, you can refer to the [notebook](https://github.com/azizbarank/California-Infectious-Diseases-Analysis/blob/main/california_disease_analysis.ipynb).
1. Importing the necessary packages:

```python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
%matplotlib inline
```

2. First quick glance at the dataset:
```python
df.head()
df.info()
df.value_counts()
```

3. Apply filtering:
   * Change the data type of the "Rate" column from object to float.
     ##### 1. Drop the unnecessary cells containing "SC".
     ##### 2. Convert the character of "*" to ''
     ##### 3. Convert the character "-" to 0
     ##### 4. Change the data type of the column from object to float for further calculation

      ```python
      filt = df['Rate'] == 'SC'
      df.drop(index=df[filt].index, inplace=True)
      df['Rate'] = df['Rate'].str.replace('*', '', regex=False)
      df['Rate'] = df['Rate'].str.replace('-', '0', regex=False)
      df['Rate'] = df['Rate'].astype('float64')
      ```
 4. Gaining insights:
    ##### 1. The most common diseases (*making a list*)
    ##### 2. The mean rates of diseases by year (*scatter plot*)
    ##### 3. The trends of each disease over the years (*line plot*)
    ##### 4. The distribution of incidence of diseases by gender (*bar plot*)
    ##### 5. The distribution of diseases by county and year (*heatmap*)
      ```python
      df.groupby('Disease')['Rate'].mean().sort_values(ascending = False)
      df_Rate_Year = df.groupby('Year')['Rate'].mean().reset_index()
      sns.set(style="whitegrid")
      plt.figure(figsize=(10, 6))
      .
      .
      .
      ```
---
## Results (Project Questions)
1. What are the most common diseases in terms of rate (between 2001-2022)?

|       Diseases     | Rate |
| -----------------  | -------- |
|Campylobacteriosis  |19.150163|
|Coccidioidomycosis  |12.000524|
|Salmonellosis	     |11.467313|
|Giardiasis	         |5.665743|
|Shigellosis	       |3.452487|
|Shiga toxin-producing E. coli (STEC) without HUS	|2.265992|
|Cryptosporidiosis	 |1.167573|
|Lyme Disease	|0.503697|
|Legionellosis	|0.400315|
|Vibrio Infection (non-Cholera)	|0.380777|

The top 3 diseases (i.e., Campylobacteriosis, Coccidioidomycosis, Salmonellosis) seem to be occuring much more frequently than the others, with more than 10 mean rate in general.

2. What is the trend of mean rates of diseases by year?
![Trends of Mean Rates of Diseases](https://github.com/azizbarank/California-Infectious-Diseases-Analysis/blob/main/images/mean_rates_year.png)

As can be seen from the plot, between the years 2002-2014, the mean rate tends to be not changing a lot. However, after 2015 until 2019, there seems to be a surge, which is followed by a brief decrease until 2021. Even though I searched for the possible causes for the surge between 2015-2021, I couldn@t find a reliable resource. It is known that there were some specific cases of pandemie in the U.S. between these years (e.g., Zika virus). Therefore, it might be that diseases like that might have increases the mean rate for that specific time period. The other interesting thing is the decrease after 2019, which was the beginning year of COVID-19. For this, it might be the case that since a lot of health care facilities were already busy with dealing with COVID-19, the other diseases were simply neglected and not reported that much.

3. What are the trends of top 10 disease over the years?
![Trends of Top 10 Diseases over the years](https://github.com/azizbarank/California-Infectious-Diseases-Analysis/blob/main/images/disease_trend.png)

In a similar way to the mean rates of all diseases above, what remarkable is that nearly all of the top 10 diseases tend to surge from 2015 onwards.

4. How is the distribution of incidence of diseases by gender?
![Distribution of incidence of diseases by gender](https://github.com/azizbarank/California-Infectious-Diseases-Analysis/blob/main/images/disease_gender.png)

In general, males tend to be affected more then females by most diseases, except; Salmonellosis and Shiga toxin-producing E. coli (STEC) without HUS. There have been a couple of studies done by National Institute of Health (NIH). For instance, when it comes to Salmonellosis, Reller et al. (2007)[^1] found out that the relative burden of salmonellosis in women has increased and that one of the reasons for this has something to do woth product consumption. In other words, what they found out was that food, especially fruit and vegetable consumption is oen of the reasons for the occurence of this disease and since women tend to consume these more than men, this disease tends to occur more frequently among them.

For the STEC, Tack et al. (2021)[^2] found out that more women are affected than men when it comes to foodborne (especially vegetable row crops and fruits), environmental and other unknown transmission modes.

5. What is the distribution of diseases by county and year?
![Distribution of Diseases by County and Years](https://github.com/azizbarank/California-Infectious-Diseases-Analysis/blob/main/images/disease_county.png)
As can be seen from the heatmap above, the top 3 counties with the highest rates of diseases are Kern, Kings and San Francisco.


## References:
[^1]: Reller, M. E., Tauxe, R. V., Kalish, L. A., & Mølbak, K. (2007). Excess salmonellosis in women in the United States: 1968–2000. *Epidemiology and Infection*, *136*(8), 1109–1117. [https://doi.org/10.1017/s0950268807009594](https://doi.org/10.1017/s0950268807009594)
[^2]: Tack, D. M., Kisselburgh, H. M., Richardson, L. C., Geissler, A., Griffin, P. M., Payne, D. C., & Gleason, B. L. (2021). Shiga Toxin-Producing Escherichia coli Outbreaks in the United States, 2010–2017. *Microorganisms*, *9*(7), 1529. [https://doi.org/10.3390/microorganisms9071529](https://doi.org/10.3390/microorganisms9071529)
