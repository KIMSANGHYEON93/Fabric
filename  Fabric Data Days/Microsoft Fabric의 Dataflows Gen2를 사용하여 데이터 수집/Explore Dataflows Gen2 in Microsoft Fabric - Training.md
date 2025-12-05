---
title: "Explore Dataflows Gen2 in Microsoft Fabric - Training"
source: "https://learn.microsoft.com/en-us/training/modules/use-dataflow-gen-2-fabric/3-explore-dataflows-gen-2"
author:
  - "[[AngieRudduck]]"
published:
created: 2025-12-03
description: "Explore Dataflows Gen2 in Microsoft Fabric"
tags:
  - "clippings"
---
## Microsoft Fabric에서 Dataflows Gen2 탐색

100 경험치

Microsoft Fabric에서는 Data Factory 워크로드나 Power BI 작업 영역, 또는 레이크하우스에서 직접 Dataflow Gen2를 생성할 수 있습니다. 이 시나리오는 데이터 수집에 중점을 두고 있으므로 **Data Factory** 워크로드 환경을 살펴보겠습니다. Dataflows Gen2는 Power Query Online을 사용하여 변환을 시각화합니다. 인터페이스 개요는 다음과 같습니다.

![Power Query 온라인 인터페이스의 스크린샷입니다.](https://learn.microsoft.com/en-us/training/wwl/use-dataflow-gen-2-fabric/media/power-query-online-overview.png)

### 1\. 파워 쿼리 리본

Dataflows Gen2는 다양한 데이터 소스 커넥터를 지원합니다. 일반적인 소스로는 클라우드 및 온프레미스 관계형 데이터베이스, Excel 또는 플랫 파일, SharePoint, SalesForce, Spark, Fabric 레이크하우스 등이 있습니다. 또한 다음과 같은 다양한 데이터 변환이 가능합니다.

- 행 필터링 및 정렬
- 피벗과 언피벗
- 병합 및 추가 쿼리
- 분할 및 조건부 분할
- 값 바꾸기 및 중복 제거
- 열 추가, 이름 바꾸기, 재정렬 또는 삭제
- 순위 및 백분율 계산기
- 상위 N과 하위 N을 선택하세요

이 리본에서 데이터 소스 연결을 만들고 관리하고, 매개변수를 관리하고, 기본 데이터 대상을 구성할 수도 있습니다.

### 2\. 쿼리 창

쿼리 창에는 다양한 데이터 소스(이제 *쿼리* 라고 함)가 표시됩니다. 이러한 쿼리는 데이터 저장소에 로드될 때 테이블이라고 합니다. 스타 스키마를 만들거나 데이터를 여러 개의 작은 테이블로 분할하는 등 동일한 데이터의 여러 사본이 필요한 경우 쿼리를 복제하거나 참조할 수 있습니다. 또한, 한 번만 가져오면 되는 경우 쿼리 로드를 비활성화할 수도 있습니다.

### 3\. 다이어그램 보기

다이어그램 뷰를 사용하면 데이터 소스가 어떻게 연결되어 있는지, 그리고 적용된 다양한 변환을 시각적으로 확인할 수 있습니다. 예를 들어, 데이터 흐름이 데이터 소스에 연결되고, 쿼리를 복제하고, 소스 쿼리에서 열을 제거한 다음, 중복 쿼리의 피벗을 해제합니다. 각 쿼리는 적용된 모든 변환이 포함된 도형으로 표시되고, 중복 쿼리는 선으로 연결됩니다. 이 뷰를 켜거나 끌 수 있습니다.

### 4\. 데이터 미리보기 창

데이터 미리 보기 창에는 데이터의 일부만 표시되므로 어떤 변환을 수행해야 하는지, 그리고 변환이 데이터에 어떤 영향을 미치는지 확인할 수 있습니다. 또한 열을 드래그 앤 드롭하여 순서를 변경하거나, 열을 마우스 오른쪽 버튼으로 클릭하여 필터링하거나 변경하는 등 미리 보기 창을 조작할 수 있습니다. 데이터 미리 보기에는 선택한 쿼리에 대한 모든 변환이 표시됩니다.

### 5\. 쿼리 설정 창

쿼리 설정 창에는 **적용된 단계가** 포함되어 있습니다. 각 변환은 단계로 표시되며, 그중 일부는 데이터 소스를 연결할 때 자동으로 적용됩니다. 변환의 복잡성에 따라 각 쿼리에 여러 단계가 적용될 수 있습니다. 대부분의 단계에는 단계를 수정할 수 있는 기어 아이콘이 있으며, 그렇지 않으면 변환을 삭제하고 다시 실행해야 합니다.

각 단계에는 마우스 오른쪽 버튼을 클릭하면 표시되는 상황에 맞는 메뉴를 통해 단계의 이름을 바꾸거나, 순서를 바꾸거나, 삭제할 수 있습니다. 쿼리 폴딩을 지원하는 데이터 소스에 연결하면 데이터 소스 쿼리를 볼 수도 있습니다.

**이 시각적 인터페이스가 유용하기는 하지만 고급 편집기를** 통해 M 코드를 볼 수도 있습니다 .

![샘플 코드가 포함된 고급 편집기의 스크린샷](https://learn.microsoft.com/en-us/training/wwl/use-dataflow-gen-2-fabric/media/power-query-advanced-editor.png)

쿼리 설정 창에서 다음 Fabric 환경의 위치 중 하나에 데이터를 저장하는 **데이터 대상 옵션을 볼 수 있습니다.**

- 레이크하우스
- 창고
- SQL 데이터베이스

Azure SQL 데이터베이스, Azure Data Explorer 또는 Azure Synapse Analytics에 데이터 흐름을 로드할 수도 있습니다.

Dataflows Gen2는 Fabric 데이터 저장소에 데이터를 수집, 변환 및 로드하는 데 필요한 코드가 거의 없거나 아예 없는 솔루션을 제공합니다. Power BI 개발자는 이러한 기능에 익숙하며, 보고서 성능을 향상시키기 위해 업스트림에서 변환 작업을 빠르게 수행할 수 있습니다.