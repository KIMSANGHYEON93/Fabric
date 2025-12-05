---
title: "Microsoft Fabric Lakehouse 만들기 | mslearn-fabric"
source: "https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/01-lakehouse.html"
author:
published:
created: 2025-12-03
description:
tags:
  - "clippings"
---
## Microsoft Fabric Lakehouse 만들기

대규모 데이터 분석 솔루션은 전통적으로 데이터가 관계형 테이블에 저장되고 SQL을 사용하여 쿼리되는 *데이터 웨어하우스를 중심으로 구축되었습니다. "빅 데이터"(높은* *볼륨*, *다양성* 및 새로운 데이터 자산의 *속도가* 특징 )의 성장과 저비용 스토리지 및 클라우드 규모의 분산 컴퓨팅 기술의 가용성으로 인해 분석 데이터 저장소에 대한 대체 접근 방식인 데이터 *레이크가* 탄생했습니다. 데이터 레이크에서 데이터는 고정된 저장 스키마를 적용하지 않고 파일로 저장됩니다. 점점 더 많은 데이터 엔지니어와 분석가가 이 두 접근 방식의 가장 좋은 기능을 결합하여 *데이터 레이크하우스* 에서 이점을 얻으려고 합니다. 여기서 데이터는 데이터 레이크의 파일로 저장되고 관계형 스키마가 메타데이터 계층으로 적용되어 기존 SQL 의미 체계를 사용하여 쿼리할 수 있습니다.

Microsoft Fabric에서 레이크하우스는 Azure Data Lake Store Gen2 기반 *OneLake 저장소에 확장성이 뛰어난 파일 저장소를 제공하며, 오픈 소스* *Delta Lake* 테이블 형식을 기반으로 테이블 및 뷰와 같은 관계형 객체를 위한 메타스토어를 제공합니다. Delta Lake를 사용하면 레이크하우스에서 SQL을 사용하여 쿼리할 수 있는 테이블 스키마를 정의할 수 있습니다.

이 실험을 완료하는 데 약 **30** 분이 걸립니다.

> **참고**: 이 연습을 완료하려면 [Microsoft Fabric 평가판](https://learn.microsoft.com/fabric/get-started/fabric-trial) 이 필요합니다.

## 작업 공간 만들기

Fabric에서 데이터 작업을 하기 전에 Fabric 평가판을 활성화하여 작업 공간을 만드세요.

1. 브라우저 에서 [Microsoft Fabric 홈페이지](https://app.fabric.microsoft.com/home?experience=fabric) 로 이동하여 `https://app.fabric.microsoft.com/home?experience=fabric` Fabric 자격 증명을 사용하여 로그인합니다.
2. 왼쪽 메뉴 모음에서 **작업 공간을** 선택하세요 (아이콘은 🗇와 비슷합니다).
3. 원하는 이름으로 새 작업 공간을 만들고, **고급 섹션에서 Fabric 용량(** *평가판*, *프리미엄* 또는 *Fabric* ) 을 포함하는 라이선스 모드를 선택합니다 .
4. 새 작업 공간이 열리면 비어 있어야 합니다.
	[![Fabric의 빈 작업 공간 스크린샷.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/new-workspace.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/new-workspace.png)

## 호숫가 주택 만들기

이제 작업 공간이 생겼으니 데이터 파일을 위한 데이터 레이크하우스를 만들 차례입니다.

1. 왼쪽 메뉴 모음에서 **'만들기'를** 선택합니다. *'새로 만들기* ' 페이지 의 *'데이터 엔지니어링 ' 섹션에서* **'Lakehouse'를** 선택합니다 . 원하는 고유한 이름을 지정합니다. "Lakehouse 스키마(공개 미리 보기)" 옵션이 비활성화되어 있는지 확인합니다.
	> **참고**: **만들기** 옵션이 사이드바에 고정되어 있지 않으면 먼저 줄임표( **…** ) 옵션을 선택해야 합니다.
	1분 정도 후에 새로운 호숫가 주택이 생성됩니다.
	[![새로운 호숫가 주택의 스크린샷.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/new-lakehouse.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/new-lakehouse.png)
2. 새로운 레이크하우스를 보고, 왼쪽의 **레이크하우스 탐색기 창을 통해 레이크하우스의 테이블과 파일을 탐색할 수 있습니다.**
	- 테이블 폴더에는 SQL 시맨틱을 사용하여 쿼리할 수 있는 테이블이 포함되어 있습니다. Microsoft Fabric 레이크하우스의 테이블 **은** Apache Spark에서 일반적으로 사용되는 오픈 소스 *Delta Lake 파일 형식을 기반으로 합니다.*
	- 파일 **폴더** 에는 관리형 델타 테이블과 연결되지 않은 레이크하우스용 OneLake 저장소의 데이터 파일이 들어 있습니다. 이 폴더에 *바로 가기를* 만들어 외부에 저장된 데이터를 참조할 수도 있습니다.
	현재 레이크하우스에는 테이블이나 파일이 없습니다.

## 파일 업로드

Fabric은 외부 소스에서 데이터를 복사하는 파이프라인과 Power Query 기반 시각적 도구를 사용하여 정의할 수 있는 데이터 흐름(Gen 2)을 포함하여 레이크하우스에 데이터를 로드하는 다양한 방법을 제공합니다. 하지만 소량의 데이터를 수집하는 가장 간단한 방법 중 하나는 로컬 컴퓨터(또는 해당되는 경우 랩 VM)에서 파일이나 폴더를 업로드하는 것입니다.

1. 에서 [sales.csv](https://raw.githubusercontent.com/MicrosoftLearning/dp-data/main/sales.csv) 파일을 다운로드하여 로컬 컴퓨터(또는 해당되는 경우 랩 VM)에 **sales.csv** `https://raw.githubusercontent.com/MicrosoftLearning/dp-data/main/sales.csv` 라는 이름으로 저장합니다.
	> **참고**: 파일을 다운로드하려면 브라우저에서 새 탭을 열고 URL을 붙여넣으세요. 데이터가 있는 페이지의 아무 곳이나 마우스 오른쪽 버튼으로 클릭하고 '다른 이름으로 **저장'을** 선택하여 페이지를 CSV 파일로 저장하세요.
2. 레이크하우스가 있는 웹 브라우저 탭으로 돌아가서 **탐색기 창의** **파일** 폴더 에 대한 **...** 메뉴에서 **새 하위 폴더를** 선택 하고 **data** 라는 이름의 하위 폴더를 만듭니다 .
3. 새 **데이터 폴더의** **...** 메뉴 에서 **업로드** 및 **파일 업로드를** 선택한 다음 로컬 컴퓨터(또는 해당되는 경우 랩 VM)에서 **sales.csv 파일을 업로드합니다.**
4. 파일을 업로드한 후 **Files/data 폴더를 선택하고 여기에 표시된 대로** **sales.csv** 파일이 업로드되었는지 확인하세요.
	[![레이크하우스에 업로드된 sales.csv 파일의 스크린샷입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/uploaded-sales-file.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/uploaded-sales-file.png)
5. **sales.csv** 파일을 선택하여 내용을 미리 보세요.

## 단축키 탐색

In many scenarios, the data you need to work with in your lakehouse may be stored in some other location. While there are many ways to ingest data into the OneLake storage for your lakehouse, another option is to instead create a *shortcut*. Shortcuts enable you to include externally sourced data in your analytics solution without the overhead and risk of data inconsistency associated with copying it.

1. In the **…** menu for the **Files** folder, select **New shortcut**.
2. View the available data source types for shortcuts. Then close the **New shortcut** dialog box without creating a shortcut.

## Load file data into a table

The sales data you uploaded is in a file, which data analysts and engineers can work with directly by using Apache Spark code. However, in many scenarios you may want to load the data from the file into a table so that you can query it using SQL.

1. In the **Explorer** pane, select the **Files/data** folder so you can see the **sales.csv** file it contains.
2. In the **…** menu for the **sales.csv** file, select **Load to Tables** > **New table**.
3. In **Load to table** dialog box, set the table name to **sales** and confirm the load operation. Then wait for the table to be created and loaded.
	> **Tip**: If the **sales** table does not automatically appear, in the **…** menu for the **Tables** folder, select **Refresh**.
4. In the **Explorer** pane, select the **sales** table that has been created to view the data.
	[![테이블 미리보기의 스크린샷입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/table-preview.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/table-preview.png)
5. In the **…** menu for the **sales** table, select **View files** to see the underlying files for this table
	[![테이블 미리보기의 스크린샷입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/delta-table-files.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/delta-table-files.png)
	Files for a delta table are stored in *Parquet* format, and include a subfolder named **\_delta\_log** in which details of transactions applied to the table are logged.

## Use SQL to query tables

When you create a lakehouse and define tables in it, a SQL endpoint is automatically created through which the tables can be queried using SQL `SELECT` statements.

1. At the top-right of the Lakehouse page, switch from **Lakehouse** to **SQL analytics endpoint**. Then wait a short time until the SQL analytics endpoint for your lakehouse opens in a visual interface from which you can query its tables.
2. Use the **New SQL query** button to open a new query editor, and enter the following SQL query:
	sql
	```sql
	SELECT Item, SUM(Quantity * UnitPrice) AS Revenue
	FROM sales
	GROUP BY Item
	ORDER BY Revenue DESC;
	```
	> **참고**: 랩 VM에서 SQL 쿼리를 입력하는 데 문제가 있는 경우, 에서 [01-Snippets.txt](https://github.com/MicrosoftLearning/mslearn-fabric/raw/main/Allfiles/Labs/01/Assets/01-Snippets.txt) `https://github.com/MicrosoftLearning/mslearn-fabric/raw/main/Allfiles/Labs/01/Assets/01-Snippets.txt` 파일을 다운로드하여 VM에 저장할 수 있습니다. 그런 다음 텍스트 파일에서 쿼리를 복사할 수 있습니다.
3. **▷ 실행** 버튼을 사용하여 쿼리를 실행하고 결과를 확인하세요. 결과에는 각 제품의 총 수익이 표시됩니다.
	[![결과가 표시된 SQL 쿼리의 스크린샷입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/sql-query.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/sql-query.png)

## 시각적 쿼리 만들기

많은 데이터 전문가가 SQL에 익숙하지만, Power BI 경험이 있는 데이터 분석가는 Power Query 기술을 적용하여 시각적 쿼리를 만들 수 있습니다.

1. 도구 모음에서 **새 SQL 쿼리** 옵션을 확장하고 **새 시각적 쿼리를** 선택합니다.
2. **여기에 표시된 대로 Power Query를 만들려면 판매** 테이블을 새 시각적 쿼리 편집기 창으로 끌어다 놓습니다.
	[![시각적 쿼리의 스크린샷입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/visual-query.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/visual-query.png)
3. **열 관리** 메뉴 에서 **열 선택을** 선택합니다 . 그런 다음 **SalesOrderNumber** 및 **SalesOrderLineNumber** 열만 선택합니다.
	[![열 선택 대화 상자의 스크린샷입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/choose-columns.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/choose-columns.png)
4. **변형** 메뉴 에서 **그룹화 기준을** 선택하세요 . 그런 다음 다음 **기본** 설정을 사용하여 데이터를 그룹화하세요.
	- **그룹화 기준**: SalesOrderNumber
	- **새 열 이름**: LineItems
	- **작업**: 고유한 값 계산
	- **열**: SalesOrderLineNumber
	작업이 완료되면 시각적 쿼리 아래의 결과 창에 각 판매 주문에 대한 품목 수가 표시됩니다.
	[![결과가 표시된 시각적 쿼리의 스크린샷입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/visual-query-results.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/visual-query-results.png)

## 자원 정리

이 연습에서는 레이크하우스를 만들고 데이터를 가져왔습니다. 레이크하우스가 OneLake 데이터 저장소에 저장된 파일과 테이블로 구성되는 방식을 살펴보았습니다. 관리되는 테이블은 SQL을 사용하여 쿼리할 수 있으며, 데이터 시각화를 지원하기 위해 기본 시맨틱 모델에 포함됩니다.

호숫가 주택 탐험을 마쳤다면 이 연습을 위해 만든 작업 공간을 삭제할 수 있습니다.

1. 왼쪽 막대에서 작업 공간 아이콘을 선택하면 해당 작업 공간에 포함된 모든 항목을 볼 수 있습니다.
2. 도구 모음에서 **작업 공간 설정을** 선택합니다.
3. **일반** 섹션 에서 **이 작업 공간 제거를** 선택합니다.