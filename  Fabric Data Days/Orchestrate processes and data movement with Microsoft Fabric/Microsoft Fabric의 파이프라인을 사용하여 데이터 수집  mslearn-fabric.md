---
title: "Microsoft Fabric의 파이프라인을 사용하여 데이터 수집 | mslearn-fabric"
source: "https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/04-ingest-pipeline.html"
author:
published:
created: 2025-12-03
description:
tags:
  - "clippings"
---
## Microsoft Fabric의 파이프라인을 사용하여 데이터 수집

데이터 레이크하우스는 클라우드 규모 분석 솔루션을 위한 일반적인 분석 데이터 저장소입니다. 데이터 엔지니어의 핵심 업무 중 하나는 여러 운영 데이터 소스에서 레이크하우스로 데이터를 수집하는 과정을 구현하고 관리하는 것입니다. Microsoft Fabric에서는 파이프라인 생성 *을 통해 데이터 수집을 위한 ETL(* *추출, 변환, 로드* ) 또는 ELT( *추출, 로드, 변환* ) 솔루션을 구현할 수 있습니다.

Fabric은 Apache Spark도 지원하여 대규모 데이터 처리를 위한 코드를 작성하고 실행할 수 있습니다. Fabric에서 파이프라인과 Spark 기능을 결합하면 외부 소스의 데이터를 레이크하우스가 기반을 둔 OneLake 스토리지로 복사하는 복잡한 데이터 수집 로직을 구현할 수 있습니다. 그런 다음 Spark 코드를 사용하여 사용자 지정 데이터 변환을 수행한 후 분석을 위해 테이블에 로드할 수 있습니다.

**이 실험을 완료하는 데 약 45** 분이 걸립니다 .

> \[!참고\] 이 연습을 완료하려면 [Microsoft Fabric 테넌트](https://learn.microsoft.com/fabric/get-started/fabric-trial) 에 액세스해야 합니다.

## 작업 공간 만들기

Fabric에서 데이터 작업을 하기 전에 Fabric 평가판을 활성화하여 작업 공간을 만드세요.

1. 브라우저 에서 [Microsoft Fabric 홈페이지](https://app.fabric.microsoft.com/home?experience=fabric-developer) 로 이동하여 `https://app.fabric.microsoft.com/home?experience=fabric-developer` Fabric 자격 증명을 사용하여 로그인합니다.
2. 왼쪽 메뉴 모음에서 **작업 공간을** 선택하세요 (아이콘은 🗇와 비슷합니다).
3. 원하는 이름으로 새 작업 공간을 만들고, **고급 섹션에서 Fabric 용량(** *평가판*, *프리미엄* 또는 *Fabric* ) 을 포함하는 라이선스 모드를 선택합니다 .
4. 새 작업 공간이 열리면 비어 있어야 합니다.
	[![Fabric의 빈 작업 공간 스크린샷.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/new-workspace.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/new-workspace.png)

## 호숫가 주택 만들기

이제 작업 공간이 생겼으니 데이터를 수집할 데이터 레이크하우스를 만들 차례입니다.

1. 왼쪽 메뉴 모음에서 **'만들기'를** 선택합니다. *'새로 만들기* ' 페이지 의 *'데이터 엔지니어링 ' 섹션에서* **'Lakehouse'를** 선택합니다 . 원하는 고유한 이름을 지정합니다. "Lakehouse 스키마(공개 미리 보기)" 옵션이 비활성화되어 있는지 확인합니다.
	> **참고**: **만들기** 옵션이 사이드바에 고정되어 있지 않으면 먼저 줄임표( **…** ) 옵션을 선택해야 합니다.
	**1분 정도 후에 테이블** 이나 **파일이** 없는 새로운 레이크하우스가 생성됩니다.
2. 왼쪽의 **탐색기** 창 에서 **파일** 노드 의 **...** 메뉴 에서 **새 하위 폴더를 선택하고** **new\_data** 라는 이름의 하위 폴더를 만듭니다 .

## 파이프라인을 생성하세요

A simple way to ingest data is to use a **Copy Data** activity in a pipeline to extract the data from a source and copy it to a file in the lakehouse.

1. On the **Home** page for your lakehouse, select **Get data** and then select **New data pipeline**, and create a new data pipeline named `Ingest Sales Data`.
2. If the **Copy Data** wizard doesn’t open automatically, select **Copy Data > Use copy assistant** in the pipeline editor page.
3. In the **Copy Data** wizard, on the **Choose data source** page, type HTTP in the search bar and then select **HTTP** in the **New sources** section.
	[![데이터 소스 선택 페이지의 스크린샷입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/choose-data-source.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/choose-data-source.png)
4. In the **Connect to data source** pane, enter the following settings for the connection to your data source:
	- **URL**: `https://raw.githubusercontent.com/MicrosoftLearning/dp-data/main/sales.csv`
	- **Connection**: Create new connection
	- **Connection name**: *Specify a unique name*
	- **Data gateway**: (none)
	- **Authentication kind**: Anonymous
5. Select **Next**. Then ensure the following settings are selected:
	- **Relative URL**: *Leave blank*
	- **Request method**: GET
	- **Additional headers**: *Leave blank*
	- **Binary copy**: Un selected
	- **Request timeout**: *Leave blank*
	- **Max concurrent connections**: *Leave blank*
6. Select **Next**, and wait for the data to be sampled and then ensure that the following settings are selected:
	- **File format**: DelimitedText
	- **Column delimiter**: Comma (,)
	- **Row delimiter**: Line feed (\\n)
	- **First row as header**: Selected
	- **Compression type**: None
7. Select **Preview data** to see a sample of the data that will be ingested. Then close the data preview and select **Next**.
8. On the **Connect to data destination** page, set the following data destination options, and then select **Next**:
	- **Root folder**: Files
	- **Folder path name**: new\_data
	- **File name**: sales.csv
	- **Copy behavior**: None
9. Set the following file format options and then select **Next**:
	- **File format**: DelimitedText
	- **Column delimiter**: Comma (,)
	- **Row delimiter**: Line feed (\\n)
	- **Add header to file**: Selected
	- **Compression type**: None
10. On the **Copy summary** page, review the details of your copy operation and then select **Save + Run**.
	A new pipeline containing a **Copy Data** activity is created, as shown here:
	[![데이터 복사 활동이 있는 파이프라인의 스크린샷입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/copy-data-pipeline.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/copy-data-pipeline.png)
11. When the pipeline starts to run, you can monitor its status in the **Output** pane under the pipeline designer. Use the **↻** (*Refresh*) icon to refresh the status, and wait until it has succeeeded.
12. In the menu bar on the left, select your lakehouse.
13. On the **Home** page, in the **Explorer** pane, expand **Files** and select the **new\_data** folder to verify that the **sales.csv** file has been copied.

## Create a notebook

1. On the **Home** page for your lakehouse, in the **Open notebook** menu, select **New notebook**.
	After a few seconds, a new notebook containing a single *cell* will open. Notebooks are made up of one or more cells that can contain *code* or *markdown* (formatted text).
2. Select the existing cell in the notebook, which contains some simple code, and then replace the default code with the following variable declaration.
	code
	```python
	table_name = "sales"
	```
3. In the **…** menu for the cell (at its top-right) select **Toggle parameter cell**. This configures the cell so that the variables declared in it are treated as parameters when running the notebook from a pipeline.
4. Under the parameters cell, use the **\+ Code** button to add a new code cell. Then add the following code to it:
	code
	```python
	from pyspark.sql.functions import *
	# Read the new sales data
	df = spark.read.format("csv").option("header","true").load("Files/new_data/*.csv")
	## Add month and year columns
	df = df.withColumn("Year", year(col("OrderDate"))).withColumn("Month", month(col("OrderDate")))
	# Derive FirstName and LastName columns
	df = df.withColumn("FirstName", split(col("CustomerName"), " ").getItem(0)).withColumn("LastName", split(col("CustomerName"), " ").getItem(1))
	# Filter and reorder columns
	df = df["SalesOrderNumber", "SalesOrderLineNumber", "OrderDate", "Year", "Month", "FirstName", "LastName", "EmailAddress", "Item", "Quantity", "UnitPrice", "TaxAmount"]
	# Load the data into a table
	df.write.format("delta").mode("append").saveAsTable(table_name)
	```
	This code loads the data from the sales.csv file that was ingested by the **Copy Data** activity, applies some transformation logic, and saves the transformed data as a table - appending the data if the table already exists.
5. Verify that your notebooks looks similar to this, and then use the **▷ Run all** button on the toolbar to run all of the cells it contains.
	[![데이터를 변환하는 매개변수 셀과 코드가 있는 노트북의 스크린샷입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/notebook.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/notebook.png)
	> **Note**: Since this is the first time you’ve run any Spark code in this session, the Spark pool must be started. This means that the first cell can take a minute or so to complete.
6. When the notebook run has completed, in the **Explorer** pane on the left, in the **…** menu for **Tables** select **Refresh** and verify that a **sales** table has been created.
7. In the notebook menu bar, use the ⚙️ **Settings** icon to view the notebook settings. Then set the **Name** of the notebook to `Load Sales` and close the settings pane.
8. In the hub menu bar on the left, select your lakehouse.
9. In the **Explorer** pane, refresh the view. Then expand **Tables**, and select the **sales** table to see a preview of the data it contains.

## Modify the pipeline

Now that you’ve implemented a notebook to transform data and load it into a table, you can incorporate the notebook into a pipeline to create a reusable ETL process.

1. In the hub menu bar on the left select the **Ingest Sales Data** pipeline you created previously.
2. On the **Activities** tab, in the **All activities** list, select **Delete data**. Then position the new **Delete data** activity to the left of the **Copy data** activity and connect its **On completion** output to the **Copy data** activity, as shown here:
	[![데이터 삭제 및 데이터 복사 활동이 있는 파이프라인의 스크린샷입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/delete-data-activity.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/delete-data-activity.png)
3. Select the **Delete data** activity, and in the pane below the design canvas, set the following properties:
	- **General**:
		- **Name**: `Delete old files`
	- **Source**
		- **Connection**: *Your lakehouse*
		- **File path type**: Wildcard file path
		- **Folder path**: Files / **new\_data**
		- **Wildcard file name**: `*.csv`
		- **Recursively**: *Selected*
	- **Logging settings**:
		- **Enable logging**: *Un selected*
	These settings will ensure that any existing.csv files are deleted before copying the **sales.csv** file.
4. In the pipeline designer, on the **Activities** tab, select **Notebook** to add a **Notebook** activity to the pipeline.
5. Select the **Copy data** activity and then connect its **On Completion** output to the **Notebook** activity as shown here:
	[![데이터 복사 및 노트북 활동이 포함된 파이프라인의 스크린샷입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/pipeline.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/pipeline.png)
6. Select the **Notebook** activity, and then in the pane below the design canvas, set the following properties:
	- **General**:
		- **Name**: `Load Sales notebook`
	- **Settings**:
		- **Notebook**: Load Sales
		- **Base parameters**: *Add a new parameter with the following properties:*
			| Name | Type | Value |
			| --- | --- | --- |
			| table\_name | String | new\_sales |
	The **table\_name** parameter will be passed to the notebook and override the default value assigned to the **table\_name** variable in the parameters cell.
7. On the **Home** tab, use the **🖫** (*Save*) icon to save the pipeline. Then use the **▷ Run** button to run the pipeline, and wait for all of the activities to complete.
	[![Dataflow 활동이 포함된 파이프라인의 스크린샷입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/pipeline-run.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/pipeline-run.png)

> *참고: "Spark SQL 쿼리는 레이크하우스 컨텍스트에서만 가능합니다. 계속하려면 레이크하우스를 첨부하세요."라는* 오류 메시지가 표시되는 경우 , 노트북을 열고 왼쪽 창에서 생성한 레이크하우스를 선택한 후 **"모든 레이크하우스 제거"를** 선택 하고 다시 추가합니다. 파이프라인 디자이너로 돌아가서 **"▷ 실행"을** 선택합니다.

1. 포털 왼쪽 가장자리에 있는 허브 메뉴 바에서 레이크하우스를 선택하세요.
2. **탐색기** 창 에서 **테이블을** 확장하고 **new\_sales** 테이블을 선택하여 포함된 데이터를 미리 볼 수 있습니다. 이 테이블은 파이프라인에서 노트북을 실행할 때 생성되었습니다.

이 연습에서는 파이프라인을 사용하여 외부 소스에서 레이크하우스로 데이터를 복사한 다음 Spark 노트북을 사용하여 데이터를 변환하고 테이블에 로드하는 데이터 수집 솔루션을 구현했습니다.

## 자원 정리

이 연습에서는 Microsoft Fabric에서 파이프라인을 구현하는 방법을 알아보았습니다.

호숫가 주택 탐험을 마쳤다면 이 연습을 위해 만든 작업 공간을 삭제할 수 있습니다.

1. 왼쪽 막대에서 작업 공간 아이콘을 선택하면 해당 작업 공간에 포함된 모든 항목을 볼 수 있습니다.
2. **작업 공간 설정을** 선택 하고 **일반** 섹션 에서 아래로 스크롤하여 **이 작업 공간 제거를** 선택합니다.
3. **삭제를** 선택하면 작업 공간이 삭제됩니다.