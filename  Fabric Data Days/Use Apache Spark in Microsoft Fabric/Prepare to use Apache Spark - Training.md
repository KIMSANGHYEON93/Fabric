---
title: "Prepare to use Apache Spark - Training"
source: "https://learn.microsoft.com/en-us/training/modules/use-apache-spark-work-files-lakehouse/2-spark"
author:
  - "[[theresa-i]]"
published:
created: 2025-12-03
description: "Prepare to use Apache Spark"
tags:
  - "clippings"
---
## Apache Spark 사용 준비

100 경험치

*Apache Spark는 Microsoft Fabric에서 Spark 풀이* 라고 하는 클러스터 내의 여러 처리 노드에서 작업을 조정하여 대규모 데이터 분석을 지원하는 분산 데이터 처리 프레임워크입니다 . 간단히 말해, Spark는 "분할 정복" 방식을 사용하여 작업을 여러 컴퓨터에 분산함으로써 대량의 데이터를 빠르게 처리합니다. 작업 분배 및 결과 수집 프로세스는 Spark가 자동으로 처리합니다.

Spark는 Java, Scala(Java 기반 스크립팅 언어), Spark R, Spark SQL, PySpark(Spark 전용 Python 버전) 등 다양한 언어로 작성된 코드를 실행할 수 있습니다. 실제로 대부분의 데이터 엔지니어링 및 분석 작업은 PySpark와 Spark SQL을 함께 사용하여 수행됩니다.

## 스파크 풀

Spark 풀은 데이터 처리 작업을 분산하는 컴퓨팅 *노드* 로 구성됩니다. 일반적인 아키텍처는 다음 다이어그램에 나와 있습니다.

![Spark 풀의 다이어그램.](https://learn.microsoft.com/en-us/training/wwl/use-apache-spark-work-files-lakehouse/media/spark-pool.png)

다이어그램에서 볼 수 있듯이 Spark 풀에는 두 종류의 노드가 포함됩니다.

1. Spark 풀의 헤드 노드는 드라이버 프로그램을 통해 분산 프로세스 를 *조정* *합니다*.
2. 풀에는 여러 개의 *작업자* 노드가 포함되어 있으며, *실행자* 프로세스가 실제 데이터 처리 작업을 수행합니다.

Spark 풀은 이 분산형 컴퓨팅 아키텍처를 사용하여 호환 가능한 데이터 저장소(예: OneLake에 기반한 데이터 레이크하우스)의 데이터에 액세스하고 이를 처리합니다.

### Microsoft Fabric의 Spark 풀

Microsoft Fabric은 각 작업 공간에 *스타터 풀을* 제공하여 최소한의 설정과 구성으로 Spark 작업을 빠르게 시작하고 실행할 수 있도록 합니다. 특정 워크로드 요구 사항이나 비용 제약 조건에 따라 스타터 풀에 포함된 노드를 최적화하도록 스타터 풀을 구성할 수 있습니다.

또한, 특정 데이터 처리 요구 사항을 지원하는 구체적인 노드 구성을 사용하여 사용자 정의 Spark 풀을 만들 수 있습니다.

작업 공간 설정의 **관리 포털 섹션에서** **용량 설정**, **데이터 엔지니어링/과학 설정** 아래에서 스타터 풀의 설정을 관리하고 새 Spark 풀을 만들 수 있습니다.

![Microsoft Fabric의 Spark 설정 페이지 스크린샷.](https://learn.microsoft.com/en-us/training/wwl/use-apache-spark-work-files-lakehouse/media/spark-settings.png)

Spark 풀에 대한 구체적인 구성 설정은 다음과 같습니다.

- **노드 패밀리**: Spark 클러스터 노드에 사용되는 가상 머신 유형입니다. 대부분의 경우 *메모리 최적화* 노드는 최적의 성능을 제공합니다.
- **자동 크기 조정**: 필요에 따라 노드를 자동으로 프로비저닝할지 여부와, 프로비저닝할 경우 풀에 할당할 초기 및 최대 노드 수입니다.
- **동적 할당**: 데이터 볼륨에 따라 작업자 노드에 *실행자* 프로세스를 동적으로 할당할지 여부입니다.

작업 공간에 하나 이상의 사용자 지정 Spark 풀을 만드는 경우, 해당 Spark 작업에 대해 특정 풀이 지정되지 않은 경우 해당 풀 중 하나(또는 스타터 풀)를 기본 풀로 설정할 수 있습니다.

## 런타임 및 환경

Spark 오픈 소스 생태계에는 여러 버전의 Spark *런타임* 이 포함되어 있으며, 이는 Apache Spark, Delta Lake, Python 및 기타 핵심 소프트웨어 구성 요소의 버전을 결정합니다. 또한 런타임 내에서 일반적인(그리고 때로는 매우 특수한) 작업을 위한 다양한 코드 라이브러리를 설치하고 사용할 수 있습니다. Spark 처리의 상당 부분이 PySpark를 사용하여 수행되므로, 다양한 Python 라이브러리를 통해 어떤 작업을 수행하든 필요한 라이브러리를 찾을 수 있습니다.

*경우에 따라 조직은 다양한 데이터 처리 작업을 지원하기 위해 여러 환경을* 정의해야 할 수 있습니다 . 각 환경은 특정 런타임 버전과 특정 작업을 수행하기 위해 설치해야 하는 라이브러리를 정의합니다. 데이터 엔지니어와 과학자는 특정 작업에 Spark 풀을 사용할 환경을 선택할 수 있습니다.

### Microsoft Fabric의 Spark 런타임

Microsoft Fabric은 여러 Spark 런타임을 지원하며, 새로운 런타임이 출시됨에 따라 지원을 계속 추가할 예정입니다. 작업 영역 설정 인터페이스를 사용하여 Spark 풀이 시작될 때 기본 환경에서 사용되는 Spark 런타임을 지정할 수 있습니다.

### Microsoft Fabric의 환경

Fabric 작업 공간에서 사용자 정의 환경을 만들면 다양한 데이터 처리 작업에 대해 특정 Spark 런타임, 라이브러리 및 구성 설정을 사용할 수 있습니다.

![Microsoft Fabric의 환경 페이지 스크린샷.](https://learn.microsoft.com/en-us/training/wwl/use-apache-spark-work-files-lakehouse/media/spark-environment.png)

환경을 만들 때 다음을 수행할 수 있습니다.

- 사용해야 하는 Spark 런타임을 지정합니다.
- 모든 환경에 설치된 기본 라이브러리를 확인하세요.
- Python 패키지 인덱스(PyPI)에서 특정 공개 라이브러리를 설치합니다.
- 패키지 파일을 업로드하여 사용자 정의 라이브러리를 설치합니다.
- 환경에서 사용해야 하는 Spark 풀을 지정합니다.
- 기본 동작을 재정의하려면 Spark 구성 속성을 지정하세요.
- 환경에서 사용할 수 있어야 하는 리소스 파일을 업로드합니다.

최소한 하나의 사용자 정의 환경을 만든 후 작업 공간 설정에서 해당 환경을 기본 환경으로 지정할 수 있습니다.

## 추가 Spark 구성 옵션

Spark 풀과 환경을 관리하는 것은 Fabric 작업 공간에서 Spark 처리를 관리하는 주요 방법입니다. 하지만 추가적인 최적화를 위해 사용할 수 있는 몇 가지 추가 옵션도 있습니다.

### 네이티브 실행 엔진

Microsoft Fabric의 네이티브 *실행 엔진* 은 레이크하우스 인프라에서 Spark 작업을 직접 실행하는 벡터화된 처리 엔진입니다. 네이티브 실행 엔진을 사용하면 Parquet 또는 Delta 파일 형식의 대용량 데이터 세트를 처리할 때 쿼리 성능을 크게 향상시킬 수 있습니다.

네이티브 실행 엔진을 사용하려면 환경 수준 또는 개별 노트북 내에서 활성화할 수 있습니다. 환경 수준에서 네이티브 실행 엔진을 활성화하려면 환경 구성에서 다음 Spark 속성을 설정하세요.

- **spark.native.enabled**: 참
- **spark.shuffle.manager**: org.apache.spark.shuffle.sort.ColumnarShuffleManager

특정 스크립트나 노트북에 대한 네이티브 실행 엔진을 활성화하려면 다음과 같이 코드 시작 부분에 다음 구성 속성을 설정하면 됩니다.

```json
%%configure 
{ 
   "conf": {
       "spark.native.enabled": "true", 
       "spark.shuffle.manager": "org.apache.spark.shuffle.sort.ColumnarShuffleManager" 
   } 
}
```

### 높은 동시성 모드

Microsoft Fabric에서 Spark 코드를 실행하면 Spark 세션이 시작됩니다. *높은 동시성 모드를* 사용하여 여러 동시 사용자 또는 프로세스에서 Spark 세션을 공유함으로써 Spark 리소스 사용 효율성을 최적화할 수 있습니다. 노트북은 실행을 위해 Spark 세션을 사용합니다. 높은 동시성 모드를 활성화하면 여러 사용자가 동일한 Spark 세션을 사용하는 노트북에서 코드를 실행할 수 있으며, 코드 격리를 통해 한 노트북의 변수가 다른 노트북의 코드에 영향을 받지 않도록 할 수 있습니다. Spark 작업에도 높은 동시성 모드를 활성화하여 비대화형 Spark 스크립트 동시 실행에도 유사한 효율성을 구현할 수 있습니다.

높은 동시성 모드를 활성화하려면 작업 공간 설정 인터페이스의 **데이터 엔지니어링/과학 섹션을 사용하세요.**

### 자동 MLFlow 로깅

MLFlow는 데이터 과학 워크로드에서 머신 러닝 학습 및 모델 배포를 관리하는 데 사용되는 오픈 소스 라이브러리입니다. MLFlow의 핵심 기능은 모델 학습 및 관리 작업을 로깅하는 기능입니다. 기본적으로 Microsoft Fabric은 MLFlow를 사용하여 데이터 과학자가 명시적으로 코드를 추가할 필요 없이 머신 러닝 실험 활동을 암묵적으로 로깅합니다. 작업 영역 설정에서 이 기능을 비활성화할 수 있습니다.

### Fabric 용량에 대한 Spark 관리

관리자는 Fabric 용량 수준에서 Spark 설정을 관리하여 조직 내 작업 공간에서 Spark 설정을 제한하고 재정의할 수 있습니다.