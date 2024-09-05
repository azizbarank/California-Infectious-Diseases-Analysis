# California-Infectious-Diseases-Analysis
## Overview
This project aims to analyse and generate insight into the infectious disease cases reported by California residents between 2001-2022. To achieve this, it uses the Python libraries of pandas, numpy, matplotlib and seaborn. Additionally, to have a clear object, five questions were defined beforehand:

### Project Questions:
* What are the most common diseases in terms of rate (between 2001-2022)?
* What is the trend of mean rates of diseases by year?
* What are the trends of each disease over the years?
* How is the distribution of incidence of diseases by gender?
* What is the distribution of diseases by county and year?

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
Below are the general steps taken for the data analysis. A few example codes are given to have an idea of what has been done. To look at the full codes, you can refer to the [notebook](aaa).
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
2. What is the trend of mean rates of diseases by year?
3. What are the trends of top 10 disease over the years?
4. How is the distribution of incidence of diseases by gender?
5. What is the distribution of diseases by county and year?
