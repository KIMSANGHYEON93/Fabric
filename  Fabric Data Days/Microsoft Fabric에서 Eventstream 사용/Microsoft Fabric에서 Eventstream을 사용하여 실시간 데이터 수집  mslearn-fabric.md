---
title: "Microsoft Fabric에서 Eventstream을 사용하여 실시간 데이터 수집 | mslearn-fabric"
source: "https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/09-real-time-analytics-eventstream.html"
author:
published:
created: 2025-12-03
description:
tags:
  - "clippings"
---
## Microsoft Fabric에서 Eventstream을 사용하여 실시간 데이터 수집

이벤트스트림은 Microsoft Fabric의 기능으로, 실시간 이벤트를 캡처, 변환 및 다양한 대상으로 라우팅합니다. 이벤트 스트림에 이벤트 데이터 원본, 대상 및 변환을 추가할 수 있습니다.

이 연습에서는 사람들이 도시 내에서 자전거를 빌릴 수 있는 자전거 공유 시스템에서 자전거 수집 지점에 대한 관찰과 관련된 이벤트 스트림을 방출하는 샘플 데이터 소스에서 데이터를 수집합니다.

이 실험을 완료하는 데 약 **30** 분이 걸립니다.

> **참고**: 이 연습을 완료하려면 [Microsoft Fabric 테넌트가](https://learn.microsoft.com/fabric/get-started/fabric-trial) 필요합니다.

## 작업 공간 만들기

Fabric에서 데이터 작업을 하기 전에 Fabric 용량이 활성화된 작업 공간을 만들어야 합니다.

1. 브라우저 에서 [Microsoft Fabric 홈페이지](https://app.fabric.microsoft.com/home?experience=fabric) 로 이동하여 `https://app.fabric.microsoft.com/home?experience=fabric` Fabric 자격 증명을 사용하여 로그인합니다.
2. 왼쪽 메뉴 모음에서 **작업 공간을** 선택하세요 (아이콘은 🗇와 비슷합니다).
3. 원하는 이름으로 새 작업 공간을 만들고 Fabric 용량( *평가판*, *프리미엄* 또는 *Fabric* )을 포함하는 라이선스 모드를 선택합니다.
4. 새로운 작업 공간이 열리면 비어 있어야 합니다.
	[![Fabric의 빈 작업 공간 스크린샷.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/new-workspace.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/new-workspace.png)

## 이벤트 하우스를 만들어 보세요

이제 작업 공간이 생겼으니 실시간 인텔리전스 솔루션에 필요한 Fabric 항목을 만들 수 있습니다. 먼저 이벤트 하우스를 만들어 보겠습니다.

1. 방금 만든 작업 공간에서 **\+ 새 항목을** 선택합니다. *새 항목 창에서* **Eventhouse를** 선택 하고 원하는 고유한 이름을 지정합니다.
2. 새로운 빈 이벤트 하우스가 보일 때까지 표시되는 모든 팁이나 메시지를 닫으세요.
	[![새로운 이벤트 하우스의 스크린샷](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/create-eventhouse.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/create-eventhouse.png)
3. 왼쪽 창에서 이벤트하우스에 이벤트하우스와 같은 이름의 KQL 데이터베이스가 포함되어 있는지 확인하세요.
4. KQL 데이터베이스를 선택하여 보세요.
	현재 데이터베이스에 테이블이 없습니다. 이 연습의 나머지 부분에서는 이벤트스트림을 사용하여 실시간 소스에서 테이블에 데이터를 로드합니다.

## 이벤트스트림 만들기

1. KQL 데이터베이스의 메인 페이지에서 **데이터 가져오기를** 선택합니다.
2. 데이터 소스에서 **'이벤트스트림'** \> **'새 이벤트스트림'을** 선택합니다. 이벤트스트림의 이름을 지정합니다 `Bicycle-data`.
	작업 공간에서 새 이벤트 스트림을 만드는 작업은 몇 분 안에 완료됩니다. 스트림을 생성하면 기본 편집 페이지로 자동 리디렉션되어 이벤트 스트림에 소스를 통합할 수 있습니다.
	[![새로운 이벤트 스트림의 스크린샷.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/empty-eventstream.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/empty-eventstream.png)

## 소스 추가

1. 이벤트스트림 캔버스에서 **샘플 데이터 사용을** 선택합니다.
2. 소스 이름을 지정 `Bicycles` 하고 **Bicycles** 샘플 데이터를 선택합니다.
	Your stream will be mapped and you will be automatically displayed on the **eventstream canvas**.
	[![이벤트스트림 캔버스를 검토하세요](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/real-time-intelligence-eventstream-sourced.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/real-time-intelligence-eventstream-sourced.png)

## Add a destination

1. Select the **Transform events or add destination** tile and search for **Eventhouse**.
2. In the **Eventhouse** pane, configure the following setup options.
	- **Data ingestion mode:**: Event processing before ingestion
	- **Destination name:**`bikes-table`
	- **Workspace:***Select the workspace you created at the beginning of this exercise*
	- **Eventhouse**: *Select your eventhouse*
	- **KQL database:***Select your KQL database*
	- **Destination table:** Create a new table named `bikes`
	- **Input data format:** JSON
	[![이벤트스트림 대상 설정.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/kql-database-event-processing-before-ingestion.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/kql-database-event-processing-before-ingestion.png)
3. In the **Eventhouse** pane, select **Save**.
4. On the toolbar, select **Publish**.
5. Wait a minute or so for the data destination to become active. Then select the **bikes-table** node in the design canvas and view the **Data preview** pane underneath to see the latest data that has been ingested:
	[![이벤트스트림의 대상 테이블.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/stream-data-preview.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/stream-data-preview.png)
6. Wait a few minutes and then use the **Refresh** button to refresh the **Data preview** pane. The stream is running perpetually, so new data may have been added to the table.
7. Beneath the eventstream design canvas, view the **Data insights** tab to see details of the data events that have been captured.

## Query captured data

The eventstream you have created takes data from the sample source of bicycle data and loads it into the database in your eventhouse. You can analyze the captured data by querying the table in the database.

1. In the menu bar on the left, select your KQL database.
2. On the **database** tab, in the toolbar for your KQL database, use the **Refresh** button to refresh the view until you see the **bikes** table under the database. Then select the **bikes** table.
	[![KQL 데이터베이스의 테이블.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/kql-table.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/kql-table.png)
3. In the **…** menu for the **bikes** table, select **Query table** > **Records ingested in the last 24 hours**.
4. In the query pane, note that the following query has been generated and run, with the results shown beneath:
	code
	```
	// See the most recent data - records ingested in the last 24 hours.
	 bikes
	 | where ingestion_time() between (now(-1d) .. now())
	```
5. Select the query code and run it to see 24 hours of data from the table.
	[![KQL 쿼리의 스크린샷.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/kql-query.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/kql-query.png)

## Transform event data

The data you’ve captured is unaltered from the source. In many scenarios, you may want to transform the data in the event stream before loading it into a destination.

1. In the menu bar on the left, select the **Bicycle-data** eventstream.
2. On the toolbar, select **Edit** to edit the eventstream.
3. In the **Transform events** menu, select **Group by** to add a new **Group by** node to the eventstream.
4. Drag a connection from the output of the **Bicycle-data** node to the input of the new **Group by** node Then use the *pencil* icon in the **Group by** node to edit it.
	[![변환 이벤트에 그룹화를 추가합니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/eventstream-add-aggregates.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/eventstream-add-aggregates.png)
5. Configure out the properties of the **Group by** settings section:
	- **Operation name:** GroupByStreet
	- **Aggregate type:***Select* Sum
	- **Field:***select* No\_Bikes. *Then select **Add** to create the function* SUM of No\_Bikes
	- **Group aggregations by (optional):** Street
	- **Time window**: Tumbling
	- **Duration**: 5 seconds
	- **Offset**: 0 seconds
	> **Note**: This configuration will cause the eventstream to calculate the total number of bicycles in each street every 5 seconds.
6. Save the configuration and return to the eventstream canvas, where an error is indicated (because you need to store the output from the transformation somewhere!).
7. Use the **+** icon to the right of the **GroupByStreet** node to add a new **Eventhouse** node.
8. Configure the new eventhouse node with the following options:
	- **Data ingestion mode:**: Event processing before ingestion
	- **Destination name:**`bikes-by-street-table`
	- **Workspace:***Select the workspace you created at the beginning of this exercise*
	- **Eventhouse**: *Select your eventhouse*
	- **KQL database:***Select your KQL database*
	- **Destination table:** Create a new table named `bikes-by-street`
	- **Input data format:** JSON
	[![그룹화된 데이터에 대한 표의 스크린샷입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/group-by-table.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/group-by-table.png)
9. In the **Eventhouse** pane, select **Save**.
10. On the toolbar, select **Publish**.
11. Wait a minute or so for the changes to become active.
12. In the design canvas, select the **bikes-by-street-table** node, and view the **data preview** pane beneath the canvas.
	[![그룹화된 데이터에 대한 표의 스크린샷입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/stream-table-with-windows.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/stream-table-with-windows.png)
	Note that the trasformed data includes the grouping field you specified (**Street**), the aggregation you specified (**SUM\_no\_Bikes**), and a timestamp field indicating the end of the 5 second tumbling window in which the event occurred (**Window\_End\_Time**).

## Query the transformed data

Now you can query the bicycle data that has been transformed and loaded into a table by your eventstream

1. In the menu bar on the left, select your KQL database.
2. 1. KQL 데이터베이스 도구 모음의 데이터베이스 탭 **에서** 새로 **고침** 버튼을 사용하여 데이터베이스 아래에 **자전거별 도로** 표가 표시될 때까지 보기를 새로 고칩니다.
3. 자전거 **별 도로 표의** **...** 메뉴에서 **데이터 쿼리** \> **100개 레코드 표시를** 선택합니다 .
4. 쿼리 창에서 다음 쿼리가 생성되어 실행되는지 확인하세요.
	암호
	```
	['bikes-by-street']
	 | take 100
	```
5. 각 5초 창 내에서 거리당 자전거 총 대수를 검색하도록 KQL 쿼리를 수정합니다.
	암호
	```
	['bikes-by-street']
	 | summarize TotalBikes = sum(tolong(SUM_No_Bikes)) by Window_End_Time, Street
	 | sort by Window_End_Time desc , Street asc
	```
6. 수정된 쿼리를 선택하여 실행합니다.
	결과는 5초 동안 각 거리에서 관찰된 자전거의 수를 보여줍니다.
	[![그룹화된 데이터를 반환하는 쿼리의 스크린샷입니다.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/kql-group-query.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/kql-group-query.png)

## 자원 정리

이 연습에서는 이벤트 스트림을 사용하여 이벤트하우스를 만들고 데이터베이스에 테이블을 구성했습니다.

KQL 데이터베이스 탐색을 마치면 이 연습을 위해 만든 작업 공간을 삭제할 수 있습니다.

1. 왼쪽 막대에서 작업 공간 아이콘을 선택하세요.
2. 도구 모음에서 **작업 공간 설정을** 선택합니다.
3. **일반** 섹션 에서 **이 작업 공간 제거를** 선택합니다.