# Lahman Baseball Database Exercise.. Again.
- this data has been made available [online](http://www.seanlahman.com/baseball-archive/statistics/) by Sean Lahman
- you can find a data dictionary [here](http://www.seanlahman.com/files/database/readme2016.txt)

## Use _PANDAS_ to find answers to the questions.
You heard right!
We've been through this before..
First with SQL, now with python/pandas.

With this, comes some rules.
You still need to connect to the Lahman Baseball database (that's where all your data lives).
However, for this project you are not allowed to use "complicated" SQL.
Complicated meaning: joins, data cleaning, case when statements, etc.

For every question you answer, this should be the extent of your SQL:
```sql
SELECT * FROM <table name>;
```

Feel free to pull in multiple tables.
Do not use filters, or manipulate the select statement.
The purpose of this exercise is to learn how to connect to a postgres database using python and pandas! Feel free to reference your SQL scripts from before and use them to validate your results.

## Setting up

We have provided an `environment.yaml` file for you to use (similar to the geospatial exercise).
Let's go ahead and use this to install our dependencies.

From Terminal or Anaconda Prompt run:
```bash
conda env create -f environment.yaml
conda activate sql-connection
jupyter notebook
```

## Connecting to a database in python (basic)

```python
import pandas as pd
from sqlalchemy import create_engine

# establish a database connection
engine = create_engine("postgres+psycop2://postgres:postgres@localhost:5432/LahmanBaseball")

# use the connection to run a query using pandas!
df = pd.read_sql("SELECT * FROM batting;", con=engine)
df.head()
```

There are 2 notebooks already in the repo that step through additional ways for connecting.

### Questions
_these are just a subset of questions from the original Lahman Baseball exercise_

* Find all players in the database who played at Vanderbilt University.
Create a list showing each player’s first and last names as well as the total salary they earned in the major leagues.
Sort this list in descending order by the total salary earned.
Which Vanderbilt player earned the most money in the majors?
* Using the fielding table, group players into three groups based on their position: label players with position OF as "Outfield", those with position "SS", "1B", "2B", and "3B" as "Infield", and those with position "P" or "C" as "Battery".
Determine the number of putouts made by each of these three groups in 2016.
* Find the player who had the most success stealing bases in 2016, where __success__ is measured as the percentage of stolen base attempts which are successful.
(A stolen base attempt results either in a stolen base or being caught stealing.)
Consider only players who attempted _at least_ 20 stolen bases.
* From 1970 – 2016, what is the largest number of wins for a team that did not win the world series?
What is the smallest number of wins for a team that did win the world series?
Doing this will probably result in an unusually small number of wins for a world series champion – determine why this is the case.
Then redo your query, excluding the problem year.
How often from 1970 – 2016 was it the case that a team with the most wins also won the world series?
What percentage of the time?
* Which managers have won the TSN Manager of the Year award in both the National League (NL) and the American League (AL)?
Give their full name and the teams that they were managing when they won the award.

### Bonus Questions!
* Analyze all the colleges in the state of Tennessee.
Which college has had the most success in the major leagues.
Use whatever metric for success you like - number of players, number of games, salaries, world series wins, etc.

* Is there any correlation between number of wins and team salary?
Use data from 2000 and later to answer this question.
As you do this analysis, keep in mind that salaries across the whole league tend to increase together, so you may want to look on a year-by-year basis.

* It is thought that since left-handed pitchers are more rare, causing batters to face them less often, that they are more effective.
Investigate this claim and present evidence to either support or dispute this claim.
First, determine just how rare left-handed pitchers are compared with right-handed pitchers.
Are left-handed pitchers more likely to win the Cy Young Award?
Are they more likely to make it into the hall of fame?
