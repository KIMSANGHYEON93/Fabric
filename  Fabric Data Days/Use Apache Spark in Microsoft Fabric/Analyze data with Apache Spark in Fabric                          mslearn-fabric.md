---
title: "Analyze data with Apache Spark in Fabric |                         mslearn-fabric"
source: "https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/02-analyze-spark.html"
author:
published:
created: 2025-12-03
description:
tags:
  - "clippings"
---
## Fabric에서 Apache Spark로 데이터 분석

이 랩에서는 Fabric 레이크하우스로 데이터를 수집하고 PySpark를 사용하여 데이터를 읽고 분석합니다.

이 실험을 완료하는 데 약 45분이 걸립니다.

> \[!참고\] 이 연습을 완료하려면 [Microsoft Fabric 테넌트](https://learn.microsoft.com/fabric/get-started/fabric-trial) 에 액세스해야 합니다.

## 작업 공간 만들기

Fabric에서 데이터 작업을 하기 전에 Fabric 용량이 활성화된 테넌트에 작업 공간을 만듭니다.

1. 브라우저 에서 [Microsoft Fabric 홈페이지](https://app.fabric.microsoft.com/home?experience=fabric-developer) 로 이동하여 `https://app.fabric.microsoft.com/home?experience=fabric-developer` Fabric 자격 증명을 사용하여 로그인합니다.
2. 왼쪽 메뉴 모음에서 **작업 공간을** 선택하세요 (아이콘은 🗇와 비슷합니다).
3. 원하는 이름으로 새 작업 공간을 만들고, **고급 섹션에서 Fabric 용량(** *평가판*, *프리미엄* 또는 *Fabric* ) 을 포함하는 라이선스 모드를 선택합니다 .
4. 새로운 작업 공간이 열리면 비어 있어야 합니다.
	[![Fabric의 빈 작업 공간 스크린샷.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/new-workspace.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/new-workspace.png)

## 레이크하우스를 만들고 파일을 업로드하세요

이제 작업 공간이 생겼으니 데이터를 위한 데이터 레이크하우스를 만들 차례입니다.

1. 왼쪽 메뉴 모음에서 **'만들기'를** 선택합니다. *'새로 만들기* ' 페이지 의 *'데이터 엔지니어링 ' 섹션에서* **'Lakehouse'를** 선택합니다 . 원하는 고유한 이름을 지정합니다. "Lakehouse 스키마(공개 미리 보기)" 옵션이 비활성화되어 있는지 확인합니다.
	> **참고**: **만들기** 옵션이 사이드바에 고정되어 있지 않으면 먼저 줄임표( **…** ) 옵션을 선택해야 합니다.
	1분 정도 후에 새로운 호숫가 주택이 생성됩니다.
	[![새로운 호숫가 주택의 스크린샷.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/new-lakehouse.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/new-lakehouse.png)
2. 새로운 레이크하우스를 보고, 왼쪽의 **레이크하우스 탐색기 창을 통해 레이크하우스의 테이블과 파일을 탐색할 수 있습니다.**

이제 레이크하우스로 데이터를 수집할 수 있습니다. 여러 가지 방법이 있지만, 지금은 로컬 컴퓨터(또는 해당되는 경우 랩 VM)에 텍스트 파일 폴더를 다운로드한 후 레이크하우스에 업로드합니다.

1. .에서 데이터 파일을 다운로드합니다 `https://github.com/MicrosoftLearning/dp-data/raw/main/orders.zip`.
2. *압축된 아카이브를 추출하고 orders* 라는 폴더가 있는지 확인합니다. 이 폴더에 2019.csv, 2020.csv, 2021.csv라는 세 개의 CSV 파일이 들어 있습니다.
3. 새 레이크하우스로 돌아가세요. **탐색기 창에서** **파일** 폴더 옆에 있는 **… 메뉴를 선택하고** **업로드** 및 **폴더 업로드를** 선택하세요 . 로컬 컴퓨터(또는 랩 VM(해당하는 경우))의 주문 폴더로 이동하여 **업로드를** 선택하세요.
4. After the files have been uploaded, expand **Files** and select the **orders** folder. Check that the CSV files have been uploaded, as shown here:
	[![새로운 Fabric 작업 공간에 업로드된 CSV 파일의 화면 사진입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/uploaded-files.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/uploaded-files.png)

## Create a notebook

You can now create a Fabric notebook to work with your data. Notebooks provide an interactive environment where you can write and run code.

1. On the menu bar on the left, select **Create**. In the *New* page, under the *Data Engineering* section, select **Notebook**.
	A new notebook named **Notebook 1** is created and opened.
	[![새로운 노트북의 스크린샷.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/new-notebook.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/new-notebook.png)
2. Fabric assigns a name to each notebook you create, such as Notebook 1, Notebook 2, etc. Click the name panel above the **Home** tab on the menu to change the name to something more descriptive.
3. Select the first cell (which is currently a code cell), and then in the top-right tool bar, use the **M↓** button to convert it to a markdown cell. The text contained in the cell will then be displayed as formatted text.
4. Use the 🖉 (Edit) button to switch the cell to editing mode, then modify the markdown as shown below.
	code
	```markdown
	# Sales order data exploration
	Use this notebook to explore sales order data
	```
	[![마크다운 셀이 있는 Fabric 노트북의 화면 사진입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/name-notebook-markdown.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/name-notebook-markdown.png)

When you have finished, click anywhere in the notebook outside of the cell to stop editing it.

## Create a DataFrame

Now that you have created a workspace, a lakehouse, and a notebook you are ready to work with your data. You will use PySpark, which is the default language for Fabric notebooks, and the version of Python that is optimized for Spark.

> \[!NOTE\] Fabric notebooks support multiple programming languages including Scala, R, and Spark SQL.

1. Select your new workspace from the left bar. You will see a list of items contained in the workspace including your lakehouse and notebook.
2. Select the lakehouse to display the Explorer pane, including the **orders** folder.
3. From the top menu, select **Open notebook**, **Existing notebook**, and then open the notebook you created earlier. The notebook should now be open next to the Explorer pane. Expand Lakehouses, expand the Files list, and select the orders folder. The CSV files that you uploaded are listed next to the notebook editor, like this:
	[![탐색기 보기에서 csv 파일의 화면 사진입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/explorer-notebook-view.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/explorer-notebook-view.png)
4. From the … menu for 2019.csv, select **Load data** > **Spark**. The following code is automatically generated in a new code cell:
	code
	```python
	df = spark.read.format("csv").option("header","true").load("Files/orders/2019.csv")
	# df now is a Spark DataFrame containing CSV data from "Files/orders/2019.csv".
	display(df)
	```

> \[!TIP\] You can hide the Explorer panes on the left by using the « icons. This gives more space for the notebook.

1. Select ▷ **Run cell** to the left of the cell to run the code.

> \[!NOTE\] The first time you run Spark code, a Spark session is started. This can take a few seconds or longer. Subsequent runs within the same session will be quicker.

1. When the cell code has completed, review the output below the cell, which should look like this:
	[![자동 생성된 코드와 데이터를 보여주는 화면 그림입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/auto-generated-load.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/auto-generated-load.png)
2. The output shows data from the 2019.csv file displayed in columns and rows. Notice that the column headers contain the first line of the data. To correct this, you need to modify the first line of the code as follows:
	code
	```python
	df = spark.read.format("csv").option("header","false").load("Files/orders/2019.csv")
	```
3. Run the code again, so that the DataFrame correctly identifies the first row as data. Notice that the column names have now changed to \_c0, \_c1, etc.
4. Descriptive column names help you make sense of data. To create meaningful column names, you need to define the schema and data types. You also need to import a standard set of Spark SQL types to define the data types. Replace the existing code with the following:
	code
	```python
	from pyspark.sql.types import *
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
	df = spark.read.format("csv").schema(orderSchema).load("Files/orders/2019.csv")
	display(df)
	```
5. Run the cell and review the output:
	[![스키마가 정의되어 있고 데이터가 있는 코드의 화면 사진입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/define-schema.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/define-schema.png)
6. This DataFrame includes only the data from the 2019.csv file. Modify the code so that the file path uses a \* wildcard to read all the files in the orders folder:
	code
	```python
	from pyspark.sql.types import *
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
	df = spark.read.format("csv").schema(orderSchema).load("Files/orders/*.csv")
	display(df)
	```
7. When you run the modified code, you should see sales for 2019, 2020, and 2021. Only a subset of the rows is displayed, so you may not see rows for every year.

> \[!NOTE\] You can hide or show the output of a cell by selecting **…** next to the result. This makes it easier to work in a notebook.

## Explore data in a DataFrame

The DataFrame object provides additional functionality such as the ability to filter, group, and manipulate data.

### Filter a DataFrame

1. Add a code cell by selecting **\+ Code** which appears when you hover the mouse above or below the current cell or its output. Alternatively, from the ribbon menu select **Edit** and **\+ Add code cell below**.
2. The following code filters the data so that only two columns are returned. It also uses *count* and *distinct* to summarize the number of records:
	code
	```python
	customers = df['CustomerName', 'Email']
	print(customers.count())
	print(customers.distinct().count())
	display(customers.distinct())
	```
3. Run the code, and examine the output:
	- The code creates a new DataFrame called **customers** which contains a subset of columns from the original **df** DataFrame. When performing a DataFrame transformation you do not modify the original DataFrame, but return a new one.
	- Another way of achieving the same result is to use the select method:
	code
	```python
	customers = df.select("CustomerName", "Email")
	```
	- The DataFrame functions *count* and *distinct* are used to provide totals for the number of customers and unique customers.
4. Modify the first line of the code by using *select* with a *where* function as follows:
	code
	```python
	customers = df.select("CustomerName", "Email").where(df['Item']=='Road-250 Red, 52')
	print(customers.count())
	print(customers.distinct().count())
	display(customers.distinct())
	```
5. Run the modified code to select only the customers who have purchased the Road-250 Red, 52 product. Note that you can “chain” multiple functions together so that the output of one function becomes the input for the next. In this case, the DataFrame created by the *select* method is the source DataFrame for the **where** method that is used to apply filtering criteria.

### Aggregate and group data in a DataFrame

1. Add a code cell, and enter the following code:
	code
	```python
	productSales = df.select("Item", "Quantity").groupBy("Item").sum()
	display(productSales)
	```
2. Run the code. You can see that the results show the sum of order quantities grouped by product. The *groupBy* method groups the rows by Item, and the subsequent *sum* aggregate function is applied to the remaining numeric columns - in this case, *Quantity*.
3. Add another code cell to the notebook, and enter the following code:
	code
	```python
	from pyspark.sql.functions import *
	yearlySales = df.select(year(col("OrderDate")).alias("Year")).groupBy("Year").count().orderBy("Year")
	display(yearlySales)
	```
4. Run the cell. Examine the output. The results now show the number of sales orders per year:
	- The *import* statement enables you to use the Spark SQL library.
	- The *select* method is used with a SQL year function to extract the year component of the *OrderDate* field.
	- The *alias* method is used to assign a column name to the extracted year value.
	- The *groupBy* method groups the data by the derived Year column.
	- The count of rows in each group is calculated before the *orderBy* method is used to sort the resulting DataFrame.
	[![Screen picture showing the results of aggregating and grouping data in a DataFrame.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/spark-sql-dataframe.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/spark-sql-dataframe.png)

## Use Spark to transform data files

A common task for data engineers and data scientists is to transform data for further downstream processing or analysis.

### Use DataFrame methods and functions to transform data

1. Add a code cell to the notebook, and enter the following:
	code
	```python
	from pyspark.sql.functions import *
	# Create Year and Month columns
	transformed_df = df.withColumn("Year", year(col("OrderDate"))).withColumn("Month", month(col("OrderDate")))
	# Create the new FirstName and LastName fields
	transformed_df = transformed_df.withColumn("FirstName", split(col("CustomerName"), " ").getItem(0)).withColumn("LastName", split(col("CustomerName"), " ").getItem(1))
	# Filter and reorder columns
	transformed_df = transformed_df["SalesOrderNumber", "SalesOrderLineNumber", "OrderDate", "Year", "Month", "FirstName", "LastName", "Email", "Item", "Quantity", "UnitPrice", "Tax"]
	# Display the first five orders
	display(transformed_df.limit(5))
	```
2. Run the cell. A new DataFrame is created from the original order data with the following transformations:
	- Year and Month columns added, based on the OrderDate column.
	- FirstName and LastName columns added, based on the CustomerName column.
	- The columns are filtered and reordered, and the CustomerName column removed.
3. Review the output and verify that the transformations have been made to the data.

You can use the Spark SQL library to transform the data by filtering rows, deriving, removing, renaming columns, and applying other data modifications.

> \[!TIP\] See the [Apache Spark dataframe](https://spark.apache.org/docs/latest/api/python/reference/pyspark.sql/dataframe.html) documentation to learn more about the DataFrame object.

### Save the transformed data

At this point you might want to save the transformed data so that it can be used for further analysis.

*Parquet* is a popular data storage format because it stores data efficiently and is supported by most large-scale data analytics systems. Indeed, sometimes the data transformation requirement is to convert data from one format such as CSV, to Parquet.

1. To save the transformed DataFrame in Parquet format, add a code cell and add the following code:
	code
	```python
	transformed_df.write.mode("overwrite").parquet('Files/transformed_data/orders')
	print ("Transformed data saved!")
	```
2. Run the cell and wait for the message that the data has been saved. Then, in the Explorer pane on the left, in the … menu for the Files node, select **Refresh**. Select the transformed\_data folder to verify that it contains a new folder named orders, which in turn contains one or more Parquet files.
3. Add a cell with the following code:
	code
	```python
	orders_df = spark.read.format("parquet").load("Files/transformed_data/orders")
	display(orders_df)
	```
4. Run the cell. A new DataFrame is created from the parquet files in the *transformed\_data/orders* folder. Verify that the results show the order data that has been loaded from the parquet files.
	[![Screen picture showing Parquet files.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/parquet-files.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/parquet-files.png)

### Save data in partitioned files

When dealing with large volumes of data, partitioning can significantly improve performance and make it easier to filter data.

1. Add a cell with code to save the dataframe, partitioning the data by Year and Month:
	code
	```python
	orders_df.write.partitionBy("Year","Month").mode("overwrite").parquet("Files/partitioned_data")
	print ("Transformed data saved!")
	```
2. Run the cell and wait for the message that the data has been saved. Then, in the Lakehouses pane on the left, in the … menu for the Files node, select **Refresh** and expand the partitioned\_data folder to verify that it contains a hierarchy of folders named *Year=xxxx*, each containing folders named *Month=xxxx*. Each month folder contains a parquet file with the orders for that month.
	[![Screen picture showing data partitioned by Year and Month.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/partitioned-data.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/partitioned-data.png)
3. Add a new cell with the following code to load a new DataFrame from the orders.parquet file:
	code
	```python
	orders_2021_df = spark.read.format("parquet").load("Files/partitioned_data/Year=2021/Month=*")
	display(orders_2021_df)
	```
4. Run the cell and verify that the results show the order data for sales in 2021. Notice that the partitioning columns specified in the path (Year and Month) are not included in the DataFrame.

## Work with tables and SQL

You’ve now seen how the native methods of the DataFrame object enable you to query and analyze data from a file. However, you may be more comfortable working with tables using SQL syntax. Spark provides a metastore in which you can define relational tables.

The Spark SQL library supports the use of SQL statements to query tables in the metastore. This provides the flexibility of a data lake with the structured data schema and SQL-based queries of a relational data warehouse - hence the term “data lakehouse”.

### Create a table

Tables in a Spark metastore are relational abstractions over files in the data lake. Tables can be *managed* by the metastore, or *external* and managed independently of the metastore.

1. Add a code cell to the notebook and enter the following code, which saves the DataFrame of sales order data as a table named *salesorders*:
	code
	```python
	# Create a new table
	df.write.format("delta").saveAsTable("salesorders")
	# Get the table description
	spark.sql("DESCRIBE EXTENDED salesorders").show(truncate=False)
	```

> \[!NOTE\] In this example, no explicit path is provided, so the files for the table will be managed by the metastore. Also, the table is saved in delta format which adds relational database capabilities to tables. This includes support for transactions, row versioning, and other useful features. Creating tables in delta format is preferred for data lakehouses in Fabric.

1. Run the code cell and review the output, which describes the definition of the new table.
2. In the **Explorer** pane, in the … menu for the Tables folder, select **Refresh**. Then expand the **Tables** node and verify that the **salesorders** table has been created.
	[![Screen picture showing that the salesorders table has been created.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/salesorder-table.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/salesorder-table.png)
3. In the … menu for the salesorders table, select **Load data** > **Spark**. A new code cell is added containing code similar to the following:
	code
	```
	df = spark.sql("SELECT * FROM [your_lakehouse].salesorders LIMIT 1000")
	display(df)
	```
4. Run the new code, which uses the Spark SQL library to embed a SQL query against the *salesorder* table in PySpark code and load the results of the query into a DataFrame.

### Run SQL code in a cell

While it’s useful to be able to embed SQL statements into a cell containing PySpark code, data analysts often just want to work directly in SQL.

1. Add a new code cell to the notebook, and enter the following code:
	code
	```
	%%sql
	SELECT YEAR(OrderDate) AS OrderYear,
	       SUM((UnitPrice * Quantity) + Tax) AS GrossRevenue
	FROM salesorders
	GROUP BY YEAR(OrderDate)
	ORDER BY OrderYear;
	```
2. Run the cell and review the results. Observe that:
	- The **%%sql** command at the beginning of the cell (called a magic) changes the language to Spark SQL instead of PySpark.
	- The SQL code references the *salesorders* table that you created previously.
	- The output from the SQL query is automatically displayed as the result under the cell.

> \[!NOTE\] For more information about Spark SQL and dataframes, see the [Apache Spark SQL](https://spark.apache.org/sql/) documentation.

## Visualize data with Spark

Charts help you to see patterns and trends faster than would be possible by scanning thousands of rows of data. Fabric notebooks include a built-in chart view but it is not designed for complex charts. For more control over how charts are created from data in DataFrames, use Python graphics libraries like *matplotlib* or *seaborn*.

### View results as a chart

1. Add a new code cell, and enter the following code:
	code
	```python
	%%sql
	SELECT * FROM salesorders
	```
2. Run the code to display data from the salesorders view you created previously. In the results section beneath the cell, select **\+ New chart**.
3. Use the **Build my own** button at the bottom-right of the results section and set the chart settings:
	- Chart type: Bar chart
	- X-axis: Item
	- Y-axis: Quantity
	- Series Group: leave blank
	- Aggregation: Sum
	- Missing and NULL values: Display as 0
	- Stacked: Unselected
4. Your chart should look similar to this:
	[![Screen picture of Fabric notebook chart view.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/built-in-chart.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/built-in-chart.png)

### Get started with matplotlib

1. Add a new code cell, and enter the following code:
	code
	```python
	sqlQuery = "SELECT CAST(YEAR(OrderDate) AS CHAR(4)) AS OrderYear, \
	                SUM((UnitPrice * Quantity) + Tax) AS GrossRevenue, \
	                COUNT(DISTINCT SalesOrderNumber) AS YearlyCounts \
	            FROM salesorders \
	            GROUP BY CAST(YEAR(OrderDate) AS CHAR(4)) \
	            ORDER BY OrderYear"
	df_spark = spark.sql(sqlQuery)
	df_spark.show()
	```
2. Run the code. It returns a Spark DataFrame containing the yearly revenue and number of orders. To visualize the data as a chart, we’ll first use the matplotlib Python library. This library is the core plotting library on which many others are based and provides a great deal of flexibility in creating charts.
3. Add a new code cell, and add the following code:
	code
	```python
	from matplotlib import pyplot as plt
	# matplotlib requires a Pandas dataframe, not a Spark one
	df_sales = df_spark.toPandas()
	# Create a bar plot of revenue by year
	plt.bar(x=df_sales['OrderYear'], height=df_sales['GrossRevenue'])
	# Display the plot
	plt.show()
	```
4. Run the cell and review the results, which consist of a column chart with the total gross revenue for each year. Review the code, and notice the following:
	- The matplotlib library requires a Pandas DataFrame, so you need to convert the Spark DataFrame returned by the Spark SQL query.
	- At the core of the matplotlib library is the *pyplot* object. This is the foundation for most plotting functionality.
	- 기본 설정으로 차트를 사용할 수 있지만, 사용자 정의 범위가 상당히 넓습니다.
5. 다음과 같이 차트를 그리려면 코드를 수정하세요.
	암호
	```python
	from matplotlib import pyplot as plt
	# Clear the plot area
	plt.clf()
	# Create a bar plot of revenue by year
	plt.bar(x=df_sales['OrderYear'], height=df_sales['GrossRevenue'], color='orange')
	# Customize the chart
	plt.title('Revenue by Year')
	plt.xlabel('Year')
	plt.ylabel('Revenue')
	plt.grid(color='#95a5a6', linestyle='--', linewidth=2, axis='y', alpha=0.7)
	plt.xticks(rotation=45)
	# Show the figure
	plt.show()
	```
6. 코드 셀을 다시 실행하여 결과를 확인하세요. 이제 차트를 더 쉽게 이해할 수 있습니다.
7. 플롯은 Figure에 포함됩니다. 이전 예제에서는 Figure가 암시적으로 생성되었지만, 명시적으로 생성할 수도 있습니다. 다음과 같이 코드를 수정하여 차트를 플롯하세요.
	암호
	```python
	from matplotlib import pyplot as plt
	# Clear the plot area
	plt.clf()
	# Create a Figure
	fig = plt.figure(figsize=(8,3))
	# Create a bar plot of revenue by year
	plt.bar(x=df_sales['OrderYear'], height=df_sales['GrossRevenue'], color='orange')
	# Customize the chart
	plt.title('Revenue by Year')
	plt.xlabel('Year')
	plt.ylabel('Revenue')
	plt.grid(color='#95a5a6', linestyle='--', linewidth=2, axis='y', alpha=0.7)
	plt.xticks(rotation=45)
	# Show the figure
	plt.show()
	```
8. 코드 셀을 다시 실행하여 결과를 확인하세요. 그림은 플롯의 모양과 크기를 결정합니다.
9. 하나의 그림에는 각기 다른 축에 여러 개의 하위 그림이 포함될 수 있습니다. 다음과 같이 코드를 수정하여 차트를 그리세요.
	암호
	```python
	from matplotlib import pyplot as plt
	# Clear the plot area
	plt.clf()
	# Create a figure for 2 subplots (1 row, 2 columns)
	fig, ax = plt.subplots(1, 2, figsize = (10,4))
	# Create a bar plot of revenue by year on the first axis
	ax[0].bar(x=df_sales['OrderYear'], height=df_sales['GrossRevenue'], color='orange')
	ax[0].set_title('Revenue by Year')
	# Create a pie chart of yearly order counts on the second axis
	ax[1].pie(df_sales['YearlyCounts'])
	ax[1].set_title('Orders per Year')
	ax[1].legend(df_sales['OrderYear'])
	# Add a title to the Figure
	fig.suptitle('Sales Data')
	# Show the figure
	plt.show()
	```
10. 코드 셀을 다시 실행하고 결과를 확인하세요.

> \[!NOTE\] matplotlib을 사용하여 플로팅하는 방법에 대해 자세히 알아보려면 [matplotlib](https://matplotlib.org/) 설명서를 참조하세요.

### seaborn 라이브러리를 이용하세요

*Matplotlib을* 사용 하면 다양한 유형의 차트를 만들 수 있지만, 최상의 결과를 얻으려면 복잡한 코드가 필요할 수 있습니다. 이러한 이유로 Matplotlib의 복잡성을 추상화하고 기능을 향상시키기 위해 새로운 라이브러리가 개발되었습니다. 이러한 라이브러리 중 하나가 seaborn입니다.

1. 노트북에 새로운 코드 셀을 추가하고 다음 코드를 입력하세요.
	암호
	```python
	import seaborn as sns
	# Clear the plot area
	plt.clf()
	# Create a bar chart
	ax = sns.barplot(x="OrderYear", y="GrossRevenue", data=df_sales)
	plt.show()
	```
2. seaborn 라이브러리를 사용하여 만든 막대 차트를 표시하는 코드를 실행합니다.
3. 다음과 같이 코드를 수정하세요.
	암호
	```python
	import seaborn as sns
	# Clear the plot area
	plt.clf()
	# Set the visual theme for seaborn
	sns.set_theme(style="whitegrid")
	# Create a bar chart
	ax = sns.barplot(x="OrderYear", y="GrossRevenue", data=df_sales)
	plt.show()
	```
4. 수정된 코드를 실행하면 seaborn을 사용하여 플롯에 대한 색상 테마를 설정할 수 있음을 알 수 있습니다.
5. 다음과 같이 코드를 다시 수정합니다.
	암호
	```python
	import seaborn as sns
	# Clear the plot area
	plt.clf()
	# Create a line chart
	ax = sns.lineplot(x="OrderYear", y="GrossRevenue", data=df_sales)
	plt.show()
	```
6. 수정된 코드를 실행하여 연간 수익을 선형 차트로 확인하세요.

> \[!NOTE\] seaborn을 사용하여 플로팅하는 방법에 대해 자세히 알아보려면 [seaborn](https://seaborn.pydata.org/index.html) 설명서를 참조하세요.

## 자원 정리

이 연습에서는 Spark를 사용하여 Microsoft Fabric의 데이터를 처리하는 방법을 알아보았습니다.

데이터 탐색을 마쳤다면 Spark 세션을 종료하고 이 연습을 위해 만든 작업 공간을 삭제할 수 있습니다.

1. 노트북 메뉴에서 **'세션 중지'를** 선택하여 Spark 세션을 종료합니다.
2. 왼쪽 막대에서 작업 공간 아이콘을 선택하면 해당 작업 공간에 포함된 모든 항목을 볼 수 있습니다.
3. **작업 공간 설정을** 선택 하고 **일반** 섹션 에서 아래로 스크롤하여 **이 작업 공간 제거를** 선택합니다.
4. **삭제를** 선택하면 작업 공간이 삭제됩니다.