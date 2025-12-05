---
title: "Use the Copy Data activity - Training"
source: "https://learn.microsoft.com/en-us/training/modules/use-data-factory-pipelines-fabric/3-copy-data"
author:
  - "[[theresa-i]]"
published:
created: 2025-12-03
description: "Use the Copy Data activity"
tags:
  - "clippings"
---
## 데이터 복사 활동 사용

100 경험치

**데이터 복사** 활동 은 데이터 파이프라인의 가장 일반적인 용도 중 하나입니다. 많은 파이프라인은 외부 소스에서 레이크하우스 파일이나 테이블로 데이터를 수집하는 데 사용되는 단일 **데이터 복사 활동으로 구성됩니다.**

**데이터 복사** 활동을 다른 활동과 결합하여 반복 가능한 데이터 수집 프로세스를 만들 수도 있습니다. 예를 들어, **데이터 삭제** 활동을 사용하여 기존 데이터를 제거하고, **데이터 복사** 활동을 사용하여 삭제된 데이터를 외부 소스의 데이터가 포함된 파일로 바꾸고, **노트북** 활동을 사용하여 파일의 데이터를 변환하고 테이블에 로드하는 Spark 코드를 실행합니다.

## 데이터 복사 도구

![Microsoft Fabric의 데이터 복사 도구 스크린샷.](https://learn.microsoft.com/en-us/training/wwl/use-data-factory-pipelines-fabric/media/copy-data.png)

**파이프라인에 데이터 복사** 활동을 추가하면 그래픽 도구가 복사 작업의 데이터 소스와 대상을 구성하는 데 필요한 단계를 안내합니다. 다양한 소스 연결이 지원되므로 대부분의 일반적인 소스에서 데이터를 수집할 수 있습니다. OneLake에서는 레이크하우스, 웨어하우스, SQL 데이터베이스 등을 지원합니다.

![Microsoft Fabric에서 SQL 데이터베이스 지원을 보여주는 데이터 복사 도구의 스크린샷입니다.](https://learn.microsoft.com/en-us/training/wwl/use-data-factory-pipelines-fabric/media/copy-sql-database.png)

## 데이터 복사 활동 설정

**파이프라인에 데이터 복사** 활동을 추가한 후에는 파이프라인 캔버스에서 해당 활동을 선택하고 아래 창에서 설정을 편집할 수 있습니다.

![Microsoft Fabric의 데이터 복사 활동 스크린샷.](https://learn.microsoft.com/en-us/training/wwl/use-data-factory-pipelines-fabric/media/copy-data-activity.png)

## 데이터 복사 활동을 사용하는 경우

변환을 적용하지 않고 지원되는 소스와 대상 간에 데이터를 직접 복사해야 하거나 원시 데이터를 가져와서 이후 파이프라인 활동에서 변환을 적용하려는 경우 **데이터 복사** 활동을 사용합니다.

데이터가 수집되는 동안 데이터에 변환을 적용하거나 여러 소스의 데이터를 병합해야 하는 경우, **데이터 흐름** 활동을 사용하여 데이터 흐름(Gen2)을 실행하는 것을 고려해 보세요. Power Query 사용자 인터페이스를 사용하여 여러 변환 단계를 포함하는 데이터 흐름(Gen2)을 정의하고 파이프라인에 포함할 수 있습니다.