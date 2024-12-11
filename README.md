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