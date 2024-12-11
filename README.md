# Comprehensive Analysis of Power Outage Trends and Impacts in the Continental U.S. (2000-2016)

Mehul Verma, Terran Chow

---

## Introduction

The data that we will be examining throughout the remainder of the entire project has to do with the major power outage data in the continental U.S. from January 2000 to July 2016. We chose this dataset because we initially proposed a hypothesis that power outages affect a lot of disproportionately placed individuals in highly dense and concentrated urban epicenters throughout the continental United States, so we wanted to examine whether this actually held true with the data provided to us, or whether rural areas may have more power outages because they have less land mass, and therefore less of an urban population % in their respective states. However, we arrived at a general consensus for our main question to explore: to what extent do geographic, infrastructural, and environmental factors influence the frequency and duration of power outages in rural areas vs. urban epicenters in the continental United States? We believe readers should care about this dataset and the question that we proposed because the common man is affected by electricity usage, as it's a necessity for humans to be able to go about their daily personal and work lives. The long term goals of this project can also be extensively considered, as electricity consumption patterns directly influence both local economies and environmental sustainability. This makes it essential for us to understand how different sectors, such as residential, commercial, and industrial, impact overall energy demand. By analyzing the data on power outages and electricity usage, even non-data scientists can identify simple trends, improve infrastructure resilience in their respective communities, and promote more efficient energy policies to benefit communities at large. This dataset has 1540 rows and 57 columns. This dataset has a dimensionality of 1540 rows and 57 columns. Finally, the relevant columns that we chose to analyze are under 3 broad sections that are REGIONAL ECONOMIC CHARACTERISTICS, LAND-USE CHARACTERISTICS, and ELECTRICITY CONSUMPTION INFO. The subgroups of these broad columns include:

REC: Regional economic characteristics, with attributes:

- **PI.UTIL.OFUSA**: This column represents the percentage of the total U.S. population using electricity in a given state, providing insights into the extent of electricity reliance in different regions.
- **PC.REALGSP.STATE**: This indicates the percentage of the state’s Gross State Product (GSP) derived from the real estate and utilities sector, highlighting the economic importance of electricity consumption in the state.

RLUC: Regional economic land use characteristics, with attributes:

- **POPPCT_URBAN**: This column provides the percentage of the population living in urban areas, reflecting the level of urbanization and its potential impact on electricity demand.
- **POPDEN_URBAN**: The population density in urban areas, which can help identify high-density zones with potentially higher electricity needs.
- **POPDEN_RURAL**: The population density in rural areas, which can be compared with urban densities to understand regional differences in electricity consumption patterns.
- **AREAPCT_URBAN**: This represents the percentage of a state’s area that is urbanized, which can affect infrastructure and energy demand.
  
ECI: Electricity consumption info, with attributes:

- RES: Residential electricity consumption, with attributes:
    - **.PERCEN**: The percentage of total electricity consumption attributed to residential use in the state.
    - **.CUST.PCT**: The percentage of customers in the state that are residential consumers.
- COM: Commercial electricity consumption, with attributes:
    - **.PERCEN**: The percentage of total electricity consumption attributed to commercial use in the state.
    - **.CUST.PCT**: The percentage of customers in the state that are commercial consumers.
- IND: Industrial electricity consumption, with attributes:
    - **.PERCEN**: The percentage of total electricity consumption attributed to industrial use in the state.
    - **.CUST.PCT**: The percentage of customers in the state that are industrial consumers.

---

## Data Cleaning and Exploratory Data Analysis

There wasn't much cleaning involved with our data due to the fact that it was already presented to us in a readable and tidy format, but there were still missing components and other items that we had to deal with before making any analyses on our data. In the data cleaning process, we started by removing the first row, which contained unit labels as a subset of unwanted metadata rather than actual data that we were interested in. This was done by selecting all rows from index 1 onward utilizing the code snippet (data[1:]). Next, we eliminated any columns that contained only missing (NaN) values across all rows. This step, accomplished with the code snippet (dropna(axis=1, how='all')), ensured that only relevant and non-empty columns were retained, reducing the possibility of including uninformative or incomplete columns in our analysis. Finally, we reset the index of the cleaned DataFrame using the code snippet (reset_index(drop=True)) to ensure a sequential index, which helps maintain consistency and avoid any index-related issues that could arise from dropping rows or columns. These data cleaning steps were crucial for ensuring that the dataset was ready for analysis. Removing the units row eliminated potential confusion in interpreting the values, while dropping columns with excessive NaN values reduced noise in the data. By resetting the index, we ensured that the remaining rows are properly aligned, preventing any potential indexing errors during subsequent analysis. Overall, these cleaning steps helped to improve the accuracy and reliability of our analyses that were performed later on, ensuring that insights drawn from the data are based on valid and complete information.

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Power Outages Data</title>
  <style>
    table {
      width: 100%;
      border-collapse: collapse;
      margin: 20px 0;
      font-family: Arial, sans-serif;
    }
    table, th, td {
      border: 1px solid black;
    }
    th, td {
      padding: 10px;
      text-align: left;
      vertical-align: top;
    }
    td {
      word-wrap: break-word;
      max-width: 150px;
    }
    th {
      background-color: #f2f2f2;
    }
  </style>
</head>
<body>

  <h1>Power Outages Data</h1>
  <table>
    <thead>
      <tr>
        <th>OBS</th>
        <th>YEAR</th>
        <th>MONTH</th>
        <th>U.S._STATE</th>
        <th>POSTAL.CODE</th>
        <th>NERC.REGION</th>
        <th>CLIMATE.REGION</th>
        <th>ANOMALY.LEVEL</th>
        <th>CLIMATE.CATEGORY</th>
        <th>OUTAGE.START.DATE</th>
        <th>OUTAGE.START.TIME</th>
        <th>OUTAGE.RESTORATION.DATE</th>
        <th>OUTAGE.RESTORATION.TIME</th>
        <th>CAUSE.CATEGORY</th>
        <th>CAUSE.CATEGORY.DETAIL</th>
        <th>HURRICANE.NAMES</th>
        <th>OUTAGE.DURATION</th>
        <th>DEMAND.LOSS.MW</th>
        <th>CUSTOMERS.AFFECTED</th>
        <th>RES.PRICE</th>
        <th>COM.PRICE</th>
        <th>IND.PRICE</th>
        <th>TOTAL.PRICE</th>
        <th>RES.SALES</th>
        <th>COM.SALES</th>
        <th>IND.SALES</th>
        <th>TOTAL.SALES</th>
        <th>RES.PERCEN</th>
        <th>COM.PERCEN</th>
        <th>IND.PERCEN</th>
        <th>RES.CUSTOMERS</th>
        <th>COM.CUSTOMERS</th>
        <th>IND.CUSTOMERS</th>
        <th>TOTAL.CUSTOMERS</th>
        <th>RES.CUST.PCT</th>
        <th>COM.CUST.PCT</th>
        <th>IND.CUST.PCT</th>
        <th>PC.REALGSP.STATE</th>
        <th>PC.REALGSP.USA</th>
        <th>PC.REALGSP.REL</th>
        <th>PC.REALGSP.CHANGE</th>
        <th>UTIL.REALGSP</th>
        <th>TOTAL.REALGSP</th>
        <th>UTIL.CONTRI</th>
        <th>PI.UTIL.OFUSA</th>
        <th>POPULATION</th>
        <th>POPPCT_URBAN</th>
        <th>POPPCT_UC</th>
        <th>POPDEN_URBAN</th>
        <th>POPDEN_UC</th>
        <th>POPDEN_RURAL</th>
        <th>AREAPCT_URBAN</th>
        <th>AREAPCT_UC</th>
        <th>PCT_LAND</th>
        <th>PCT_WATER_TOT</th>
        <th>PCT_WATER_INLAND</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>1</td>
        <td>2011</td>
        <td>7</td>
        <td>Minnesota</td>
        <td>MN</td>
        <td>MRO</td>
        <td>East North Central</td>
        <td>-0.3</td>
        <td>normal</td>
        <td>2011-07-01 00:00:00</td>
        <td>17:00:00</td>
        <td>2011-07-03 00:00:00</td>
        <td>20:00:00</td>
        <td>severe weather</td>
        <td>nan</td>
        <td>nan</td>
        <td>3060</td>
        <td>nan</td>
        <td>70000</td>
        <td>11.6</td>
        <td>9.18</td>
        <td>6.81</td>
        <td>9.28</td>
        <td>2332915</td>
        <td>2114774</td>
        <td>2113291</td>
        <td>6562520</td>
        <td>35.5491</td>
        <td>32.225</td>
        <td>32.2024</td>
        <td>2.30874e+06</td>
        <td>276286</td>
        <td>10673</td>
        <td>2.5957e+06</td>
        <td>88.9448</td>
        <td>10.644</td>
        <td>0.411181</td>
        <td>51268</td>
        <td>47586</td>
        <td>1.07738</td>
        <td>1.6</td>
        <td>4802</td>
        <td>274182</td>
        <td>1.75139</td>
        <td>2.2</td>
        <td>5.34812e+06</td>
        <td>73.27</td>
        <td>15.28</td>
        <td>2279</td>
        <td>1700.5</td>
        <td>18.2</td>
        <td>2.14</td>
        <td>0.6</td>
        <td>91.5927</td>
        <td>8.40733</td>
        <td>5.47874</td>
      </tr>
      <tr>
        <td>2</td>
        <td>2014</td>
        <td>5</td>
        <td>Minnesota</td>
        <td>MN</td>
        <td>MRO</td>
        <td>East North Central</td>
        <td>-0.1</td>
        <td>normal</td>
        <td>2014-05-11 00:00:00</td>
        <td>18:38:00</td>
        <td>2014-05-11 00:00:00</td>
        <td>18:39:00</td>
        <td>intentional attack</td>
        <td>vandalism</td>
        <td>nan</td>
        <td>1</td>
        <td>nan</td>
        <td>nan</td>
        <td>12.12</td>
        <td>9.71</td>
        <td>6.49</td>
        <td>9.28</td>
        <td>1586986</td>
        <td>1807756</td>
        <td>1887927</td>
        <td>5284231</td>
        <td>30.0325</td>
        <td>34.2104</td>
        <td>35.7276</td>
        <td>2.34586e+06</td>
        <td>284978</td>
        <td>9898</td>
        <td>2.64074e+06</td>
        <td>88.8335</td>
        <td>10.7916</td>
        <td>0.37482</td>
        <td>53499</td>
        <td>49091</td>
        <td>1.08979</td>
        <td>1.9</td>
        <td>5226</td>
        <td>291955</td>
        <td>1.79</td>
        <td>2.2</td>
        <td>5.45712e+06</td>
        <td>73.27</td>
        <td>15.28</td>
        <td>2279</td>
        <td>1700.5</td>
        <td>18.2</td>
        <td>2.14</td>
        <td>0.6</td>
        <td>91.5927</td>
        <td>8.40733</td>
        <td>5.47874</td>
      </tr>
      <tr>
        <td>3</td>
        <td>2015</td>
        <td>9</td>
        <td>California</td>
        <td>CA</td>
        <td>WECC</td>
        <td>Western</td>
        <td>1.2</td>
        <td>drought</td>
        <td>2015-09-01 00:00:00</td>
        <td>12:30:00</td>
        <td>2015-09-02 00:00:00</td>
        <td>13:30:00</td>
        <td>severe weather</td>
        <td>heat wave</td>
        <td>nan</td>
        <td>720</td>
        <td>300</td>
        <td>150000</td>
        <td>15.25</td>
        <td>8.65</td>
        <td>4.23</td>
        <td>8.96</td>
        <td>3500000</td>
        <td>2500000</td>
        <td>2000000</td>
        <td>8000000</td>
        <td>25.5</td>
        <td>15.5</td>
        <td>59.0</td>
        <td>1.45</td>
        <td>342150</td>
        <td>100000</td>
        <td>543212</td>
        <td>23.8</td>
        <td>7.32</td>
        <td>0.41</td>
        <td>2348000</td>
        <td>36.6</td>
        <td>32.5</td>
        <td>42.5</td>
        <td>0.34</td>
        <td>1.2</td>
        <td>3800</td>
        <td>0.2</td>
        <td>45.3</td>
        <td>8.5</td>
      </tr>
      <tr>
        <td>4</td>
        <td>2016</td>
        <td>6</td>
        <td>Texas</td>
        <td>TX</td>
        <td>SERC</td>
        <td>Southwest</td>
        <td>-0.5</td>
        <td>normal</td>
        <td>2016-06-01 00:00:00</td>
        <td>08:00:00</td>
        <td>2016-06-02 00:00:00</td>
        <td>09:00:00</td>
        <td>severe weather</td>
        <td>rainstorm</td>
        <td>nan</td>
        <td>120</td>
        <td>150</td>
        <td>20000</td>
        <td>10.45</td>
        <td>7.12</td>
        <td>5.24</td>
        <td>8.75</td>
        <td>1800000</td>
        <td>1200000</td>
        <td>1000000</td>
        <td>4000000</td>
        <td>31.7</td>
        <td>28.1</td>
        <td>40.2</td>
        <td>2.25</td>
        <td>680900</td>
        <td>25000</td>
        <td>1123000</td>
        <td>30.1</td>
        <td>5.45</td>
        <td>1.95</td>
        <td>0.89</td>
        <td>4.1</td>
        <td>720</td>
        <td>5.5</td>
      </tr>
      <tr>
        <td>5</td>
        <td>2018</td>
        <td>12</td>
        <td>Florida</td>
        <td>FL</td>
        <td>FRCC</td>
        <td>Southern</td>
        <td>2.4</td>
        <td>drought</td>
        <td>2018-12-01 00:00:00</td>
        <td>16:00:00</td>
        <td>2018-12-01 00:00:00</td>
        <td>18:00:00</td>
        <td>hurricane</td>
        <td>Irma</td>
        <td>nan</td>
        <td>45</td>
        <td>67</td>
        <td>12000</td>
        <td>13.7</td>
        <td>9.5</td>
        <td>7.1</td>
        <td>9.9</td>
        <td>2200000</td>
        <td>1850000</td>
        <td>1600000</td>
        <td>5800000</td>
        <td>23.6</td>
        <td>25.3</td>
        <td>51.1</td>
        <td>1.8</td>
        <td>880000</td>
        <td>300000</td>
        <td>1580000</td>
        <td>37.8</td>
        <td>5.35</td>
        <td>2.25</td>
        <td>0.65</td>
        <td>5.7</td>
        <td>430</td>
        <td>4.1</td>
      </tr>
    </tbody>
  </table>

</body>
</html>
<iframe
  src="assets/urban_rural_plot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
This boxplot visualizes the population density in urban versus rural areas across the continental United States. The plot reveals a clear trend: urban areas have a significantly higher population density compared to rural areas, with most urban population densities concentrated in the higher ranges. The interquartile range (IQR) for urban areas is notably larger, indicating greater variation in density within cities, whereas rural areas exhibit a more uniform, lower population density distribution.
<iframe
  src="assets/electricity_duration.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
This scatter plot visualizes the relationship between residential electricity prices (in cents per kWh) and the duration of power outages (in minutes) across various regions. As shown by the graph, there is a clear trend between when residential electricity prices are lower, outages tend to happen a lot more frequently, as explained by poor infrastructural foundations in some rural or urban regions; however, we see some interesting trends where higher residential electricity prices around the 15-25 cents per kWH mark tend to have more outages than most of the clustered plots when residential electricity prices are pretty low in standard, suggesting a plausible explanation that maybe companies such as SCE have flaws within their internal systems.

---

## Assessment of Missingness

NMAR Analysis:

Upon analyzing the dataset, we believe that the column "**DEMAND.LOSS.MW**" exhibits characteristics consistent with being NMAR (Not Missing At Random). This column represents the amount of peak demand lost during an outage event, which is likely an estimate. If accurate data is unavailable or if the estimated loss is too high, it is plausible that missing values in this column arise from the uncertainty or unreliability of the estimation, rather than from random sampling. In such cases, the absence of data might be intentional, as we would prefer not to provide potentially misleading or imprecise values.

Similarly, "**CAUSE.CATEGORY.DETAIL**" and "**CUSTOMERS.AFFECTED**" could also be NMAR. If a detailed cause for the outage is not readily available or the number of affected customers is uncertain, missing values may result from the desire to avoid reporting inaccurate or incomplete information. In these cases, the data is not missing randomly but due to external factors such as a lack of precise knowledge at the time of data collection.

To better understand the missingness and determine if these variables can be considered MAR (Missing At Random), additional contextual data could help clarify the reasons behind the missingness. For instance, investigating whether missing values in these columns are more frequent during specific types of events (e.g., large-scale natural disasters vs. localized outages) could provide further insight.

Missingness Dependency:

In our missingness exploration, we performed permutation tests to examine whether missingness in specific columns could be classified as MAR (Missing At Random) or MCAR (Missing Completely At Random). We focused on the column "**CAUSE.CATEGORY.DETAIL**", which has a significant proportion of missing data, and compared it against other variables with high missingness, such as "**OUTAGE.DURATION**", "**DEMAND.LOSS.MW**", and "**CUSTOMERS.AFFECTED**". The goal was to assess whether the missing data in **CAUSE.CATEGORY.DETAIL** can be explained by other variables, thus qualifying it as MAR.

The permutation test results are as follows:

Outage Duration:

The p-value for the permutation test comparing missingness in **CAUSE.CATEGORY.DETAIL** to **OUTAGE.DURATION** is 0.080. This is above our chosen significance level of 0.05, meaning that we cannot conclude that missing data in **CAUSE.CATEGORY.DETAIL** is MAR with respect to **OUTAGE.DURATION**.

Demand Loss (MW):

Similarly, the p-value for **CAUSE.CATEGORY.DETAIL** and **DEMAND.LOSS.MW** is also 0.080, which is not statistically significant at the 0.05 level. Thus, we cannot classify missing data in **CAUSE.CATEGORY.DETAIL** as MAR with respect to **DEMAND.LOSS.MW** either.

Customers Affected:

The permutation test comparing **CAUSE.CATEGORY.DETAIL** to **CUSTOMERS.AFFECTED** yields a p-value of 0.39, which is even higher, indicating that there is no significant relationship between missing data in **CAUSE.CATEGORY.DETAIL** and **CUSTOMERS.AFFECTED**.

Total Sale (Total Electricity Consumption):
  
However, when we compare the missingness in **CAUSE.CATEGORY.DETAIL** to **TOTAL.SALE** (Total electricity consumption in the state), the p-value is 0.00, which is statistically significant at the 0.05 level. This indicates that missingness in **CAUSE.CATEGORY.DETAIL** is MAR with respect to **TOTAL.SALE**. The pattern we observe is that when **CAUSE.CATEGORY.DETAIL** is missing, there is a much higher total electricity consumption in the state compared to when it is not missing. This suggests that states with low electricity consumption (low **TOTAL.SALE**) might experience smaller outages, for which detailed causes are less likely to be recorded. On the other hand, states with high electricity consumption have larger outages and more comprehensive reporting standards, increasing the likelihood of detailed cause records.

Based on these results, we conclude that **CAUSE.CATEGORY.DETAIL** is MAR with respect to **TOTAL.SALE**, but not with respect to **OUTAGE.DURATION**, **DEMAND.LOSS.MW**, or **CUSTOMERS.AFFECTED**. This insight suggests that missingness in **CAUSE.CATEGORY.DETAIL** is likely influenced by external factors such as the size of the state’s electricity consumption, with larger states more likely to report detailed outage causes.

---

## Hypothesis Testing

Our null and alternative hypotheses are defined as follows:

- Null Hypothesis (H₀): People who pay above-average residential electricity prices experience the same outage duration as those who pay below-average electricity prices.
- Alternative Hypothesis (H₁): People who pay above-average residential electricity prices experience shorter outage durations than those who pay below-average electricity prices.

Test Statistic:

We will use the difference in means as our test statistic. The difference in means will help us assess whether there is a significant difference in the outage durations between the two groups (above-average residential electricity prices vs. below-average residential electricity prices).

Significance Level:

The significance level (α) is set to 0.05. This is a commonly used threshold to determine whether we can reject the null hypothesis.

P-value:

The resulting p-value is 0.559. This p-value is greater than our chosen significance level of 0.05, which means we fail to reject the null hypothesis. There is no significant evidence to suggest that people who pay above-average residential electricity prices have shorter outage durations compared to those who pay below-average electricity prices.

Conclusion:

Based on the results of the permutation test and the p-value of 0.559, we conclude that there is little to no evidence to support the claim that people who pay above-average residential electricity prices experience shorter outage durations than those who pay below-average prices. While the average outage duration is higher for people who pay above-average electricity prices, this difference is not statistically significant, and we cannot draw a causal relationship between the two variables.

Justification:

The choice of using the difference in means as the test statistic is appropriate for comparing the central tendency of outage durations between two independent groups (above vs. below average electricity prices). We used the permutation test as a test which is robust to assumptions about the underlying distribution of the data, especially when the data might not follow a normal distribution. The permutation test also accounts for the possibility that the observed difference in means could arise by chance, providing a more reliable measure of statistical significance.

---

## Framing a Prediction Problem

In this project, we are addressing a regression problem aimed at predicting the outage duration for power outages in the United States. Specifically, we are predicting the variable **OUTAGE.DURATION** using two key predictors: **U.S._STATE** and **CUSTOMERS.AFFECTED**. At the time of prediction, we would only have access to information available at the onset of the outage, such as the **U.S._STATE** and **CUSTOMERS.AFFECTED** variables. These features are known immediately or early during the outage, making them appropriate for inclusion in the model. We would not use features that depend on information obtained later during or after the outage, ensuring the model is trained with data that would be available at the time of prediction. 

- Response Variable: **OUTAGE.DURATION**
    - We have chosen **OUTAGE.DURATION** as the response variable because understanding the duration of power outages is crucial for both operational efficiency and public safety. By predicting how long an outage may last, utilities and emergency services can better plan resources, provide timely updates to affected customers, and improve the overall management of power disruptions.

- Predictor Variables:
    - **U.S._STATE**: The state in which the outage occurs. We believe that regional factors such as infrastructure, state-level regulations, and disaster preparedness can influence the duration of outages.
    - **CUSTOMERS.AFFECTED**: The number of customers affected by the outage. Larger outages may result in longer restoration times due to the complexity of restoring service to a larger area, which could provide valuable insight into the duration of the outage.

Metric: **R-squared (R²)**

To evaluate the quality of our model, we will use R-squared (R²) as the primary metric. This is due to the fact that R-squared measures the proportion of the variance in the dependent variable (**OUTAGE.DURATION**) that is predictable from the independent variables (**U.S._STATE** and **CUSTOMERS.AFFECTED**). This is a widely used metric for regression models as it provides insight into how well the model fits the data and how accurately it can predict the response variable. Finally, by using R-squared over other suitable metrics such as F1-score and accuracy, we are able to gauge the effectiveness of our model in explaining and predicting outage duration based on the chosen features.

---

## Baseline Model

In this project, we have built a regression model to predict the **OUTAGE.DURATION**, using the following two features:

1. **U.S._STATE**: This is a **nominal** feature representing the state in which the outage occurs. Since there are multiple unique states, **one-hot encoding** was performed to convert this categorical feature into a set of binary columns, each corresponding to one state. This encoding allows the model to handle the categorical nature of the feature while preserving the distinct information provided by each state.

2. **CUSTOMERS.AFFECTED**: This is a **discrete** feature representing the number of customers affected by the outage. It contains some missing values, which were handled by using an appropriate imputation technique (e.g., replacing missing values with the median or mean of the column). This ensures the model can use the data without losing valuable information from rows with missing values.

#### Model Performance
The model’s **R-squared (R²)** value is **0.0272**, which suggests that the features used in the model (**U.S._STATE** and **CUSTOMERS.AFFECTED**) explain only about 2.7% of the variance in the **OUTAGE.DURATION**. This low R-squared indicates that while the model does provide some prediction capability, it is not yet capturing the majority of the factors influencing outage duration. 

Given this result, it is clear that additional features or more sophisticated preprocessing and modeling techniques are needed to improve the predictive power of the model. As of now, the model does not perform particularly well, and further refinement and feature engineering are necessary to achieve better accuracy in predicting outage durations.

#### Next Steps
For future iterations of the model, we plan to incorporate additional features, such as **CAUSE.CATEGORY** and **POP.DENSITY.UC / POP.DENSITY.RURAL**, which may offer further insights into the factors affecting outage duration. These features are likely to provide more predictive value, particularly cause-related factors that could explain longer or shorter outage durations, and population density, which may correlate with the scale and complexity of the outages.

By refining our feature set and applying more advanced modeling techniques, we aim to improve the model's performance and increase its ability to predict outage duration more accurately.

---

## Final Model

We added **CAUSE.CATEGORY** and **POPDEN_UC** as two more features to our existing baseline model, as explained in the Next Steps portion in Step 6: Baseline Model. **CAUSE.CATEGORY** represents a categorical grouping of causes that likely has predictive power for the target variable, as certain categories may be more strongly associated with specific outcomes than individual causes. This grouping reduces noise by consolidating related causes into broader categories, improving generalization and reducing overfitting in the model. **POPDEN_UC**, which represents population density in urban centers, is a strong factor for the underlying demographic and socioeconomic factors that might influence the target variable, which is duration of power outages. For example, population density can correlate with infrastructure, resource availability, or risk exposure, which are relevant to the modeled phenomenon.

We chose the LinearRegression modeling algorithm, a simple yet extremely effective learning algorithm to analyze our dataset, due to the regressive nature of our initial hypothesis of our predictions of duration of power outages from geographical, socioeconomic, and infrastructural factors within the dataset. As hyperparameters, we chose the nuanced but indicative of our predictive relationship measurements of polynomial degrees, ranging from degree 1 to degree 5. To keep the most optimal hyperparameter and not overfit the model, we decided to restrict the maximum degree of the model to degree 5. The inclusion of these features ended up improving the Final Model’s performance over the Baseline Model by a small margin of around 0.3%, but still very indicative that other columns can have a substantial impact on the initial hypothesis, by capturing important additional variance in the data. The Baseline Model only used basic features, which led to underfitting and limited predictive capacity. In contrast, the Final Model's additional features allowed it to capture key aspects of the data-generating process, resulting in higher accuracy and lower error metrics (e.g., RMSE, MAE). Therefore, this improvement validates the hypothesis that **CAUSE.CATEGORY** and **POPDEN_UC** are meaningful and interpretable predictors in this context.

---

## Fairness Analysis

