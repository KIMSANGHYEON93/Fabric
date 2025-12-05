---
title: "Components of Eventstream - Training"
source: "https://learn.microsoft.com/en-us/training/modules/explore-event-streams-microsoft-fabric/2-eventstream-components"
author:
  - "[[theresa-i]]"
published:
created: 2025-12-03
description: "Explore the main components of Eventstream"
tags:
  - "clippings"
---
## 이벤트스트림의 구성 요소

100 경험치

Fabric의 이벤트스트림 기능은 스트리밍 데이터 소스에서 이벤트를 수집하고, 선택적 변환을 통해 처리하고, 다양한 목적지로 전달하는 파이프라인을 생성하는 방식으로 작동합니다. 이벤트스트림은 이벤트가 발생한 위치에서 처리, 분석 또는 조치가 필요한 위치로 이벤트를 전달하는 전달 메커니즘입니다.

시각적 편집기인 이벤트스트림 캔버스를 사용하면 소스, 변환, 대상 등 다양한 노드를 드래그 앤 드롭하여 파이프라인을 설계할 수 있습니다. 파이프라인을 통과하는 이벤트 데이터를 실시간으로 확인할 수도 있습니다. 이벤트스트림을 사용하기 위해 코드를 작성하거나 인프라를 관리할 필요가 없습니다.

![이벤트 스트림의 스크린샷.](https://learn.microsoft.com/en-us/training/wwl/explore-event-streams-microsoft-fabric/media/real-time-intelligence-eventstream-workflow.png)

이벤트 스트림의 스크린샷.

**이 이미지는 이벤트스트림 캔버스를 보여줍니다. Bicycles** 라는 실시간 데이터 소스가 있는데 , 여기에는 자전거 위치, 자전거 대여소 도로명 등을 포함한 도시 자전거 대여 데이터가 포함됩니다. **Bicycle-data는** **Bicycles** 데이터 소스 에서 데이터를 수집하는 이벤트스트림입니다. 이 데이터는 자전거 대여소 도로명별 자전거 수를 합산하는 **GroupByStreet** 라는 연산을 통해 변환됩니다. 이 데이터는 이벤트하우스의 **Bikes-by-street-table** 이라는 테이블에 저장됩니다 .

이벤트스트림의 주요 구성 요소는 다음과 같습니다.

- **소스**: 소스는 이벤트 데이터의 출처입니다. Microsoft 소스에서 데이터를 스트리밍할 수 있고, Microsoft가 아닌 플랫폼에서 데이터를 수집할 수도 있습니다.
- **변환**: 이벤트 스트림에서 데이터가 흐르는 대로 변환하여 저장하기 전에 필터링, 요약 및 재구성할 수 있습니다. 사용 가능한 변환의 예로는 SQL 코드, 필터, 필드 관리, 집계, 그룹화 기준, 확장 및 조인이 있습니다.
- **목적지**: 목적지는 변환된 이벤트 데이터가 저장, 추가 처리, 알림 또는 다른 시스템과의 통합을 위해 이동하는 곳입니다. 스트림의 데이터를 이벤트하우스 또는 레이크하우스의 테이블, 사용자 지정 엔드포인트, 추가 처리를 위한 파생 스트림 또는 작업을 트리거하는 Fabric Activator 등 다양한 목적지로 라우팅할 수 있습니다.