# Introduction
This is a practice case study. Using salary data I will intend to find the industries that are most welcoming to minorities by answering the following quesitons:
- What are the average salaires for each gender by industry
- What are the average salaires for each gender with a college education by industry 
- What are the average salaires for each race by industry
- What are the average salaires for each race with a college education by industry 


# The Data
I am using data from a web app on the askamanager.org website (https://www.askamanager.org/ 2022/04/how-much-money-do-you-make-5.html). This form allows the user to enter their demographic and salary info anonymously and then see a table comparing their data to other users. The table contains 28,015 records allowing an analysis of salaries based on industry, years of experience, and personal demographics.

The data is hosted on Google sheets at: https://docs.google.com/spreadsheets/d/1IPS5dBSGtwYVbjsfbaMCYIWnOuRmJcbequohNxCyGVw/edit?resourcekey#gid=1625408792. I downloaded it as a .csv file.


# Data Exploration
## Descriptions of Variables:
- Timestamp: a unique string automatically assigned to the record, not relevant to the analysis
- age: a string of seven age brackets the user can choose from
- industry: a string entered by the user
- job_title: a string entered by the user
- job_title_info: a string entered by the user to add notes about their job title
- annual_salary: a numeric for currency, no decimal places
- additional: a string entered by the user for information about the user's annual salary
- currency: a string three characters long with seven different values the user can choose from
- other_info: a string entered by the user for information about the currency they selected
- income_context: a string entered by the user
- country: a string entered by the user
- state: a string entered by the user
- city: a string entered by the user
- years_exp: a string of eight years brackets the user can choose from
- years_exp_in_field: a string of eight years brackets the user can choose from
- education: a string of six levels of education the user can choose from
- gender: a string of five genders the user can choose from
- race: a string of fourty eight races the user can choose from

## Nulls and NA's For Each Variable:
Variable	Nulls
Timestamp	0
age	0
industry	73
job_title	0
job_title_info	0
annual_salary	0
additional	7,280
currency	0
other_info	27,805
income_context	0
country	0
state	5,004
city	0
years_exp	0
years_exp_in_field	0
education	217
gender	169
race	173

## Unique Values For Each Variable (that are not numeric or have a fixed number of values for the user to choose from):
Variable	Unique Values
Timestamp	0
age	0
industry	1,100
job_title	13,068
job_title_info	20,776
annual_salary	3,652
additional	847
currency	11
other_info	109
income_context	2,851
country	306
state	132
city	4,460
years_exp	8
years_exp_in_field	8
education	6
gender	5
race	49

## Observations
- Timestamp: not relevent OMIT
- industry: has _____ unique values, so similar values will be grouped
- job_title: has too many unique values to be useful OMIT
- job_title_info: has too many null values to be useful OMIT
- annual_salary: is relevent and useable as is
- additional: has too many null values to be useful OMIT
- currency: is relevent and useable as is
- other_info: has too many null values to be useful OMIT
- income_context: has too many null values to be useful OMIT
- country: is not relevent, only currency is OMIT
- state: has too many unique values to be useful OMIT
- city: has no value without state OMIT
- years_exp: is relevent and useable as is
- years_exp_in_field: is relevent and useable as is
- education: a string of six levels of education the user can choose from
- gender: a string of five genders the user can choose from
- race: a string of fourty eight races the user can choose from, so similar values will be grouped

## Relevent Record Counts (did after nulls and na's removed)
- There are 5,461 records for males.
- There are 21,346 records for gender value woman
- There are 743 records for gender value non-binary.
- There are 4,694 records for race other than White.

# Data Cleaning
√- Leading and trailing spaces removed from the industry variable.
√- Duplicate records removed.
√- Records with null values found in the industry, education, gender and race vaiables removed.
√- All alphabetcal characters in strings converted to upper case.
√- Punctuation marks removed from all variables
√- Data type of annual_salary changed to integer
√- Replace the user selected string "COLLEGE EDUCATION" with "BACHELORS DEGREE" to differentiate it from "MASTER'S DEGREE," and "PHD."

## Filtering
√- Age
-- The age for earning an annual salary can be assumed to apply only to adults. The age bracket for under 18 will be removed.
-- Many workers aged sixty five and older do not work a 40 hour workweek which will skew the results, so the 65 and over age bracket will be removed.

√- Industry has over one thousand unique values and has to be grouped so that plots can be produced. This number will be pared down to fifteen

√ - Annual salary
-- The national minimum wage is $7.
-- An annual salary can be assumbed to be for a minimum of a 40 hour workweek.
-- $7 X 40 hours X 52 weeks = $14,560 minimum annual_salary

√ -- remove values above one million in annual_salary to prevent skewing of data

√-- remove other from currency

√- education change some college to high school

√ - Gender values "Other or prefer not to answer" and "Prefer not to answer" are irrelevant and will be removed.

 √- Race has fourty eight values the user could choose from. One value "another option not listed here," will skew the results, so those records will be removed.


## New Variables
- For records with a currency other than U.S. dollars, the annaul_salary must be converted to U.S. dollars. The name of the variable will be annual_salary_USD. These are the exchange rates used:
AUD/NZD 1.53
CAD 1.35
EUR 1.08
GBP 1.26


Results: There majority of users are female and non-binary; in fact, 3.9 times more than male. Minority races are 16.9% of all users. (did after nulls and na's removed)
Conclusion: we can see from the tables that how many hours I slept the previous night does not significantly predict the amount of steps I take the next day.

![image](https://github.com/Peter-Thibodeau/salary_survey/assets/158618486/95962147-e3f0-4f4c-aa77-52a1fe48153f)
