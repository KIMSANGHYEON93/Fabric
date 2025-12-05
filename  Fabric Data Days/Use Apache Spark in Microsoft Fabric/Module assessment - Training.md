---
title: "Module assessment - Training"
source: "https://learn.microsoft.com/en-us/training/modules/use-apache-spark-work-files-lakehouse/8-knowledge-check"
author:
  - "[[theresa-i]]"
published:
created: 2025-12-03
description: "Knowledge check"
tags:
  - "clippings"
---
## 모듈 평가

완전한 200 경험치

- 10분

이 평가는 모듈에 대한 이해도를 평가합니다. 이전과는 달리, 개별 답변에 대한 피드백은 제공되지 않고 정답 여부만 제공됩니다. 이는 학습 내용을 측정하기 위한 것입니다. 시작하기 전에 모듈 자료를 충분히 검토하세요.

AI가 생성한 콘텐츠 이 모듈 평가의 질문과 답변 선택지는 AI를 사용하여 생성되었으며 인간 작성자가 검토했습니다.

---

1. Your organization needs to analyze customer data stored in a lakehouse and visualize demographic distributions using Spark in Microsoft Fabric. Which Spark feature would facilitate this analysis?

- Built-in machine learning algorithms for customer segmentation.
- **Dataframe API for structured data manipulation and Spark SQL for querying. (Correct)**
- RDDs for unstructured data processing.

2. What is the expected result of executing the following PySpark command: `df.groupBy('Category').agg({'SalesAmount': 'sum'})`?

- **A new dataframe with each category and the sum of sales amounts for each category. (Correct)**
- A list of categories with their corresponding total sales amounts.
- A dataframe with each category and the average sales amounts for each category.

3. When creating a custom environment in Microsoft Fabric, which setting allows you to use a specific version of Apache Spark for your tasks?

- Choose the node family type in the Spark pool configuration.
- **Specify the Spark runtime in the environment settings. (Correct)**
- Enable high concurrency mode in the workspace settings.

4. You have created a dataframe from a CSV file and want to save it as a Delta table in the Spark catalog for future SQL queries. Which method should you use?

- `df.write.mode("overwrite").parquet("path")`
- **`df.write.format("delta").saveAsTable("table_name")` (Correct)**
- `df.createOrReplaceTempView("view_name")`

5. Which SQL magic command should you use in a Microsoft Fabric notebook to execute SQL queries directly?

- `%%pyspark`
- **`%%sql` (Correct)**
- `%%spark`

6. In Microsoft Fabric, what is the purpose of setting a default Spark pool in a workspace?

- To limit the number of Spark jobs that can run concurrently in the workspace.
- **To automatically assign a Spark pool to jobs when no specific pool is specified. (Correct)**
- To enforce the use of memory optimized nodes for all tasks.

7. Which Spark Dataframe method is most efficient for finding the maximum value in a column of numerical data?

- **agg (Correct)**
- groupBy
- filter

8. Which practice should be followed to optimize data processing performance in a Spark pool using the native execution engine in Microsoft Fabric?

- Set the Spark pool to use CPU optimized nodes exclusively.
- **Enable the native execution engine at the environment level by setting relevant Spark properties. (Correct)**
- Disable dynamic allocation to ensure consistent resource allocation.

9. You have a dataframe with a column named 'Date' in a string format, and you need to convert it to a date format for further analysis. Which PySpark method would you use?

- selectExpr
- filter
- **withColumn (Correct)**

---

## 피드백

이 페이지가 도움이 되었나요?

아니요

원본 텍스트

번역 평가

보내주신 의견은 Google 번역을 개선하는 데 사용됩니다.