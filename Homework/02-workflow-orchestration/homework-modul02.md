# Module 2 Homework: workflow_orchestration

This document contains the complete solutions for **Module 2 Homework**  
(Data Engineering Zoomcamp 2026 – DataTalksClub).

All commands, SQL queries, and answers are included directly in this Markdown file as required.

---

##  Ana Nurkaromah

- Homework: Modul_02_workflow_orchestration
- Topic: workflow_orchestration - kestra
- Dataset: 
  NYC TLC Taxi datasets provided by DataTalksClub:

  https://github.com/DataTalksClub/nyc-tlc-data/releases/tag/green

  The download links follow the pattern:

  https://github.com/DataTalksClub/nyc-tlc-data/releases/download/{taxi}/{file}.gz

- Extend the existing ETL workflows to process **NYC Yellow and Green Taxi data** for the year **2021 (January – July)**.

## Question 1.
### Task
Within the execution for `Yellow` Taxi data for the year `2020` and month `12`: what is the uncompressed file size (i.e. the output file `yellow_tripdata_2020-12.csv` of the `extract` task)?
- 128.3 MB
- 134.5 MB
- 364.7 MB
- 692.6 MB

### Command
🛠 Tools Used
- Kestra
- PostgreSQL
- Docker
- NYC TLC Taxi Dataset

Kestra -> Executions -> Output (for yellow 12/2020)
-> extract | outputFiles | yellow-tripdata_2020-12.csv
128.3 MiB

Kestra reports file size in **MiB**:

### Answer
:white_check_mark:**128.3 MiB**


## Question 2.
### Task
What is the rendered value of the variable `file` when the inputs `taxi` is set to `green`, `year` is set to `2020`, and `month` is set to `04` during execution?
- `{{inputs.taxi}}_tripdata_{{inputs.year}}-{{inputs.month}}.csv` 
- `green_tripdata_2020-04.csv`
- `green_tripdata_04_2020.csv`
- `green_tripdata_2020.csv`

### Command
we use render to get the string when variable inputs are involved, thus the
output here would not be choice 1, but that is actually our file variable format, so just 
'plug and chug' here to get your answer.

Variable definition:
```jinja
{{inputs.taxi}}_tripdata_{{inputs.year}}-{{inputs.month}}.csv
```

### Answer
:white_check_mark:**`green_tripdata_2020-04.csv`**


## Question 3. 
### Task
How many rows are there for the `Yellow` Taxi data for all CSV files in the year 2020?
- 13,537.299
- 24,648,499
- 18,324,219
- 29,430,127

### Command
Verification method:
-Checked total rows after loading all Yellow Taxi 2020 CSV files
-Verified in BigQuery table details

### Answer
:white_check_mark: **24,648,499**



## Question 4.
### Task
How many rows are there for the `Green` Taxi data for all CSV files in the year 2020?
- 5,327,301
- 936,199
- 1,734,051
- 1,342,034

### Command
Explanation:
-Green Taxi data for 2020 is not available for all months
-Row count reflects only months with existing data
-Verified in BigQuery table details after ETL execution

### Answer
:white_check_mark: ANSWER **1,734,051**


## Question 5.
### Task
How many rows are there for the `Yellow` Taxi data for the March 2021 CSV file?
- 1,428,092
- 706,911
- 1,925,152
- 2,561,031


### Answer
:white_check_mark: ANSWER **1,925,152**


## Question 6.
### Task
How would you configure the timezone to New York in a Schedule trigger?
- Add a `timezone` property set to `EST` in the `Schedule` trigger configuration  
- Add a `timezone` property set to `America/New_York` in the `Schedule` trigger configuration
- Add a `timezone` property set to `UTC-5` in the `Schedule` trigger configuration
- Add a `location` property set to `New_York` in the `Schedule` trigger configuration  

### Answer
:white_check_mark: ANSWER **`America/New_York`**

