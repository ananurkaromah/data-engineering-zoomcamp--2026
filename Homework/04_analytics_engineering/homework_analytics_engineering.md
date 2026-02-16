## Module 4 homework_analytics_engineering
This document contains the complete solutions for **Module 4 Homework**  
(Data Engineering Zoomcamp 2026 – DataTalksClub).

---

###  Ana Nurkaromah

#### Q1: dbt run --select int_trips_unioned builds which models?
**▶️ Command**
```dbt run --select int_trips_unioned```

🔎 Explanation
The --select flag in dbt runs only the specified model without including upstream (+) or downstream dependencies.
Since no dependency operator is added, dbt will build only the selected model.

**✅ Final Answer**
int_trips_unioned only
<br /> 
<br />

#### Q2: New value 6 appears in payment_type. What happens on dbt test?
**▶️ Command**
dbt test

🔎 Explanation
If a new unexpected value appears and the model has an accepted_values test defined for payment_type, dbt will fail the test.

dbt returns a non-zero exit code when a test fails.

**✅ Final Answer : dbt fails the test with non-zero exit code**
<br /> 
<br />

#### Q3: Count of records in fct_monthly_zone_revenue?
**▶️ Command**
```
SELECT COUNT(*)
FROM {{ ref('fct_monthly_zone_revenue') }};

(or directly from warehouse)

SELECT COUNT(*)
FROM analytics.fct_monthly_zone_revenue;
```

📊 Output: 12184

**✅ Final Answer : 12,184**
<br /> 
<br />

#### Q4: Zone with highest revenue for Green taxis in 2020?
**▶️ Command**
```
SELECT 
    zone,
    SUM(total_amount) AS total_revenue
FROM analytics.fct_trips
WHERE service_type = 'Green'
  AND EXTRACT(YEAR FROM pickup_datetime) = 2020
GROUP BY zone
ORDER BY total_revenue DESC
LIMIT 1;
```

📊 Output: East Harlem North

**✅ Final Answer : East Harlem North**
<br /> 
<br />

#### Q5: Total trips for Green taxis in October 2019?
**▶️ Command**
```
SELECT COUNT(*) 
FROM analytics.fct_trips
WHERE service_type = 'Green'
  AND EXTRACT(YEAR FROM pickup_datetime) = 2019
  AND EXTRACT(MONTH FROM pickup_datetime) = 10;
```
📊 Output: 384624

**✅ Final Answer : 384,624**
<br /> 
<br /> 

#### Q6: Count of records in stg_fhv_tripdata (filter dispatching_base_num IS NULL)?
**▶️ Command**
```
SELECT COUNT(*)
FROM analytics.stg_fhv_tripdata
WHERE dispatching_base_num IS NULL;
```
📊 Output: 43244693

**✅ Final Answer: 43,244,693**