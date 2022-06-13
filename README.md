# World COVID-19 Vaccinations ETL_Case_Study

Track COVID-19 vaccinations and manufactures used around the world using extract, transform, and load functionality.

## Contributers

- <strong>Hana Tafesse</strong>
- <strong>Tanisha Cooper</strong>

## Background:

The momentum of the Covid-19 pandemic has tapered. There has been a push for people to get vaccinated prior to returning to high-risk jobs, visiting countries, and vacationing. 

We wanted to understand Covid-19 vaccination around the world. According to each country's population, are people fully vaccinated? Which country has the highest fully vaccinated population per one hundred? What vaccination manufacturers are being used? Here we take a look at an analysis of COVID-19 vaccinations per country and the manufacturers they use.

We collected data from [COVID-19 World Vaccination Progress](https://www.kaggle.com/datasets/gpreda/covid-world-vaccination-progress "COVID-19 World Vaccination Progress") and [COVID-19 Ranking of Vaccinations and Manufactuers Used](https://www.kaggle.com/code/raulalmuzara/covid-19-ranking-of-vaccinations-and-vaccines-used "COVID-19 Ranking of Vaccinations and Manufactuers Used")

We successfully was able to <strong>Extract</strong>, <strong>Transform</strong>, and <strong>Load</strong> our data to pgAdmin using connection. Below, we will provide detail insight on how we uploaded our data to the database to analyze the data. 


## Data Analysis:

<strong>What countries have the most fully COVID-19 vaccinated people? (List Top/Bottom 5 Countries) Help to identify countries that are doing well and are struggling. We can explore and apply tactics we get from the top countries to that of the bottom countries.</strong>

<strong>***Analysis:***</strong> 

Top 5 Countries Most Fully COVID-19 Vaccinated People

1. China
2. India
3. United States
4. Brazil
5. Indonesia

![Top 5 Countries Most Fully COVID-19 Vaccinated People](/Images/top_fullyvacc_df.png)

Bottom 5 Countries Most Fully COVID-19 Vaccinated People

1. Pitcairn
2. Tokelau
3. Niue
4. Falkland Islands
5. Montserrat

![Bottom 5 Countries Most Fully COVID-19 Vaccinated People](/Images/bottom_fullyvacc_df.png)

<strong>In the top/bottom 5 countries with the most fully COVID-19 vaccinated people, what are the manufacturers they use? Reduce cost by ordering commonly used vaccines by manufacturers.</strong>

<strong>***Analysis:***</strong> 
> *[Top 5 Country Manufacturers](https://github.com/TanishaCooper/ETL_Case_Study/blob/None/Images/top_manufactures_df.png "Top 5 Country Manufacturers")*
>>
> *[Bottom 5 Country Manufacturers](https://github.com/TanishaCooper/ETL_Case_Study/blob/None/Images/bottom_manufactures_df.png "Bottom 5 Country Manufacturers")*


<strong>Based on population (fully vaccinated per 100), what percent of people are fully vaccinated in Top/Bottom 5 Countries? Help to debunk that countries with larger populations have a higher chance to have “more” vaccinated people than countries with a smaller population.</strong>

<strong>***Analysis:***</strong>

Pitcairn, though listed in bottom 5 of countries with people_fully_vaccinated, has the most people vaccinated according to population at 100%.

Niue falls within the bottom 5 of countries with people_full_vaccinated and comes in at second with the most people vaccinated based on population at 87.79%.

![Top/Bottom 5 Countries Vaccinated based on Population](/Images/pop_fully_vaccinated_hundred_df.png "Top/Bottom 5 Countries Vaccinated based on Population")

<strong>By total vaccinations, what is the top manufacture used in United States?</strong>

<strong>***Analysis:***</strong>

United States top manufacturer is Pfizer/BioNTech

![United States Top COVID-19 Manufacturers](/Images/united_states_manufacturers_df.png "United States Top COVID-19 Manufacturers")

## Data Extract, Transform, and Load Process

#### Prework

Created <strong>covid_vaccination_db</strong> in ***postgreSQL***

Using csv files - we determine the layout of the tables and columns we wanted to load in ***postgreSQL***:

> Layout Outline:

   * Table_1
      - country_vaccinations
   * Columns_1
      - id (pk)
      - country
      - total_vaccinations
      - people_fully_vaccinated
      - people_fully_vaccinated_per_hundred
      - manufacturer

   * Table_2
      - country_manufacturer
   * Columns_2
      - id (pk)
      - country (Fk)
      - date	
      - manufacturer
      - total_vaccinations

# Extract:

    - Extracted Two Datasets (As of March 2022) from Resources folder
        1. Country_vaccinations_by_manufacturer.csv
        2. Country_vaccinations.csv 
    - Loaded CSV files (both datasets)
    - Read CSV files using Pandas
    - Reviewed both dataframes to validate the data we needed according to our tentative outline above

# Transform:

## Data Wrangling

### <strong>country_vaccinations dataset</strong>

- #### Created a filtered dataframe to indicate specific columns
- #### Converted index column (used as primary key later) and rename the column headers
- #### Dropped rows with NaN values
- #### Created variables to collect data for the ***for loop*** and pull data into transformed dataframe
- #### Iterated over each country to collect in ***for loop*** the latest values for columns to place in dataframe
- #### Created dataframe where each country can be associated to a desired value 

![country_vaccination_df](/Images/country_vaccination_df.png)

### <strong>country_manufacturer dataset</strong>

- #### Cleaned multiple dates from csv file prior to upload (most challenging was to use a for loop using Pandas)
- #### Created a filtered dataframe to indicate specific columns
- #### Converted index column (used as primary key later) and rename the column headers
- #### Dropped rows with NaN values

![country_manufacturer dataset](/Images/country_vacc_manu_transformed.png)

  ### Tools Used in Data Transformation

  1. Python
  2. Pandas
  3. Numpy
  4. DataFrame_Image
  5. Jupyter Notebook

# Load:

 - Created a connection to postgreSQL (pgAdmin 4)
 - Created table (country_vaccinations) and load dataframe data
 - Confirmed data has been added by querying the 'country_vaccinations' table

 - Created table (country_manufactuer) and load dataframe data
 - Confirmed data has been added by querying the 'country_manufactuer' table 

 - Joined tables to answer analysis question 4


## Files 

[Load Queries File](/Files/load_data_queries.txt "Load Queries")

[SQL Queries for Analysis](/Files/sql_queries.txt "postgreSQL Queries")
