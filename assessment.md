### Data Manipulation

---

#### Renaming attributes to improve query efficiency and adhere to naming conventions

```sql

EXEC sp_rename 'dbo.sample_data.Current Status', 'current_status', 'COLUMN';

```

```sql

EXEC sp_rename 'dbo.sample_data.Initially Signed Up Date', 'initial_signup_date', 'COLUMN';

```

```sql

EXEC sp_rename 'dbo.sample_data.Source', 'source', 'COLUMN';

```

```sql

EXEC sp_rename 'dbo.sample_data.Week No', 'week_number', 'COLUMN';

```

After basic EDA an outlier was found, where the signup date was in 2030. This datapoint was kept in the set as the other information is no doubt applicable. 

---

#### Business task 1

- What is the overall “Sign up Started” -> “Completed Training” conversion rate by week
(assume the first week starts on 4/1/23 and ends 4/7/23)?

---

Below is a CTE to calculate the conversion rate for week 1:

```sql

WITH Status_Counts AS 
	(SELECT
		SUM(CASE WHEN current_status = 'Signed Up Started' THEN 1 ELSE 0 END) AS signed_up,
		SUM(CASE WHEN current_status = 'Completed Training' THEN 1 ELSE 0 END) AS completed_training
		FROM sample_data
		WHERE week_number = 'Week 1'
)
SELECT
	signed_up,
	completed_training,
	CASE
		WHEN signed_up = 0 THEN 0
		ELSE (completed_training * 100 / signed_up)
	END AS conversion_rate_week_1
FROM Status_Counts

```

Results below:

![image](https://github.com/user-attachments/assets/e48ec368-2b35-4355-91bb-989fb6c1f60a)

---

Below is a CTE to calculate the conversion rate for week 2:

```sql

WITH Status_Counts AS 
	(SELECT
		SUM(CASE WHEN current_status = 'Signed Up Started' THEN 1 ELSE 0 END) AS signed_up,
		SUM(CASE WHEN current_status = 'Completed Training' THEN 1 ELSE 0 END) AS completed_training
		FROM sample_data
		WHERE week_number = 'Week 2'
)
SELECT
	signed_up,
	completed_training,
	CASE
		WHEN signed_up = 0 THEN 0
		ELSE (completed_training * 100 / signed_up)
	END AS conversion_rate_week_2
FROM Status_Counts

```

Query results below: 

![image](https://github.com/user-attachments/assets/d953bd47-0271-4141-9217-99e9f6a65f22)

---

Below is a CTE to calculate the conversion rate for week 3:

```sql

WITH Status_Counts AS 
	(SELECT
		SUM(CASE WHEN current_status = 'Signed Up Started' THEN 1 ELSE 0 END) AS signed_up,
		SUM(CASE WHEN current_status = 'Completed Training' THEN 1 ELSE 0 END) AS completed_training
		FROM sample_data
		WHERE week_number = 'Week 3'
)
SELECT
	signed_up,
	completed_training,
	CASE
		WHEN signed_up = 0 THEN 0
		ELSE (completed_training * 100 / signed_up)
	END AS conversion_rate_week_3
FROM Status_Counts

```

Query results below: 

![image](https://github.com/user-attachments/assets/38492895-7d4c-4784-b6c0-7b194be6a7bd)

---

Below is a CTE to calculate the conversion rate for week 4:

```sql

WITH Status_Counts AS 
	(SELECT
		SUM(CASE WHEN current_status = 'Signed Up Started' THEN 1 ELSE 0 END) AS signed_up,
		SUM(CASE WHEN current_status = 'Completed Training' THEN 1 ELSE 0 END) AS completed_training
		FROM sample_data
		WHERE week_number = 'Week 4'
)
SELECT
	signed_up,
	completed_training,
	CASE
		WHEN signed_up = 0 THEN 0
		ELSE (completed_training * 100 / signed_up)
	END AS conversion_rate_week_4
FROM Status_Counts

```

Query results below:

![image](https://github.com/user-attachments/assets/709e3f77-a7cf-4b05-86aa-0b661d5e7d20)


---

#### Business task 2

- How has the overall conversion rate changed over time?

---

For this task, I exported the edited dataset for use in Tableau.

The most applicable chart type for this business task would be a line chart to show the conversion rate change over the one month period.

Line Chart below: 

![image](https://github.com/user-attachments/assets/395480dd-5bbb-434b-a81c-ad3ba53c2ac0)

Observations are as follows:

- The conversion rate was substantially higher in weeks 1 and 2, being up at 88% consistently.
- The conversion rate was lowest during week 3 at 47%, climbing to 66% in week 4.
- Important to note that although conversion rates are lower for week 3 and 4, the actual count of users converting was drastically higher in weeks 3 and 4.

---

#### Business Task 3

- What is the main reason that the overall conversion rate changed so drastically?

For this question, a stacked bar chart would best display these data.

![image](https://github.com/user-attachments/assets/a340db4d-a8b6-4e7f-b44a-f622e56e8483)

Observations are as follows: 

- Clear peaks of user engagement are observed in weeks 3 and 4 of the month, with email campaigns and paid social media interactions being far higher. This is supported by the conversions showed previously, suggesting a correlation between higher engagement and higher conversions.

---

### Business Task 4

- Only that there is an outlier that contains a date of 2030
- Other than that I have run out of time! 

  
