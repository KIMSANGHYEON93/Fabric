---
title: "Visualize data in a Spark notebook - Training"
source: "https://learn.microsoft.com/en-us/training/modules/use-apache-spark-work-files-lakehouse/6-visualize-data"
author:
  - "[[theresa-i]]"
published:
created: 2025-12-03
description: "Visualize data in a Spark notebook"
tags:
  - "clippings"
---
## Spark Notebook에서 데이터 시각화

100 경험치

데이터 쿼리 결과를 분석하는 가장 직관적인 방법 중 하나는 차트로 시각화하는 것입니다. Microsoft Fabric의 Notebook은 사용자 인터페이스에서 몇 가지 기본적인 차트 기능을 제공하며, 이 기능으로 원하는 결과를 얻지 못할 경우 다양한 Python 그래픽 라이브러리 중 하나를 사용하여 노트북에서 데이터 시각화를 만들고 표시할 수 있습니다.

## 내장된 노트북 차트 사용

Spark Notebook에서 데이터프레임을 표시하거나 SQL 쿼리를 실행하면 결과가 코드 셀 아래에 표시됩니다. 기본적으로 결과는 테이블로 렌더링되지만, 결과 뷰를 차트로 변경하고 차트 속성을 사용하여 차트가 데이터를 시각화하는 방식을 사용자 지정할 수도 있습니다(아래 그림 참조).

![카테고리별 제품 수를 나타낸 노트북 차트의 스크린샷입니다.](https://learn.microsoft.com/en-us/training/wwl/use-apache-spark-work-files-lakehouse/media/notebook-chart.png)

노트북에 내장된 차트 기능은 데이터를 시각적으로 빠르게 요약할 때 유용합니다. 데이터 형식을 더욱 세부적으로 제어하고 싶다면 그래픽 패키지를 사용하여 나만의 시각화를 만드는 것을 고려해 보세요.

## 코드에서 그래픽 패키지 사용

코드에서 데이터 시각화를 생성하는 데 사용할 수 있는 다양한 그래픽 패키지가 있습니다. 특히 Python은 다양한 패키지를 지원하며, 대부분은 기본 **Matplotlib** 라이브러리를 기반으로 합니다. 그래픽 라이브러리의 출력은 노트북에서 렌더링할 수 있으므로, 코드를 결합하여 데이터를 수집하고 조작하고, 인라인 데이터 시각화 및 마크다운 셀을 사용하여 주석을 제공하는 것이 용이합니다.

예를 들어, 다음 PySpark 코드를 사용하여 이 모듈에서 이전에 살펴본 가상 제품 데이터에서 데이터를 집계하고, Matplotlib을 사용하여 집계된 데이터에서 차트를 만들 수 있습니다.

```python
from matplotlib import pyplot as plt

# Get the data as a Pandas dataframe
data = spark.sql("SELECT Category, COUNT(ProductID) AS ProductCount \
                  FROM products \
                  GROUP BY Category \
                  ORDER BY Category").toPandas()

# Clear the plot area
plt.clf()

# Create a Figure
fig = plt.figure(figsize=(12,8))

# Create a bar plot of product counts by category
plt.bar(x=data['Category'], height=data['ProductCount'], color='orange')

# Customize the chart
plt.title('Product Counts by Category')
plt.xlabel('Category')
plt.ylabel('Products')
plt.grid(color='#95a5a6', linestyle='--', linewidth=2, axis='y', alpha=0.7)
plt.xticks(rotation=70)

# Show the plot area
plt.show()
```

Matplotlib 라이브러리는 Spark 데이터프레임이 아닌 Pandas 데이터프레임에 데이터를 저장해야 하므로, **toPandas** 메서드를 사용하여 변환합니다. 그런 다음 지정된 크기의 그림을 생성하고, 결과 플롯을 표시하기 전에 사용자 지정 속성 구성을 사용하여 막대 차트를 그립니다.

이 코드로 생성된 차트는 다음 이미지와 비슷하게 보입니다.

![카테고리별 제품 수를 보여주는 막대형 차트의 스크린샷입니다.](https://learn.microsoft.com/en-us/training/wwl/use-apache-spark-work-files-lakehouse/media/chart.png)

Matplotlib 라이브러리를 사용하여 다양한 종류의 차트를 만들 수 있습니다. 또는 선호하는 경우 **Seaborn** 과 같은 다른 라이브러리를 사용하여 고도로 사용자 정의된 차트를 만들 수도 있습니다.