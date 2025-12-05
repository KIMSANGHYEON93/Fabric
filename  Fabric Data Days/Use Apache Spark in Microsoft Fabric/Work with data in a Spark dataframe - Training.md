---
title: "Work with data in a Spark dataframe - Training"
source: "https://learn.microsoft.com/en-us/training/modules/use-apache-spark-work-files-lakehouse/4-dataframe"
author:
  - "[[theresa-i]]"
published:
created: 2025-12-03
description: "Work with data in a Spark dataframe"
tags:
  - "clippings"
---
## Spark 데이터프레임에서 데이터 작업

100 경험치

*Spark는 기본적으로 복원력 있는 분산 데이터* 세트 (RDD) 라는 데이터 구조를 사용합니다. RDD와 직접 연동되는 코드를 작성할 *수도 있지만, Spark에서 구조화된 데이터를 처리하는 데 가장 일반적으로 사용되는 데이터 구조는* *Spark SQL* 라이브러리 의 일부로 제공되는 *데이터프레임 입니다. Spark의 데이터프레임은 널리 사용되는* *Pandas* Python 라이브러리 의 데이터프레임과 유사 하지만, Spark의 분산 처리 환경에서 작동하도록 최적화되어 있습니다.

데이터프레임을 사용하여 데이터 작업을 하는 방법을 알아보기 위해 가상의 예를 살펴보겠습니다. lakehouse의 **Files/data** 폴더 에 **products.csv 라는 쉼표로 구분된 텍스트 파일에 다음 데이터가 있다고 가정해 보겠습니다.**

```csv
ProductID,ProductName,Category,ListPrice
771,"Mountain-100 Silver, 38",Mountain Bikes,3399.9900
772,"Mountain-100 Silver, 42",Mountain Bikes,3399.9900
773,"Mountain-100 Silver, 44",Mountain Bikes,3399.9900
...
```

### 스키마 추론

Spark 노트북에서 다음 PySpark 코드를 사용하여 파일 데이터를 데이터프레임에 로드하고 처음 10개 행을 표시할 수 있습니다.

```python
%%pyspark
df = spark.read.load('Files/data/products.csv',
    format='csv',
    header=True
)
display(df.limit(10))
```

시작 부분의 줄 은 *magic* `%%pyspark` 이라고 하며 , 이 셀에 사용된 언어가 PySpark임을 Spark에 알려줍니다. Notebook 인터페이스의 도구 모음에서 기본 언어로 사용할 언어를 선택한 다음, magic 을 사용하여 특정 셀에 대해 해당 언어를 재정의할 수 있습니다. 예를 들어, 제품 데이터 예제에 대한 동일한 Scala 코드는 다음과 같습니다.

```scala
%%spark
val df = spark.read.format("csv").option("header", "true").load("Files/data/products.csv")
display(df.limit(10))
```

이 마법은 `%%spark` Scala를 지정하는 데 사용됩니다.

두 코드 샘플 모두 다음과 같은 출력을 생성합니다.

| 제품 ID | 제품 이름 | 범주 | 가격표 |
| --- | --- | --- | --- |
| 771 | 마운틴-100 실버, 38 | 산악 자전거 | 3399.9900 |
| 772 | 마운틴-100 실버, 42 | 산악 자전거 | 3399.9900 |
| 773 | 마운틴-100 실버, 44 | 산악 자전거 | 3399.9900 |
| ... | ... | ... | ... |

### 명시적 스키마 지정

이전 예제에서 CSV 파일의 첫 번째 행에는 열 이름이 포함되어 있었고, Spark는 포함된 데이터에서 각 열의 데이터 유형을 유추할 수 있었습니다. 또한, 다음 CSV 예제처럼 데이터 파일에 열 이름이 포함되지 않은 경우, 데이터에 대한 명시적인 스키마를 지정할 수 있습니다.

```csv
771,"Mountain-100 Silver, 38",Mountain Bikes,3399.9900
772,"Mountain-100 Silver, 42",Mountain Bikes,3399.9900
773,"Mountain-100 Silver, 44",Mountain Bikes,3399.9900
...
```

**다음 PySpark 예제는 product-data.csv** 라는 파일에서 이 형식으로 로드할 데이터프레임에 대한 스키마를 지정하는 방법을 보여줍니다.

```python
from pyspark.sql.types import *
from pyspark.sql.functions import *

productSchema = StructType([
    StructField("ProductID", IntegerType()),
    StructField("ProductName", StringType()),
    StructField("Category", StringType()),
    StructField("ListPrice", FloatType())
    ])

df = spark.read.load('Files/data/product-data.csv',
    format='csv',
    schema=productSchema,
    header=False)
display(df.limit(10))
```

결과는 다시 다음과 유사합니다.

| 제품 ID | 제품 이름 | 범주 | 가격표 |
| --- | --- | --- | --- |
| 771 | 마운틴-100 실버, 38 | 산악 자전거 | 3399.9900 |
| 772 | 마운틴-100 실버, 42 | 산악 자전거 | 3399.9900 |
| 773 | 마운틴-100 실버, 44 | 산악 자전거 | 3399.9900 |
| ... | ... | ... | ... |

## 데이터 프레임 필터링 및 그룹화

Dataframe 클래스의 메서드를 사용하여 포함된 데이터를 필터링, 정렬, 그룹화하고 기타 조작할 수 있습니다. 예를 들어, 다음 코드 예제는 **select** 메서드를 사용하여 이전 예제의 제품 데이터가 포함된 **df** 데이터프레임 에서 **ProductID** 및 **ListPrice** 열을 검색합니다.

```python
pricelist_df = df.select("ProductID", "ListPrice")
```

The results from this code example would look something like this:

| ProductID | ListPrice |
| --- | --- |
| 771 | 3399.9900 |
| 772 | 3399.9900 |
| 773 | 3399.9900 |
| ... | ... |

In common with most data manipulation methods, **select** returns a new dataframe object.

You can "chain" methods together to perform a series of manipulations that results in a transformed dataframe. For example, this example code chains the **select** and **where** methods to create a new dataframe containing the **ProductName** and **ListPrice** columns for products with a category of **Mountain Bikes** or **Road Bikes**:

```python
bikes_df = df.select("ProductName", "Category", "ListPrice").where((df["Category"]=="Mountain Bikes") | (df["Category"]=="Road Bikes"))
display(bikes_df)
```

The results from this code example would look something like this:

| ProductName | Category | ListPrice |
| --- | --- | --- |
| Mountain-100 Silver, 38 | Mountain Bikes | 3399.9900 |
| Road-750 Black, 52 | Road Bikes | 539.9900 |
| ... | ... | ... |

To group and aggregate data, you can use the **groupBy** method and aggregate functions. For example, the following PySpark code counts the number of products for each category:

```python
counts_df = df.select("ProductID", "Category").groupBy("Category").count()
display(counts_df)
```

The results from this code example would look something like this:

| Category | count |
| --- | --- |
| Headsets | 3 |
| Wheels | 14 |
| Mountain Bikes | 32 |
| ... | ... |

## Saving a dataframe

You'll often want to use Spark to transform raw data and save the results for further analysis or downstream processing. The following code example saves the dataFrame into a *parquet* file in the data lake, replacing any existing file of the same name.

```python
bikes_df.write.mode("overwrite").parquet('Files/product_data/bikes.parquet')
```

### Partitioning the output file

Partitioning is an optimization technique that enables Spark to maximize performance across the worker nodes. More performance gains can be achieved when filtering data in queries by eliminating unnecessary disk IO.

To save a dataframe as a partitioned set of files, use the **partitionBy** method when writing the data. The following example saves the **bikes\_df** dataframe (which contains the product data for the *mountain bikes* and *road bikes* categories), and partitions the data by category:

```python
bikes_df.write.partitionBy("Category").mode("overwrite").parquet("Files/bike_data")
```

The folder names generated when partitioning a dataframe include the partitioning column name and value in a ***column=value*** format, so the code example creates a folder named **bike\_data** that contains the following subfolders:

- **Category=Mountain Bikes**
- **Category=Road Bikes**

Each subfolder contains one or more parquet files with the product data for the appropriate category.

## 분할된 데이터 로드

분할된 데이터를 데이터프레임으로 읽어올 때, 분할된 필드에 명시적 값이나 와일드카드를 지정하여 계층 구조 내 모든 폴더의 데이터를 로드할 수 있습니다. 다음 예제는 **Road Bikes** 카테고리의 제품에 대한 데이터를 로드합니다.

```python
road_bikes_df = spark.read.parquet('Files/bike_data/Category=Road Bikes')
display(road_bikes_df.limit(5))
```