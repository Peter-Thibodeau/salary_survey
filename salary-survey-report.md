# Introduction
This is a practice case study. I intend to find the industries that are most welcoming to minorities by answering the following questions:
1. What are the average salaries for each gender by industry
2. What are the average salaries for each gender with a college education by industry 
3. What are the average salaries for each race by industry
4. What are the average salaries for each race with a college education by industry 


# Data Source
I am using data from a web app on the askamanager.org website (https://www.askamanager.org/2022/04/how-much-money-do-you-make-5.html). The app allows users to anonymously enter their demographic and salary info and then see a table comparing their data to other users.

The data is hosted on Google Sheets at: https://docs.google.com/spreadsheets/d/1IPS5dBSGtwYVbjsfbaMCYIWnOuRmJcbequohNxCyGVw/edit?resourcekey#gid=1625408792. I downloaded it as a .csv file.


# Data Exploration
The table contains 28,014 records and 17 variables.

## Variable Descriptions
| Variable           | Datatype | Description |
| :---               | :---     | :--- |
| timestamp          | datetime | a unique string automatically assigned to each new record
| age                | string   | 7 strings that the user can choose from for age bracket
| industry           | string   | entered by the user
| job_title          | string   | entered by the user
| job_title_info     | string   | entered by the user
| annual_salary      | integer  | entered by the user
| additional         | string   | entered by the user for including a note about annaul_salary
| currency           | string   | 17 strings that the user can choose from 
| other_info         | string   | entered by the user for including a note about currency
| income_context     | string   | entered by the user to include additional information about themselves
| country            | string   | entered by the user
| state              | string   | entered by the user
| city               | string   | entered by the user
| years_exp          | string   | 8 strings that the user can choose from
| years_exp_in_field | string   | 8 strings that the user can choose from
| education          | string   |  6 strings that the user can choose from
| gender             | string   |  5 strings that the user can choose from
| race               | string   |  48 strings that the user can choose from

## Nulls and Unique Values
| Variable           | Null     | Unique  |
| :---| :--- | :--- |
| timestamp          | 0        | 0            |
| age                | 0        | 0            |
| industry           | 73       | 1,101        |
| job_title          | 0        | 13,068       |
| job_title_info     | 0        | 20,776       |
| annual_salary      | 0        | 3,652        |
| additional         | 7,280    | 847          |
| currency           | 0        | 11           |
| other_info         | 27,805   | 109          |
| income_context     | 0        | 2,851        |
| country            | 0        | 306          |
| state              | 5,004    | 132          |
| city               | 0        | 4,460        |
| years_exp          | 0        | 8            |
| years_exp_in_field | 0        | 8            |
| education          | 217      | 6            |
| gender             | 169      | 5            |
| race               | 173      | 49           |

## Variable Handling
| Variable           | Note                                      | Omit|
| :--- | :--- | :--- |
| timestamp          | not relevant to analysis                  | Omit|
| age                | not relevant to analysis                  | Omit|
| industry           | consolidate 1,101 values to 16            ||
| job_title          | has too many unique values to be useful   | Omit|
| job_title_info     | has too many null values to be useful     | Omit|
| annual_salary      | use as is                                 ||
| additional         | has too many null values to be useful     | Omit|
| currency           | use as is                                 ||
| other_info         | has too many null values to be useful     | Omit|
| income_context     | has too many null values to be useful     | Omit|
| country            | location will not be used in the analysis | Omit|
| state              | location will not be used in the analysis | Omit|
| city               | location will not be used in the analysis | Omit|
| years_exp          | use as is                                 ||
| years_exp_in_field | use as is                                 ||
| education          | use as is                                 ||
| gender             | use as is                                 ||
| race               | consolidate 48 values to 6                ||

# Data Cleaning
- Remove leading and trailing spaces.
- Remove duplicate records.
- Remove null values in industry, education, gender, and race variables.
- Change strings to upper case.
- Remove punctuation marks.
- Change the datatype of annual_salary to an integer.

## Filtering
**Age**  
The age for earning an annual salary can be assumed to apply only to adults, so remove records with the string "under 18."
Many workers aged 65 and older do not work a 40-hour work week, which will skew the results, so remove records with the string "65 and over."

**Annual salary**  
Assuming a work week is at least 40 hours and the national minimum wage is $7, the minimum annual_salary will be  $7 X 40 hours X 52 weeks = $14,560.
Annual salaries above one million will skew the results, so remove those records.

**Currency**
Remove the string "other."
Remove currencies present in less than 10% of total records.

**Education**  
Change the string "some college" to "high school."
Change the string "college education" to "bachelor's degree."

**Gender**   
Remove records with strings "Other or prefer not to answer" and "Prefer not to answer."

**Race**   
Remove records with the string "another option not listed here."

The table now contains 22,142 records and 9 variables.

## New Variables
Records with a currency other than U.S. dollars must be converted to U.S. dollars for a meaningful comparison. The new variable's name will be annual_salary_USD, and its datatype will be decimal. These are the exchange rates used:

| Country       | U.S. Dollars |
|---------------|--------------|
| Australia     | 1.53         |
| Canada        | 1.35         |
| Europe        | 1.08         |
| Great Britain | 1.26         |
