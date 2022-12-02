# Data Engineer Take Home

Welcome!  You’ve advanced to the stage where we want to get a feel for how you use code to solve problems.  

## Why we do this

We want to get a sense for your technical, analytical, and communication skills: coding, systems design, analysis, and writing.

## How we score your test response

We'll score your submission against a rubric of items in two categories:

Technical skill:

* Code. Most data pipeline type tasks require writing code, and this is something we'll expect you to do quite often. We like code that is easy to read and maintain, performance usually comes second. We like to say make it work, then make it fast.
* Integration. Writing code is only a part of deploying a service, at the end of this exercise we'd like to understand how you think in terms of deploying code to production. As this is an exercise, we encourage you to do what you can in terms of the assignment and describe additional steps you might take in a real-world scenario in the writeup

Non-technical skill:

* Requirement Analysis.  Requests for data ingestion come at various levels of specificity. We’ll evaluate your understanding of the requirements and the steps you took to satisfy them.
* Simplicity.  Is your solution easy to understand? Is the route you took to get to an answer as simple as it should be but no more?
* Communication.  Because Upshot is 100% remote, we place a high value on written communication.  We’ll evaluate the clarity of your reasoning, and the completeness of your writing.

If you pass the test, we'll then get on a video call where you'll present your solution and go through a technical interview with more members of our team. You'll want to come prepared with any further questions you have about Upshot, the team, or the role.

## Guidelines

* Please time-box the exercise to a few hours. You have one week from the day we sent you the exercise to send us your submission.
* If you need any help or clarification, email us.
* As you proceed, use a Git repository to host all your files.
* Submit your results as a [Git Bundle](https://utappia.org/2015/04/27/git-bundle-backup/) that you submit via the link your recruiter sent at the bottom of the email where we shared the assignment. Do _not_ post your git repo publicly anywhere on the internet.
* Do not include the source data in your Git repository or resultant archive.
* We expect your solution to contain all the instructions to reproduce the environment you used to run this test

## Tasks

### Overview

This test simulates a data pipeline where your application will ingest data from an API, store the files, transform the data into tabular form and load the data into a relational database. Finally you will export a summary of the data into a CSV file.

### Part zero: Setup your containerized environment

docker-compose file to specify two services
- a Postgres database container
- a container to run your your python code

### Part one: Extract the data

Write code to ingest data from the API endpoints:

* [competitions](https://api.football-data.org/v4/competitions)
* [teams within the competitions](https://api.football-data.org/v4/competitions/{id}/teams)

Take care to adhere to clean coding principles and follow usual best practices, especially with regard to code readability.

You can find the full documentation for the API [here](https://www.football-data.org/documentation/quickstart)

You should apply for an API Key [here](https://www.football-data.org/client/register).

Expect the API to be throttled so ensure you handle the rate limits appropriately.

### Part two: store the data in files

To help you trace and debug your data pipeline, files that have been extracted from the API endpoints should be persisted on a local folder. Feel free to partition the folder in a way that make sense and allow you to observe what your application is doing over multiple runs.

### Part three: Load a subset of the data into Postgres tables

Create the following tables in the local database:

   **dim_teams** - stores the id and names of the football teams e.g.
   | id    | name         |
   |-------|--------------|
   | 1234  | Liverpool FC |

   **dim_competitions** - stores the id and names of the competitions e.g.

   | id    | name            |
   |-------|-----------------|
   | 234   | Premiere League |

   **fact_competitions** - stores the records of teams that played in each of the competitions e.g.
   | competition_id | team_id    |
   |----------------|------------|
   |   3456         |  987       |

Transform and load the data you've extracted from the API into the 3 tables listed above.

### Part three: Export a summary CSV

Export a summary of the data. The summary should indicate the number of teams per competition in descending order. Store the results in a `csv` file in the `outputs` folder

If you have extracted and loaded the data correctly, the summary should match the table below:

| Competition    |  Number of Teams    |
|----------------|---------------------|
| Copa Libertadores | 47 |
| UEFA Champions League | 46 |
| FIFA World Cup | 32 |
| European Championship | 24 |
| Championship | 24 |
| Serie A | 20 |
| Primera Division | 20 |
| Premier League | 20 |
| Ligue 1 | 20 |
| Campeonato Brasileiro Série A | 20 |
| Primeira Liga | 18 |
| Eredivisie | 18 |
| Bundesliga | 18 |

### Part four: documentation

Add the following documentation to the `README` file:

1. Explain how to run the code and the setup you documented in parts one, two, and three.
2. Include any packaging steps we may need to follow.
3. Explain the tools you used and the thought process of why you picked a specific tool or approach.

Include all of the above documentation, including the `README`, along with all of your code in a git bundle that you send back to us.

### Notes on completing these tasks

* There is no right way to do this. We are interested in the choices that you make, how you justify them, and your development process.
* Make sure that your code is executable and contain all the instruction on how to recreate the environment with the required package dependencies.
* Consider what kind of error handling, logging and testing is appropriate. Note that APIs have rate limits so your application should handle that.
* All data loaded into the Postgres database should be persisted.
* You are allowed to use any packages or tools that you see fit to get the task done. Be prepared to discuss your choices in the interview.
