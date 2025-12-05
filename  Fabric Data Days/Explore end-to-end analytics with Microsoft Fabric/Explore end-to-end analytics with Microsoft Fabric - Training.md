---
title: "Explore end-to-end analytics with Microsoft Fabric - Training"
source: "https://learn.microsoft.com/en-us/training/modules/introduction-end-analytics-use-microsoft-fabric/2-explore-analytics-fabric"
author:
  - "[[AngieRudduck]]"
published:
created: 2025-12-03
description: "Explore end-to-end analytics with Microsoft Fabric"
tags:
  - "clippings"
---
## Microsoft Fabric을 사용하여 종단 간 분석을 살펴보세요

100 경험치

확장 가능한 분석은 복잡하고 분산되어 있으며 비용이 많이 들 수 있습니다. Microsoft Fabric은 다양한 도구와 서비스를 하나의 플랫폼으로 통합하는 사용하기 쉬운 단일 제품을 제공하여 분석 솔루션을 간소화합니다.

Fabric은 모든 데이터가 OneLake에 단일 개방형 포맷으로 저장되는 통합 SaaS *(Software-as-a-Service* ) 플랫폼입니다. OneLake는 플랫폼 내 모든 분석 엔진에서 접근 가능하며, 인터넷에 연결된 어디에서나 확장성, 비용 효율성 및 접근성을 보장합니다.

## 원레이크

*OneLake* 는 Fabric의 중앙 집중식 데이터 스토리지 아키텍처로, 시스템 간 데이터 이동이나 복사 필요성을 없애 협업을 지원합니다. OneLake는 여러 지역과 클라우드에 분산된 데이터를 이동이나 복제 없이 단일 논리적 레이크에 통합합니다.

*OneLake는 Azure Data Lake Storage* (ADLS)를 기반으로 하며 Delta, Parquet, CSV, JSON 등 다양한 형식을 지원합니다. Fabric의 모든 컴퓨팅 엔진은 데이터를 OneLake에 자동으로 저장하여 이동이나 복제 없이 직접 액세스할 수 있도록 합니다. 테이블 형식의 데이터의 경우, Fabric의 분석 엔진은 Delta-Parquet 형식으로 데이터를 작성하며, 모든 엔진은 이 형식과 원활하게 상호 작용합니다.

*바로가기는* OneLake 외부의 파일이나 저장 위치에 대한 참조로, 기존 클라우드 데이터를 복사하지 않고도 액세스할 수 있도록 합니다. 바로가기는 데이터 일관성을 보장하고 Fabric이 소스와 동기화 상태를 유지할 수 있도록 합니다.

![서버리스 컴퓨팅의 기반으로 동일한 OneLake 데이터 스토리지와 Delta-Parquet 스토리지 형식에 액세스하는 워크로드를 포함하는 OneLake 아키텍처 다이어그램입니다.](https://learn.microsoft.com/en-us/training/wwl/introduction-end-analytics-use-microsoft-fabric/media/onelake-architecture.png)

서버리스 컴퓨팅의 기반으로 동일한 OneLake 데이터 스토리지와 Delta-Parquet 스토리지 형식에 액세스하는 워크로드를 포함하는 OneLake 아키텍처 다이어그램입니다.

## 작업 공간

Microsoft Fabric에서 작업 영역은 데이터, 보고서 및 기타 자산을 구성하고 관리하는 데 도움이 되는 논리적 컨테이너 역할을 합니다. 작업 영역은 리소스를 명확하게 분리하여 액세스를 제어하고 보안을 유지하는 것을 더욱 쉽게 해줍니다.

각 작업 공간은 고유한 권한 집합을 가지므로 권한이 있는 사용자만 콘텐츠를 보거나 수정할 수 있습니다. 이러한 구조는 비즈니스 및 IT 사용자 모두에게 엄격한 액세스 제어를 유지하는 동시에 팀 협업을 지원합니다.

작업 공간을 사용하면 컴퓨팅 리소스를 관리하고 Git과 연동하여 버전 관리를 할 수 있습니다. 컴퓨팅 설정을 구성하여 성능과 비용을 최적화할 수 있으며, Git 연동을 통해 변경 사항을 추적하고, 코드에서 협업하고, 작업 내역을 관리할 수 있습니다.

## 행정 및 거버넌스

Fabric의 OneLake는 중앙에서 관리되며 협업을 위해 개방되어 있습니다. 데이터는 한곳에서 안전하게 관리되므로 사용자는 필요한 데이터를 쉽게 찾고 액세스할 수 있습니다. Fabric 관리는 *관리자 포털* 에서 중앙 집중식으로 관리됩니다.

관리 포털에서 그룹 및 권한을 관리하고, 데이터 소스 및 게이트웨이를 구성하고, 사용량 및 성능을 모니터링할 수 있습니다. 또한 관리 포털에서 Fabric 관리 API 및 SDK에 액세스하여 일반적인 작업을 자동화하고 Fabric을 다른 시스템과 통합할 수 있습니다.

OneLake *카탈로그는* 데이터 거버넌스를 분석, 모니터링 및 유지하는 데 도움을 줍니다. 민감도 레이블, 항목 메타데이터, 데이터 새로 고침 상태에 대한 지침을 제공하여 거버넌스 상태 및 개선 조치에 대한 통찰력을 제공합니다.