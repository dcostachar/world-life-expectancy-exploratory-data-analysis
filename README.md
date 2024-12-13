# Life Expectancy Around the World: Data Cleaning and Exploratory Data Analysis with SQL

Author: Charlene D'Costa <br />
Date: December 9, 2024 <br />
Final Project for the Analyst Builder: MySQL for Data Analytics course. <br />

[World Life Expectancy Dataset](https://github.com/dcostachar/world-life-expectancy-exploratory-data-analysis/blob/main/WorldLifeExpectancy%20(3).csv)

# Project Overview

<details>
  <summary>Defining the business problem.</summary>

<br />

For this project, I performed data cleaning and exploratory data analysis (EDA) in SQL, using a real-world dataset of
global life expectancy spanning 15 years. The goal was to work with the raw data to understand its structure, assess its
quality, handle issues like duplicates and missing values, and uncover patterns and relationships in the data.

The process produced a cleaned dataset with insights into global life expectancy trends and correlations with factors
such as GDP, development status, BMI, and adult mortality. The EDA also prepared the data for integration into
visualization platforms, enabling impactful storytelling and empowering businesses and researchers to make data-driven
decisions confidently.

</details>

# Data Cleaning

<details>
  <summary>Cleaning the data for analysis. </summary> 

<br />

In this section, I will import and clean the dataset to ensure it is ready for analysis. I will use DuckDB as my SQL
database and connect it to DataGrip, my integrated development environment (IDE), to perform the analysis.

## Importing the Dataset

A major advantage of DuckDB is the ability to create a table and query data directly from a file, eliminating the need
to load the data into a database beforehand. Therefore, I’ll begin by creating the table.

Upon initial inspection of the table, I noticed NULL values in the Status and Life Expectancy columns. I will
address these later on as I proceed with data cleaning.

```sql 
CREATE TABLE world_life_expectancy AS
SELECT *
FROM 'WorldLifeExpectancy.csv';
```

| Country     | Year | Status     | Life expectancy | Adult Mortality | infant deaths | percentage expenditure | Measles | BMI  | under-five deaths | Polio | Diphtheria | HIV/AIDS | GDP  | thinness  1-19 years | thinness 5-9 years | Schooling | Row\_ID |
|:------------|:-----|:-----------|:----------------|:----------------|:--------------|:-----------------------|:--------|:-----|:------------------|:------|:-----------|:---------|:-----|:---------------------|:-------------------|:----------|:--------|
| Afghanistan | 2022 | Developing | 65              | 263             | 62            | 71.3                   | 1154    | 19.1 | 83                | 6     | 65         | 0.1      | 584  | 17.2                 | 17.3               | 10.1      | 1       |
| Afghanistan | 2021 | Developing | 59.9            | 271             | 64            | 73.5                   | 492     | 18.6 | 86                | 58    | 62         | 0.1      | 613  | 17.5                 | 17.5               | 10        | 2       |
| Afghanistan | 2020 | Developing | 59.9            | 268             | 66            | 73.2                   | 430     | 18.1 | 89                | 62    | 64         | 0.1      | 632  | 17.7                 | 17.7               | 9.9       | 3       |
| Afghanistan | 2019 | Developing | 59.5            | 272             | 69            | 78.2                   | 2787    | 17.6 | 93                | 67    | 67         | 0.1      | 670  | 17.9                 | 18                 | 9.8       | 4       |
| Afghanistan | 2018 | Developing | null            | 275             | 71            | 7.1                    | 3013    | 17.2 | 97                | 68    | 68         | 0.1      | 64   | 18.2                 | 18.2               | 9.5       | 5       |
| Afghanistan | 2017 | Developing | 58.8            | 279             | 74            | 79.7                   | 1989    | 16.7 | 102               | 66    | 66         | 0.1      | 553  | 18.4                 | 18.4               | 9.2       | 6       |
| Afghanistan | 2016 | Developing | 58.6            | 281             | 77            | 56.8                   | 2861    | 16.2 | 106               | 63    | 63         | 0.1      | 446  | 18.6                 | 18.7               | 8.9       | 7       |
| Afghanistan | 2015 | Developing | 58.1            | 287             | 80            | 25.9                   | 1599    | 15.7 | 110               | 64    | 64         | 0.1      | 373  | 18.8                 | 18.9               | 8.7       | 8       |
| Afghanistan | 2014 | null       | 57.5            | 295             | 82            | 10.9                   | 1141    | 15.2 | 113               | 63    | 63         | 0.1      | 370  | 19                   | 19.1               | 8.4       | 9       |
| Afghanistan | 2013 | Developing | 57.3            | 295             | 84            | 17.2                   | 1990    | 14.7 | 116               | 58    | 58         | 0.1      | 273  | 19.2                 | 19.3               | 8.1       | 10      |
| Afghanistan | 2012 | Developing | 57.3            | 291             | 85            | 1.4                    | 1296    | 14.2 | 118               | 58    | 58         | 0.1      | 25   | 19.3                 | 19.5               | 7.9       | 11      |
| Afghanistan | 2011 | Developing | 57              | 293             | 87            | 15.3                   | 466     | 13.8 | 120               | 5     | 5          | 0.1      | 219  | 19.5                 | 19.7               | 6.8       | 12      |
| Afghanistan | 2010 | Developing | 56.7            | 295             | 87            | 11.1                   | 798     | 13.4 | 122               | 41    | 41         | 0.1      | 199  | 19.7                 | 19.9               | 6.5       | 13      |
| Afghanistan | 2009 | Developing | 56.2            | 3               | 88            | 16.9                   | 2486    | 13   | 122               | 36    | 36         | 0.1      | 188  | 19.9                 | 2.2                | 6.2       | 14      |
| Afghanistan | 2008 | Developing | 55.3            | 316             | 88            | 10.6                   | 8762    | 12.6 | 122               | 35    | 33         | 0.1      | 118  | 2.1                  | 2.4                | 5.9       | 15      |
| Afghanistan | 2007 | Developing | 54.8            | 321             | 88            | 10.4                   | 6532    | 12.2 | 122               | 24    | 24         | 0.1      | 115  | 2.3                  | 2.5                | 5.5       | 16      |
| Albania     | 2022 | Developing | 77.8            | 74              | 0             | 365                    | 0       | 58   | 0                 | 99    | 99         | 0.1      | 3954 | 1.2                  | 1.3                | 14.2      | 17      |
| Albania     | 2021 | null       | 77.5            | 8               | 0             | 428.7                  | 0       | 57.2 | 1                 | 98    | 98         | 0.1      | 4576 | 1.2                  | 1.3                | 14.2      | 18      |
| Albania     | 2020 | Developing | 77.2            | 84              | 0             | 430.9                  | 0       | 56.5 | 1                 | 99    | 99         | 0.1      | 4415 | 1.3                  | 1.4                | 14.2      | 19      |
| Albania     | 2019 | Developing | 76.9            | 86              | 0             | 412.4                  | 9       | 55.8 | 1                 | 99    | 99         | 0.1      | 4248 | 1.3                  | 1.4                | 14.2      | 20      |

To confirm the data has been imported correctly, I will verify the number of rows in the table. I expect 2,941 rows, as
the original CSV file contained 2,942 rows (including the header). Additionally, I will ensure that all data types have
been correctly identified and stored. Since everything checks out, I will proceed.

```sql 
SELECT COUNT(*)
FROM world_life_expectancy;

DESCRIBE world_life_expectancy;
```

| count\_star\(\) |
|:----------------|
| 2941            |

| column\_name           | column\_type | null | key  | default | extra |
|:-----------------------|:-------------|:-----|:-----|:--------|:------|
| Country                | VARCHAR      | YES  | null | null    | null  |
| Year                   | BIGINT       | YES  | null | null    | null  |
| Status                 | VARCHAR      | YES  | null | null    | null  |
| Life expectancy        | DOUBLE       | YES  | null | null    | null  |
| Adult Mortality        | BIGINT       | YES  | null | null    | null  |
| infant deaths          | BIGINT       | YES  | null | null    | null  |
| percentage expenditure | DOUBLE       | YES  | null | null    | null  |
| Measles                | BIGINT       | YES  | null | null    | null  |
| BMI                    | DOUBLE       | YES  | null | null    | null  |
| under-five deaths      | BIGINT       | YES  | null | null    | null  |
| Polio                  | BIGINT       | YES  | null | null    | null  |
| Diphtheria             | BIGINT       | YES  | null | null    | null  |
| HIV/AIDS               | DOUBLE       | YES  | null | null    | null  |
| GDP                    | BIGINT       | YES  | null | null    | null  |
| thinness  1-19 years   | DOUBLE       | YES  | null | null    | null  |
| thinness 5-9 years     | DOUBLE       | YES  | null | null    | null  |
| Schooling              | DOUBLE       | YES  | null | null    | null  |
| Row\_ID                | BIGINT       | YES  | null | null    | null  |

## Identifying and Removing Duplicates

I'll start by identifying duplicates. Since each year should be unique for each country, I will use `CONCAT` to combine
the Country and Year columns, creating a unique identifier for each row (similar to a primary key). Then, I will use
`GROUP BY` on the Country, Year, and the concatenated identifier columns, along with `COUNT` to check for duplicate
entries. Finally, I'll use `HAVING` to filter rows where the count of the concatenated identifier is greater than 1,
highlighting duplicates.

```sql 
SELECT Country, Year, CONCAT(Country, Year), COUNT (CONCAT(Country, Year))
FROM world_life_expectancy
GROUP BY Country, Year, CONCAT(Country, Year)
HAVING COUNT (CONCAT(Country, Year)) > 1;
```

| Country  | Year | concat\(Country, "Year"\) | count\(concat\(Country, "Year"\)\) |
|:---------|:-----|:--------------------------|:-----------------------------------|
| Senegal  | 2009 | Senegal2009               | 2                                  |
| Zimbabwe | 2019 | Zimbabwe2019              | 2                                  |
| Ireland  | 2022 | Ireland2022               | 2                                  |

Now that I’ve identified 3 duplicate rows, I need to match them with their unique Row ID to ensure the correct rows
are removed. I will do this by using the `ROW_NUMBER()` window function, partitioned by the unique combination of
country and year. I will then use the result in a subquery to display only the rows that are not the first occurrence
for each combination, which can then be removed.

```sql 
SELECT *
FROM (SELECT Row_ID,
             CONCAT(Country, Year),
             ROW_NUMBER() OVER (PARTITION BY CONCAT(Country, Year) ORDER BY CONCAT(Country, Year)) AS Row_Num
      FROM world_life_expectancy)
         AS Row_Table
WHERE Row_Num > 1;
```

| Row\_ID | concat\(Country, "Year"\) | Row\_Num |
|:--------|:--------------------------|:---------|
| 1251    | Ireland2022               | 2        |
| 2265    | Senegal2009               | 2        |
| 2929    | Zimbabwe2019              | 2        |

Now, I'll use the query above to remove the duplicate Row_IDs from the original table.

```sql 

DELETE
FROM world_life_expectancy
WHERE Row_ID IN (SELECT Row_ID
                 FROM (SELECT Row_ID,
                              CONCAT(Country, Year),
                              ROW_NUMBER() OVER (PARTITION BY CONCAT(Country, Year) ORDER BY CONCAT(Country, Year)) AS Row_Num
                       FROM world_life_expectancy)
                          AS Row_Table
                 WHERE Row_Num > 1);
```

If I run the query above again, it should return an empty table, indicating that the query executed correctly. Since
this is the case, I will proceed.

```sql 
SELECT *
FROM (SELECT Row_ID,
             CONCAT(Country, Year),
             ROW_NUMBER() OVER (PARTITION BY CONCAT(Country, Year) ORDER BY CONCAT(Country, Year)) AS Row_Num
      FROM world_life_expectancy)
         AS Row_Table
WHERE Row_Num > 1;
```

## Identifying and Handling NULL Values

From the initial inspection of the table, I noticed some missing/NULL values in the Status and Life Expectancy columns.
I’ll address these missing values, starting with the Status column by identifying all rows with NULLs. This
returns 8 rows.

```sql
SELECT *
FROM world_life_expectancy
WHERE Status IS NULL;
```

| Country                  | Year | Status | Life expectancy | Adult Mortality | infant deaths | percentage expenditure | Measles | BMI  | under-five deaths | Polio | Diphtheria | HIV/AIDS | GDP  | thinness  1-19 years | thinness 5-9 years | Schooling | Row\_ID |
|:-------------------------|:-----|:-------|:----------------|:----------------|:--------------|:-----------------------|:--------|:-----|:------------------|:------|:-----------|:---------|:-----|:---------------------|:-------------------|:----------|:--------|
| Afghanistan              | 2014 | null   | 57.5            | 295             | 82            | 10.9                   | 1141    | 15.2 | 113               | 63    | 63         | 0.1      | 370  | 19                   | 19.1               | 8.4       | 9       |
| Albania                  | 2021 | null   | 77.5            | 8               | 0             | 428.7                  | 0       | 57.2 | 1                 | 98    | 98         | 0.1      | 4576 | 1.2                  | 1.3                | 14.2      | 18      |
| Georgia                  | 2012 | null   | 73.9            | 128             | 1             | 9.4                    | 1356    | 48.6 | 1                 | 82    | 82         | 0.1      | 154  | 2.8                  | 2.9                | 12.2      | 989     |
| Georgia                  | 2010 | null   | 72.7            | 132             | 1             | 70.5                   | 216     | 47.5 | 2                 | 74    | 75         | 0.1      | 928  | 2.9                  | 3                  | 11.8      | 991     |
| United States of America | 2021 | null   | 79.1            | 14              | 23            | 0                      | 667     | 69.1 | 27                | 93    | 95         | 0.1      | 0    | 0.8                  | 0.6                | 0         | 2798    |
| Vanuatu                  | 2020 | null   | 71.6            | 135             | 0             | 447.5                  | 0       | 51.7 | 0                 | 65    | 64         | 0.1      | 3167 | 1.5                  | 1.4                | 10.8      | 2847    |
| Zambia                   | 2016 | null   | 57.4            | 368             | 30            | 143.9                  | 26      | 2.2  | 47                | 93    | 94         | 9.1      | 1139 | 6.7                  | 6.6                | 11.6      | 2915    |
| Zambia                   | 2012 | null   | 49.3            | 554             | 34            | 121.9                  | 45      | 18.4 | 55                | 84    | 82         | 17       | 691  | 7.1                  | 7                  | 10.7      | 2919    |

Since all of these countries already have statuses in other years, we can take the status from a different year and fill
it into the rows where the status is missing. This is based on the assumption that a country's status remains consistent
throughout the dataset. First, I will confirm that each country has a populated status in at least one row. Since there
are only two statuses, "Developed" and "Developing," I will proceed.

```sql
SELECT DISTINCT(Status)
FROM world_life_expectancy
WHERE Status <> '';
```

| Status     |
|:-----------|
| Developing |
| Developed  |

Now, I'll create a list of all countries with the status "Developing".

```sql
SELECT DISTINCT(Country)
FROM world_life_expectancy
WHERE Status = 'Developing';
```

| Country                            |
|:-----------------------------------|
| Afghanistan                        |
| Albania                            |
| Algeria                            |
| Angola                             |
| Antigua and Barbuda                |
| Argentina                          |
| Armenia                            |
| Azerbaijan                         |
| Bahamas                            |
| Bahrain                            |
| Bangladesh                         |
| Barbados                           |
| Belarus                            |
| Belize                             |
| Benin                              |
| Bhutan                             |
| Bolivia \(Plurinational State of\) |
| Bosnia and Herzegovina             |
| Botswana                           |
| Brazil                             |

Now, I will create a subquery based on the query above to update the status of countries with a NULL value, setting them
to "Developing" if and only if they are present in the list above that isolates all developing countries.

```sql
UPDATE world_life_expectancy
SET Status = 'Developing'
WHERE Status IS NULL
  AND Country IN (SELECT DISTINCT(Country)
                  FROM world_life_expectancy
                  WHERE Status = 'Developing');
```

Now, I'll do the same for countries with the status "Developed".

```sql
UPDATE world_life_expectancy
SET Status = 'Developed'
WHERE Status IS NULL
  AND Country IN (SELECT DISTINCT(Country)
                  FROM world_life_expectancy
                  WHERE Status = 'Developed');
```

Checking there are no more NULL values in the Status column. Since there are none, I will proceed to the Life Expectancy
column.

```sql
SELECT *
FROM world_life_expectancy
WHERE Status IS NULL;
```

I'll begin by identifying the rows with missing values in the Life Expectancy column. This query returns 2 rows.

```sql
SELECT *
FROM world_life_expectancy
WHERE "Life expectancy" IS NULL;
```

| Country     | Year | Status     | Life expectancy | Adult Mortality | infant deaths | percentage expenditure | Measles | BMI  | under-five deaths | Polio | Diphtheria | HIV/AIDS | GDP  | thinness  1-19 years | thinness 5-9 years | Schooling | Row\_ID |
|:------------|:-----|:-----------|:----------------|:----------------|:--------------|:-----------------------|:--------|:-----|:------------------|:------|:-----------|:---------|:-----|:---------------------|:-------------------|:----------|:--------|
| Afghanistan | 2018 | Developing | null            | 275             | 71            | 7.1                    | 3013    | 17.2 | 97                | 68    | 68         | 0.1      | 64   | 18.2                 | 18.2               | 9.5       | 5       |
| Albania     | 2018 | Developing | null            | 88              | 0             | 437.1                  | 28      | 55.1 | 1                 | 99    | 99         | 0.1      | 4437 | 1.4                  | 1.5                | 13.3      | 21      |

From inspecting the life expectancy data, I observed that life expectancy tends to increase incrementally year over
year. Given this pattern and the fact that both countries identified above have life expectancy data for the preceding
and following years, I will fill in the missing values by calculating the average of the life expectancy from these
years. To achieve this, I will use a self-join to first retrieve the life expectancy values for the previous and
following years and then compute their average.

```sql
SELECT t1.Country,
       t1.Year,
       t1."Life expectancy",
       t2.Country,
       t2.Year,
       t2."Life expectancy",
       t3.Country,
       t3.Year,
       t3."Life expectancy"
FROM world_life_expectancy t1
         JOIN world_life_expectancy t2
              ON t1.Country = t2.Country
                  AND t1.Year = t2.Year - 1
         JOIN world_life_expectancy t3
              ON t1.Country = t3.Country
                  AND t1.Year = t3.Year + 1
WHERE t1."Life expectancy" IS NULL;
```

| Country     | Year | Life expectancy | Country     | Year | Life expectancy | Country     | Year | Life expectancy |
|:------------|:-----|:----------------|:------------|:-----|:----------------|:------------|:-----|:----------------|
| Afghanistan | 2018 | null            | Afghanistan | 2019 | 59.5            | Afghanistan | 2017 | 58.8            |
| Albania     | 2018 | null            | Albania     | 2019 | 76.9            | Albania     | 2017 | 76.2            |

I will now modify the query above to calculate the average using life expectancy data from the previous and following
years.

```sql
SELECT t1.Country,
       t1.Year,
       t1."Life expectancy",
       t2.Country,
       t2.Year,
       t2."Life expectancy",
       t3.Country,
       t3.Year,
       t3."Life expectancy",
       ROUND((t2."Life expectancy" + t3."Life expectancy") / 2, 1) AS Avg
FROM world_life_expectancy t1
    JOIN world_life_expectancy t2
ON t1.Country = t2.Country
    AND t1.Year = t2.Year -1
    JOIN world_life_expectancy t3
    ON t1.Country = t3.Country
    AND t1.Year = t3.Year +1
WHERE t1."Life expectancy" IS NULL;
```

Moving on to the final step, I will use the averages calculated above to populate the missing data in the Life
Expectancy column in the original table.

```sql
-- creating a temporary table with the calculated averages 
CREATE TABLE temp_life_exp AS
SELECT t1.Row_ID,
       ROUND((t2."Life expectancy" + t3."Life expectancy") / 2, 1) AS Avg
FROM world_life_expectancy t1
JOIN world_life_expectancy t2
    ON t1.Country = t2.Country
    AND t1.Year = t2.Year -1
JOIN world_life_expectancy t3
    ON t1.Country = t3.Country
    AND t1.Year = t3.Year +1
WHERE t1."Life expectancy" IS NULL;

-- updating the original table using the temporary table
UPDATE world_life_expectancy
SET "Life expectancy" = (SELECT Avg
                         FROM temp_life_exp
                         WHERE temp_life_exp.Row_ID = world_life_expectancy.Row_ID)
WHERE Row_ID IN (SELECT Row_ID
                 FROM temp_life_exp);
```

Checking my work to make sure there are no more NULL values in the Life Expectancy column. This query returns 0 rows so
we know that the updates were made successfully.

```sql
SELECT *
FROM world_life_expectancy
WHERE "Life expectancy" IS NULL;
```

Now that I’ve removed duplicates and addressed NULL/missing values, the dataset looks sufficiently cleaned to
proceed to the next stage. In this phase, I will conduct exploratory data analysis (EDA) to gain a deeper understanding
of the data, uncover patterns, and identify relationships between variables. The queries I create will generate new
tables that highlight these insights, which can then be input into data visualization software to present key findings
from the analysis.

</details>

# Exploratory Data Analysis

<details>
  <summary>Uncovering patterns and analyzing relationships between variables. </summary>

## Total Increase in Life Expectancy

I’ll begin by analyzing how each country has progressed in life expectancy over the past 15 years (the duration for
which this data was collected). By comparing the highest and lowest life expectancy values for each country, we can gain
insights into which countries have made the most significant improvements in increasing the life expectancy of their
populations. This will be achieved using the `MIN` and `MAX` functions, combined with `GROUP BY` to group data by each
country.

During the analysis, I noticed that some countries have a life expectancy value of 0. Since a life expectancy of 0 is
not possible, this likely indicates missing or incomplete data, so I will account for this by filtering out rows where
the `MIN` or `MAX` life expectancy is 0 to ensure the accuracy of the results and avoid skewing the aggregations.

**From the results, we observe that Haiti, Zimbabwe, Eritrea, and Uganda have experienced the largest increases in life
expectancy during these 15 years, with notable gains of ~20-28 years, highlighting significant progress in
these countries.**

```sql
SELECT Country,
       MIN("Life expectancy"),
       MAX("Life expectancy"),
       ROUND(MAX("Life expectancy") - MIN("Life expectancy"), 1) AS Life_Increase_15_Yrs
FROM world_life_expectancy
GROUP BY Country
HAVING MIN("Life expectancy") <> 0
   AND MAX("Life expectancy") <> 0
ORDER BY Life_Increase_15_Yrs DESC;
```

| Country                            | min\("Life expectancy"\) | max\("Life expectancy"\) | Life\_Increase\_15\_Yrs |
|:-----------------------------------|:-------------------------|:-------------------------|:------------------------|
| Haiti                              | 36.3                     | 65                       | 28.7                    |
| Zimbabwe                           | 44.3                     | 67                       | 22.7                    |
| Eritrea                            | 45.3                     | 67                       | 21.7                    |
| Uganda                             | 46.6                     | 67                       | 20.4                    |
| Botswana                           | 46                       | 65.7                     | 19.7                    |
| Rwanda                             | 48.3                     | 68                       | 19.7                    |
| Zambia                             | 43.8                     | 63                       | 19.2                    |
| Niger                              | 50                       | 69                       | 19                      |
| United Republic of Tanzania        | 49.2                     | 67                       | 17.8                    |
| Liberia                            | 50                       | 67                       | 17                      |
| Ethiopia                           | 51.2                     | 68                       | 16.8                    |
| Congo                              | 52.6                     | 68                       | 15.4                    |
| South Africa                       | 53.7                     | 69                       | 15.3                    |
| Malawi                             | 43.1                     | 58.3                     | 15.2                    |
| Sierra Leone                       | 39                       | 54                       | 15                      |
| Bolivia \(Plurinational State of\) | 62.6                     | 77                       | 14.4                    |
| Swaziland                          | 45.6                     | 58.9                     | 13.3                    |
| Central African Republic           | 45.6                     | 58                       | 12.4                    |
| Portugal                           | 76.6                     | 89                       | 12.4                    |
| Iraq                               | 64.7                     | 77                       | 12.3                    |

## Average Global Life Expectancy

Next, I’ll analyze global trends in life expectancy by calculating the average life expectancy for each year, excluding
rows where life expectancy is 0 as done previously. **The results show that, overall, global life expectancy has
increased by ~5 years over the 15-year period of data collection (2007–2022).**

```sql
SELECT Year, ROUND(AVG ("Life expectancy"), 1) AS Avg_Life_Increase
FROM world_life_expectancy
WHERE "Life expectancy" <> 0
GROUP BY Year
ORDER BY Year;
```

| Year | Avg\_Life\_Increase |
|:-----|:--------------------|
| 2007 | 66.8                |
| 2008 | 67.1                |
| 2009 | 67.4                |
| 2010 | 67.4                |
| 2011 | 67.6                |
| 2012 | 68.2                |
| 2013 | 68.7                |
| 2014 | 69                  |
| 2015 | 69.4                |
| 2016 | 69.9                |
| 2017 | 70                  |
| 2018 | 70.7                |
| 2019 | 70.9                |
| 2020 | 71.2                |
| 2021 | 71.5                |
| 2022 | 71.6                |

## GDP and Life Expectancy

Next, I’ll analyze the correlation between a country’s GDP and life expectancy. **The results show that countries with
lower GDPs tend to have life expectancies of ~20–30 years lower than those with higher GDPs. This indicates a
positive correlation between GDP and life expectancy, where lower GDPs are associated with shorter life spans.** This
relationship is logical, as countries with limited financial resources often lack the ability to invest adequately in
healthcare, housing, education, and other social infrastructure critical to improving quality of life.

```sql
SELECT Country,
       ROUND(AVG("Life expectancy"), 1) AS Avg_Life_Exp,
       ROUND(AVG(GDP), 1)               AS Avg_GDP
FROM world_life_expectancy
GROUP BY Country
HAVING Avg_Life_Exp > 0
   AND Avg_GDP > 0
ORDER BY Avg_GDP ASC;
```

| Country                  | Avg\_Life\_Exp | Avg\_GDP |
|:-------------------------|:---------------|:---------|
| Somalia                  | 53.3           | 55.8     |
| Burundi                  | 55.5           | 137.9    |
| Eritrea                  | 60.7           | 194.6    |
| Malawi                   | 49.9           | 237.6    |
| Liberia                  | 57.5           | 246.3    |
| Niger                    | 57             | 259.9    |
| Ethiopia                 | 59.1           | 265      |
| Sierra Leone             | 46.1           | 271.6    |
| Senegal                  | 62.6           | 274.7    |
| Guinea                   | 56             | 279.5    |
| Rwanda                   | 59.3           | 300.1    |
| Madagascar               | 62.7           | 314.2    |
| Togo                     | 56.7           | 317.1    |
| Tajikistan               | 66.7           | 335.8    |
| Afghanistan              | 58.2           | 340.1    |
| Central African Republic | 48.5           | 363      |
| Mozambique               | 53.4           | 365.1    |
| Guinea-Bissau            | 55.4           | 384.4    |
| Nepal                    | 66.5           | 395.4    |
| Burkina Faso             | 55.6           | 410.5    |

## Average Life Expectancy in High-GDP vs. Low-GDP Countries

I will further investigate the finding above by calculating the average life expectancy in high-GDP and low-GDP
countries. Using a threshold of 1500 (which appears to be the midpoint of the dataset when ordered by GDP), I will use a
`CASE` statement to categorize countries into either a high or low GDP group and calculate their average life expectancy
accordingly. **The results show that high-GDP countries have an average life expectancy of ~74 years, while
low-GDP countries have an average of ~65 years—a significant difference of about 9 years.** This further supports
the positive correlation between GDP and life expectancy highlighted earlier.

```sql
SELECT SUM(CASE WHEN GDP >= 1500 THEN 1 ELSE 0 END)                    High_GDP,
       AVG(CASE WHEN GDP >= 1500 THEN "Life expectancy" ELSE NULL END) High_GDP_Life_Exp,
       SUM(CASE WHEN GDP <= 1500 THEN 1 ELSE 0 END)                    Low_GDP,
       AVG(CASE WHEN GDP <= 1500 THEN "Life expectancy" ELSE NULL END) Low_GDP_Life_Exp,
FROM world_life_expectancy;
```

| High\_GDP | High\_GDP\_Life\_Exp | Low\_GDP | Low\_GDP\_Life\_Exp |
|:----------|:---------------------|:---------|:--------------------|
| 1326      | 74.20414781297133    | 1612     | 64.6996898263028    |

## Development Status and Life Expectancy

Now, I’ll move on to analyzing the correlation between a country’s development status and life expectancy. **Consistent
with our prior analysis, the results show that developed countries have a significantly higher average life expectancy
of ~80 years, compared to an average of ~67 years for developing countries.**

```sql
SELECT Status,
       ROUND(AVG("Life expectancy"), 1) AS Avg_Life_Exp,
       COUNT(DISTINCT Country)
FROM world_life_expectancy
GROUP BY Status;
```

| Status     | Avg\_Life\_Exp | count\(DISTINCT Country\) |
|:-----------|:---------------|:--------------------------|
| Developing | 66.8           | 161                       |
| Developed  | 79.2           | 32                        |

## BMI and Life Expectancy

Next, I’ll analyze the correlation between BMI (body mass index) and life expectancy. **The results are interesting
because, while we initially observe a positive correlation between low BMI and low life expectancy, this relationship
weakens beyond a certain point. In fact, we start to see countries with high BMI and high life expectancy, such as the
USA. This trend is typically observed only in countries with a developed status.** This could be an interesting
relationship to graph and explore further.

```sql
SELECT Country,
       ROUND(AVG("Life expectancy"), 1) AS Avg_Life_Exp,
       ROUND(AVG(BMI), 1)               AS Avg_BMI
FROM world_life_expectancy
GROUP BY Country
HAVING Avg_Life_Exp > 0
   AND Avg_BMI > 0
ORDER BY Avg_BMI DESC;
```

| Country                            | Avg\_Life\_Exp | Avg\_BMI |
|:-----------------------------------|:---------------|:---------|
| Kiribati                           | 65.1           | 69.4     |
| Malta                              | 80.4           | 66.2     |
| Qatar                              | 77             | 65.7     |
| Micronesia \(Federated States of\) | 68.2           | 65.2     |
| Tonga                              | 72.5           | 62.9     |
| Samoa                              | 73.6           | 62.9     |
| Kuwait                             | 73.8           | 59.6     |
| Spain                              | 82.1           | 58.7     |
| Greece                             | 81.2           | 58.7     |
| United States of America           | 78.1           | 58.5     |
| Hungary                            | 73.8           | 56.9     |
| Estonia                            | 74.9           | 56.7     |
| New Zealand                        | 81.3           | 56.6     |
| Turkey                             | 73.9           | 56.4     |
| Sweden                             | 82.5           | 56.2     |
| Italy                              | 82.2           | 56.2     |
| Australia                          | 81.8           | 55.9     |
| Canada                             | 81.7           | 55.9     |
| Denmark                            | 79.3           | 55.8     |
| Czechia                            | 76.8           | 55.7     |

## Adult Mortality and Life Expectancy

Lastly, I’ll examine the correlation between adult mortality and life expectancy. Using a window function, I will
calculate a yearly rolling total of adult mortality per country, providing an interesting perspective on year-over-year
trends. **The results reveal significantly higher cumulative adult mortality over 15 years in developing countries
compared to developed countries.**

```sql
SELECT Country, Year, "Life expectancy", "Adult Mortality", SUM ("Adult Mortality") OVER(PARTITION BY Country ORDER BY Year) AS Rolling_Total
FROM world_life_expectancy;
```

| Country                            | Year | Life expectancy | Adult Mortality | Rolling\_Total |
|:-----------------------------------|:-----|:----------------|:----------------|:---------------|
| Azerbaijan                         | 2007 | 66.6            | 16              | 16             |
| Azerbaijan                         | 2008 | 67.5            | 151             | 167            |
| Azerbaijan                         | 2009 | 67.8            | 146             | 313            |
| Azerbaijan                         | 2010 | 67.8            | 154             | 467            |
| Azerbaijan                         | 2011 | 68.4            | 154             | 621            |
| Azerbaijan                         | 2012 | 68.4            | 162             | 783            |
| Azerbaijan                         | 2013 | 69.2            | 154             | 937            |
| Azerbaijan                         | 2014 | 73              | 14              | 951            |
| Azerbaijan                         | 2015 | 73              | 141             | 1092           |
| Azerbaijan                         | 2016 | 78              | 132             | 1224           |
| Azerbaijan                         | 2017 | 71.1            | 13              | 1237           |
| Azerbaijan                         | 2018 | 71.6            | 125             | 1362           |
| Azerbaijan                         | 2019 | 71.9            | 123             | 1485           |
| Azerbaijan                         | 2020 | 72.2            | 121             | 1606           |
| Azerbaijan                         | 2021 | 72.5            | 119             | 1725           |
| Azerbaijan                         | 2022 | 72.7            | 118             | 1843           |
| Bolivia \(Plurinational State of\) | 2007 | 62.6            | 243             | 243            |
| Bolivia \(Plurinational State of\) | 2008 | 63.3            | 238             | 481            |
| Bolivia \(Plurinational State of\) | 2009 | 63.9            | 234             | 715            |
| Bolivia \(Plurinational State of\) | 2010 | 64.5            | 23              | 738            |

This concludes my data cleaning and exploratory data analysis SQL project, which examined global life expectancy trends
and their correlations with factors such as GDP, development status, BMI, and adult mortality.

</details>
