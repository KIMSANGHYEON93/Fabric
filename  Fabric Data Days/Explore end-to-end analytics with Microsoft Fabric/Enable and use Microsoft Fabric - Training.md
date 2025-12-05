---
title: "Enable and use Microsoft Fabric - Training"
source: "https://learn.microsoft.com/en-us/training/modules/introduction-end-analytics-use-microsoft-fabric/4-use-fabric"
author:
  - "[[AngieRudduck]]"
published:
created: 2025-12-03
description: "Enable and use Microsoft Fabric"
tags:
  - "clippings"
---
## Microsoft Fabric 활성화 및 사용

100 경험치

Microsoft Fabric의 엔드투엔드 기능을 활용하려면 먼저 조직에서 해당 기능을 활성화해야 합니다. 조직에서 Fabric을 활성화하려면 다음 역할 중 하나를 포함하여 IT 부서와 협력해야 할 수도 있습니다.

- *Fabric 관리자(이전 Power BI 관리자)*: Fabric 설정 및 구성을 관리합니다.
- *Power Platform 관리자*: Fabric을 포함한 Power Platform 서비스를 감독합니다.
- *Microsoft 365 관리자*: Fabric을 포함한 조직 전체의 Microsoft 서비스를 관리합니다.

## Microsoft Fabric 활성화

**관리자는 Power BI 서비스의 관리 포털 > 테넌트 설정** 에서 Fabric을 활성화할 수 있습니다 . Fabric은 전체 조직 또는 특정 Microsoft 365 또는 Microsoft Entra 보안 그룹에 대해 활성화할 수 있습니다. 관리자는 또한 용량 수준에서 다른 사용자에게 이 기능을 위임할 수 있습니다.

![Fabric 항목을 활성화할 수 있는 Fabric 관리 포털의 스크린샷입니다.](https://learn.microsoft.com/en-us/training/wwl/introduction-end-analytics-use-microsoft-fabric/media/enable-fabric.png)

Fabric 항목을 활성화할 수 있는 Fabric 관리 포털의 스크린샷입니다.

## 작업 공간 만들기

워크스페이스는 레이크하우스, 웨어하우스, 보고서 등의 항목을 생성하고 관리할 수 있는 협업 환경입니다. 모든 데이터는 OneLake에 저장되며 워크스페이스를 통해 액세스할 수 있습니다. 워크스페이스는 또한 데이터 계보 보기를 지원하여 데이터 흐름과 종속성을 시각적으로 보여줌으로써 투명성과 의사 결정을 향상시킵니다.

*작업 공간 설정* 에서 다음을 구성할 수 있습니다.

- Fabric 기능을 사용하기 위한 라이센스 유형입니다.
- 작업 공간에 대한 OneDrive 액세스.
- Azure Data Lake Gen2 저장소 연결.
- 버전 제어를 위한 Git 통합.
- 성능 최적화를 위한 Spark 워크로드 설정.

*작업 공간 액세스는 관리자*, *기여자*, *멤버*, *뷰어의* 네 가지 역할을 통해 관리할 수 있습니다 . 이러한 역할은 작업 공간의 모든 항목에 적용되며 협업을 위해 예약해야 합니다. 더욱 세부적인 액세스 제어를 위해서는 비즈니스 요구 사항에 따라 항목 수준 권한을 사용하세요.

Microsoft Fabric의 OneLake 카탈로그는 사용자가 조직 내 다양한 데이터 원본을 쉽게 찾고 액세스할 수 있도록 지원합니다. 사용자는 데이터 원본을 탐색하고 연결하여 필요에 맞는 데이터를 확보할 수 있습니다. 사용자는 공유된 항목만 볼 수 있습니다. OneLake 카탈로그 사용 시 고려해야 할 사항은 다음과 같습니다.

- 작업 공간이나 도메인(구현된 경우)별로 결과를 좁힙니다.
- 기본 카테고리를 탐색하여 관련 데이터를 빠르게 찾으세요.
- 키워드 또는 품목 유형별로 필터링합니다.

![OneLake 카탈로그의 스크린샷.](https://learn.microsoft.com/en-us/training/wwl/introduction-end-analytics-use-microsoft-fabric/media/onelake-catalog.png)

OneLake 카탈로그의 스크린샷.

## Fabric 워크로드로 항목 만들기

Fabric 지원 작업 공간을 생성한 후 Fabric에서 항목을 생성할 수 있습니다. Fabric의 각 워크로드는 데이터 저장, 처리 및 분석을 위한 다양한 항목 유형을 제공합니다. Fabric 워크로드에는 다음이 포함됩니다.

- **데이터 엔지니어링**: 레이크하우스를 만들고 워크플로를 운영화하여 데이터 자산을 구축, 변환, 공유합니다.
- **데이터 팩토리**: 데이터를 수집, 변환, 조정합니다.
- **데이터 과학**: 머신 러닝을 사용하여 추세를 감지하고, 이상치를 식별하고, 값을 예측합니다.
- **데이터웨어하우스**: 분석을 위해 기존 웨어하우스에서 여러 소스를 결합합니다.
- **데이터베이스**: 데이터를 삽입, 쿼리, 추출하는 도구를 사용하여 데이터베이스를 만들고 관리합니다.
- **산업 솔루션**: 기존의 틀을 깨는 산업 데이터 솔루션을 활용하세요.
- **실시간 인텔리전스**: 스트리밍 데이터를 처리, 모니터링, 분석합니다.
- **Power BI**: 데이터 기반의 의사 결정을 내리기 위한 보고서와 대시보드를 만듭니다.

Fabric은 Power BI, Azure Synapse Analytics, Azure Data Factory와 같은 기존 Microsoft 도구의 기능을 통합 플랫폼으로 제공합니다. 또한 Fabric은 데이터 메시 아키텍처를 지원하여 중앙 집중식 거버넌스를 유지하면서도 분산된 데이터 소유권을 제공합니다. 이러한 설계 덕분에 Azure 리소스에 직접 액세스할 필요가 없어 데이터 워크플로가 간소화됩니다.

## Fabric의 Copilot으로 생산성 향상

Microsoft Copilot in Fabric은 모든 Fabric 워크로드에서 생산성을 향상시키고 인사이트를 가속화하는 생성형 AI 비서입니다. Copilot은 대규모 언어 모델(LLM)을 사용하여 데이터 전문가, 셀프서비스 사용자 및 비즈니스 사용자에게 지능적인 지원을 제공합니다.

### 작업 부하 전반에 걸친 Copilot 기능

Copilot은 각 Fabric 워크로드에 맞는 맞춤형 지원을 제공합니다.

- **데이터 엔지니어링 및 데이터 과학**: 지능형 코드 완성, 자동화된 일상 업무, 업계 표준 코드 템플릿, 그리고 특정 업무에 맞춰 조정되는 상황에 맞는 코드 제안 기능을 제공합니다. Copilot은 데이터 준비, 파이프라인 구축 및 인사이트 생성을 지원합니다.
- **데이터 팩토리**: 데이터 변환을 위한 지능형 코드 생성과 복잡한 작업에 대한 코드 설명을 제공하여 일반 시민과 전문 데이터 관리자를 모두 지원하는 AI 강화 툴셋입니다.
- **데이터 웨어하우스 및 SQL 데이터베이스**: 자연어-SQL 변환, 코드 완성, 빠른 작업 및 지능형 인사이트 제공. 사용자는 원하는 내용을 일반 언어로 설명할 수 있으며, Copilot은 적절한 SQL 쿼리를 생성합니다.
- **Power BI**: 자동 보고서 생성, 보고서 페이지 요약 생성, 더 나은 Q&A 기능을 위한 동의어 생성, 자연어 기반 데이터 쿼리 기능을 제공합니다. 비즈니스 사용자는 Copilot을 사용하여 더 많은 인사이트를 도출하고 보고서 데이터와 소통할 수도 있습니다.
- **실시간 인텔리전스**: 자연어 질문을 Kusto Query Language(KQL) 쿼리로 변환하는 고급 AI 도구로, 숙련된 사용자와 시민 데이터 과학자 모두를 위해 데이터 분석을 간소화합니다.

### Copilot 활성화

관리자는 Power BI 서비스의 **관리 포털 > 테넌트 설정** 에서 Copilot을 활성화해야 합니다.

Copilot은 코드 작성, 쿼리 생성, 보고서 작성 등 일반적인 작업에 AI 지원을 제공하여 사용자의 업무 효율성을 높입니다. 이러한 지원은 기술 사용자와 비즈니스 사용자 모두에게 제공되며, 조직의 보안 정책을 준수합니다.