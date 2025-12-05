---
title: "Module assessment - Training"
source: "https://learn.microsoft.com/en-us/training/modules/use-data-factory-pipelines-fabric/7-knowledge-check"
author:
  - "[[theresa-i]]"
published:
created: 2025-12-03
description: "Knowledge check"
tags:
  - "clippings"
---
## 모듈 평가

완전한 200 경험치

- 3분

## 지식을 확인하세요
1. 데이터 파이프라인이란 무엇인가요?

- OneLake 저장소의 특수 폴더로, 레이크하우스에서 데이터를 내보낼 수 있습니다.
- **데이터 수집 또는 변환 프로세스를 조율하기 위한 일련의 활동 (Correct)**
- 저장된 Power Query

2. 파이프라인을 사용하여 각 실행마다 지정된 이름의 폴더에 데이터를 복사하려고 합니다. 어떻게 해야 할까요?

- 각 폴더 이름에 대해 하나씩 여러 파이프라인을 만듭니다.
- 데이터 흐름(Gen2) 사용
- **파이프라인에 매개변수를 추가하고 이를 사용하여 각 실행에 대한 폴더 이름을 지정합니다. (Correct)**

3. 이전에 여러 활동이 포함된 파이프라인을 실행한 적이 있습니다. 각 활동을 완료하는 데 걸린 시간을 확인하는 가장 좋은 방법은 무엇인가요?

- 파이프라인을 다시 실행하고 각 활동의 타이밍을 측정하여 출력을 관찰합니다.
- **실행 기록에서 실행 세부 정보를 확인하세요. (Correct)**
- Lakehouse의 기본 데이터 세트에 대한 **새로 고침된** 값을 확인하세요.
---

## 다음 단원: 요약

[이전의](https://learn.microsoft.com/en-us/training/modules/use-data-factory-pipelines-fabric/6-exercise-pipelines/) [다음](https://learn.microsoft.com/en-us/training/modules/use-data-factory-pipelines-fabric/8-summary/)

도움이 필요하신가요? 통해 구체적인 피드백을 남겨주세요 .

---

이번 모듈 평가는 Microsoft Fabric의 **데이터 파이프라인(Data Pipeline)**, 즉 데이터 이동과 작업 흐름을 제어하는 **오케스트레이션(Orchestration)** 기능을 얼마나 잘 이해하고 활용할 수 있는지를 묻고 있습니다.

단순히 데이터를 옮기는 것을 넘어, **자동화(Automation)**와 **모니터링(Monitoring)**까지 아우르는 데이터 엔지니어의 핵심 역량입니다. 하나씩 명쾌하게 풀어드리겠습니다.

---

### 1. 데이터 파이프라인이란 무엇인가요?

## 1. 🎯 출제 의도 파악 (The Hook)

- **핵심 주제:** **Pipeline(파이프라인)**과 **Dataflow(데이터 흐름)**의 역할 차이를 정확히 구분할 수 있는지 묻습니다.
    
- **함정:** '데이터 변환'이라는 단어가 나오면 무조건 Dataflow라고 생각하기 쉽지만, '조율(Orchestrate)'이라는 단어가 핵심입니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: 데이터 수집 또는 변환 프로세스를 조율하기 위한 일련의 활동 (A sequence of activities to orchestrate data ingestion or transformation processes)**
    
- **논리적 흐름:**
    
    1. 파이프라인은 그 자체로 데이터를 변환하는 엔진이라기보다, **"지휘자"**에 가깝습니다.
        
    2. "데이터 복사(Copy Activity) → 노트북 실행(Notebook) → 성공 시 메일 발송(Outlook)" 처럼 일련의 **활동(Activities)**을 순서대로 연결하고 제어(Control Flow)하는 것이 주 목적입니다.
        
    3. 따라서 **"조율(Orchestrate)"**이라는 키워드가 나오면 정답은 파이프라인입니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **OneLake 저장소의 특수 폴더:** 파이프라인은 로직(Logic)이지 저장소(Storage)가 아닙니다.
    
- **저장된 Power Query:** 이것은 **Dataflow Gen2**에 대한 설명입니다. Dataflow는 데이터를 변환하는 '작업자'이고, 파이프라인은 그 작업자에게 일을 시키는 '관리자'입니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **비유:** 공장에 비유하자면, **Dataflow/Notebook**은 기계(실제 작업)이고, **Pipeline**은 공정 관리 시스템(작업 순서 및 스케줄링)입니다. 복잡한 로직은 파이프라인에서 구현하지 말고 노트북이나 SP(Stored Procedure)를 호출하는 구조로 짜세요.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **데이터 파이프라인은 데이터를 직접 요리하는 쉐프가 아니라, 주방 전체를 지휘하는 매니저(Orchestrator)입니다.**
    

---

### 2. 파이프라인을 사용하여 각 실행마다 지정된 이름의 폴더에 데이터를 복사하려고 합니다. 어떻게 해야 할까요?

## 1. 🎯 출제 의도 파악 (The Hook)

- **핵심 주제:** 파이프라인의 **재사용성(Reusability)**과 **동적 구성(Dynamic Configuration)** 능력을 테스트합니다.
    
- 매일매일 폴더 이름이 바뀌는데(예: 2023-10-01, 2023-10-02), 그때마다 파이프라인을 새로 만들 것인가? 라는 질문입니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: 파이프라인에 매개변수를 추가하고 이를 사용하여 각 실행에 대한 폴더 이름을 지정합니다. (Add parameters to the pipeline and use them to specify the folder name for each run)**
    
- **논리적 흐름:**
    
    1. **매개변수(Parameter)**는 파이프라인이 실행될 때 외부에서 값을 받아오는 변수입니다.
        
    2. 파이프라인 설정에서 `FolderName`이라는 매개변수를 만들고, Copy Activity의 대상 경로(Destination Path)에 `@pipeline().parameters.FolderName`과 같은 식(Expression)을 넣습니다.
        
    3. 이렇게 하면 하나의 파이프라인으로 매번 다른 폴더에 데이터를 저장할 수 있습니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **각 폴더 이름에 대해 하나씩 여러 파이프라인을 만듭니다:** 유지보수의 악몽입니다. 1년 365일 치 365개의 파이프라인을 만들 수는 없습니다. (하드코딩의 최후)
    
- **데이터 흐름(Gen2) 사용:** 도구를 바꾸는 것이 정답이 아닙니다. 파이프라인 내에서 해결할 수 있는 문제입니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **Expression 활용:** 매개변수를 직접 입력받을 수도 있지만, 실무에서는 **시스템 변수**를 더 많이 씁니다. 예를 들어 `@formatDateTime(utcNow(), 'yyyy/MM/dd')` 식을 쓰면 매개변수 입력 없이도 자동으로 오늘 날짜 폴더를 생성합니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **하드코딩 하지 마세요. '매개변수(Parameter)'와 '동적 콘텐츠(Expression)'를 쓰면 파이프라인 하나로 천 가지 상황을 처리합니다.**
    

---

### 3. 이전에 여러 활동이 포함된 파이프라인을 실행한 적이 있습니다. 각 활동을 완료하는 데 걸린 시간을 확인하는 가장 좋은 방법은 무엇인가요?

## 1. 🎯 출제 의도 파악 (The Hook)

- **핵심 주제:** 데이터 엔지니어링의 필수 덕목인 **모니터링(Monitoring)과 디버깅(Debugging)** 방법을 묻습니다.
    
- 문제가 생겼거나 성능이 느려졌을 때 어디를 봐야 하는지 아는 것은 매우 중요합니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: 실행 기록에서 실행 세부 정보를 확인하세요. (Check the run details in the run history)**
    
- **논리적 흐름:**
    
    1. Fabric의 모니터링 허브나 파이프라인 캔버스 하단의 **출력(Output)** 탭에서는 과거 실행 기록(Run History)을 제공합니다.
        
    2. 특정 실행 ID(Run ID)를 클릭하면 각 활동(Activity) 별로 **성공 여부, 시작 시간, 종료 시간, 소요 시간(Duration)**이 간트 차트(Gantt Chart)나 리스트 형태로 상세히 나옵니다.
        
    3. 이것이 병목 구간(Bottleneck)을 찾는 가장 정확한 방법입니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **파이프라인을 다시 실행하고...:** 이미 끝난 과거의 기록을 보려는 것인데, 다시 실행하는 것은 자원 낭비이며, 그때와 상황이 달라(데이터 양 등) 정확한 비교가 안 됩니다.
    
- **Lakehouse의 기본 데이터 세트에 대한 새로 고침된 값을 확인하세요:** 데이터가 들어왔는지는 알 수 있지만, 그 과정에서 **'얼마나 시간이 걸렸는지'**는 데이터만 보고 알 수 없습니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **모니터링 팁:** "안경 모양 아이콘(Spectacles Icon)"을 찾으세요. 실행 세부 정보 창에서 특정 활동의 **'입력(Input)'**과 **'출력(Output)'** JSON을 확인하면, 몇 건의 데이터를 읽어서 몇 건을 썼는지까지 정확히 알 수 있습니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **추측하지 말고 기록을 보세요. '실행 기록(Run History)'에 모든 활동의 성적표(소요 시간, 상태)가 적혀 있습니다.**