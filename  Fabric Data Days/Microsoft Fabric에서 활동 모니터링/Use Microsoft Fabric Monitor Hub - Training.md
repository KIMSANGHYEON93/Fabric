---
title: "Use Microsoft Fabric Monitor Hub - Training"
source: "https://learn.microsoft.com/en-us/training/modules/monitor-fabric-items/3-use-monitor-hub"
author:
  - "[[wwlpublish]]"
published:
created: 2025-12-03
description: "Use Microsoft Fabric Monitor Hub"
tags:
  - "clippings"
---
## Microsoft Fabric Monitor Hub 사용

100 경험치

시각화 도구는 모니터링을 더욱 쉽게 만들어 줍니다. 추세나 이상 징후를 파악하는 데 도움이 됩니다. Monitor Hub는 Microsoft Fabric의 모니터링 시각화 도구입니다. Monitor Hub는 선택된 Fabric 항목 및 프로세스에서 데이터를 수집하고 집계합니다. Fabric 활동 데이터를 공통 인터페이스에 저장하므로 Fabric에서 여러 데이터 통합, 변환, 이동 및 분석 활동의 상태를 개별적으로 모니터링할 필요 없이 한 곳에서 확인할 수 있습니다.

## 모니터 허브에 표시되는 활동

Microsoft Fabric Monitor 허브에서 모니터링 메타데이터를 볼 수 있는 일부 활동은 다음과 같습니다.

- 데이터 파이프라인 실행 내역
- 데이터 흐름 실행
- 데이터마트 및 의미 모델 새로 고침
- Spark 작업 및 Notebook 실행 기록 및 작업 세부 정보

## 모니터 허브 보기

모니터 허브는 Fabric 탐색 창에서 **모니터를 선택하여 열 수 있습니다.**

![Microsoft Fabric Monitor 허브 인터페이스의 스크린샷입니다.](https://learn.microsoft.com/en-us/training/wwl/monitor-fabric-items/media/monitor-hub.png)

Microsoft Fabric Monitor 허브 인터페이스의 스크린샷입니다.

## Fabric 활동 세부 정보 보기

모니터 허브의 각 활동을 선택하고 선택한 활동에 대해 여러 작업을 수행할 수 있습니다. 작업은 활동별로 다르며, 활동 열기, 재시도, 활동 세부 정보 또는 이전 실행 보기 등의 옵션이 있습니다. 이 정보를 보려면 활동 위에 마우스를 올리면 나타나는 줄임표를 선택하세요.

![Microsoft Fabric Monitor 허브 세부정보 인터페이스의 스크린샷입니다.](https://learn.microsoft.com/en-us/training/wwl/monitor-fabric-items/media/view-monitor-hub-details.png)

Microsoft Fabric Monitor 허브 세부정보 인터페이스의 스크린샷입니다.

**'세부 정보 보기'를** 선택하면 선택한 활동에 맞게 맞춤 설정된 화면이 나타나며, 활동 중 발생한 상황을 명확하게 보여줍니다. 다음과 같은 메타데이터를 볼 수 있습니다.

- 활동 상태
- 시작 및 종료 시간
- 지속
- 활동 통계

## Fabric 활동 중에 무슨 일이 일어났는지 조사하세요

활동 중 발생한 상황을 조사하기 위해 Monitor 허브의 일부 활동에는 실행 세부 정보를 자세히 살펴볼 수 있는 하이퍼링크가 포함되어 있습니다. 오류 및 실행 성공/실패에 대한 정보가 제공됩니다. 여러 항목에 걸쳐 Spark 활동을 볼 수 있습니다. Notebooks, Spark Job Definitions 및 Pipelines에서 트리거된 Spark 애플리케이션을 볼 수 있습니다. 자세한 내용은 [Apache Spark 모니터링 개요를 참조하세요.](https://learn.microsoft.com/en-us/fabric/data-engineering/spark-monitoring-overview)