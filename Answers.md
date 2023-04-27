# Data Cleansing Steps:
In a single query, perform the following operations and generate a new table in the data_mart schema named clean_weekly_sales:

**1. Convert the week_date to a DATE format**

**2. Add a week_number as the second column for each week_date value, for example any value from the 1st of January to 7th of January will be 1, 8th to 14th will be 2 etc**

**3. Add a month_number with the calendar month for each week_date value as the 3rd column**

**4. Add a calendar_year column as the 4th column containing either 2018, 2019 or 2020 values**

**5. Add a new column called age_band after the original segment column using the following mapping on the number inside the segment value**

|segment|	age_band|
|-------|---------|
|1|	Young Adults|
|2|	Middle Aged|
|3 or 4	|Retirees|

**6. Add a new demographic column using the following mapping for the first letter in the segment values:**

|segment	|demographic|
|---------|-----------|
|C|	Couples|
|F|	Families|

**7. Ensure all null string values with an "unknown" string value in the original segment column as well as the new age_band and demographic columns**

**8. Generate a new avg_transaction column as the sales value divided by transactions rounded to 2 decimal places for each record**

![a1](https://user-images.githubusercontent.com/130475600/234912205-ea644d28-c017-4349-a0ee-1fccdb6d7eb8.PNG)

# Data Exploration

**1. What day of the week is used for each week_date value?**

![a1](https://user-images.githubusercontent.com/130475600/234916542-714951a8-82c4-432a-9790-0a695947a703.PNG)

| w_day     |
| --------- |
| monday    |

**2.What range of week numbers are missing from the dataset?**

![a2](https://user-images.githubusercontent.com/130475600/234919489-e753fe34-7bfc-4227-a6eb-3a6dad541594.PNG)

A total of 28 rows were return. 

**3. How many total transactions were there for each year in the dataset?**

![a3](https://user-images.githubusercontent.com/130475600/234921098-a1fae133-7ebd-44dd-98e7-fff2202a1785.PNG)

| year_number | total_transactions |
| ----------- | ------------------ |
| 2019        | 365639285          |
| 2018        | 346406460          |
| 2020        | 375813651          |

**4.What is the total sales for each region for each month?**

![a4](https://user-images.githubusercontent.com/130475600/234925403-dffa2a32-3f18-4536-94c2-062accc55fc0.PNG)

| region        | month_number | sum        |
| ------------- | ------------ | ---------- |
| AFRICA        | 3            | 567767480  |
| AFRICA        | 4            | 1911783504 |
| AFRICA        | 5            | 1647244738 |
| AFRICA        | 6            | 1767559760 |
| AFRICA        | 7            | 1960219710 |
| AFRICA        | 8            | 1809596890 |
| AFRICA        | 9            | 276320987  |
| ASIA          | 3            | 529770793  |
| ASIA          | 4            | 1804628707 |
| ASIA          | 5            | 1526285399 |
| ASIA          | 6            | 1619482889 |
| ASIA          | 7            | 1768844756 |
| ASIA          | 8            | 1663320609 |
| ASIA          | 9            | 252836807  |
| CANADA        | 3            | 144634329  |
| CANADA        | 4            | 484552594  |
| CANADA        | 5            | 412378365  |
| CANADA        | 6            | 443846698  |
| CANADA        | 7            | 477134947  |
| CANADA        | 8            | 447073019  |
| CANADA        | 9            | 69067959   |
| EUROPE        | 3            | 35337093   |
| EUROPE        | 4            | 127334255  |
| EUROPE        | 5            | 109338389  |
| EUROPE        | 6            | 122813826  |
| EUROPE        | 7            | 136757466  |
| EUROPE        | 8            | 122102995  |
| EUROPE        | 9            | 18877433   |
| OCEANIA       | 3            | 783282888  |
| OCEANIA       | 4            | 2599767620 |
| OCEANIA       | 5            | 2215657304 |
| OCEANIA       | 6            | 2371884744 |
| OCEANIA       | 7            | 2563459400 |
| OCEANIA       | 8            | 2432313652 |
| OCEANIA       | 9            | 372465518  |
| SOUTH AMERICA | 3            | 71023109   |
| SOUTH AMERICA | 4            | 238451531  |
| SOUTH AMERICA | 5            | 201391809  |
| SOUTH AMERICA | 6            | 218247455  |
| SOUTH AMERICA | 7            | 235582776  |
| SOUTH AMERICA | 8            | 221166052  |
| SOUTH AMERICA | 9            | 34175583   |
| USA           | 3            | 225353043  |
| USA           | 4            | 759786323  |
| USA           | 5            | 655967121  |
| USA           | 6            | 703878990  |
| USA           | 7            | 760331754  |
| USA           | 8            | 712002790  |
| USA           | 9            | 110532368  |

**5. What is the total count of transactions for each platform** 

![a5](https://user-images.githubusercontent.com/130475600/234927719-3c5a9a06-97e9-4070-bd1f-1b3d007b82dd.PNG)

| platform | t_transactions |
| -------- | -------------- |
| Shopify  | 5925169        |
| Retail   | 1081934227     |

**6. What is the percentage of sales for Retail vs Shopify for each month?**

![A6](https://user-images.githubusercontent.com/130475600/234931630-9513302d-c86e-4cf2-bed0-d2d7de49cd21.PNG)

| year_number | month_number | retail_perc | shopify_perc |
| ----------- | ------------ | ----------- | ------------ |
| 2018        | 3            | 97.92       | 2.08         |
| 2018        | 4            | 97.93       | 2.07         |
| 2018        | 5            | 97.73       | 2.27         |
| 2018        | 6            | 97.76       | 2.24         |
| 2018        | 7            | 97.75       | 2.25         |
| 2018        | 8            | 97.71       | 2.29         |
| 2018        | 9            | 97.68       | 2.32         |
| 2019        | 3            | 97.71       | 2.29         |
| 2019        | 4            | 97.80       | 2.20         |
| 2019        | 5            | 97.52       | 2.48         |
| 2019        | 6            | 97.42       | 2.58         |
| 2019        | 7            | 97.35       | 2.65         |
| 2019        | 8            | 97.21       | 2.79         |
| 2019        | 9            | 97.09       | 2.91         |
| 2020        | 3            | 97.30       | 2.70         |
| 2020        | 4            | 96.96       | 3.04         |
| 2020        | 5            | 96.71       | 3.29         |
| 2020        | 6            | 96.80       | 3.20         |
| 2020        | 7            | 96.67       | 3.33         |
| 2020        | 8            | 96.51       | 3.49         |

**7. What is the percentage of sales by demographic for each year in the dataset?**

![a7](https://user-images.githubusercontent.com/130475600/234933399-eddbb903-8418-4a0f-8217-d4290c30c63e.PNG)

| year_number | couples_perc | families_perc | unknown_perc |
| ----------- | ------------ | ------------- | ------------ |
| 2018        | 26.38        | 31.99         | 41.63        |
| 2019        | 27.28        | 32.47         | 40.25        |
| 2020        | 28.72        | 32.73         | 38.55        |

**8. Which age_band and demographic values contribute the most to Retail sales?**

![a8](https://user-images.githubusercontent.com/130475600/234935063-6f94abd5-3f61-4266-8abb-9f7c116a3c7b.PNG)

| age_band     | demographics | total_sales | contributed |
| ------------ | ------------ | ----------- | ----------- |
| unknown      | unknown      | 16067285533 | 40.52       |
| Retirees     | Families     | 6634686916  | 16.73       |
| Retirees     | Couples      | 6370580014  | 16.07       |
| Middle Aged  | Families     | 4354091554  | 10.98       |
| Young Adults | Couples      | 2602922797  | 6.56        |
| Middle Aged  | Couples      | 1854160330  | 4.68        |
| Young Adults | Families     | 1770889293  | 4.47        |

