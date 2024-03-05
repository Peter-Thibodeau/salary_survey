-- because plotting will be done with tableau, deletions and updates were used to make permanent changes to the data

-- omit uncecessary columns 
ALTER TABLE salariesA
  DROP COLUMN job_title,
  DROP COLUMN job_title_info,
  DROP COLUMN additional,
  DROP COLUMN other_info,
  DROP COLUMN income_context,
  DROP COLUMN country,
  DROP COLUMN state,
  DROP COLUMN City;


-- count nulls and NA's For Each Variable
SELECT 
  COUNT(age)
  from salariesA
  where age = ''; -- repeat for all variables


-- change case to upper
UPDATE salariesA
  set industry = UPPER(industry)
  WHERE industry!= UPPER(industry); -- repeat for education, gender and race


-- count unique values for each variable (that are not numeric or have a fixed number of values for the user to choose from) 
SELECT 
	COUNT(DISTINCT age) AS age,
	COUNT(DISTINCT industry) AS industry,
	COUNT(DISTINCT years_exp) AS years_exp,
	COUNT(DISTINCT years_exp_field) AS years_exp_field,
	COUNT(DISTINCT education) AS education,
	COUNT(DISTINCT gender) AS gender,
	COUNT(DISTINCT race) AS race
	FROM salariesA;

	
-- count genders that will be included
SELECT 
  COUNT(gender)
  FROM salariesA
  WHERE gender = 'MAN' -- repeat for non-binary and woman, get total of all three;


-- remove leading and trailing spaces
UPDATE salariesA
  SET industry = UPPER(industry)
  WHERE industry != UPPER(industry) -- repeat for education, gender and race;


-- remove records with null values 
DELETE
  FROM salariesA
  WHERE  industry = '' -- repeat for education, gender and race;


-- replace college degree with bachelors degree in education field
UPDATE SQLiteC
  SET education = REPLACE(education, "COLLEGE DEGREE", "BACHELORS DEGREE")
  WHERE education = "COLLEGE DEGREE";


-- remove unecessary ages
DELETE FROM SQLiteC
  WHERE age = "under 18"; -- repeat for 65 or over


-- remove characters from annual_salary
  UPDATE SQLiteEages
    set annual_salary = LTRIM(annual_salary, "$")
    WHERE TRUE;

  UPDATE SQLiteEages
    set annual_salary = REPLACE(annual_salary, ",", '')
    WHERE TRUE;

-- delete industry if condition met
UPDATE SQLiteFpunc
  SET industry = REPLACE(industry, "ACCOUNTING, BANKING & FINANCE%", "ACCOUNTING, BANKING, FINANCE")
  WHERE industry = " ACCOUNTING, BANKING, FINANCE %" -- repeat for other industries (there are over 1,000)


-- convert annual_salary to integer
UPDATE  cast(annual_salary AS integer) 
  SET annual_salary = cast(annual_salary AS integer)
  WHERE TRUE;

-- delete annual_salary if condition met
  DELETE FROM SQLiteFpunc
    WHERE annual_salary < 14561;

  DELETE FROM SQLiteFpunc
    WHERE annual_salary > 999999;


-- delete gender if condition met
DELETE FROM SQLiteGannsal
  WHERE gender = "OTHER OR PREFER NOT TO ANSWER";


-- delete currency if condition met
DELETE FROM SQLiteGannsal
  WHERE currency = "OTHER ";


-- alter education SQLiteFpunc
UPDATE SQLiteFpunc
  SET education = REPLACE(eduction, "SOME COLLEGE", "HIGH SCHOOL")
  WHERE education = "SOME COLLEGE"


-- alter race
UPDATE SQLiteFpunc
  SET race = REPLACE(race, "ASIAN OR ASIAN AMERICAN%", " ASIAN OR ASIAN AMERICAN ")
  WHERE race = " ASIAN OR ASIAN AMERICAN%" -- repeat for Black, Hispanic, Middle Eastern and Native American


-- convert currency other than USD to value of USD
UPDATE SQLiteNcurr
  SET annual_salary = annual_salary * 1.35
  WHERE currency = "CAD"


-- get annual_salary for each gender
SELECT 
  avg(annual_salary)
  FROM salaries
  group by gender

	
-- get annual_salary for each gender with a bachelor's degre
SELECT 
  avg(annual_salary)
  FROM salaries
  WHERE education = "BACHELORS DEGREE"
  GROUP BY gender


