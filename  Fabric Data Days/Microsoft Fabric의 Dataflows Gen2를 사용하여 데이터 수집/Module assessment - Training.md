---
title: "Module assessment - Training"
source: "https://learn.microsoft.com/en-us/training/modules/use-dataflow-gen-2-fabric/6-knowledge-check"
author:
  - "[[AngieRudduck]]"
published:
created: 2025-12-03
description: "Knowledge check"
tags:
  - "clippings"
---
## 모듈 평가

완전한 200 경험치
1. Your organization wants to reduce data preparation time by reusing data transformations across multiple projects. How can Dataflows Gen2 facilitate this requirement?

- **By creating reusable dataflows that apply consistent transformations. (Correct)**
- By automatically generating machine learning transformations.
- By integrating directly with Azure Synapse Analytics for automated workflows.

2. Which of the following is a limitation of using Dataflows Gen2 in Microsoft Fabric?

- **They are not a replacement for a data warehouse. (Correct)**
- They lack support for transforming data from cloud-based sources.
- They require extensive coding for data transformations.

3. When incorporating a Dataflow Gen2 into a pipeline, what step ensures the dataflow runs automatically without manual intervention?

- **Configuring a trigger to schedule automatic execution (Correct)**
- Manually executing the dataflow from the pipeline interface
- Linking the dataflow directly to a Power BI report

4. In your data pipeline, you have included a Dataflow Gen2 for transforming raw sales data. What is an advantage of adding this dataflow to your pipeline before other activities?

- It ensures the dataflow is executed faster than other pipeline activities.
- It reduces the need for data validation in downstream activities.
- **It allows for data transformations to be completed before executing scripts or stored procedures. (Correct)**

5. To support Power BI reporting, your company needs to transform data closer to the source. Why would Dataflows Gen2 be an ideal solution in this scenario?

- They provide a manual interface for data transformations
- **They allow transformations to be performed upstream, improving report performance (Correct)**
- They replace the need for a data warehouse

6. How do Dataflows Gen2 simplify data integration compared to traditional data pipelines?

- **By providing a low-code interface that ingests data from various sources. (Correct)**
- By automatically generating machine learning models for data analysis.
- By supporting row-level security for sensitive data.

7. Your organization wants to expose data to a large group of data analysts without making the data source complexity apparent. How can Dataflows Gen2 assist in this situation?

- By automatically updating data models using artificial intelligence.
- By implementing row-level security to restrict data access based on user roles.
- **By simplifying data source complexity and exposing only the dataflows to the analysts. (Correct)**

8. What is an essential step when configuring a Dataflow Gen2 to ensure it can be reused for different data sources?

- Setting a static data destination for all transformations.
- **Parameterizing the data source connections. (Correct)**
- Hardcoding the data source credentials in the dataflow.

9. Which component is often overlooked but is essential for automating data refresh in a Dataflow Gen2?

- **Scheduling the dataflow in a pipeline. (Correct)**
- Applying data masking on sensitive columns.
- Integrating the dataflow with Power BI Desktop.
---

## 다음 단원: 요약

[이전의](https://learn.microsoft.com/en-us/training/modules/use-dataflow-gen-2-fabric/5-exercise/) [다음](https://learn.microsoft.com/en-us/training/modules/use-dataflow-gen-2-fabric/7-summary/)

도움이 필요하신가요? 통해 구체적인 피드백을 남겨주세요 .

---

## 피드백

이번 모듈 평가는 **"Dataflows Gen2"**에 대한 심층적인 이해를 묻고 있습니다.

Fabric에서 Dataflow Gen2는 **"Low-code(코드 작성 최소화) 데이터 변환 도구"**이자, Power BI 사용자들에게 익숙한 Power Query의 클라우드 진화형입니다.

코딩 없이 데이터를 처리하고 싶거나, 비즈니스 로직을 재사용하고 싶을 때 가장 강력한 무기입니다.

시니어 엔지니어의 시각으로 명쾌하게 풀어드리겠습니다.

---

### 1. Your organization wants to reduce data preparation time by reusing data transformations across multiple projects. How can Dataflows Gen2 facilitate this requirement?

## 1. 🎯 출제 의도 파악 (The Hook)

- **핵심 주제:** Dataflow의 **재사용성(Reusability)**과 **모듈화** 능력을 묻습니다.
    
- 매번 새로 만드는 것이 아니라, 한 번 만든 로직을 어떻게 우려먹을(?) 수 있는지 묻는 것입니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: By creating reusable dataflows that apply consistent transformations.**
    
- **논리적 흐름:**
    
    1. Dataflow Gen2는 **Linked Entities(연결된 엔터티)** 기능을 지원합니다.
        
    2. 예를 들어, '환율 계산' Dataflow를 하나 만들어두면, 재무팀, 영업팀, 인사팀 프로젝트에서 이 Dataflow를 **참조(Reference)**하여 똑같은 로직을 재사용할 수 있습니다.
        
    3. 이를 통해 전사적으로 일관된 데이터 변환 로직을 유지하고 준비 시간을 단축합니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **By automatically generating machine learning transformations:** ML 변환은 부차적인 기능이지, '재사용성'의 핵심 메커니즘이 아닙니다.
    
- **By integrating directly with Azure Synapse...:** Synapse와의 통합이 재사용성을 보장하는 것은 아닙니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **설계 팁:** **Staging Dataflow(1차 추출)**와 **Transformation Dataflow(2차 가공)**를 분리하세요. 원본 데이터를 가져오는 놈 따로, 계산하는 놈 따로 만들어야 나중에 유지보수가 쉽고 재사용하기 좋습니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **잘 만든 Dataflow 하나, 열 프로젝트 안 부럽다. (로직 공유 및 참조 가능)**
    

---

### 2. Which of the following is a limitation of using Dataflows Gen2 in Microsoft Fabric?

## 1. 🎯 출제 의도 파악 (The Hook)

- **핵심 주제:** Dataflow Gen2의 **역할과 한계(Scope)**를 명확히 아는지 묻습니다.
    
- Dataflow는 '요리사(ETL)'이지 '냉장고(Storage)'가 아님을 이해해야 합니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: They are not a replacement for a data warehouse.**
    
- **논리적 흐름:**
    
    1. Dataflow Gen2는 데이터를 가져와서 변환하고 어딘가(Lakehouse, Warehouse)에 싣는(Load) **ETL 도구**입니다.
        
    2. 그 자체로 대규모 데이터를 영구 보관하고, 복잡한 SQL 쿼리를 서빙하며, 트랜잭션을 관리하는 **Data Warehouse**의 기능을 대체할 수 없습니다.
        
    3. 요리사(Dataflow)가 요리는 잘해도, 음식을 보관하는 창고(Warehouse)가 될 순 없습니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **They require extensive coding...:** 정반대입니다. Dataflow는 **Low-code/No-code**가 핵심 장점입니다.
    
- **They lack support for transforming data from cloud-based sources:** Azure, AWS, Google 등 대부분의 클라우드 소스를 지원합니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **주의:** Dataflow 내에도 데이터가 저장되는 'Staging' 공간이 있긴 하지만, 이걸 믿고 Warehouse를 안 만들면 안 됩니다. 이건 임시 저장소일 뿐입니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **Dataflow는 '데이터를 나르는 파이프'이지, '데이터를 쌓아두는 댐'이 아닙니다.**
    

---

### 3. When incorporating a Dataflow Gen2 into a pipeline, what step ensures the dataflow runs automatically without manual intervention?

## 1. 🎯 출제 의도 파악 (The Hook)

- **핵심 주제:** **자동화(Automation)**를 위한 **트리거(Trigger)** 개념입니다.
    
- 파이프라인 안에서 사람 손을 타지 않게 만드는 장치가 무엇인지 묻습니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: Configuring a trigger to schedule automatic execution**
    
- **논리적 흐름:**
    
    1. 파이프라인이나 Dataflow를 자동으로 실행하려면 **스케줄 트리거(Schedule Trigger)**나 **이벤트 트리거(Event Trigger)**가 필요합니다.
        
    2. 파이프라인에 Dataflow 활동을 넣었다면, 그 파이프라인 자체에 "매일 아침 9시 실행"과 같은 스케줄을 걸어줘야 자동화가 완성됩니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **Manually executing...:** 질문이 "without manual intervention(수동 개입 없이)"이므로 오답입니다.
    
- **Linking... to Power BI:** 이건 리포팅 연결이지 실행 자동화와는 무관합니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **운영 팁:** Dataflow 자체에도 스케줄 기능이 있지만, 전후 관계(Notebook 실행 후 -> Dataflow 실행)를 제어하려면 **Data Factory Pipeline** 안에 넣어서 오케스트레이션 하는 것이 정석입니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **자동화의 완성은 '스케줄링 트리거' 설정입니다.**
    

---

### 4. In your data pipeline, you have included a Dataflow Gen2 for transforming raw sales data. What is an advantage of adding this dataflow to your pipeline before other activities?

## 1. 🎯 출제 의도 파악 (The Hook)

- **핵심 주제:** 데이터 파이프라인의 **작업 순서(Dependency)**와 **전처리(Preprocessing)**의 중요성입니다.
    
- 왜 더러운 데이터를 먼저 씻고 나서 요리를 해야 하는지 묻습니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: It allows for data transformations to be completed before executing scripts or stored procedures.**
    
- **논리적 흐름:**
    
    1. 데이터 엔지니어링의 기본 원칙: **Garbage In, Garbage Out.**
        
    2. 분석 스크립트나 저장 프로시저(Stored Procedure)를 실행하기 전에, Dataflow로 결측치 제거, 타입 변환 등 **전처리(Transformation)**를 먼저 끝내야 합니다.
        
    3. 깨끗한 데이터가 준비된 상태(Success)에서 후속 작업을 진행해야 에러를 방지할 수 있습니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **It ensures the dataflow is executed faster...:** 순서가 빠르다고 속도가 빨라지는 건 아닙니다.
    
- **It reduces the need for data validation in downstream...:** 일부 줄여주긴 하지만, 검증 로직 자체를 없애는 건 위험합니다. 가장 정확한 답은 '작업 완료 보장'입니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **설계 원칙:** 파이프라인 디자인 패턴 중 **"Ingest -> Clean -> Transform -> Serve"** 순서를 항상 기억하세요. Dataflow는 Clean/Transform 단계의 핵심입니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **청소(Dataflow)가 끝나야 파티(Script/Proc)를 시작할 수 있습니다. 선후 관계를 명확히 하세요.**
    

---

### 5. To support Power BI reporting, your company needs to transform data closer to the source. Why would Dataflows Gen2 be an ideal solution in this scenario?

## 1. 🎯 출제 의도 파악 (The Hook)

- **핵심 주제:** BI 성능 최적화의 황금률인 **Roche's Maxim** (데이터 변환은 가능한 상류에서 수행하라)을 묻습니다.
    
- Power BI(Desktop)에서 무거운 작업을 하지 말라는 뜻입니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: They allow transformations to be performed upstream, improving report performance**
    
- **논리적 흐름:**
    
    1. Power BI 리포트 안(Dataset)에서 복잡한 변환을 하면, 사용자가 리포트를 열 때마다 혹은 새로고침할 때마다 느려집니다.
        
    2. Dataflow Gen2를 사용하여 데이터 소스 쪽(Upstream)에서 미리 변환을 다 해놓고, Power BI는 결과만 가져가게 하면 리포트가 매우 가벼워집니다.
        
    3. 이를 **"Shift Left"** (데이터 파이프라인의 왼쪽/앞단으로 로직 이동) 전략이라고 합니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **They provide a manual interface...:** 수동 인터페이스 제공이 목적이 아닙니다.
    
- **They replace the need for a data warehouse:** 2번 문제와 동일한 오답 패턴입니다. 창고를 대체하진 않습니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **성능 튜닝:** "Power BI가 너무 느려요"라는 민원의 90%는 Power Query에서 무거운 작업을 직접 하고 있기 때문입니다. 그 로직을 떼서 **Dataflow Gen2**로 옮기세요. 해결됩니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **변환은 미리미리(Upstream), 리포트는 가볍게! 이것이 BI 성능 최적화의 핵심입니다.**
    

---

### 6. How do Dataflows Gen2 simplify data integration compared to traditional data pipelines?

## 1. 🎯 출제 의도 파악 (The Hook)

- **핵심 주제:** Dataflow Gen2의 정체성인 **"Low-code / Visual Interface"**의 장점을 묻습니다.
    
- 코딩(Python/SQL)과 비교했을 때의 편의성입니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: By providing a low-code interface that ingests data from various sources.**
    
- **논리적 흐름:**
    
    1. 전통적인 파이프라인은 연결 정보를 JSON으로 짜거나 복잡한 코딩이 필요했습니다.
        
    2. Dataflow Gen2(Power Query)는 **드래그 앤 드롭**, **클릭**만으로 수백 개의 데이터 소스(SAP, Salesforce, Excel, SQL 등)에 연결하고 데이터를 가져옵니다.
        
    3. 이것이 통합(Integration)을 단순화하는 핵심 요소입니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **By automatically generating machine learning models...:** ML 모델 자동 생성은 Dataflow의 주 기능이 아닙니다 (AutoML 등이 따로 있습니다).
    
- **By supporting row-level security...:** RLS는 주로 데이터 웨어하우스나 Power BI Semantic Model 단계에서 적용합니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **현업 조언:** 코딩을 못하는 현업 분석가에게 데이터를 쥐어줄 때 "Dataflow 쓰세요"라고 하면 정말 좋아합니다. 엑셀이랑 비슷하거든요.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **복잡한 코딩 없이 클릭만으로 다양한 소스를 연결하는 'Low-code'의 마법입니다.**
    

---

### 7. Your organization wants to expose data to a large group of data analysts without making the data source complexity apparent. How can Dataflows Gen2 assist in this situation?

## 1. 🎯 출제 의도 파악 (The Hook)

- **핵심 주제:** 데이터 **추상화(Abstraction)** 계층으로서의 Dataflow 역할입니다.
    
- 분석가들에게 "복잡한 건 내가 할게, 너흰 깨끗한 것만 가져가"라고 하는 상황입니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: By simplifying data source complexity and exposing only the dataflows to the analysts.**
    
- **논리적 흐름:**
    
    1. 원천 시스템(ERP, CRM)은 테이블 이름도 암호 같고(T001, KNA1 등), 조인 로직도 복잡합니다.
        
    2. 엔지니어가 Dataflow Gen2로 이를 깔끔하게 정리하고 컬럼명도 한글/영문으로 예쁘게 바꿉니다.
        
    3. 분석가들은 원천 시스템 대신 이 **Dataflow**에만 연결하면 되므로, 복잡성을 몰라도 업무가 가능합니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **By automatically updating data models...:** AI가 모델을 업데이트해주는 기능이 아닙니다.
    
- **By implementing row-level security...:** 보안이 아니라 '복잡성 은폐'가 질문의 요지입니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **비유:** 식당 손님(분석가)에게 주방의 난장판(복잡한 소스)을 보여주지 마세요. 깔끔하게 플레이팅 된 요리(Dataflow 결과물)만 서빙하세요.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **Dataflow는 복잡한 데이터 소스를 가려주는 훌륭한 '가림막(Abstraction Layer)'입니다.**
    

---

### 8. What is an essential step when configuring a Dataflow Gen2 to ensure it can be reused for different data sources?

## 1. 🎯 출제 의도 파악 (The Hook)

- **핵심 주제:** **매개변수화(Parameterization)**입니다.
    
- 개발 서버(Dev)용 Dataflow와 운영 서버(Prod)용 Dataflow를 따로 만들지 않으려면 어떻게 해야 할까요?
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: Parameterizing the data source connections.**
    
- **논리적 흐름:**
    
    1. 데이터 소스 경로(URL, 서버 주소 등)를 하드코딩(고정값 입력)하면 재사용이 불가능합니다.
        
    2. 이를 **매개변수(Parameter)**로 설정해두면, 나중에 파라미터 값만 'Server_A'에서 'Server_B'로 바꾸면 로직 변경 없이 다른 소스에 붙을 수 있습니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **Hardcoding the data source credentials:** 하드코딩은 유지보수의 적입니다. 절대 금지!
    
- **Setting a static data destination:** 목적지를 고정하는 것은 소스 재사용성과는 관련이 적습니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **필수 스킬:** Power Query에서 `Manage Parameters` 기능은 무조건 마스터하세요. Dev/Test/Prod 환경 이관 시 이거 없으면 야근 확정입니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **환경이 바뀔 때마다 코드를 고치기 싫다면, 접속 정보는 반드시 '매개변수'로 빼두세요.**
    

---

### 9. Which component is often overlooked but is essential for automating data refresh in a Dataflow Gen2?

## 1. 🎯 출제 의도 파악 (The Hook)

- **핵심 주제:** Dataflow의 **실행 주체(Orchestrator)**를 찾는 문제입니다.
    
- Dataflow를 만들어만 놓고 "왜 안 돌아가지?" 하는 초보자의 실수를 짚어냅니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: Scheduling the dataflow in a pipeline.**
    
- **논리적 흐름:**
    
    1. Dataflow Gen2는 만들고 저장(Publish)한다고 해서 스스로 매일 돌지 않습니다.
        
    2. 반드시 **Pipeline**에 포함시켜 스케줄을 걸거나, 설정에서 **Refresh Schedule**을 켜야 합니다.
        
    3. 엔터프라이즈 환경에서는 의존성 관리를 위해 주로 **Pipeline**을 사용합니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **Applying data masking...:** 보안 기능이지 자동화 기능이 아닙니다.
    
- **Integrating... with Power BI Desktop:** 데스크탑은 수동 도구입니다. 자동화는 클라우드 서비스(Service/Fabric) 레벨에서 일어납니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **체크리스트:** Dataflow 만들고 나서 끝? 아니죠. "누가(Pipeline/Schedule), 언제(Time)" 실행할지 설정했는지 꼭 확인하세요.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **자동차(Dataflow)를 샀으면 운전자(Pipeline Scheduler)를 고용해야 굴러갑니다.**