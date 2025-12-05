---
title: "Eventstream sources and destinations - Training"
source: "https://learn.microsoft.com/en-us/training/modules/explore-event-streams-microsoft-fabric/3-setup-eventstreams"
author:
  - "[[theresa-i]]"
published:
created: 2025-12-03
description: "Create Eventstream sources and destinations"
tags:
  - "clippings"
---
## 이벤트스트림 소스 및 대상

100 경험치

Fabric에서 이벤트 스트림을 생성하면 다양한 데이터 소스에 연결하고, 선택적으로 이벤트 스트림을 변환하고, 변환되거나 처리된 데이터를 여러 목적지로 라우팅할 수 있습니다. 이 단원에서는 이벤트 스트림 소스와 목적지를 살펴보겠습니다.

## 이벤트스트림 소스

Microsoft 소스에서 데이터를 스트리밍할 수 있으며 다음을 포함한 Microsoft가 아닌 플랫폼에서 데이터를 수집할 수도 있습니다.

- Azure Event Hubs, Azure IoT Hubs, Azure Service Bus, 데이터베이스 서비스의 CDC(변경 데이터 캡처) 피드 등과 같은 **Microsoft 소스입니다.**
- **Azure 이벤트** (Azure Blob Storage 이벤트 등)
- Fabric 작업 공간의 항목 변경, OneLake 데이터 저장소의 데이터 변경, Fabric 작업과 관련된 이벤트와 같은 **Fabric 이벤트입니다.**
- Apache Kafka, Google Cloud Pub/Sub, MQTT(Message Queuing Telemetry Transport)와 같은 **외부 소스**

## 이벤트스트림 소스 구성

이벤트 스트림을 생성한 후 이벤트 스트림 캔버스를 사용하여 데이터 소스를 추가할 수 있습니다. 실시간 허브에서 새 소스를 생성하거나 기존 소스에 연결할 수 있습니다.

![이벤트스트림 캔버스에서 소스를 구성하는 방법을 보여주는 스크린샷입니다.](https://learn.microsoft.com/en-us/training/wwl/explore-event-streams-microsoft-fabric/media/configure-sources.png)

이벤트스트림 캔버스에서 소스를 구성하는 방법을 보여주는 스크린샷입니다.

## 이벤트스트림 목적지

스트리밍 데이터는 가치를 유지하기 위해 즉각적인 처리 및 저장이 필요합니다. 이벤트 스트림의 대상은 처리된 데이터를 쿼리, 보고서, 대시보드, 알림, 작업 또는 다른 시스템과의 통합에 사용할 수 있는 엔드포인트 역할을 합니다. 스트림의 데이터를 다음 대상에 로드할 수 있습니다.

- **Eventhouse**: 이 대상을 사용하면 실시간 이벤트 데이터를 Eventhouse로 수집할 수 있으며, Eventhouse에서 Kusto Query Language(KQL)를 사용하여 데이터를 쿼리하고 분석할 수 있습니다.
- **레이크하우스**: 이 목적지를 사용하면 실시간 이벤트를 레이크하우스에 가져오기 전에 변환할 수 있습니다. 실시간 이벤트는 델타 레이크 형식으로 변환된 후 지정된 레이크하우스 테이블에 저장됩니다.
- **파생 스트림: 파생 스트림은** **콘텐츠 기반 라우팅을** 지원하는 원본 데이터 스트림의 변형된 버전이라고 할 수 있습니다 . 파생 스트림을 사용하면 *기본 스트림 또는 원본 스트림의 데이터 하위 집합을 데이터* *콘텐츠* 에 따라 다른 목적지로 라우팅할 수 있습니다 . 예를 들어, IoT 센서 데이터를 필터링하여 고온 경보를 Fabric Activator로 전송하고, 시간당 평균 데이터를 KQL 데이터베이스로 라우팅할 수 있습니다.
- **Fabric Activator**: 실시간 이벤트 데이터를 이벤트 감지 엔진에 직접 연결하여 스트리밍 데이터에서 특정 패턴이나 조건이 감지될 때 자동으로 조치를 트리거합니다. 데이터가 특정 임계값에 도달하거나 패턴과 일치하면 Activator는 알림을 보내거나, Power Automate 워크플로를 실행하거나, 기타 자동화된 응답을 트리거할 수 있습니다.
- **사용자 지정 엔드포인트**: 이 대상을 사용하면 실시간 이벤트를 사용자 지정 엔드포인트로 라우팅할 수 있습니다. 이 대상은 Microsoft Fabric 외부의 외부 시스템이나 사용자 지정 애플리케이션으로 실시간 데이터를 전송하려는 경우 유용합니다.

이벤트 스트림 내에서 여러 대상에 동시에 연결할 수 있으며, 서로 영향을 주거나 충돌하지 않습니다.

## 이벤트스트림 대상 구성

이벤트스트림 대상은 이벤트스트림 캔버스에서 구성할 수 있습니다. 데이터 소스가 연결되거나 선택적 변환이 적용된 후에 대상을 지정할 수 있습니다.

![이벤트스트림 캔버스에서 대상을 구성하는 방법을 보여주는 스크린샷입니다.](https://learn.microsoft.com/en-us/training/wwl/explore-event-streams-microsoft-fabric/media/eventstream-destinations.png)

이벤트스트림 캔버스에서 대상을 구성하는 방법을 보여주는 스크린샷입니다.

이미지의 이벤트스트림 캔버스는 다음을 보여줍니다.

- **목적지 드롭다운 추가**: 새로운 목적지를 구성하기 위해
- **구성된 3개의 대상**: 파생 스트림, Fabric Activator 및 Eventhouse
- GroupByStreet 변환의 출력이 파생 스트림으로 라우팅되고, 이 스트림이 모든 역에 자전거가 있는지 확인하기 위해 Activator로 라우팅되고, 거리별 자전거 수를 KQL 데이터베이스에 삽입하기 위해 Eventhouse로 라우팅되는 **콘텐츠 기반 라우팅**