# Power Outages in the Continental United States (January 2000 - June 2016)

Mehul Verma, Terran Chow

---

## Introduction

The data that we will be examining throughout the remainder of the entire project has to do with the major power outage data in the continental U.S. from January 2000 to July 2016. We chose this dataset because we initially proposed a hypothesis that power outages affect a lot of disproportionately placed individuals in highly dense and concentrated urban epicenters throughout the continental United States, so we wanted to examine whether this actually held true with the data provided to us, or whether rural areas may have more power outages because they have less land mass, and therefore less of an urban population % in their respective states. We believe readers should care about this dataset and the question that we proposed because the common man is affected by electricity usage, as it's a necessity for humans to be able to go about their daily personal and work lives. The long term goals of this project can also be extensively considered, as electricity consumption patterns directly influence both local economies and environmental sustainability. This makes it essential for us to understand how different sectors, such as residential, commercial, and industrial, impact overall energy demand. By analyzing the data on power outages and electricity usage, even non-data scientists can identify simple trends, improve infrastructure resilience in their respective communities, and promote more efficient energy policies to benefit communities at large. This dataset has 1540 rows and 57 columns. The data that we will be examining throughout the remainder of the entire project has to do with the major power outage data in the continental U.S. from January 2000 to July 2016. We chose this dataset because we initially proposed a hypothesis that power outages affect a lot of disproportionately placed individuals in highly dense and concentrated urban epicenters throughout the continental United States, so we wanted to examine whether this actually held true with the data provided to us, or whether rural areas may have more power outages because they have less land mass, and therefore less of an urban population % in their respective states. We believe readers should care about this dataset and the question that we proposed because the common man is affected by electricity usage, as it's a necessity for humans to be able to go about their daily personal and work lives. The long term goals of this project can also be extensively considered, as electricity consumption patterns directly influence both local economies and environmental sustainability. This makes it essential for us to understand how different sectors, such as residential, commercial, and industrial, impact overall energy demand. By analyzing the data on power outages and electricity usage, even non-data scientists can identify simple trends, improve infrastructure resilience in their respective communities, and promote more efficient energy policies to benefit communities at large. This dataset has a dimensionality of 1540 rows and 57 columns. Finally, the relevant columns that we chose to analyze are under 3 broad sections that are REGIONAL ECONOMIC CHARACTERISTICS, LAND-USE CHARACTERISTICS, and ELECTRICITY CONSUMPTION INFO. The subgroups of these broad columns include:

REC: Regional economic characteristics, with attributes:

- PI.UTIL.OFUSA: This column represents the percentage of the total U.S. population using electricity in a given state, providing insights into the extent of electricity reliance in different regions.
- PC.REALGSP.STATE: This indicates the percentage of the state’s Gross State Product (GSP) derived from the real estate and utilities sector, highlighting the economic importance of electricity consumption in the state.

RLUC: Regional economic land use characteristics, with attributes:

- POPPCT_URBAN: This column provides the percentage of the population living in urban areas, reflecting the level of urbanization and its potential impact on electricity demand.
- POPDEN_URBAN: The population density in urban areas, which can help identify high-density zones with potentially higher electricity needs.
- POPDEN_RURAL: The population density in rural areas, which can be compared with urban densities to understand regional differences in electricity consumption patterns.
- AREAPCT_URBAN: This represents the percentage of a state’s area that is urbanized, which can affect infrastructure and energy demand.
  
ECI: Electricity consumption info, with attributes:

- RES: Residential electricity consumption, with attributes:
    - .PERCEN: The percentage of total electricity consumption attributed to residential use in the state.
    - .CUST.PCT: The percentage of customers in the state that are residential consumers.
- COM: Commercial electricity consumption, with attributes:
    - .PERCEN: The percentage of total electricity consumption attributed to commercial use in the state.
    - .CUST.PCT: The percentage of customers in the state that are commercial consumers.
- IND: Industrial electricity consumption, with attributes:
    - .PERCEN: The percentage of total electricity consumption attributed to industrial use in the state.
    - .CUST.PCT: The percentage of customers in the state that are industrial consumers.

---

## Data Cleaning and Exploratory Data Analysis

There wasn't much cleaning involved with our data due to the fact that it was already presented to us in a readable and tidy format, but there were still missing components and other items that we had to deal with before making any analyses on our data. In the data cleaning process, we started by removing the first row, which contained unit labels as a subset of unwanted metadata rather than actual data that we were interested in. This was done by selecting all rows from index 1 onward utilizing the code snippet (data[1:]). Next, we eliminated any columns that contained only missing (NaN) values across all rows. This step, accomplished with the code snippet (dropna(axis=1, how='all')), ensured that only relevant and non-empty columns were retained, reducing the possibility of including uninformative or incomplete columns in our analysis. Finally, we reset the index of the cleaned DataFrame using the code snippet (reset_index(drop=True)) to ensure a sequential index, which helps maintain consistency and avoid any index-related issues that could arise from dropping rows or columns. These data cleaning steps were crucial for ensuring that the dataset was ready for analysis. Removing the units row eliminated potential confusion in interpreting the values, while dropping columns with excessive NaN values reduced noise in the data. By resetting the index, we ensured that the remaining rows are properly aligned, preventing any potential indexing errors during subsequent analysis. Overall, these cleaning steps helped to improve the accuracy and reliability of our analyses that were performed later on, ensuring that insights drawn from the data are based on valid and complete information.

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

# NMAR Analysis

Upon analyzing the dataset, we believe that the column "Demand.Loss.MW" exhibits characteristics consistent with being NMAR (Not Missing At Random). This column represents the amount of peak demand lost during an outage event, which is likely an estimate. If accurate data is unavailable or if the estimated loss is too high, it is plausible that missing values in this column arise from the uncertainty or unreliability of the estimation, rather than from random sampling. In such cases, the absence of data might be intentional, as we would prefer not to provide potentially misleading or imprecise values.

Similarly, "Cause.CATEGORY.DETAIL" and "Customers.AFFECTED" could also be NMAR. If a detailed cause for the outage is not readily available or the number of affected customers is uncertain, missing values may result from the desire to avoid reporting inaccurate or incomplete information. In these cases, the data is not missing randomly but due to external factors such as a lack of precise knowledge at the time of data collection.

To better understand the missingness and determine if these variables can be considered MAR (Missing At Random), additional contextual data could help clarify the reasons behind the missingness. For instance, investigating whether missing values in these columns are more frequent during specific types of events (e.g., large-scale natural disasters vs. localized outages) could provide further insight.

# Missingness Dependency
In our missingness exploration, we performed permutation tests to examine whether missingness in specific columns could be classified as MAR (Missing At Random) or MCAR (Missing Completely At Random). We focused on the column "CAUSE.CATEGORY.DETAIL", which has a significant proportion of missing data, and compared it against other variables with high missingness, such as "OUTAGE.DURATION", "DEMAND.LOSS.MW", and "CUSTOMERS.AFFECTED". The goal was to assess whether the missing data in CAUSE.CATEGORY.DETAIL can be explained by other variables, thus qualifying it as MAR.

The permutation test results are as follows:

- Outage Duration:

The p-value for the permutation test comparing missingness in CAUSE.CATEGORY.DETAIL to OUTAGE.DURATION is 0.080. This is above our chosen significance level of 0.05, meaning that we cannot conclude that missing data in CAUSE.CATEGORY.DETAIL is MAR with respect to OUTAGE.DURATION.

- Demand Loss (MW):

Similarly, the p-value for CAUSE.CATEGORY.DETAIL and DEMAND.LOSS.MW is also 0.080, which is not statistically significant at the 0.05 level. Thus, we cannot classify missing data in CAUSE.CATEGORY.DETAIL as MAR with respect to DEMAND.LOSS.MW either.

- Customers Affected:

The permutation test comparing CAUSE.CATEGORY.DETAIL to CUSTOMERS.AFFECTED yields a p-value of 0.39, which is even higher, indicating that there is no significant relationship between missing data in CAUSE.CATEGORY.DETAIL and CUSTOMERS.AFFECTED.

- Total Sale (Total Electricity Consumption):
  
However, when we compare the missingness in CAUSE.CATEGORY.DETAIL to TOTAL.SALE (Total electricity consumption in the state), the p-value is 0.00, which is statistically significant at the 0.05 level. This indicates that missingness in CAUSE.CATEGORY.DETAIL is MAR with respect to TOTAL.SALE. The pattern we observe is that when CAUSE.CATEGORY.DETAIL is missing, there is a much higher total electricity consumption in the state compared to when it is not missing. This suggests that states with low electricity consumption (low TOTAL.SALE) might experience smaller outages, for which detailed causes are less likely to be recorded. On the other hand, states with high electricity consumption have larger outages and more comprehensive reporting standards, increasing the likelihood of detailed cause records.

Based on these results, we conclude that CAUSE.CATEGORY.DETAIL is MAR with respect to TOTAL.SALE, but not with respect to OUTAGE.DURATION, DEMAND.LOSS.MW, or CUSTOMERS.AFFECTED. This insight suggests that missingness in CAUSE.CATEGORY.DETAIL is likely influenced by external factors such as the size of the state’s electricity consumption, with larger states more likely to report detailed outage causes.

---

## Hypothesis Testing

Our null and alternative hypotheses are defined as follows:

- Null Hypothesis (H₀): People who pay above-average residential electricity prices experience the same outage duration as those who pay below-average electricity prices.
- Alternative Hypothesis (H₁): People who pay above-average residential electricity prices experience shorter outage durations than those who pay below-average electricity prices.

- Test Statistic:

We will use the difference in means as our test statistic. The difference in means will help us assess whether there is a significant difference in the outage durations between the two groups (above-average residential electricity prices vs. below-average residential electricity prices).

- Significance Level:

The significance level (α) is set to 0.05. This is a commonly used threshold to determine whether we can reject the null hypothesis.

- P-value:

The resulting p-value is 0.559. This p-value is greater than our chosen significance level of 0.05, which means we fail to reject the null hypothesis. There is no significant evidence to suggest that people who pay above-average residential electricity prices have shorter outage durations compared to those who pay below-average electricity prices.

- Conclusion:

Based on the results of the permutation test and the p-value of 0.559, we conclude that there is little to no evidence to support the claim that people who pay above-average residential electricity prices experience shorter outage durations than those who pay below-average prices. While the average outage duration is higher for people who pay above-average electricity prices, this difference is not statistically significant, and we cannot draw a causal relationship between the two variables.

- Justification:

The choice of using the difference in means as the test statistic is appropriate for comparing the central tendency of outage durations between two independent groups (above vs. below average electricity prices). We used the permutation test as a test which is robust to assumptions about the underlying distribution of the data, especially when the data might not follow a normal distribution. The permutation test also accounts for the possibility that the observed difference in means could arise by chance, providing a more reliable measure of statistical significance.