---
title: "Work with data using Spark SQL - Training"
source: "https://learn.microsoft.com/en-us/training/modules/use-apache-spark-work-files-lakehouse/5-spark-sql"
author:
  - "[[theresa-i]]"
published:
created: 2025-12-03
description: "Work with data using Spark SQL"
tags:
  - "clippings"
---
## Spark SQL을 사용하여 데이터 작업

100 경험치

Dataframe API는 Spark SQL이라는 Spark 라이브러리의 일부로, 데이터 분석가가 SQL 표현식을 사용하여 데이터를 쿼리하고 조작할 수 있도록 해줍니다.

## Spark 카탈로그에서 데이터베이스 객체 생성

Spark 카탈로그는 뷰 및 테이블과 같은 관계형 데이터 객체를 위한 메타스토어입니다. Spark 런타임은 이 카탈로그를 사용하여 Spark 지원 언어로 작성된 코드를 일부 데이터 분석가나 개발자에게 더 친숙할 수 있는 SQL 표현식과 원활하게 통합할 수 있습니다.

Spark 카탈로그에서 쿼리를 위해 데이터프레임의 데이터를 사용할 수 있게 하는 가장 간단한 방법 중 하나는 다음 코드 예제에서 볼 수 있듯이 임시 뷰를 만드는 것입니다.

```python
df.createOrReplaceTempView("products_view")
```

뷰 *는* 임시적이므로 현재 세션이 종료되면 자동으로 삭제됩니다. 카탈로그에 저장되는 *테이블을 생성하여 Spark SQL을 사용하여 쿼리할 수 있는 데이터베이스를 정의할 수도 있습니다.*

테이블은 카탈로그와 연결된 저장 위치에 기본 데이터를 저장하는 메타데이터 구조입니다. Microsoft Fabric에서 *관리형 테이블의 데이터는 데이터 레이크에 표시된* **테이블** 저장 위치 에 저장되며 , Spark를 사용하여 생성된 모든 테이블은 해당 위치에 나열됩니다.

이 메서드를 사용하여 빈 테이블을 만들 `spark.catalog.createTable` 거나, 해당 메서드를 사용하여 데이터프레임을 테이블로 저장할 수 있습니다 `saveAsTable`. 관리형 테이블을 삭제하면 해당 테이블의 기본 데이터도 삭제됩니다.

예를 들어, 다음 코드는 데이터 프레임을 **products** 라는 이름의 새 테이블로 저장합니다.

```python
df.write.format("delta").saveAsTable("products")
```

또한, 이 메서드를 사용하여 *외부* 테이블을 생성할 수 있습니다 `spark.catalog.createExternalTable`. 외부 테이블은 카탈로그에 메타데이터를 정의하지만, 기본 데이터는 외부 저장소 위치(일반적으로 레이크하우스의 **파일** 저장소 영역에 있는 폴더)에서 가져옵니다. 외부 테이블을 삭제해도 기본 데이터는 삭제되지 않습니다.

## Spark SQL API를 사용하여 데이터 쿼리하기

어떤 언어로 작성된 코드에서든 Spark SQL API를 사용하여 카탈로그의 데이터를 쿼리할 수 있습니다. 예를 들어, 다음 PySpark 코드는 SQL 쿼리를 사용하여 **products** 테이블의 데이터를 데이터프레임으로 반환합니다.

```python
bikes_df = spark.sql("SELECT ProductID, ProductName, ListPrice \
                      FROM products \
                      WHERE Category IN ('Mountain Bikes', 'Road Bikes')")
display(bikes_df)
```

코드 예제의 결과는 다음 표와 유사합니다.

| 제품 ID | 제품 이름 | 가격표 |
| --- | --- | --- |
| 771 | 마운틴-100 실버, 38 | 3399.9900 |
| 839 | 로드-750 블랙, 52 | 539.9900 |
| ... | ... | ... |

## SQL 코드 사용

이전 예제에서는 Spark SQL API를 사용하여 Spark 코드에 SQL 표현식을 삽입하는 방법을 보여주었습니다. 노트북에서는 `%%sql` 다음과 같이 카탈로그의 객체를 쿼리하는 SQL 코드를 실행하는 데에도 이 기능을 사용할 수 있습니다.

```sql
%%sql

SELECT Category, COUNT(ProductID) AS ProductCount
FROM products
GROUP BY Category
ORDER BY Category
```

SQL 코드 예제는 노트북에 테이블로 자동 표시되는 결과 집합을 반환합니다.

| 범주 | 제품 개수 |
| --- | --- |
| 비브 반바지 | 3 |
| 자전거 거치대 | 1 |
| 자전거 스탠드 | 1 |
| ... | ... |