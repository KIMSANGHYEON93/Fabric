---
title: "Query and report on data in your Fabric lakehouse - Training"
source: "https://learn.microsoft.com/en-us/training/modules/describe-medallion-architecture/4-query-report-data"
author:
  - "[[theresa-i]]"
published:
created: 2025-12-03
description: "Query and report on data in your Fabric lakehouse"
tags:
  - "clippings"
---
## Fabric 레이크하우스의 데이터 쿼리 및 보고

100 경험치

메달리온 아키텍처가 구축되었으므로 이제 데이터 팀과 비즈니스 부서는 이를 활용하여 데이터를 쿼리하고 보고할 수 있습니다. Fabric에는 SQL 분석 엔드포인트와 Power BI 시맨틱 모델의 Direct Lake 모드를 포함하여 레이크하우스의 데이터를 쿼리하고 보고할 수 있는 다양한 도구와 기술이 포함되어 있습니다.

## 레이크하우스에서 데이터 쿼리

팀은 SQL을 사용하여 골드 계층의 데이터를 탐색하고 쿼리할 수 있습니다. 메달리온 아키텍처의 모든 계층에서 T-SQL 언어를 사용하여 델타 테이블의 데이터를 분석하고, 함수를 저장하고, 뷰를 생성하고, SQL 보안을 적용할 수 있습니다. 또한 SQL 분석 엔드포인트를 사용하여 쿼리 도구 및 애플리케이션에서 레이크하우스에 연결할 수 있습니다.

Fabric의 SQL 분석 엔드포인트를 사용하면 시각적 쿼리 환경을 사용하여 쿼리를 작성하고, 의미 모델을 관리하고, 데이터를 쿼리할 수 있습니다.

![Fabric 사용자 인터페이스의 SQL 분석 엔드포인트 스크린샷입니다.](https://learn.microsoft.com/en-us/training/wwl/describe-medallion-architecture/media/sql-endpoint-silver.png)

SQL 분석 엔드포인트를 사용하여 데이터를 탐색하는 것 외에도 Power BI 시맨틱 모델을 사용하여 데이터를 탐색할 수 있습니다. 시맨틱 모델은 비즈니스 친화적인 용어를 사용하여 데이터를 보는 방식입니다. 일반적으로 특정 비즈니스 영역과 관련된 데이터 도메인을 나타내는 팩트와 해당 데이터 도메인의 데이터를 분석할 수 있는 차원으로 구성된 스타 스키마로 표현됩니다. 레이크하우스를 만들면 기본 시맨틱 모델이 자동으로 생성됩니다. 기본이 아닌 사용자 지정 Power BI 시맨틱 모델을 만들 수도 있습니다.

![테이블 간의 관계가 포함된 Power BI 의미 모델의 스크린샷입니다.](https://learn.microsoft.com/en-us/training/wwl/describe-medallion-architecture/media/dataset-relationships.png)

**데이터 분석가는 Direct Lake** 모드를 사용하여 의미 모델에 연결할 수 있습니다 . 이 모드에서는 의미 모델이 레이크하우스의 Delta 테이블에서 직접 데이터에 액세스합니다.

## 다양한 요구 사항에 맞게 메달리온 레이어를 맞춤 설정하세요

메달리온 레이어를 다양한 요구 사항에 맞게 조정하면 특정 사용 사례에 맞춰 데이터 처리 및 액세스를 최적화할 수 있습니다. 이러한 레이어를 맞춤 설정함으로써 각 레이어의 구조와 구성이 다양한 사용자 그룹의 요구 사항에 맞게 조정되도록 하여 성능, 사용 편의성, 그리고 다양한 이해관계자를 위한 데이터 관련성을 향상시킬 수 있습니다.

다양한 대상이나 도메인에 맞춰 여러 개의 골드 레이어를 생성하면 메달리온 아키텍처의 유연성이 더욱 강화됩니다. 재무, 영업, 데이터 과학 등 각 분야는 특정 분석 요구 사항을 충족하는 최적화된 골드 레이어를 가질 수 있습니다.

일부 애플리케이션, 타사 도구 또는 시스템에는 특정 데이터 형식이 필요합니다. 메달리온 아키텍처를 활용하여 정제되고 적절한 형식의 데이터를 생성할 수 있습니다.