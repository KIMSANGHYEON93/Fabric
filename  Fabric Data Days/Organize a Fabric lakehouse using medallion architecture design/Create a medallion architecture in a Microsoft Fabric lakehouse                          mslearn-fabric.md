---
title: "Create a medallion architecture in a Microsoft Fabric lakehouse |                         mslearn-fabric"
source: "https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/03b-medallion-lakehouse.html"
author:
published:
created: 2025-12-03
description:
tags:
  - "clippings"
---
## Microsoft Fabric 레이크하우스에서 메달리온 아키텍처 만들기

이 연습에서는 노트북을 사용하여 Fabric 레이크하우스에 메달리온 아키텍처를 구축합니다. 작업 공간을 만들고, 레이크하우스를 생성하고, 브론즈 레이어에 데이터를 업로드하고, 데이터를 변환하여 실버 델타 테이블에 로드하고, 다시 데이터를 변환하여 골드 델타 테이블에 로드한 후, 시맨틱 모델을 탐색하고 관계를 생성합니다.

**이 운동을 완료하는 데 약 45** 분이 소요됩니다.

> \[!참고\] 이 연습을 완료하려면 [Microsoft Fabric 테넌트](https://learn.microsoft.com/fabric/get-started/fabric-trial) 에 액세스해야 합니다.

## 작업 공간 만들기

Fabric에서 데이터 작업을 하기 전에 Fabric 평가판을 활성화하여 작업 공간을 만드세요.

1. 브라우저 에서 [Microsoft Fabric 홈페이지](https://app.fabric.microsoft.com/home?experience=fabric-developer) 로 이동하여 `https://app.fabric.microsoft.com/home?experience=fabric-developer` Fabric 자격 증명을 사용하여 로그인합니다.
2. 왼쪽 메뉴 모음에서 **작업 공간을** 선택하세요 (아이콘은 🗇와 비슷합니다).
3. 원하는 이름으로 새 작업 공간을 만들고, **고급 섹션에서 Fabric 용량(** *평가판*, *프리미엄* 또는 *Fabric* ) 을 포함하는 라이선스 모드를 선택합니다 .
4. 새 작업 공간이 열리면 비어 있어야 합니다.
	[![Fabric의 빈 작업 공간 스크린샷.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/new-workspace.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/new-workspace.png)

## 레이크하우스를 만들고 청동 레이어에 데이터를 업로드하세요

이제 작업 공간이 생겼으니 분석할 데이터를 위한 데이터 레이크하우스를 만들 차례입니다.

1. 방금 만든 작업 공간에서 **\+ 새 항목** 버튼을 선택하여 **Sales** 라는 이름의 새 **Lakehouse를** 만듭니다.
	약 1분 후, 비어 있는 새 레이크하우스가 생성됩니다. 다음으로, 분석을 위해 데이터 레이크하우스에 데이터를 수집합니다. 여러 가지 방법이 있지만, 이 연습에서는 로컬 컴퓨터(또는 해당되는 경우 랩 VM)에 텍스트 파일을 다운로드한 후 레이크하우스에 업로드합니다.
2. 이 연습에 필요한 데이터 파일을 에서 다운로드하세요 `https://github.com/MicrosoftLearning/dp-data/blob/main/orders.zip`. 파일을 추출하여 로컬 컴퓨터(또는 해당되는 경우 랩 VM)에 원래 이름으로 저장하세요. 3년간의 판매 데이터가 포함된 파일 3개(2019.csv, 2020.csv, 2021.csv)가 있어야 합니다.
3. 레이크하우스가 있는 웹 브라우저 탭으로 돌아가서 **탐색기 창의** **파일** 폴더 에 대한 **... 메뉴에서** **새 하위 폴더를** 선택 하고 **bronze** 라는 이름의 폴더를 만듭니다 .
4. In the **…** menu for the **bronze** folder, select **Upload** and **Upload files**, and then upload the 3 files (2019.csv, 2020.csv, and 2021.csv) from your local computer (or lab VM if applicable) to the lakehouse. Use the shift key to upload all 3 files at once.
5. After the files have been uploaded, select the **bronze** folder; and verify that the files have been uploaded, as shown here:
	[![Screenshot of uploaded products.csv file in a lakehouse.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/bronze-files.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/bronze-files.png)

## Transform data and load to silver Delta table

Now that you have some data in the bronze layer of your lakehouse, you can use a notebook to transform the data and load it to a delta table in the silver layer.

1. On the **Home** page while viewing the contents of the **bronze** folder in your data lake, in the **Open notebook** menu, select **New notebook**.
	After a few seconds, a new notebook containing a single *cell* will open. Notebooks are made up of one or more cells that can contain *code* or *markdown* (formatted text).
2. When the notebook opens, rename it to `Transform data for Silver` by selecting the **Notebook xxxx** text at the top left of the notebook and entering the new name.
	[![Screenshot of a new notebook named Transform data for silver.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/sales-notebook-rename.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/sales-notebook-rename.png)
3. Select the existing cell in the notebook, which contains some simple commented-out code. Highlight and delete these two lines - you will not need this code.
	> **Note**: Notebooks enable you to run code in a variety of languages, including Python, Scala, and SQL. In this exercise, you’ll use PySpark and SQL. You can also add markdown cells to provide formatted text and images to document your code.
4. **Paste** the following code into the cell:
	code
	```python
	from pyspark.sql.types import *
	    
	# Create the schema for the table
	orderSchema = StructType([
	    StructField("SalesOrderNumber", StringType()),
	    StructField("SalesOrderLineNumber", IntegerType()),
	    StructField("OrderDate", DateType()),
	    StructField("CustomerName", StringType()),
	    StructField("Email", StringType()),
	    StructField("Item", StringType()),
	    StructField("Quantity", IntegerType()),
	    StructField("UnitPrice", FloatType()),
	    StructField("Tax", FloatType())
	    ])
	    
	# Import all files from bronze folder of lakehouse
	df = spark.read.format("csv").option("header", "false").schema(orderSchema).load("Files/bronze/*.csv")
	    
	# Display the first 10 rows of the dataframe to preview your data
	display(df.head(10))
	```
5. Use the **\*\*▷** (*Run cell*)\*\* button on the left of the cell to run the code.
	> **Note**: Since this is the first time you’ve run any Spark code in this notebook, a Spark session must be started. This means that the first run can take a minute or so to complete. Subsequent runs will be quicker.
6. When the cell command has completed, **review the output** below the cell, which should look similar to this:
	| Index | SalesOrderNumber | SalesOrderLineNumber | OrderDate | CustomerName | Email | Item | Quantity | UnitPrice | Tax |
	| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
	| 1 | SO49172 | 1 | 2021-01-01 | Brian Howard | brian23@adventure-works.com | Road-250 Red, 52 | 1 | 2443.35 | 195.468 |
	| 2 | SO49173 | 1 | 2021-01-01 | Linda Alvarez | linda19@adventure-works.com | Mountain-200 Silver, 38 | 1 | 2071.4197 | 165.7136 |
	| … | … | … | … | … | … | … | … | … | … |
	The code you ran loaded the data from the CSV files in the **bronze** folder into a Spark dataframe, and then displayed the first few rows of the dataframe.
	> **Note**: You can clear, hide, and auto-resize the contents of the cell output by selecting the **…** menu at the top left of the output pane.
7. Now you’ll **add columns for data validation and cleanup**, using a PySpark dataframe to add columns and update the values of some of the existing columns. Use the **\+ Code** button to **add a new code block** and add the following code to the cell:
	code
	```python
	from pyspark.sql.functions import when, lit, col, current_timestamp, input_file_name
	    
	# Add columns IsFlagged, CreatedTS and ModifiedTS
	df = df.withColumn("FileName", input_file_name()) \
	    .withColumn("IsFlagged", when(col("OrderDate") < '2019-08-01',True).otherwise(False)) \
	    .withColumn("CreatedTS", current_timestamp()).withColumn("ModifiedTS", current_timestamp())
	    
	# Update CustomerName to "Unknown" if CustomerName null or empty
	df = df.withColumn("CustomerName", when((col("CustomerName").isNull() | (col("CustomerName")=="")),lit("Unknown")).otherwise(col("CustomerName")))
	```
	The first line of the code imports the necessary functions from PySpark. You’re then adding new columns to the dataframe so you can track the source file name, whether the order was flagged as being a before the fiscal year of interest, and when the row was created and modified.
	Finally, you’re updating the CustomerName column to “Unknown” if it’s null or empty.
8. Run the cell to execute the code using the **\*\*▷** (*Run cell*)\*\* button.
9. Next, you’ll define the schema for the **sales\_silver** table in the sales database using Delta Lake format. Create a new code block and add the following code to the cell:
	code
	```python
	# Define the schema for the sales_silver table
	    
	from pyspark.sql.types import *
	from delta.tables import *
	    
	DeltaTable.createIfNotExists(spark) \
	    .tableName("sales.sales_silver") \
	    .addColumn("SalesOrderNumber", StringType()) \
	    .addColumn("SalesOrderLineNumber", IntegerType()) \
	    .addColumn("OrderDate", DateType()) \
	    .addColumn("CustomerName", StringType()) \
	    .addColumn("Email", StringType()) \
	    .addColumn("Item", StringType()) \
	    .addColumn("Quantity", IntegerType()) \
	    .addColumn("UnitPrice", FloatType()) \
	    .addColumn("Tax", FloatType()) \
	    .addColumn("FileName", StringType()) \
	    .addColumn("IsFlagged", BooleanType()) \
	    .addColumn("CreatedTS", DateType()) \
	    .addColumn("ModifiedTS", DateType()) \
	    .execute()
	```
10. Run the cell to execute the code using the **\*\*▷** (*Run cell*)\*\* button.
11. Select the **…** in the Tables section of the Explorer pane and select **Refresh**. You should now see the new **sales\_silver** table listed. The **▲** (triangle icon) indicates that it’s a Delta table.
	> **Note**: If you don’t see the new table, wait a few seconds and then select **Refresh** again, or refresh the entire browser tab.
12. Now you’re going to perform an **upsert operation** on a Delta table, updating existing records based on specific conditions and inserting new records when no match is found. Add a new code block and paste the following code:
	code
	```python
	# Update existing records and insert new ones based on a condition defined by the columns SalesOrderNumber, OrderDate, CustomerName, and Item.
	from delta.tables import *
	    
	deltaTable = DeltaTable.forPath(spark, 'Tables/sales_silver')
	    
	dfUpdates = df
	    
	deltaTable.alias('silver') \
	  .merge(
	    dfUpdates.alias('updates'),
	    'silver.SalesOrderNumber = updates.SalesOrderNumber and silver.OrderDate = updates.OrderDate and silver.CustomerName = updates.CustomerName and silver.Item = updates.Item'
	  ) \
	   .whenMatchedUpdate(set =
	    {
	          
	    }
	  ) \
	 .whenNotMatchedInsert(values =
	    {
	      "SalesOrderNumber": "updates.SalesOrderNumber",
	      "SalesOrderLineNumber": "updates.SalesOrderLineNumber",
	      "OrderDate": "updates.OrderDate",
	      "CustomerName": "updates.CustomerName",
	      "Email": "updates.Email",
	      "Item": "updates.Item",
	      "Quantity": "updates.Quantity",
	      "UnitPrice": "updates.UnitPrice",
	      "Tax": "updates.Tax",
	      "FileName": "updates.FileName",
	      "IsFlagged": "updates.IsFlagged",
	      "CreatedTS": "updates.CreatedTS",
	      "ModifiedTS": "updates.ModifiedTS"
	    }
	  ) \
	  .execute()
	```
13. Run the cell to execute the code using the **\*\*▷** (*Run cell*)\*\* button.
	This operation is important because it enables you to update existing records in the table based on the values of specific columns, and insert new records when no match is found. This is a common requirement when you’re loading data from a source system that may contain updates to existing and new records.
	You now have data in your silver delta table that is ready for further transformation and modeling.
14. After running the last cell, select the **Run** tab above the ribbon and then select **Stop session** to stop the compute resource being used by the notebook.

## Explore data in the silver layer using the SQL endpoint

Now that you have data in your silver layer, you can use the SQL analytics endpoint to explore the data and perform some basic analysis. This is useful if you’re familiar with SQL and want to do some basic exploration of your data. In this exercise we’re using the SQL endpoint view in Fabric, but you can use other tools like SQL Server Management Studio (SSMS) and Azure Data Explorer.

1. Navigate back to your workspace and notice that you now have several items listed. Select the **Sales SQL analytics endpoint** to open your lakehouse in the SQL analytics endpoint view.
	[![Screenshot of the SQL endpoint in a lakehouse.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/sql-endpoint-item.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/sql-endpoint-item.png)
2. Select **New SQL query** from the ribbon, which will open a SQL query editor. Note that you can rename your query using the **…** menu item next to the existing query name in the Explorer pane.
	Next, you’ll run two sql queries to explore the data.
3. Paste the following query into the query editor and select **Run**:
	sql
	```sql
	SELECT YEAR(OrderDate) AS Year
	    , CAST (SUM(Quantity * (UnitPrice + Tax)) AS DECIMAL(12, 2)) AS TotalSales
	FROM sales_silver
	GROUP BY YEAR(OrderDate) 
	ORDER BY YEAR(OrderDate)
	```
	This query calculates the total sales for each year in the sales\_silver table. Your results should look like this:
	[![Screenshot of the results of a SQL query in a lakehouse.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/total-sales-sql.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/total-sales-sql.png)
4. Next you’ll review which customers are purchasing the most (in terms of quantity). Paste the following query into the query editor and select **Run**:
	sql
	```sql
	SELECT TOP 10 CustomerName, SUM(Quantity) AS TotalQuantity
	FROM sales_silver
	GROUP BY CustomerName
	ORDER BY TotalQuantity DESC
	```
	This query calculates the total quantity of items purchased by each customer in the sales\_silver table, and then returns the top 10 customers in terms of quantity.
	Data exploration at the silver layer is useful for basic analysis, but you’ll need to transform the data further and model it into a star schema to enable more advanced analysis and reporting. You’ll do that in the next section.

## Transform data for gold layer

You have successfully taken data from your bronze layer, transformed it, and loaded it into a silver Delta table. Now you’ll use a new notebook to transform the data further, model it into a star schema, and load it into gold Delta tables.

You could have done all of this in a single notebook, but for this exercise you’re using separate notebooks to demonstrate the process of transforming data from bronze to silver and then from silver to gold. This can help with debugging, troubleshooting, and reuse.

1. Return to the workspace home page and create a new notebook called `Transform data for Gold`.
2. In the Explorer pane, add your **Sales** lakehouse by selecting **Add data items** and then selecting the **Sales** lakehouse you created earlier. You should see the **sales\_silver** table listed in the **Tables** section of the explorer pane.
3. In the existing code block, remove the commented text and **add the following code** to load data to your dataframe and start building your star schema, then run it:
	code
	```python
	# Load data to the dataframe as a starting point to create the gold layer
	df = spark.read.table("Sales.sales_silver")
	```
	> **Note**: If you receive a `[TooManyRequestsForCapacity]` error when running the first cell, make sure you stopped the session previously running in the first notebook.
4. **Add a new code block** and paste the following code to create your date dimension table and run it:
	code
	```python
	from pyspark.sql.types import *
	from delta.tables import*
	    
	# Define the schema for the dimdate_gold table
	DeltaTable.createIfNotExists(spark) \
	    .tableName("sales.dimdate_gold") \
	    .addColumn("OrderDate", DateType()) \
	    .addColumn("Day", IntegerType()) \
	    .addColumn("Month", IntegerType()) \
	    .addColumn("Year", IntegerType()) \
	    .addColumn("mmmyyyy", StringType()) \
	    .addColumn("yyyymm", StringType()) \
	    .execute()
	```
	> **Note**: You can run the `display(df)` command at any time to check the progress of your work. In this case, you’d run ‘display(dfdimDate\_gold)’ to see the contents of the dimDate\_gold dataframe.
5. In a new code block, **add and run the following code** to create a dataframe for your date dimension, **dimdate\_gold**:
	code
	```python
	from pyspark.sql.functions import col, dayofmonth, month, year, date_format
	    
	# Create dataframe for dimDate_gold
	    
	dfdimDate_gold = df.dropDuplicates(["OrderDate"]).select(col("OrderDate"), \
	        dayofmonth("OrderDate").alias("Day"), \
	        month("OrderDate").alias("Month"), \
	        year("OrderDate").alias("Year"), \
	        date_format(col("OrderDate"), "MMM-yyyy").alias("mmmyyyy"), \
	        date_format(col("OrderDate"), "yyyyMM").alias("yyyymm"), \
	    ).orderBy("OrderDate")
	# Display the first 10 rows of the dataframe to preview your data
	display(dfdimDate_gold.head(10))
	```
6. You’re separating the code out into new code blocks so that you can understand and watch what’s happening in the notebook as you transform the data. In another new code block, **add and run the following code** to update the date dimension as new data comes in:
	code
	```python
	from delta.tables import *
	    
	deltaTable = DeltaTable.forPath(spark, 'Tables/dimdate_gold')
	    
	dfUpdates = dfdimDate_gold
	    
	deltaTable.alias('gold') \
	  .merge(
	    dfUpdates.alias('updates'),
	    'gold.OrderDate = updates.OrderDate'
	  ) \
	   .whenMatchedUpdate(set =
	    {
	          
	    }
	  ) \
	 .whenNotMatchedInsert(values =
	    {
	      "OrderDate": "updates.OrderDate",
	      "Day": "updates.Day",
	      "Month": "updates.Month",
	      "Year": "updates.Year",
	      "mmmyyyy": "updates.mmmyyyy",
	      "yyyymm": "updates.yyyymm"
	    }
	  ) \
	  .execute()
	```
	The date dimension is now set up. Now you’ll create your customer dimension.
7. To build out the customer dimension table, **add a new code block**, paste and run the following code:
	code
	```python
	from pyspark.sql.types import *
	from delta.tables import *
	    
	# Create customer_gold dimension delta table
	DeltaTable.createIfNotExists(spark) \
	    .tableName("sales.dimcustomer_gold") \
	    .addColumn("CustomerName", StringType()) \
	    .addColumn("Email",  StringType()) \
	    .addColumn("First", StringType()) \
	    .addColumn("Last", StringType()) \
	    .addColumn("CustomerID", LongType()) \
	    .execute()
	```
8. In a new code block, **add and run the following code** to drop duplicate customers, select specific columns, and split the “CustomerName” column to create “First” and “Last” name columns:
	code
	```python
	from pyspark.sql.functions import col, split
	    
	# Create customer_silver dataframe
	    
	dfdimCustomer_silver = df.dropDuplicates(["CustomerName","Email"]).select(col("CustomerName"),col("Email")) \
	    .withColumn("First",split(col("CustomerName"), " ").getItem(0)) \
	    .withColumn("Last",split(col("CustomerName"), " ").getItem(1)) 
	    
	# Display the first 10 rows of the dataframe to preview your data
	display(dfdimCustomer_silver.head(10))
	```
	Here you have created a new DataFrame dfdimCustomer\_silver by performing various transformations such as dropping duplicates, selecting specific columns, and splitting the “CustomerName” column to create “First” and “Last” name columns. The result is a DataFrame with cleaned and structured customer data, including separate “First” and “Last” name columns extracted from the “CustomerName” column.
9. Next we’ll **create the ID column for our customers**. In a new code block, paste and run the following:
	code
	```python
	from pyspark.sql.functions import monotonically_increasing_id, col, when, coalesce, max, lit
	    
	dfdimCustomer_temp = spark.read.table("Sales.dimCustomer_gold")
	    
	MAXCustomerID = dfdimCustomer_temp.select(coalesce(max(col("CustomerID")),lit(0)).alias("MAXCustomerID")).first()[0]
	    
	dfdimCustomer_gold = dfdimCustomer_silver.join(dfdimCustomer_temp,(dfdimCustomer_silver.CustomerName == dfdimCustomer_temp.CustomerName) & (dfdimCustomer_silver.Email == dfdimCustomer_temp.Email), "left_anti")
	    
	dfdimCustomer_gold = dfdimCustomer_gold.withColumn("CustomerID",monotonically_increasing_id() + MAXCustomerID + 1)
	# Display the first 10 rows of the dataframe to preview your data
	display(dfdimCustomer_gold.head(10))
	```
	Here you’re cleaning and transforming customer data (dfdimCustomer\_silver) by performing a left anti join to exclude duplicates that already exist in the dimCustomer\_gold table, and then generating unique CustomerID values using the monotonically\_increasing\_id() function.
10. Now you’ll ensure that your customer table remains up-to-date as new data comes in. **In a new code block**, paste and run the following:
	code
	```python
	from delta.tables import *
	deltaTable = DeltaTable.forPath(spark, 'Tables/dimcustomer_gold')
	    
	dfUpdates = dfdimCustomer_gold
	    
	deltaTable.alias('gold') \
	  .merge(
	    dfUpdates.alias('updates'),
	    'gold.CustomerName = updates.CustomerName AND gold.Email = updates.Email'
	  ) \
	   .whenMatchedUpdate(set =
	    {
	          
	    }
	  ) \
	 .whenNotMatchedInsert(values =
	    {
	      "CustomerName": "updates.CustomerName",
	      "Email": "updates.Email",
	      "First": "updates.First",
	      "Last": "updates.Last",
	      "CustomerID": "updates.CustomerID"
	    }
	  ) \
	  .execute()
	```
11. Now you’ll **repeat those steps to create your product dimension**. In a new code block, paste and run the following:
	code
	```python
	from pyspark.sql.types import *
	from delta.tables import *
	    
	DeltaTable.createIfNotExists(spark) \
	    .tableName("sales.dimproduct_gold") \
	    .addColumn("ItemName", StringType()) \
	    .addColumn("ItemID", LongType()) \
	    .addColumn("ItemInfo", StringType()) \
	    .execute()
	```
12. **Add another code block** to create the **product\_silver** dataframe.
	code
	```python
	from pyspark.sql.functions import col, split, lit, when
	    
	# Create product_silver dataframe
	    
	dfdimProduct_silver = df.dropDuplicates(["Item"]).select(col("Item")) \
	    .withColumn("ItemName",split(col("Item"), ", ").getItem(0)) \
	    .withColumn("ItemInfo",when((split(col("Item"), ", ").getItem(1).isNull() | (split(col("Item"), ", ").getItem(1)=="")),lit("")).otherwise(split(col("Item"), ", ").getItem(1))) 
	    
	# Display the first 10 rows of the dataframe to preview your data
	display(dfdimProduct_silver.head(10))
	```
13. Now you’ll create IDs for your **dimProduct\_gold table**. Add the following syntax to a new code block and run it:
	code
	```python
	from pyspark.sql.functions import monotonically_increasing_id, col, lit, max, coalesce
	    
	#dfdimProduct_temp = dfdimProduct_silver
	dfdimProduct_temp = spark.read.table("Sales.dimProduct_gold")
	    
	MAXProductID = dfdimProduct_temp.select(coalesce(max(col("ItemID")),lit(0)).alias("MAXItemID")).first()[0]
	    
	dfdimProduct_gold = dfdimProduct_silver.join(dfdimProduct_temp,(dfdimProduct_silver.ItemName == dfdimProduct_temp.ItemName) & (dfdimProduct_silver.ItemInfo == dfdimProduct_temp.ItemInfo), "left_anti")
	    
	dfdimProduct_gold = dfdimProduct_gold.withColumn("ItemID",monotonically_increasing_id() + MAXProductID + 1)
	    
	# Display the first 10 rows of the dataframe to preview your data
	display(dfdimProduct_gold.head(10))
	```
	This calculates the next available product ID based on the current data in the table, assigns these new IDs to the products, and then displays the updated product information.
14. Similar to what you’ve done with your other dimensions, you need to ensure that your product table remains up-to-date as new data comes in. **In a new code block**, paste and run the following:
	code
	```python
	from delta.tables import *
	    
	deltaTable = DeltaTable.forPath(spark, 'Tables/dimproduct_gold')
	            
	dfUpdates = dfdimProduct_gold
	            
	deltaTable.alias('gold') \
	  .merge(
	        dfUpdates.alias('updates'),
	        'gold.ItemName = updates.ItemName AND gold.ItemInfo = updates.ItemInfo'
	        ) \
	        .whenMatchedUpdate(set =
	        {
	               
	        }
	        ) \
	        .whenNotMatchedInsert(values =
	         {
	          "ItemName": "updates.ItemName",
	          "ItemInfo": "updates.ItemInfo",
	          "ItemID": "updates.ItemID"
	          }
	          ) \
	          .execute()
	```
	Now that you have your dimensions built out, the final step is to create the fact table.
15. **In a new code block**, paste and run the following code to create the **fact table**:
	code
	```python
	from pyspark.sql.types import *
	from delta.tables import *
	    
	DeltaTable.createIfNotExists(spark) \
	    .tableName("sales.factsales_gold") \
	    .addColumn("CustomerID", LongType()) \
	    .addColumn("ItemID", LongType()) \
	    .addColumn("OrderDate", DateType()) \
	    .addColumn("Quantity", IntegerType()) \
	    .addColumn("UnitPrice", FloatType()) \
	    .addColumn("Tax", FloatType()) \
	    .execute()
	```
16. **In a new code block**, paste and run the following code to create a **new dataframe** to combine sales data with customer and product information include customer ID, item ID, order date, quantity, unit price, and tax:
	code
	```python
	from pyspark.sql.functions import col
	    
	dfdimCustomer_temp = spark.read.table("Sales.dimCustomer_gold")
	dfdimProduct_temp = spark.read.table("Sales.dimProduct_gold")
	    
	df = df.withColumn("ItemName",split(col("Item"), ", ").getItem(0)) \
	    .withColumn("ItemInfo",when((split(col("Item"), ", ").getItem(1).isNull() | (split(col("Item"), ", ").getItem(1)=="")),lit("")).otherwise(split(col("Item"), ", ").getItem(1))) \
	    
	    
	# Create Sales_gold dataframe
	    
	dffactSales_gold = df.alias("df1").join(dfdimCustomer_temp.alias("df2"),(df.CustomerName == dfdimCustomer_temp.CustomerName) & (df.Email == dfdimCustomer_temp.Email), "left") \
	        .join(dfdimProduct_temp.alias("df3"),(df.ItemName == dfdimProduct_temp.ItemName) & (df.ItemInfo == dfdimProduct_temp.ItemInfo), "left") \
	    .select(col("df2.CustomerID") \
	        , col("df3.ItemID") \
	        , col("df1.OrderDate") \
	        , col("df1.Quantity") \
	        , col("df1.UnitPrice") \
	        , col("df1.Tax") \
	    ).orderBy(col("df1.OrderDate"), col("df2.CustomerID"), col("df3.ItemID"))
	    
	# Display the first 10 rows of the dataframe to preview your data
	    
	display(dffactSales_gold.head(10))
	```
17. **이제 새 코드 블록** 에서 다음 코드를 실행하여 판매 데이터가 최신 상태로 유지되도록 하세요 .
	암호
	```python
	from delta.tables import *
	    
	deltaTable = DeltaTable.forPath(spark, 'Tables/factsales_gold')
	    
	dfUpdates = dffactSales_gold
	    
	deltaTable.alias('gold') \
	  .merge(
	    dfUpdates.alias('updates'),
	    'gold.OrderDate = updates.OrderDate AND gold.CustomerID = updates.CustomerID AND gold.ItemID = updates.ItemID'
	  ) \
	   .whenMatchedUpdate(set =
	    {
	          
	    }
	  ) \
	 .whenNotMatchedInsert(values =
	    {
	      "CustomerID": "updates.CustomerID",
	      "ItemID": "updates.ItemID",
	      "OrderDate": "updates.OrderDate",
	      "Quantity": "updates.Quantity",
	      "UnitPrice": "updates.UnitPrice",
	      "Tax": "updates.Tax"
	    }
	  ) \
	  .execute()
	```
	여기서는 Delta Lake의 병합 작업을 사용하여 factsales\_gold 테이블을 새로운 판매 데이터(dffactSales\_gold)로 동기화하고 업데이트합니다. 이 작업은 기존 데이터(silver 테이블)와 새 데이터(updates DataFrame)의 주문 날짜, 고객 ID, 품목 ID를 비교하여 일치하는 레코드를 업데이트하고 필요에 따라 새 레코드를 삽입합니다.

이제 보고 및 분석에 사용할 수 있는 큐레이팅되고 모델링된 **골드** 레이어가 생겼습니다.

## (선택 사항) 의미 모델을 만듭니다.

**참고**: 이 작업은 전적으로 선택 사항이지만 의미 모델을 만들고 편집하려면 Power BI 라이선스 또는 Fabric F64 SKU가 필요합니다.

이제 작업 공간에서 골드 레이어를 사용하여 보고서를 생성하고 데이터를 분석할 수 있습니다. 작업 공간에서 의미 모델에 직접 액세스하여 보고를 위한 관계 및 측정값을 생성할 수 있습니다.

**레이크하우스를 생성할 때 자동으로 생성되는 기본 의미 모델을** 사용할 수 없습니다 . 이 연습에서 생성한 골드 테이블을 포함하는 새로운 의미 모델을 탐색기에서 생성해야 합니다.

1. 작업 공간에서 **Sales** Lakehouse로 이동합니다.
2. 탐색기 보기의 리본에서 **새 의미 모델을** 선택합니다.
3. 새로운 의미 모델에 **Sales\_Gold라는** 이름을 지정합니다.
4. 의미 모델에 포함할 변환된 골드 테이블을 선택하고 **확인을** 선택합니다.
	- 딤데이트\_골드
	- dimcustomer\_gold
	- dimproduct\_gold
	- 사실세일즈\_골드
	이렇게 하면 Fabric에서 의미 모델이 열리고 여기서 다음과 같이 관계와 측정값을 만들 수 있습니다.
	[![Screenshot of a semantic model in Fabric.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/dataset-relationships.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/dataset-relationships.png)

여기에서 본인이나 데이터 팀 구성원은 레이크하우스의 데이터를 기반으로 보고서와 대시보드를 만들 수 있습니다. 이러한 보고서는 레이크하우스의 골드 레이어에 직접 연결되므로 항상 최신 데이터를 반영합니다.

## 자원 정리

이 연습에서는 Microsoft Fabric 레이크하우스에서 메달리온 아키텍처를 만드는 방법을 알아보았습니다.

호숫가 주택 탐험을 마쳤다면 이 연습을 위해 만든 작업 공간을 삭제할 수 있습니다.

1. 왼쪽 막대에서 작업 공간 아이콘을 선택하면 해당 작업 공간에 포함된 모든 항목을 볼 수 있습니다.
2. **도구 모음의 …** 메뉴 에서 **작업 공간 설정을** 선택합니다 .
3. **일반** 섹션 에서 **이 작업 공간 제거를** 선택합니다.