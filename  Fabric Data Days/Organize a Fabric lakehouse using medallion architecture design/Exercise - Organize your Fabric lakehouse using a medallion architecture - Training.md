---
title: "Exercise - Organize your Fabric lakehouse using a medallion architecture - Training"
source: "https://learn.microsoft.com/en-us/training/modules/describe-medallion-architecture/6-exercise"
author:
  - "[[theresa-i]]"
published:
created: 2025-12-03
description: "Exercise - Organize your Fabric lakehouse using a medallion architecture"
tags:
  - "clippings"
---
## 연습 - 메달리온 구조를 사용하여 Fabric 레이크하우스 구성하기

완전한 100 경험치

- 45분

이제 Fabric에서 레이크하우스를 만들고 메달리온 아키텍처를 통해 데이터를 이동할 차례입니다. 또한 Fabric 레이크하우스에서 데이터를 쿼리하고 보고하는 방법도 알아봅니다.

운동을 시작하고 지시를 따르세요.
. 

다음 중 어떤 계층 세트가 데이터 관리를 위한 Medallion 아키텍처와 일반적으로 연관되어 있습니까?

원시, 광택, 정제

청동, 은, 금

Correct

초급, 중급, 최종

2. 

지속적으로 증가하는 대규모 데이터를 처리할 때 Fabric에서 데이터 변환에 가장 적합한 도구는 무엇입니까?

데이터 흐름(Gen2)

파이프라인

노트북

Correct

3. 

레이크하우스의 여러 층을 별도의 작업 공간에 보관하는 이점은 무엇입니까?

이를 통해 보안을 강화하고, 용량 사용을 관리하고, 비용 효율성을 최적화할 수 있습니다.

Correct

동료와 데이터를 공유하는 것이 더 쉬워집니다.

레이크하우스의 여러 층을 별도의 작업 공간에 보관하는 것에는 아무런 이점이 없습니다.
---

## 다음 단원: 모듈 평가

[이전의](https://learn.microsoft.com/en-us/training/modules/describe-medallion-architecture/5-secure-govern/) [다음](https://learn.microsoft.com/en-us/training/modules/describe-medallion-architecture/7-knowledge-check/)

도움이 필요하신가요? 통해 구체적인 피드백을 남겨주세요 .

---

이번 퀴즈는 데이터 엔지니어링 아키텍처의 표준인 **메달리온 아키텍처(Medallion Architecture)**와 이를 Fabric 환경에서 어떻게 구성하고 운영할지에 대한 **설계 및 운영 능력**을 테스트하는 문제입니다.

실무 아키텍트로서 가장 고민을 많이 해야 하는 부분이기도 합니다. 명쾌하게 정리해 드리겠습니다.

---

### 1. 다음 중 어떤 계층 세트가 데이터 관리를 위한 Medallion 아키텍처와 일반적으로 연관되어 있습니까?

## 1. 🎯 출제 의도 파악 (The Hook)

- 데이터 레이크하우스 디자인 패턴의 **업계 표준 용어**를 알고 있는지 묻는 아주 기본적인 문제입니다.
    
- **Databricks**와 **Microsoft**가 공통적으로 밀고 있는 아키텍처 개념입니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: 청동, 은, 금 (Bronze, Silver, Gold)**
    
- **논리적 흐름:**
    
    1. **Bronze (청동):** 원본 소스 시스템에서 데이터를 그대로 가져와 저장하는 **Raw(원시) 데이터** 계층입니다. 변경 없이 역사적 기록을 남깁니다.
        
    2. **Silver (은):** Bronze 데이터를 정제(Cleanse), 필터링, 중복 제거한 **신뢰할 수 있는 데이터** 계층입니다. 엔지니어들이 주로 작업하는 구간입니다.
        
    3. **Gold (금):** 비즈니스 로직을 적용하여 집계(Aggregation)하고, 보고서나 ML 모델이 바로 소비할 수 있게 만든 **최종 데이터** 계층입니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **원시, 광택, 정제 / 초급, 중급, 최종:** 그럴듯해 보이지만, 업계에서 약속된 공식 용어가 아닙니다. 다른 엔지니어와 대화할 때 "실버 레이어 문제가..."라고 해야 알아듣습니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **실무 Tip:** 가끔 **"Platinum"** 레이어를 두기도 합니다. Gold보다 더 요약된 임원 보고용 KPI 테이블을 따로 관리할 때 씁니다. 하지만 기본은 무조건 청/은/금입니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **원시(Raw)는 Bronze, 정제(Clean)는 Silver, 비즈니스용(Biz)은 Gold. 이 3단계를 외우세요.**
    

---

### 2. 지속적으로 증가하는 대규모 데이터를 처리할 때 Fabric에서 데이터 변환에 가장 적합한 도구는 무엇입니까?

## 1. 🎯 출제 의도 파악 (The Hook)

- **"대규모(Large-scale)"**와 **"데이터 변환(Transformation)"**이라는 조건에서 어떤 컴퓨팅 엔진을 선택해야 하는지 묻습니다.
    
- Low-code(Dataflow)와 Code-first(Notebook) 사이의 성능적 차이를 이해해야 합니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: 노트북 (Notebook)**
    
- **논리적 흐름:**
    
    1. **Apache Spark**는 분산 병렬 처리를 통해 페타바이트급 데이터를 처리하도록 설계되었습니다. Fabric의 **Notebook**은 이 Spark 엔진을 직접 다루는 도구입니다.
        
    2. Dataflow Gen2도 훌륭하지만, 데이터 양이 폭발적으로 늘어나거나 복잡한 커스텀 로직(복잡한 수학 연산, 비정형 데이터 파싱 등)이 필요할 때는 Spark 코드로 작성된 Notebook이 성능과 유연성 면에서 압도적입니다.
        
    3. "지속적으로 증가하는 대규모"라는 수식어는 Spark(Notebook)를 쓰라는 강력한 신호입니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **데이터 흐름(Gen2):** 중소 규모 데이터나 단순/중간 복잡도의 변환에는 시각적이고 빠릅니다. 하지만 초대용량 데이터 처리에서는 Spark Notebook보다 세밀한 튜닝이 어렵습니다.
    
- **파이프라인:** 데이터를 '이동(Copy)'하거나 작업 순서를 '조율(Orchestrate)'하는 관리자이지, 데이터 내부를 뜯어고치는 '변환' 작업의 주체는 아닙니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **성능 최적화:** Notebook을 쓸 때는 데이터가 커질수록 **파티셔닝(Partitioning)** 전략(예: 날짜별 폴더링)을 잘 짜야 속도가 느려지지 않습니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **데이터가 너무 크고 복잡하다 싶으면 고민하지 말고 Spark Notebook을 꺼내드세요.**
    

---

### 3. 레이크하우스의 여러 층을 별도의 작업 공간에 보관하는 이점은 무엇입니까?

## 1. 🎯 출제 의도 파악 (The Hook)

- Fabric의 **워크스페이스(Workspace)**가 단순한 폴더가 아니라 **보안 및 거버넌스의 경계(Boundary)**라는 점을 이해하는지 묻습니다.
    
- 왜 귀찮게 Bronze, Silver, Gold를 한곳에 안 두고 쪼개는지 묻는 것입니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: 이를 통해 보안을 강화하고, 용량 사용을 관리하고, 비용 효율성을 최적화할 수 있습니다.**
    
- **논리적 흐름:**
    
    1. **보안(Security):** Bronze(Raw)에는 민감한 개인정보(PII)가 있을 수 있습니다. 이를 별도 워크스페이스에 두고 소수의 엔지니어만 접근하게 하고, Gold 워크스페이스는 분석가 전원에게 오픈하는 식으로 **RBAC(권한 제어)**를 할 수 있습니다.
        
    2. **용량(Capacity):** 무거운 ETL 작업이 도는 Silver 워크스페이스에는 고성능 용량(F64)을 할당하고, 조회만 하는 Gold에는 저성능 용량(F8)을 할당해 **비용을 최적화**할 수 있습니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **동료와 데이터를 공유하는 것이 더 쉬워집니다:** 오히려 워크스페이스가 쪼개지면 공유 설정(Shortcut 등)을 한 번 더 해줘야 하므로, 공유의 편의성보다는 **통제와 관리**가 주 목적입니다.
    
- **아무런 이점이 없습니다:** Fabric 아키텍처 설계를 전혀 이해하지 못한 오답입니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **현업 권장:** 처음에는 하나의 워크스페이스에서 시작하더라도, 조직이 커지면 무조건 **[Data Ingestion], [Data Engineering], [Data Consumption]** 등으로 워크스페이스를 나누게 됩니다. 미리 분리하는 습관을 들이세요.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **워크스페이스 분리는 '보안 벽'을 세우고 '컴퓨팅 비용'을 따로 정산하기 위한 최고의 전략입니다.**