---
title: "모니터링 허브에서 Fabric 활동 모니터링 | mslearn-fabric"
source: "https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/18-monitor-hub.html"
author:
published:
created: 2025-12-03
description:
tags:
  - "clippings"
---
## 모니터링 허브에서 Fabric 활동을 모니터링합니다.

Microsoft Fabric의 모니터링 *허브는* 활동을 모니터링할 수 있는 중앙 공간을 제공합니다. 모니터링 허브를 사용하여 보기 권한이 있는 항목과 관련된 이벤트를 검토할 수 있습니다.

이 실험을 완료하는 데 약 **30** 분이 걸립니다.

> **참고**: 이 연습을 완료하려면 [Microsoft Fabric 테넌트](https://learn.microsoft.com/fabric/get-started/fabric-trial) 에 액세스해야 합니다.

## 작업 공간 만들기

Fabric에서 데이터 작업을 하기 전에 Fabric 용량이 활성화된 테넌트에 작업 공간을 만듭니다.

1. 브라우저 에서 [Microsoft Fabric 홈페이지](https://app.fabric.microsoft.com/home?experience=fabric-developer) 로 이동하여 `https://app.fabric.microsoft.com/home?experience=fabric-developer` Fabric 자격 증명을 사용하여 로그인합니다.
2. 왼쪽 메뉴 모음에서 **작업 공간을** 선택하세요 (아이콘은 🗇와 비슷합니다).
3. 원하는 이름으로 새 작업 공간을 만들고, **고급 섹션에서 Fabric 용량(** *평가판*, *프리미엄* 또는 *Fabric* ) 을 포함하는 라이선스 모드를 선택합니다 .
4. 새로운 작업 공간이 열리면 비어 있어야 합니다.
	[![Fabric의 빈 작업 공간 스크린샷.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/new-workspace.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/new-workspace.png)

## 호숫가 주택 만들기

이제 작업 공간이 생겼으니 데이터를 위한 데이터 레이크하우스를 만들 차례입니다.

1. 왼쪽 메뉴 모음에서 **'만들기'를** 선택합니다. *'새로 만들기* ' 페이지 의 *'데이터 엔지니어링 ' 섹션에서* **'Lakehouse'를** 선택합니다 . 원하는 고유한 이름을 지정합니다. "Lakehouse 스키마(공개 미리 보기)" 옵션이 비활성화되어 있는지 확인합니다.
	> **참고**: **만들기** 옵션이 사이드바에 고정되어 있지 않으면 먼저 줄임표( **…** ) 옵션을 선택해야 합니다.
	1분 정도 후에 새로운 호숫가 주택이 생성됩니다.
	[![새로운 호숫가 주택의 스크린샷.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/new-lakehouse.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/new-lakehouse.png)
2. 새로운 레이크하우스를 보고, 왼쪽의 **레이크하우스 탐색기 창을 통해 레이크하우스의 테이블과 파일을 탐색할 수 있습니다.**
	현재 레이크하우스에는 테이블이나 파일이 없습니다.

## 데이터 흐름 생성 및 모니터링

Microsoft Fabric에서는 데이터 흐름(Gen2)을 사용하여 다양한 소스의 데이터를 수집할 수 있습니다. 이 연습에서는 데이터 흐름을 사용하여 CSV 파일에서 데이터를 가져와 레이크하우스의 테이블에 로드합니다.

1. **레이크** 하우스 홈페이지의 데이터 가져오기 메뉴에서 새 **데이터** **흐름 Gen2를** 선택합니다 .
2. 새로운 데이터 흐름의 이름을 지정 `Get Product Data` 하고 **만들기를** 선택합니다.
	[![새로운 데이터 흐름의 스크린샷.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/new-data-flow.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/new-data-flow.png)
3. 데이터 흐름 디자이너에서 **'텍스트/CSV 파일에서 가져오기'를** 선택합니다. 그런 다음 데이터 가져오기 마법사를 완료하여 익명 인증을 사용하여 데이터 연결을 만듭니다 `https://raw.githubusercontent.com/MicrosoftLearning/dp-data/main/products.csv`. 마법사를 완료하면 데이터 흐름 디자이너에 다음과 같이 데이터 미리보기가 표시됩니다.
	[![데이터 흐름 쿼리의 스크린샷.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/data-flow-query.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/data-flow-query.png)
4. Publish the dataflow.
5. In the navigation bar on the left, select **Monitor** to view the monitoring hub and observe that your dataflow is in-progress (if not, refresh the view until you see it).
	[![진행 중인 데이터 흐름이 있는 모니터링 허브의 스크린샷입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/monitor-dataflow.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/monitor-dataflow.png)
6. Wait for a few seconds, and then refresh the page until the status of the dataflow is **Succeeded**.
7. In the navigation pane, select your lakehouse. Then expand the **Tables** folder to verify that a table named **products** has been created and loaded by the dataflow (you may need to refresh the **Tables** folder).
	[![레이크하우스 페이지의 제품 테이블 스크린샷입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/products-table.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/products-table.png)

## Create and monitor a Spark notebook

In Microsoft Fabric, you can use notebooks to run Spark code.

1. On the menu bar on the left, select **Create**. In the *New* page, under the *Data Engineering* section, select **Notebook**.
	A new notebook named **Notebook 1** is created and opened.
	[![새로운 노트북의 스크린샷.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/new-notebook.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/new-notebook.png)
2. At the top left of the notebook, select **Notebook 1** to view its details, and change its name to `Query Products`.
3. In the notebook editor, in the **Explorer** pane, select **Add data items** and then select **Existing data sources**.
4. Add the lakehouse you created previously.
5. Expand the lakehouse item until you reach the **products** table.
6. In the **…** menu for the **products** table, select **Load data** > **Spark**. This adds a new code cell to the notebook as shown here:
	[![테이블을 쿼리하는 코드가 있는 노트북의 스크린샷입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/load-spark.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/load-spark.png)
7. Use the **▷ Run all** button to run all cells in the notebook. It will take a moment or so to start the Spark session, and then the results of the query will be shown under the code cell.
	[![쿼리 결과가 있는 노트북의 스크린샷입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/notebook-output.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/notebook-output.png)
8. On the toolbar, use the **◻** (*Stop session*) button to stop the Spark session.
9. In the navigation bar, select **Monitor** to view the monitoring hub, and note that the notebook activity is listed.
	[![노트북 활동이 포함된 모니터링 허브의 스크린샷입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/monitor-notebook.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/monitor-notebook.png)

## Monitor history for an item

Some items in a workspace might be run multiple times. You can use the monitoring hub to view their run history.

1. In the navigation bar, return to the page for your workspace. Then use the **↻** (*Refresh now*) button for your **Get Product Data** dataflow to re-run it.
2. In the navigation pane, select the **Monitor** page to view the monitoring hub and verify that the dataflow is in-progress.
3. In the **…** menu for the **Get Product Data** dataflow, select **Historical runs** to view the run history for the dataflow:
	[![모니터링 허브의 과거 실행 보기의 스크린샷입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/historical-runs.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/historical-runs.png)
4. **...** 메뉴 에서 과거 실행 내역을 보려면 세부 **정보 보기를** 선택하세요.
5. **세부 정보** 창을 닫고 **기본 보기로 돌아가기** 버튼을 사용하여 기본 모니터링 허브 페이지로 돌아갑니다.

## 모니터링 허브 보기 사용자 정의

이 연습에서는 몇 가지 활동만 실행했으므로 모니터링 허브에서 이벤트를 찾는 것은 비교적 쉽습니다. 하지만 실제 환경에서는 많은 이벤트를 검색해야 할 수도 있습니다. 필터 및 기타 뷰 사용자 지정 기능을 사용하면 더 쉽게 검색할 수 있습니다.

1. 모니터링 허브에서 **필터** 버튼을 사용하여 다음 필터를 적용하세요.
	- **상태**: 성공
	- **항목 유형**: Dataflow Gen2
	필터를 적용하면 성공적으로 실행된 데이터 흐름만 나열됩니다.
	[![필터가 적용된 모니터링 허브의 스크린샷입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/monitor-filter.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/monitor-filter.png)
2. **열 옵션** 버튼을 사용하여 다음 열을 보기에 포함합니다( **적용** 버튼을 사용하여 변경 사항을 적용합니다).
	- 활동 이름
	- 상태
	- 품목 유형
	- 시작 시간
	- 제출자
	- 위치
	- 종료 시간
	- 지속
	- 새로고침 유형
	모든 열을 보려면 수평으로 스크롤해야 할 수도 있습니다.
	[![사용자 정의 열이 있는 모니터링 허브의 스크린샷입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/monitor-columns.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/monitor-columns.png)

## 자원 정리

이 연습에서는 레이크하우스, 데이터 흐름, Spark 노트북을 만들었고 모니터링 허브를 사용하여 항목 활동을 확인했습니다.

호숫가 주택 탐험을 마쳤다면 이 연습을 위해 만든 작업 공간을 삭제할 수 있습니다.

1. 왼쪽 막대에서 작업 공간 아이콘을 선택하면 해당 작업 공간에 포함된 모든 항목을 볼 수 있습니다.
2. **도구 모음의 …** 메뉴 에서 **작업 공간 설정을** 선택합니다 .
3. **일반** 섹션 에서 **이 작업 공간 제거를** 선택합니다.