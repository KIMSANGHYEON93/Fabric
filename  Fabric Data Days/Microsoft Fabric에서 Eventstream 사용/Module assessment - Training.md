---
title: "Module assessment - Training"
source: "https://learn.microsoft.com/en-us/training/modules/explore-event-streams-microsoft-fabric/6-knowledge-check"
author:
  - "[[theresa-i]]"
published:
created: 2025-12-03
description: "Check your knowledge of Eventstream in Real-Time Intelligence"
tags:
  - "clippings"
---
## 모듈 평가

완전한 200 경험치

- 10분

이 평가는 모듈에 대한 이해도를 평가합니다. 이전과는 달리, 개별 답변에 대한 피드백은 제공되지 않고 정답 여부만 제공됩니다. 이는 학습 내용을 측정하기 위한 것입니다. 시작하기 전에 모듈 자료를 충분히 검토하세요.

AI가 생성한 콘텐츠 이 모듈 평가의 질문과 답변 선택지는 AI를 사용하여 생성되었으며 인간 작성자가 검토했습니다.

---
1. What advantage does the 'Derived stream' destination offer in an eventstream setup?

- It stores data in Delta Lake format for historical analysis.
- **It enables content-based routing to multiple destinations based on data content. (Correct)**
- It triggers workflows based on data patterns.

2. Your organization needs to integrate real-time event data with an external system for custom processing. Which eventstream destination should be configured?

- **Custom endpoint (Correct)**
- Fabric Activator
- Derived stream

3. When configuring an eventstream pipeline, you need to ensure that real-time data from Azure IoT Hub is transformed into a standardized format for downstream compatibility. Which transformation should you use to achieve this?

- Aggregate transformation to summarize data
- **Manage fields transformation to change data types and rename fields (Correct)**
- Filter transformation to exclude irrelevant data

4. You are troubleshooting an eventstream pipeline where data from Azure Service Bus is being transformed but not reaching the intended destination. What could be the most likely cause of this issue?

- Incorrect source configuration in the eventstream canvas
- Absence of a transformation step in the pipeline
- **Misconfigured destination settings in the eventstream canvas (Correct)**

5. When routing real-time event data to trigger specific actions based on detected patterns, which destination is most appropriate?

- Eventhouse
- Lakehouse
- **Fabric Activator (Correct)**

6. Which transformation should be used to filter out invalid data in an eventstream pipeline?

- Join
- **Filter (Correct)**
- Union

7. While setting up an eventstream pipeline, you realize that data is being ingested and stored, but it needs enrichment with additional fields for clarity. Which transformation should you use to add calculated fields to the data?

- Expand transformation
- Filter transformation
- **Manage fields transformation (Correct)**

8. Your organization needs to standardize the format of incoming data from multiple sources before combining them into a single stream. Which transformation should be used to ensure consistent data structure?

- Join transformation
- **Manage fields transformation (Correct)**
- Expand transformation

9. Which transformation would be most suitable for ensuring that incoming data streams have consistent naming conventions before being routed to their destination?

- Union transformation
- Join transformation
- **Manage fields transformation (Correct)**
## 다음 단원: 요약

[이전의](https://learn.microsoft.com/en-us/training/modules/explore-event-streams-microsoft-fabric/5-exercise/) [다음](https://learn.microsoft.com/en-us/training/modules/explore-event-streams-microsoft-fabric/7-summary/)

도움이 필요하신가요? 통해 구체적인 피드백을 남겨주세요 .

---

이번 모듈 평가는 Microsoft Fabric의 **Real-Time Intelligence (실시간 인텔리전스)** 핵심 기능인 **Eventstream(이벤트스트림)**의 구성과 변환(Transformation)에 대한 내용입니다.

실시간 데이터 처리는 데이터 엔지니어링에서 가장 까다로운 분야 중 하나지만, Fabric은 이를 **No-code/Low-code** 방식으로 아주 쉽게 풀어냈습니다. 특히 **"데이터를 어디로 보낼지(Destination)"**와 **"어떻게 다듬을지(Transformation)"**를 묻는 문제가 집중적으로 출제되었습니다.

시니어의 관점에서 명쾌하게 정리해 드리겠습니다.

---

### 1. What advantage does the 'Derived stream' destination offer in an eventstream setup?

## 1. 🎯 출제 의도 파악 (The Hook)

- **핵심 주제:** Eventstream 내에서 파생 스트림(Derived Stream)의 역할을 묻습니다.
    
- **함정:** 단순히 데이터를 저장하는 것이 아니라, 데이터를 **"중간에서 분기(Branching)"**하거나 **"조건부로 라우팅"**하는 논리적 개념을 이해해야 합니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: It enables content-based routing to multiple destinations based on data content.**
    
- **논리적 흐름:**
    
    1. **Derived stream(파생 스트림)**은 원본 스트림에서 특정 조건(Filter)이나 변환(Transform)을 거친 후 생성되는 새로운 스트림입니다.
        
    2. 예를 들어, 전체 로그 중 "Error" 로그만 필터링하여 'Derived Stream A'로 만들고, 이를 경보 시스템으로 보낼 수 있습니다.
        
    3. 즉, 데이터의 내용(Content)에 따라 경로를 나누는(Routing) 역할을 수행합니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **It stores data in Delta Lake format...:** 이것은 **Lakehouse** Destination에 대한 설명입니다. 파생 스트림은 저장소가 아니라 흐름(Flow)입니다.
    
- **It triggers workflows...:** 이것은 **Fabric Activator**에 대한 설명입니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **설계 팁:** 복잡한 로직을 하나의 스트림에 다 넣지 마세요. Raw Stream -> Clean Stream -> Aggregated Stream 처럼 **파생 스트림을 단계별로 연결**해야 디버깅이 쉽습니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **파생 스트림은 데이터의 물길을 나누는 '교차로' 역할을 하여 콘텐츠 기반 라우팅을 가능하게 합니다.**
    

---

### 2. Your organization needs to integrate real-time event data with an external system for custom processing. Which eventstream destination should be configured?

## 1. 🎯 출제 의도 파악 (The Hook)

- **핵심 주제:** Fabric 내부가 아닌 **외부(External)** 시스템과의 연동 방법을 묻습니다.
    
- 키워드는 **"External system"**과 **"Custom processing"**입니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: Custom endpoint**
    
- **논리적 흐름:**
    
    1. Lakehouse, KQL Database, Activator 등은 모두 Microsoft Fabric **내부** 아이템입니다.
        
    2. Fabric 밖의 시스템(예: 회사의 레거시 API, 타사 솔루션)으로 데이터를 실시간 전송하려면, 특정 URL로 데이터를 쏘아주는 **Custom endpoint (사용자 지정 앱)** 목적지를 사용해야 합니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **Fabric Activator:** Fabric 내부의 알림/동작 감지 도구입니다.
    
- **Derived stream:** 스트림 내부의 중간 단계일 뿐, 외부로 나가는 문이 아닙니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **활용:** 주로 **Azure Functions**나 **Logic Apps**의 HTTP Trigger URL을 Custom Endpoint로 등록해서, Fabric 이벤트를 받아 복잡한 비즈니스 로직을 수행하게 만듭니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **Fabric 밖으로 데이터를 보내고 싶다면 무조건 'Custom endpoint'입니다.**
    

---

### 3. When configuring an eventstream pipeline, you need to ensure that real-time data from Azure IoT Hub is transformed into a standardized format for downstream compatibility. Which transformation should you use to achieve this?

## 1. 🎯 출제 의도 파악 (The Hook)

- **핵심 주제:** 데이터의 **구조(Schema)**와 **타입(Type)**을 변경하는 변환 도구를 찾으라는 문제입니다.
    
- 키워드는 **"Standardized format(표준화된 형식)"**, **"Change data types(데이터 유형 변경)"**입니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: Manage fields transformation to change data types and rename fields**
    
- **논리적 흐름:**
    
    1. IoT 데이터는 종종 날짜가 문자열(String)로 오거나, 필드명이 기계적(e.g., `temp_v1`)인 경우가 많습니다.
        
    2. 이를 `Temperature`로 바꾸거나(Rename), 숫자로 형변환(Cast)하는 작업은 **Manage fields(필드 관리)** 변환의 주 업무입니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **Aggregate transformation:** 합계나 평균을 구하는 것이지 형식을 바꾸는 게 아닙니다.
    
- **Filter transformation:** 데이터를 버리는 것이지 구조를 바꾸는 게 아닙니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **필수 작업:** IoT 데이터 수집 시 **Manage fields**는 선택이 아닌 필수입니다. 소스에서 오는 JSON 구조가 가끔 바뀌어도, 여기서 딱 잡아줘야 뒷단의 DB가 터지지 않습니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **이름 바꾸기, 타입 바꾸기, 컬럼 추가/삭제는 모두 'Manage fields' 담당입니다.**
    

---

### 4. You are troubleshooting an eventstream pipeline where data from Azure Service Bus is being transformed but not reaching the intended destination. What could be the most likely cause of this issue?

## 1. 🎯 출제 의도 파악 (The Hook)

- **핵심 주제:** **트러블슈팅(Troubleshooting)** 능력입니다.
    
- 데이터 흐름의 단계(Source -> Transform -> Destination) 중 어디가 끊겼는지 추론해야 합니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: Misconfigured destination settings in the eventstream canvas**
    
- **논리적 흐름:**
    
    1. 문제 지문에서 **"transformed"**라고 했습니다. 즉, 소스에서 데이터를 가져와 변환까지는 성공했다는 뜻입니다.
        
    2. 소스(Source)와 변환(Transform)이 정상이면, 남은 범인은 **목적지(Destination)** 뿐입니다.
        
    3. 목적지 테이블 이름이 틀렸거나, 권한이 없거나, 연결 설정이 잘못되었을 확률이 높습니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **Incorrect source configuration:** 소스가 잘못되었으면 변환 단계까지 데이터가 오지도 않았을 것입니다.
    
- **Absence of a transformation step:** 변환 단계가 없다고 데이터가 도착하지 않는 건 아닙니다(Raw Data로라도 들어갑니다).
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **디버깅:** Eventstream 캔버스에서 각 단계 사이의 선(Line)을 클릭해 보세요. **"Data Preview"** 기능을 통해 어디까지 데이터가 흘러왔는지 눈으로 확인할 수 있습니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **변환까지 됐는데 안 들어간다면? 범인은 무조건 '도착지(Destination)' 설정입니다.**
    

---

### 5. When routing real-time event data to trigger specific actions based on detected patterns, which destination is most appropriate?

## 1. 🎯 출제 의도 파악 (The Hook)

- **핵심 주제:** 데이터 저장(Storage)이 목적이 아니라 **행동(Action/Trigger)**이 목적인 도구를 묻습니다.
    
- 키워드는 **"Trigger specific actions"**, **"Detected patterns"**입니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: Fabric Activator**
    
- **논리적 흐름:**
    
    1. 데이터가 특정 조건(예: 온도 > 100도)을 만족할 때 이메일을 보내거나 Teams 메시지를 보내는 등 **행동**을 취하는 도구는 **Fabric Activator (Data Activator)**입니다.
        
    2. Eventstream에서 Activator를 목적지로 설정하여 실시간 모니터링 및 경보 시스템을 구축합니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **Eventhouse:** KQL Database를 사용하는 실시간 분석/저장소입니다. 저장은 잘하지만 직접 행동(이메일 발송 등)을 하지는 않습니다.
    
- **Lakehouse:** 배치 분석을 위한 저장소입니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **명칭 변경:** Fabric 내에서 **Reflex**라는 이름으로 불리기도 했습니다. "데이터가 튀면 반사 신경(Reflex)처럼 반응한다"고 외우시면 쉽습니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **패턴 감지 후 '행동(Action)'을 해야 한다면 답은 Fabric Activator입니다.**
    

---

### 6. Which transformation should be used to filter out invalid data in an eventstream pipeline?

## 1. 🎯 출제 의도 파악 (The Hook)

- **핵심 주제:** 데이터 정제의 가장 기본인 **행(Row) 삭제** 기능을 묻습니다.
    
- 키워드는 **"Filter out(걸러내다)"**, **"Invalid data(유효하지 않은 데이터)"**입니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: Filter**
    
- **논리적 흐름:**
    
    1. 특정 조건(예: `value IS NOT NULL` 또는 `status != 'error'`)에 맞지 않는 데이터를 흐름에서 제외시키는 변환은 **Filter(필터)**입니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **Join:** 두 데이터를 합치는 것입니다.
    
- **Union:** 두 데이터를 위아래로 붙이는 것입니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **비용 절감:** 불필요한 데이터는 소스 바로 뒤에서 **Filter**로 날려버리세요. 뒤단으로 갈수록 컴퓨팅 비용과 저장소 비용만 낭비됩니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **쓰레기 데이터는 'Filter'로 조기에 차단하세요.**
    

---

### 7. While setting up an eventstream pipeline, you realize that data is being ingested and stored, but it needs enrichment with additional fields for clarity. Which transformation should you use to add calculated fields to the data?

## 1. 🎯 출제 의도 파악 (The Hook)

- **핵심 주제:** 기존 데이터에 **새로운 정보(컬럼)를 추가**하는 변환입니다.
    
- 키워드는 **"Add calculated fields(계산된 필드 추가)"**, **"Enrichment(보강)"**입니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: Manage fields transformation**
    
- **논리적 흐름:**
    
    1. 이번 모듈 평가에서 **"Manage fields"**는 만능키입니다.
        
    2. 필드 이름 변경, 타입 변경뿐만 아니라, **새로운 필드를 추가(Add field)**하고 간단한 식(Expression)이나 정적 값을 넣는 것도 **Manage fields**에서 수행합니다.
        
    3. 예를 들어, `Environment`라는 필드를 추가하고 값을 `Production`으로 고정하는 작업 등이 가능합니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **Expand transformation:** 배열(Array) 데이터를 여러 행으로 펼칠 때 사용합니다.
    
- **Filter transformation:** 데이터를 줄이는 것이지 추가하는 게 아닙니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **헷갈림 주의:** SQL에서는 `Derived Column`이라고 부르는 기능이 여기서는 `Manage fields` 안에 포함되어 있습니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **필드를 추가하거나 값을 채워 넣는 것도 'Manage fields'의 역할입니다.**
    

---

### 8. Your organization needs to standardize the format of incoming data from multiple sources before combining them into a single stream. Which transformation should be used to ensure consistent data structure?

## 1. 🎯 출제 의도 파악 (The Hook)

- **핵심 주제:** 서로 다른 소스(Source A, Source B)의 **스키마(Schema)를 일치**시키는 작업입니다.
    
- 합치기(Union) 전에 모양을 맞춰야 합니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: Manage fields transformation**
    
- **논리적 흐름:**
    
    1. A 시스템은 고객명을 `CustName`으로 주고, B 시스템은 `Customer_Name`으로 줍니다.
        
    2. 이를 하나로 합치려면 둘 다 `CustomerName`으로 통일해야 합니다.
        
    3. 필드명을 변경하고 구조를 맞추는 작업은 역시 **Manage fields**입니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **Join / Expand:** 구조를 일치시키는(Standardize) 기능이 아닙니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **패턴:** **[Source A] -> [Manage Fields] + [Source B] -> [Manage Fields] => [Union]** 이 패턴이 실시간 데이터 통합의 정석입니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **데이터를 합치기 전 'Manage fields'로 규격(스키마)을 통일하세요.**
    

---

### 9. Which transformation would be most suitable for ensuring that incoming data streams have consistent naming conventions before being routed to their destination?

## 1. 🎯 출제 의도 파악 (The Hook)

- **핵심 주제:** 8번 문제와 거의 동일합니다. **"Naming conventions(명명 규칙)"**을 맞추는 변환입니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: Manage fields transformation**
    
- **논리적 흐름:**
    
    1. 카멜 케이스(`camelCase`), 스네이크 케이스(`snake_case`) 등 중구난방인 필드명을 하나로 통일하는 작업입니다.
        
    2. 필드 이름 변경(Rename) = **Manage fields**.
        

## 3. ❌ 오답 분석 (The Distractors)

- **Union transformation:** 합치는 행위이지 이름을 바꾸는 행위가 아닙니다.
    
- **Join transformation:** 옆으로 붙이는 행위입니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **시험 꿀팁:** 이번 모듈(Eventstream Transformation)에서 **"필드(Field), 컬럼(Column), 타입(Type), 이름(Name), 구조(Structure/Format)"** 이야기가 나오면 정답은 90% 이상 **Manage fields**입니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **필드 이름이나 규칙을 고치는 작업은 고민하지 말고 'Manage fields'를 선택하세요.**