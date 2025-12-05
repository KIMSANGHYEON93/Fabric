---
title: "Fabric에서 Apache Spark로 데이터 분석 | mslearn-fabric"
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
4. 파일 업로드가 완료되면 **파일을 확장하고** **주문** 폴더를 선택하세요 . CSV 파일이 업로드되었는지 확인하세요(아래 그림 참조).
	[![새로운 Fabric 작업 공간에 업로드된 CSV 파일의 화면 사진입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/uploaded-files.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/uploaded-files.png)

## 노트북 만들기

이제 데이터 작업을 위한 Fabric 노트북을 만들 수 있습니다. 노트북은 코드를 작성하고 실행할 수 있는 대화형 환경을 제공합니다.

1. 왼쪽 메뉴 모음에서 **'만들기'를** 선택합니다. *'새로 만들기* ' 페이지 의 *'데이터 엔지니어링 ' 섹션에서* **'노트북'을** 선택합니다 .
	**Notebook 1** 이라는 이름의 새 노트북이 생성되어 열립니다.
	[![새로운 노트북의 스크린샷.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/new-notebook.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/new-notebook.png)
2. Fabric은 사용자가 만든 각 노트북에 노트북 1, 노트북 2 등과 같은 이름을 지정합니다. 메뉴의 **홈 탭 위에 있는 이름 패널을 클릭하면 이름을 더 설명적인 이름으로 변경할 수 있습니다.**
3. 첫 번째 셀(현재는 코드 셀)을 선택한 다음, 오른쪽 상단 도구 모음에서 **M↓** 버튼을 사용하여 마크다운 셀로 변환합니다. 그러면 셀에 포함된 텍스트가 서식이 적용된 텍스트로 표시됩니다.
4. 🖉 (편집) 버튼을 사용하여 셀을 편집 모드로 전환한 다음, 아래와 같이 마크다운을 수정합니다.
	암호
	```markdown
	# Sales order data exploration
	Use this notebook to explore sales order data
	```
	[![마크다운 셀이 있는 Fabric 노트북의 화면 사진입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/name-notebook-markdown.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/name-notebook-markdown.png)

작업이 끝나면 셀 외부의 노트북 아무 곳이나 클릭하여 편집을 중지합니다.

## DataFrame 만들기

이제 작업 공간, 레이크하우스, 노트북을 만들었으니 데이터 작업을 시작할 준비가 되었습니다. Fabric 노트북의 기본 언어인 PySpark와 Spark에 최적화된 Python 버전을 사용하게 됩니다.

> \[!NOTE\] Fabric 노트북은 Scala, R, Spark SQL을 포함한 여러 프로그래밍 언어를 지원합니다.

1. 왼쪽 막대에서 새 작업 공간을 선택하세요. 레이크하우스와 노트북을 포함하여 작업 공간에 포함된 항목 목록이 표시됩니다.
2. **주문** 폴더를 포함한 탐색기 창을 표시하려면 레이크하우스를 선택하세요 .
3. 상단 메뉴에서 **'노트북 열기'**, **'기존 노트북'을** 차례로 선택한 다음, 앞서 만든 노트북을 엽니다. 이제 탐색기 창 옆에 노트북이 열려 있을 것입니다. 'Lakehouses'를 확장하고 '파일' 목록을 확장한 다음 '주문' 폴더를 선택합니다. 업로드한 CSV 파일이 노트북 편집기 옆에 다음과 같이 나열됩니다.
	[![탐색기 보기에서 csv 파일의 화면 사진입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/explorer-notebook-view.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/explorer-notebook-view.png)
4. 2019.csv의... 메뉴에서 **'데이터 로드'** \> **'Spark'를** 선택합니다. 다음 코드가 새 코드 셀에 자동으로 생성됩니다.
	암호
	```python
	df = spark.read.format("csv").option("header","true").load("Files/orders/2019.csv")
	# df now is a Spark DataFrame containing CSV data from "Files/orders/2019.csv".
	display(df)
	```

> \[!TIP\] 왼쪽의 탐색기 창을 숨기려면 « 아이콘을 사용하세요. 이렇게 하면 노트북 공간을 더 확보할 수 있습니다.

1. 코드를 실행하려면 셀 왼쪽의 ▷ **셀 실행을 선택하세요.**

> \[!NOTE\] Spark 코드를 처음 실행하면 Spark 세션이 시작됩니다. 이 과정은 몇 초 이상 걸릴 수 있습니다. 같은 세션 내에서 이후 실행 시 더 빠르게 진행됩니다.

1. 셀 코드가 완료되면 셀 아래의 출력을 검토하세요. 출력은 다음과 같습니다.
	[![자동 생성된 코드와 데이터를 보여주는 화면 그림입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/auto-generated-load.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/auto-generated-load.png)
2. 출력은 2019.csv 파일의 데이터를 열과 행으로 표시합니다. 열 머리글에 데이터의 첫 줄이 포함되어 있는 것을 확인할 수 있습니다. 이를 수정하려면 코드의 첫 줄을 다음과 같이 수정해야 합니다.
	암호
	```python
	df = spark.read.format("csv").option("header","false").load("Files/orders/2019.csv")
	```
3. 코드를 다시 실행하여 DataFrame이 첫 번째 행을 데이터로 올바르게 식별하도록 합니다. 열 이름이 \_c0, \_c1 등으로 변경된 것을 확인할 수 있습니다.
4. 설명적인 열 이름은 데이터를 이해하는 데 도움이 됩니다. 의미 있는 열 이름을 만들려면 스키마와 데이터 유형을 정의해야 합니다. 또한 데이터 유형을 정의하기 위해 표준 Spark SQL 유형 집합을 가져와야 합니다. 기존 코드를 다음으로 바꾸세요.
	암호
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
5. 셀을 실행하고 출력을 검토하세요.
	[![스키마가 정의되어 있고 데이터가 있는 코드의 화면 사진입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/define-schema.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/define-schema.png)
6. 이 DataFrame에는 2019.csv 파일의 데이터만 포함됩니다. 파일 경로에 \* 와일드카드를 사용하여 orders 폴더의 모든 파일을 읽도록 코드를 수정하세요.
	암호
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
7. 수정된 코드를 실행하면 2019년, 2020년, 2021년의 매출을 볼 수 있습니다. 행의 하위 집합만 표시되므로 모든 연도의 행을 볼 수 없을 수도 있습니다.

> **\[!참고\] 결과 옆의 …** 아이콘을 선택하여 셀의 출력을 숨기거나 표시할 수 있습니다 . 이렇게 하면 노트북에서 작업하기가 더 쉬워집니다.

## DataFrame에서 데이터 탐색

DataFrame 객체는 데이터를 필터링, 그룹화, 조작하는 등의 추가 기능을 제공합니다.

### DataFrame 필터링

1. 현재 셀이나 해당 출력 위나 아래에 마우스를 올리면 나타나는 **'+ 코드'** 를 선택하여 코드 셀을 추가합니다. 또는 리본 메뉴에서 **'편집'을** 선택 하고 **'+ 아래에 코드 셀 추가'를** 선택합니다.
2. 다음 코드는 두 개의 열만 반환되도록 데이터를 필터링합니다. 또한 *count* 와 *distinct를* 사용하여 레코드 수를 요약합니다.
	암호
	```python
	customers = df['CustomerName', 'Email']
	print(customers.count())
	print(customers.distinct().count())
	display(customers.distinct())
	```
3. 코드를 실행하고 출력을 살펴보세요.
	- **이 코드는 원래 df** DataFrame 의 열 하위 집합을 포함하는 **customers** 라는 새 DataFrame을 생성합니다 . DataFrame 변환을 수행할 때 원래 DataFrame을 수정하는 대신 새 DataFrame을 반환합니다.
	- 동일한 결과를 얻는 또 다른 방법은 select 메서드를 사용하는 것입니다.
	암호
	```python
	customers = df.select("CustomerName", "Email")
	```
	- DataFrame 함수 *count* 와 *distinct는* 고객 수와 고유 고객 수에 대한 합계를 제공하는 데 사용됩니다.
4. *다음과 같이 select* 와 *where* 함수를 사용하여 코드의 첫 번째 줄을 수정합니다 .
	암호
	```python
	customers = df.select("CustomerName", "Email").where(df['Item']=='Road-250 Red, 52')
	print(customers.count())
	print(customers.distinct().count())
	display(customers.distinct())
	```
5. 수정된 코드를 실행하여 Road-250 Red, 52 제품을 구매한 고객만 선택합니다. 여러 함수를 "체인"하여 한 함수의 출력이 다음 함수의 입력이 되도록 할 수 있습니다. 이 경우, *select* 메서드로 생성된 DataFrame은 필터링 기준을 적용하는 데 사용되는 **where** 메서드 의 원본 DataFrame입니다.

### DataFrame에서 데이터 집계 및 그룹화

1. 코드 셀을 추가하고 다음 코드를 입력하세요.
	암호
	```python
	productSales = df.select("Item", "Quantity").groupBy("Item").sum()
	display(productSales)
	```
2. 코드를 실행해 보세요. 결과에 제품별로 그룹화된 주문 수량 합계가 표시되는 것을 확인할 수 있습니다. *groupBy* 메서드는 행을 Item별로 그룹화하고, 이후 *sum* 집계 함수는 나머지 숫자 열(이 경우 *Quantity)* 에 적용됩니다.
3. 노트북에 다른 코드 셀을 추가하고 다음 코드를 입력합니다.
	암호
	```python
	from pyspark.sql.functions import *
	yearlySales = df.select(year(col("OrderDate")).alias("Year")).groupBy("Year").count().orderBy("Year")
	display(yearlySales)
	```
4. 셀을 실행하고 출력을 검토하세요. 이제 연간 판매 주문 수가 표시됩니다.
	- import 문 *을* 사용하면 Spark SQL 라이브러리를 사용할 수 있습니다.
	- select 메서드 *는 SQL year 함수와 함께 사용되어* *OrderDate* 필드 의 연도 구성 요소를 추출합니다 .
	- 별칭 방법은 추출된 연도 값에 열 이름을 지정하는 데 사용됩니다 *.*
	- groupBy 메서드 *는* 파생된 Year 열을 기준으로 데이터를 그룹화합니다.
	- *orderBy* 메서드를 사용하여 결과 DataFrame을 정렬하기 전에 각 그룹의 행 개수가 계산됩니다.
	[![DataFrame에서 데이터를 집계하고 그룹화한 결과를 보여주는 화면 그림입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/spark-sql-dataframe.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/spark-sql-dataframe.png)

## Spark를 사용하여 데이터 파일을 변환합니다.

데이터 엔지니어와 데이터 과학자의 일반적인 업무는 후속 처리나 분석을 위해 데이터를 변환하는 것입니다.

### DataFrame 메서드와 함수를 사용하여 데이터를 변환합니다.

1. 노트북에 코드 셀을 추가하고 다음을 입력합니다.
	암호
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
2. 셀을 실행합니다. 다음 변환을 사용하여 원래 주문 데이터에서 새 DataFrame이 생성됩니다.
	- OrderDate 열을 기반으로 연도 및 월 열이 추가되었습니다.
	- CustomerName 열을 기반으로 FirstName과 LastName 열이 추가되었습니다.
	- 열이 필터링되고 순서가 변경되었으며, CustomerName 열이 제거되었습니다.
3. 출력을 검토하고 데이터에 변환이 적용되었는지 확인합니다.

Spark SQL 라이브러리를 사용하면 행 필터링, 열 파생, 제거, 이름 변경, 기타 데이터 수정 적용을 통해 데이터를 변환할 수 있습니다.

> \[!TIP\] DataFrame 개체에 대해 자세히 알아보려면 [Apache Spark 데이터프레임 설명서를 참조하세요.](https://spark.apache.org/docs/latest/api/python/reference/pyspark.sql/dataframe.html)

### 변환된 데이터를 저장합니다

이 시점에서는 변환된 데이터를 저장하여 추가 분석에 사용할 수 있습니다.

*Parquet은* 데이터를 효율적으로 저장하고 대부분의 대규모 데이터 분석 시스템에서 지원되기 때문에 널리 사용되는 데이터 저장 형식입니다. 실제로 CSV와 같은 특정 형식의 데이터를 Parquet으로 변환해야 하는 경우도 있습니다.

1. 변환된 DataFrame을 Parquet 형식으로 저장하려면 코드 셀을 추가하고 다음 코드를 추가합니다.
	암호
	```python
	transformed_df.write.mode("overwrite").parquet('Files/transformed_data/orders')
	print ("Transformed data saved!")
	```
2. 셀을 실행하고 데이터가 저장되었다는 메시지가 표시될 때까지 기다립니다. 그런 다음 왼쪽 탐색기 창의 파일 노드에 있는 … 메뉴에서 **새로 고침을** 선택합니다. transformed\_data 폴더를 선택하여 orders라는 새 폴더가 있는지 확인합니다. 이 폴더에는 하나 이상의 Parquet 파일이 있습니다.
3. 다음 코드를 사용하여 셀을 추가합니다.
	암호
	```python
	orders_df = spark.read.format("parquet").load("Files/transformed_data/orders")
	display(orders_df)
	```
4. *셀을 실행합니다. transformed\_data/orders* 폴더 의 Parquet 파일에서 새 DataFrame이 생성됩니다 . Parquet 파일에서 로드된 주문 데이터가 결과에 표시되는지 확인합니다.
	[![Parquet 파일을 보여주는 화면 사진입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/parquet-files.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/parquet-files.png)

### 분할된 파일에 데이터 저장

대량의 데이터를 처리할 때 파티셔닝을 사용하면 성능이 크게 향상되고 데이터 필터링이 더 쉬워집니다.

1. 데이터프레임을 저장하는 코드가 있는 셀을 추가하고 데이터를 연도와 월별로 분할합니다.
	암호
	```python
	orders_df.write.partitionBy("Year","Month").mode("overwrite").parquet("Files/partitioned_data")
	print ("Transformed data saved!")
	```
2. 셀을 실행하고 데이터가 저장되었다는 메시지가 표시될 때까지 기다립니다. 그런 다음 왼쪽 Lakehouses 창의 파일 노드에 있는 … 메뉴에서 **새로 고침을 선택하고 partitioned\_data 폴더를 확장하여** *Year=xxxx* 라는 이름의 폴더 계층 구조가 있는지 확인합니다 . 각 폴더는 *Month=xxxx* 라는 이름의 폴더를 포함합니다. 각 월별 폴더에는 해당 월의 주문 내역이 담긴 Parquet 파일이 있습니다.
	[![연도와 월별로 분할된 데이터를 보여주는 화면 그림입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/partitioned-data.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/partitioned-data.png)
3. orders.parquet 파일에서 새 DataFrame을 로드하려면 다음 코드를 사용하여 새 셀을 추가합니다.
	암호
	```python
	orders_2021_df = spark.read.format("parquet").load("Files/partitioned_data/Year=2021/Month=*")
	display(orders_2021_df)
	```
4. 셀을 실행하고 결과에 2021년 판매 주문 데이터가 표시되는지 확인합니다. 경로에 지정된 분할 열(년 및 월)은 DataFrame에 포함되지 않습니다.

## 테이블과 SQL 작업

이제 DataFrame 객체의 네이티브 메서드를 사용하여 파일의 데이터를 쿼리하고 분석하는 방법을 살펴보았습니다. 하지만 SQL 구문을 사용하여 테이블을 다루는 것이 더 편할 수도 있습니다. Spark는 관계형 테이블을 정의할 수 있는 메타스토어를 제공합니다.

Spark SQL 라이브러리는 메타스토어의 테이블을 쿼리하는 SQL 문을 지원합니다. 이는 관계형 데이터 웨어하우스의 구조화된 데이터 스키마와 SQL 기반 쿼리를 통해 데이터 레이크의 유연성을 제공합니다. 따라서 "데이터 레이크하우스"라는 용어가 탄생했습니다.

### 테이블 만들기

Spark 메타스토어의 테이블은 데이터 레이크의 파일에 대한 관계형 추상화입니다. 테이블은 메타스토어에서 *관리 하거나,* *외부* 에서 메타스토어와 독립적으로 관리할 수 있습니다.

1. 노트북에 코드 셀을 추가하고 다음 코드를 입력하여 판매 주문 데이터의 DataFrame을 *salesorders* 라는 이름의 테이블로 저장합니다.
	암호
	```python
	# Create a new table
	df.write.format("delta").saveAsTable("salesorders")
	# Get the table description
	spark.sql("DESCRIBE EXTENDED salesorders").show(truncate=False)
	```

> \[!NOTE\] 이 예에서는 명시적인 경로가 제공되지 않으므로 테이블 파일은 메타스토어에서 관리됩니다. 또한 테이블은 델타 형식으로 저장되어 테이블에 관계형 데이터베이스 기능을 추가합니다. 여기에는 트랜잭션, 행 버전 관리 및 기타 유용한 기능이 포함됩니다. Fabric의 데이터 레이크하우스에서는 델타 형식으로 테이블을 생성하는 것이 좋습니다.

1. 코드 셀을 실행하고 새 테이블의 정의를 설명하는 출력을 검토합니다.
2. **탐색기** 창의 테이블 폴더에서... 메뉴를 열고 새로 고침을 선택합니다 . **그런** 다음 **테이블 노드를 확장하여** **salesorders** 테이블이 생성되었는지 확인합니다.
	[![판매 주문 테이블이 생성되었음을 보여주는 화면 그림입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/salesorder-table.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/salesorder-table.png)
3. salesorders 테이블의... 메뉴에서 **데이터 로드** \> **Spark를** 선택합니다. 다음과 유사한 코드가 포함된 새 코드 셀이 추가됩니다.
	암호
	```
	df = spark.sql("SELECT * FROM [your_lakehouse].salesorders LIMIT 1000")
	display(df)
	```
4. *Spark SQL 라이브러리를 사용하여 PySpark 코드의 salesorder* 테이블 에 대한 SQL 쿼리를 내장하고 쿼리 결과를 DataFrame에 로드하는 새 코드를 실행합니다.

### 셀에서 SQL 코드 실행

PySpark 코드가 포함된 셀에 SQL 문을 내장할 수 있는 기능은 유용하지만, 데이터 분석가는 종종 SQL에서 직접 작업하고 싶어합니다.

1. 노트북에 새로운 코드 셀을 추가하고 다음 코드를 입력하세요.
	암호
	```
	%%sql
	SELECT YEAR(OrderDate) AS OrderYear,
	       SUM((UnitPrice * Quantity) + Tax) AS GrossRevenue
	FROM salesorders
	GROUP BY YEAR(OrderDate)
	ORDER BY OrderYear;
	```
2. 셀을 실행하고 결과를 검토하세요. 다음 사항을 확인하세요.
	- 셀의 시작 부분에 있는 %% **sql** 명령(매직이라고 함)은 언어를 PySpark 대신 Spark SQL로 변경합니다.
	- SQL 코드는 이전에 만든 *salesorders 테이블을 참조합니다.*
	- SQL 쿼리의 출력은 자동으로 셀 아래에 결과로 표시됩니다.

> \[!NOTE\] Spark SQL 및 데이터프레임에 대한 자세한 내용은 [Apache Spark SQL](https://spark.apache.org/sql/) 설명서를 참조하세요.

## Spark로 데이터 시각화

차트를 사용하면 수천 행의 데이터를 스캔하는 것보다 더 빠르게 패턴과 추세를 파악할 수 있습니다. Fabric 노트북에는 차트 뷰가 내장되어 있지만 복잡한 차트용으로 설계되지 않았습니다. DataFrames의 데이터에서 차트를 생성하는 방식을 더욱 세부적으로 제어하려면 *matplotlib* 이나 *seaborn과* 같은 Python 그래픽 라이브러리를 사용하세요.

### 결과를 차트로 보기

1. 새로운 코드 셀을 추가하고 다음 코드를 입력하세요.
	암호
	```python
	%%sql
	SELECT * FROM salesorders
	```
2. 이전에 만든 판매 주문 뷰의 데이터를 표시하는 코드를 실행합니다. 셀 아래의 결과 섹션에서 **\+ 새 차트를** 선택합니다.
3. 결과 섹션의 오른쪽 하단에 있는 ' **내 차트 만들기** ' 버튼 을 사용하여 차트 설정을 지정합니다.
	- 차트 유형: 막대형 차트
	- X축: 항목
	- Y축: 수량
	- 시리즈 그룹: 비워두세요
	- 집계: 합계
	- 누락된 값 및 NULL 값: 0으로 표시
	- 스택: 선택되지 않음
4. 차트는 다음과 비슷하게 보여야 합니다.
	[![Fabric 노트북 차트 보기의 화면 사진입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/built-in-chart.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/built-in-chart.png)

### matplotlib 시작하기

1. 새로운 코드 셀을 추가하고 다음 코드를 입력하세요.
	암호
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
2. 코드를 실행하세요. 연간 매출과 주문 건수가 포함된 Spark DataFrame을 반환합니다. 데이터를 차트로 시각화하기 위해 먼저 matplotlib Python 라이브러리를 사용하겠습니다. 이 라이브러리는 다른 많은 라이브러리의 기반이 되는 핵심 플로팅 라이브러리이며, 차트를 만드는 데 매우 유연하게 사용할 수 있습니다.
3. 새로운 코드 셀을 추가하고 다음 코드를 추가합니다.
	암호
	```python
	from matplotlib import pyplot as plt
	# matplotlib requires a Pandas dataframe, not a Spark one
	df_sales = df_spark.toPandas()
	# Create a bar plot of revenue by year
	plt.bar(x=df_sales['OrderYear'], height=df_sales['GrossRevenue'])
	# Display the plot
	plt.show()
	```
4. 셀을 실행하고 결과를 검토하세요. 각 연도의 총 매출을 나타내는 세로 막대형 차트가 나타납니다. 코드를 검토하고 다음을 확인하세요.
	- matplotlib 라이브러리에는 Pandas DataFrame이 필요하므로 Spark SQL 쿼리에서 반환된 Spark DataFrame을 변환해야 합니다.
	- matplotlib 라이브러리의 핵심은 *pyplot* 객체입니다. 이는 대부분의 플로팅 기능의 기반이 됩니다.
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