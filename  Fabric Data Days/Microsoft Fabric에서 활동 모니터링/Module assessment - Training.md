---
title: "Module assessment - Training"
source: "https://learn.microsoft.com/en-us/training/modules/monitor-fabric-items/6-knowledge-check"
author:
  - "[[wwlpublish]]"
published:
created: 2025-12-03
description: "Knowledge check"
tags:
  - "clippings"
---
## 모듈 평가

완전한 200 경험치

- 5분

## 지식을 확인하세요

---
1. 

Microsoft Fabric에서 Monitor 허브의 주요 기능은 무엇입니까?

사용자가 데이터 파이프라인을 수정하고 업데이트할 수 있습니다.

새로운 데이터 통합 ​​프로세스를 만드는 플랫폼을 제공합니다.

선택된 Fabric 품목과 프로세스에서 데이터를 수집하고 집계하여 다양한 활동을 모니터링하기 위한 공통 인터페이스를 제공합니다.

Correct

2. 

Microsoft Fabric에서 Activator의 주요 기능은 무엇입니까?

Activator는 Microsoft Fabric에서 사용자 인터페이스를 디자인하는 도구입니다.

Activator는 Microsoft Fabric에서 데이터베이스를 만들고 관리하는 데 사용됩니다.

Activator는 작업을 트리거하는 이벤트의 자동 처리를 가능하게 합니다.

Correct

3. 

모범 사례를 모니터링하는 데 있어 중요한 측면은 무엇입니까?

모니터링할 항목을 식별하고, 정기적으로 데이터를 수집하고 분석하고, 로그와 지표를 정기적으로 검토하고, 편차가 발생하면 조치를 취하고, 모니터링 데이터를 사용하여 성능을 최적화합니다.

Correct

정상적인 동작에서 벗어난 동작이 나타날 때만 로그와 지표를 검토합니다.

이상 현상이 발생할 때만 데이터를 수집하고 분석합니다.

## 다음 단원: 요약

[이전의](https://learn.microsoft.com/en-us/training/modules/monitor-fabric-items/5-exercise/) [다음](https://learn.microsoft.com/en-us/training/modules/monitor-fabric-items/7-summary/)

도움이 필요하신가요? 통해 구체적인 피드백을 남겨주세요 .

---

## 피드백

이번 모듈 평가는 Microsoft Fabric의 **운영(Operations)** 및 **자동화(Automation)** 측면을 다루고 있습니다.

데이터 파이프라인을 아무리 잘 만들어도, 모니터링이 안 되면 "눈 가리고 운전하는 것"과 같고, 액션이 없으면 "데이터를 보고만 있는 것"과 같습니다. 엔지니어링의 완성을 위한 필수 지식들입니다.

명쾌하게 정리해 드리겠습니다.

---

### 1. Microsoft Fabric에서 Monitor 허브의 주요 기능은 무엇입니까?

## 1. 🎯 출제 의도 파악 (The Hook)

- **핵심 주제:** Fabric 내 모든 작업의 **상태를 확인하는 중앙 관제소**가 어디인지 묻습니다.
    
- **함정:** '수정(Modify)'이나 '생성(Create)' 같은 개발 단계의 용어와 '모니터링(Monitor)'을 구분해야 합니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: 선택된 Fabric 품목과 프로세스에서 데이터를 수집하고 집계하여 다양한 활동을 모니터링하기 위한 공통 인터페이스를 제공합니다.**
    
- **논리적 흐름:**
    
    1. Fabric은 Lakehouse, Warehouse, Pipeline, Spark Job 등 수많은 아이템이 돌아갑니다.
        
    2. **Monitor Hub(모니터링 허브)**는 이 모든 아이템의 실행 결과(성공/실패), 소요 시간, 사용자 등을 **하나의 화면(Centralized View)**에서 보여주는 역할을 합니다.
        
    3. 즉, 개별 워크스페이스에 들어가지 않고도 전체 현황을 파악할 수 있는 **공통 인터페이스**입니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **사용자가 데이터 파이프라인을 수정하고 업데이트할 수 있습니다:** 수정은 해당 아이템(Pipeline Canvas) 내부에서 합니다. 모니터링 허브는 **읽기 전용(View)**에 가깝습니다.
    
- **새로운 데이터 통합 프로세스를 만드는 플랫폼을 제공합니다:** 만드는 작업은 **Create Hub**나 워크스페이스에서 수행합니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **실무 꿀팁:** 모니터링 허브에 들어가면 가장 먼저 **필터(Filter)**를 눌러 **"Status = Failed"**만 체크하세요. 수백 개의 성공 로그 속에서 실패한 놈만 빠르게 낚아채는 것이 퇴근 시간을 앞당기는 비결입니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **Monitor Hub는 수정하는 곳이 아니라, 모든 작업의 성적표(성공/실패)를 한눈에 보는 상황실입니다.**
    

---

### 2. Microsoft Fabric에서 Activator의 주요 기능은 무엇입니까?

## 1. 🎯 출제 의도 파악 (The Hook)

- **핵심 주제:** **"데이터에 반응하여 행동(Action)하기"**입니다.
    
- 단순히 데이터를 보여주는 것(Dashboard)과, 특정 조건에 따라 알림을 보내는 것(Activator)을 구분해야 합니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: Activator는 작업을 트리거하는 이벤트의 자동 처리를 가능하게 합니다.**
    
- **논리적 흐름:**
    
    1. **Fabric Activator**는 데이터의 변화(예: 매출 급감, 온도 상승)를 감지하여 **이벤트**로 인식합니다.
        
    2. 이 이벤트가 발생했을 때 Teams 메시지 발송, 이메일 전송, Power Automate 실행 등의 **작업(Action)을 트리거**하는 것이 주 기능입니다.
        
    3. 과거 'Data Activator' 또는 'Reflex'라고 불렸던 기능입니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **사용자 인터페이스를 디자인하는 도구:** 이것은 **Power BI**나 Power Apps의 영역입니다.
    
- **데이터베이스를 만들고 관리:** 이것은 **Lakehouse**나 **Warehouse**의 역할입니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **활용 사례:** Power BI 보고서를 보다가 "이 숫자 100 넘으면 나한테 알려줘"라고 설정하는 기능이 바로 Activator입니다. 더 이상 하루 종일 대시보드만 쳐다보고 있을 필요가 없습니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **데이터가 말을 걸게 만드세요. 조건(Event)이 맞으면 행동(Action)하는 것이 Activator입니다.**
    

---

### 3. 모범 사례를 모니터링하는 데 있어 중요한 측면은 무엇입니까?

## 1. 🎯 출제 의도 파악 (The Hook)

- **핵심 주제:** **능동적 모니터링(Proactive)** vs **수동적 모니터링(Reactive)**의 태도를 묻습니다.
    
- 사고가 터지고 나서 수습하는 것과, 터지기 전에 징후를 살피는 것의 차이입니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: 모니터링할 항목을 식별하고, 정기적으로 데이터를 수집하고 분석하고, 로그와 지표를 정기적으로 검토하고, 편차가 발생하면 조치를 취하고, 모니터링 데이터를 사용하여 성능을 최적화합니다.**
    
- **논리적 흐름:**
    
    1. **정상 상태(Baseline)**를 알아야 **비정상(Anomaly)**을 감지할 수 있습니다. 이를 위해선 평소에도 데이터를 정기적으로 수집해야 합니다.
        
    2. 단순히 에러를 잡는 것을 넘어, 모니터링 데이터를 기반으로 **성능 최적화(Optimization)**까지 연결하는 것이 진정한 모범 사례(Best Practice)입니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **정상적인 동작에서 벗어난 동작이 나타날 때만... / 이상 현상이 발생할 때만...:** - 전형적인 **사후 약방문(Reactive)** 방식입니다. 사고가 나야만 로그를 본다면, 이미 비즈니스에 피해가 간 뒤입니다. 예방이 불가능한 방식이므로 오답입니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **필수 도구:** Fabric 관리자라면 **"Fabric Capacity Metrics App"**을 반드시 설치해서 매일 보셔야 합니다. 우리 회사의 CU(Compute Unit)를 누가 얼마나 쓰고 있는지, 언제 **Throttling(속도 제한)**이 걸릴지 미리 아는 것이 모니터링의 핵심입니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **소 잃고 외양간 고치지 마세요. 사고가 없어도 로그를 보고 최적화하는 것이 진짜 엔지니어입니다.**