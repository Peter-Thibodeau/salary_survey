# Introduction
This is a practice case study. I intend to find the industries that are most welcoming to minorities by answering the following questions:
| What are the average salaries for each gender by industry
| What are the average salaries for each gender with a college education by industry 
| What are the average salaries for each race by industry
| What are the average salaries for each race with a college education by industry 


# Data Source
I am using data from a web app on the askamanager.org website (https://www.askamanager.org/ 2022/04/how-much-money-do-you-make-5.html). This form allows users to anonymously enter their demographic and salary info and then see a table comparing their data to other users. The table contains 28,015 records, allowing an analysis of salaries based on industry, years of experience, and personal demographics.

The data is hosted on Google Sheets at: https://docs.google.com/spreadsheets/d/1IPS5dBSGtwYVbjsfbaMCYIWnOuRmJcbequohNxCyGVw/edit?resourcekey#gid=1625408792. I downloaded it as a .csv file.


# Data Exploration
## Variable Descriptions
| Variable           | Datatype | Description |
| :---               | :---     | :--- |
| timestamp          | datetime | a unique string automatically assigned to each new record
| age                | string   | seven strings that the user can choose from for age bracket
| industry           | string   | entered by the user
| job_title          | string   | entered by the user
| job_title_info     | string   | entered by the user
| annual_salary      | integer  | entered by the user
| additional         | string   | entered by the user for including a note about annaul_salary
| currency           | string   | seventeen strings that the user can choose from 
| other_info         | string   | entered by the user for including a note about currency
| income_context     | string   | entered by the user for including additional information about themselves
| country            | string   | entered by the user
| state              | string   | entered by the user
| city               | string   | entered by the user
| years_exp          | string   | eight strings that the user can choose from
| years_exp_in_field | string   | eight strings that the user can choose from
| education          | string   |  six strings that the user can choose from
| gender             | string   |  five strings that the user can choose from
| race               | string   |  forty-eight strings that the user can choose from

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
industry:   
1. has 1,101 unique values, remove values that are less than ten percent of all records  
2. consolidate the remaining into 16 values to make plotting manageable
   
| Variable           | Keep or Omit                              | OMIT|
| :--- | :--- | :--- |
| timestamp          | not relevant                             |
| age                | 
| industry
| job_title          | has too many unique values to be useful   | OMIT|
| job_title_info     | has too many null values to be useful     | OMIT|
| annual_salary      | use as is                                 ||
| additional         | has too many null values to be useful     | OMIT|
| currency           | use as is                                 ||
| other_info         | has too many null values to be useful     | OMIT|
| income_context     | has too many null values to be useful     | OMIT|
| country            | location will not be used in the analysis | OMIT|
| state              | location will not be used in the analysis | OMIT|
| city               | location will not be used in the analysis | OMIT|
| years_exp          | use as is                                 ||
| years_exp_in_field | use as is                                 ||
| education          | use as is                                 ||
| gender             | use as is                                 ||
| race               | has forty-eight unique values             ||

timestamp,not relevant,OMIT
job_title,has too many unique values to be useful,OMIT
job_title_info,has too many null values to be useful,OMIT
annual_salary,use as is
additional,has too many null values to be useful,OMIT
currency,use as is
other_info,has too many null values to be useful,OMIT
income_context,has too many null values to be useful,OMIT
country,location will not be used in the analysis,OMIT
state,location will not be used in the analysis,OMIT
city,location will not be used in the analysis,OMIT
years_exp,use as is
years_exp_in_field, use as is
education, use as is
gender, use as is
race,has forty-eight unique values, many of which are similar, and can be consolidated into six values

# Data Cleaning
Remove leading and trailing spaces.
Remove duplicate records.
Remove null values in industry, education, gender, and race variables.
Change strings to upper case.
Remove punctuation marks.
Change the datatype of annual_salary to integer.

## Filtering
Age  
The age for earning an annual salary can be assumed to apply only to adults, so remove records with the string "under 18."
Many workers aged sixty-five and older do not work a 40-hour work week, which will skew the results, so remove records with the string "65 and over."

Annual salary  
Assuming that a work week is at least 40 hours and the national minimum wage is $7, the minimum annual_salary will be  $7 X 40 hours X 52 weeks = $14,560.
Annual salaries above one million will skew the results, so remove those records.

Currency
Remove the string "other."
Remove currencies present in less than ten percent of total records.

Education 
Change the string "some college" to "high school."
Change the string "college education" to "bachelor's degree."

Gender 
Remove records with strings "Other or prefer not to answer" and "Prefer not to answer."

Race 
Remove records with the string "another option not listed here."


## New Variables
Records with a currency other than U.S. dollars must be converted to U.S. dollars for a meaningful comparison. The name of the new variable will be annual_salary_USD. These are the exchange rates used:

Country       Exchange rate in U.S. dollars |
------------| | ----------------------------| |
| Austrailia    | 1.53                          |
| Canada        | 1.35                          |
| Europe        | 1.08                          |
| Great Britain | 1.26                          |
