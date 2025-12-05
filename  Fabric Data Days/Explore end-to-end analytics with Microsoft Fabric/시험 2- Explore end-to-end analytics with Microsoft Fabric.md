이번 문제는 Microsoft Fabric의 **핵심 철학(통합성)**과 **기술적 기반(스토리지 포맷, ETL 도구)**을 묻는 아주 기본적인 개념 확인 문제입니다.

DP-700 시험 초반부에 반드시 등장하는 기초 점수 확보용 문제들이니, 명확하게 개념을 잡고 넘어가겠습니다.

---

### 1. 데이터 프로젝트에서 Microsoft Fabric을 사용하는 주요 이점은 무엇입니까?

## 1. 🎯 출제 의도 파악 (The Hook)

- 이 문제는 Microsoft Fabric이 기존의 Azure Synapse, Data Factory, Power BI 등을 개별로 조합해 쓰던 방식과 다른 **"SaaS형 통합 플랫폼"**이라는 정체성을 이해하고 있는지 묻습니다.
    
- 키워드는 **"통합(Unified)"**과 **"단일 환경(Single Environment)"**입니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: 데이터 프로젝트에 대한 협업을 위한 단일하고 통합된 환경을 제공합니다.**
    
- **논리적 흐름:**
    
    1. 과거에는 데이터 엔지니어(ETL), 데이터 과학자(ML), 비즈니스 분석가(BI)가 서로 다른 도구와 저장소를 사용했습니다(Silo 현상).
        
    2. Microsoft Fabric은 이 모든 워크로드를 하나의 SaaS 포털, 하나의 스토리지(**OneLake**) 위에서 통합했습니다.
        
    3. 따라서 데이터 복제 없이, 모든 직군이 **하나의 환경**에서 실시간으로 협업할 수 있는 것이 가장 큰 이점입니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **데이터 전문가는 협업 없이 독립적으로 작업할 수 있습니다:** Fabric의 철학인 '협업'과 정반대입니다. 사일로(Silo)를 만드는 것은 구형 방식입니다.
    
- **가용성을 보장하려면 시스템 전체에서 데이터를 복제해야 합니다:** Fabric의 **OneLake**는 "One Copy"를 지향합니다. 데이터를 복제하지 않고 **Shortcut**을 통해 원본을 그대로 참조하는 것이 핵심 기술입니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **현업 관점:** 통합 환경의 진짜 장점은 **"권한 관리의 단순화"**입니다. 예전에는 DB 권한 따로, Data Lake 권한 따로, Power BI 권한 따로 줬어야 했는데, 이제는 **Workspace** 단위로 멤버를 초대하면 끝입니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **Fabric은 엔지니어, 과학자, 분석가가 데이터를 복제하지 않고 한곳에서 일하는 'All-in-One' 플랫폼입니다.**
    

---

### 2. Fabric의 OneLake의 기본 저장 형식은 무엇입니까?

## 1. 🎯 출제 의도 파악 (The Hook)

- 이 문제는 Fabric의 성능과 호환성을 책임지는 **오픈 소스 표준 포맷**이 무엇인지 묻습니다.
    
- 단순히 파일 형식이 아니라, 트랜잭션(ACID)을 지원하는 **레이크 포맷**을 찾아야 합니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: 델타-파켓 (Delta-Parquet)**
    
- **논리적 흐름:**
    
    1. **Parquet**: 데이터를 열(Column) 기반으로 압축하여 저장하는 고성능 파일 포맷입니다.
        
    2. **Delta Lake**: Parquet 파일들에 트랜잭션 로그(Log)를 더해 ACID(데이터 무결성)와 시간 여행(Time Travel) 기능을 제공하는 기술입니다.
        
    3. Fabric의 모든 엔진(SQL, Spark, KQL 등)은 내부적으로 데이터를 저장할 때 이 **Delta-Parquet** 형식을 표준으로 사용합니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **JSON / CSV:** 데이터를 수집(Ingest)할 때 흔히 쓰이는 소스 형식이지만, 저장 효율과 검색 속도가 떨어져 분석용 내부 저장 포맷으로는 적합하지 않습니다. (예: 인덱싱 불가, 압축 효율 낮음)
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **성능 Tip:** Fabric은 일반적인 Delta-Parquet보다 더 최적화된 **V-Order**라는 기술을 기본적으로 적용합니다. 쓰기(Write) 속도는 약간 느려질 수 있어도, 읽기(Read) 속도는 비약적으로 빨라지니 끄지 말고 그대로 두세요.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **Fabric의 심장은 'Delta Lake'이며, 데이터의 몸체는 'Parquet'입니다. (Delta Log + Parquet Data)**
    

---

### 3. 데이터를 이동하고 변환하는 데 어떤 Fabric 경험이 사용됩니까?

## 1. 🎯 출제 의도 파악 (The Hook)

- Microsoft Fabric 내의 여러 "경험(Experience)" 즉, 워크로드(Workload)의 역할을 구분할 수 있는지 묻습니다.
    
- 키워드는 **"이동(Move)"**과 **"변환(Transform)"** = **ETL**입니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: 데이터 팩토리 (Data Factory)**
    
- **논리적 흐름:**
    
    1. **Data Factory**는 Azure의 대표적인 ETL 서비스입니다.
        
    2. Fabric 내에서도 **Data Pipeline**(오케스트레이션 및 대량 이동)과 **Dataflow Gen2**(시각적 데이터 변환) 기능을 포함하는 경험(Experience)을 **Data Factory**라고 부릅니다.
        
    3. 데이터를 A에서 B로 옮기거나, 포맷을 바꾸는 작업의 주체입니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **데이터 과학 (Data Science):** 데이터를 탐색하고 ML 모델을 만드는 곳입니다(Notebook, Experiment).
    
- **데이터 웨어하우징 (Data Warehousing):** 정제된 데이터를 저장하고 SQL로 서빙(Serving)하는 곳입니다. 물론 Stored Procedure로 변환할 수 있지만, "이동(Move)"의 주 도구는 아닙니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **도구 선택 가이드:** 대용량 데이터를 단순히 복사(Copy)할 때는 **Pipeline**의 Copy Activity가 가장 빠르고 저렴합니다. 하지만 비즈니스 로직을 넣어 복잡하게 데이터를 볶아야 한다면 **Dataflow Gen2**나 **Notebook**을 호출하세요.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **데이터를 '옮기고(Copy)' '고치는(Transform)' ETL 작업의 본부는 무조건 Data Factory입니다.**

- 1분

데이터 전문가는 점점 더 대규모 데이터를 안전하게 처리하고, 규정을 준수하며, 비용 효율적인 방식으로 작업할 수 있어야 한다는 기대를 받고 있습니다. 동시에 기업은 데이터를 더욱 효과적이고 신속하게 활용하여 더 나은 의사 결정을 내리기를 원합니다.

Microsoft Fabric은 조직이 바로 이러한 목표를 달성할 수 있도록 지원하는 도구와 서비스 모음입니다. 이 모듈에서는 Fabric의 OneLake 스토리지, Fabric에 포함된 워크로드, 조직에서 Fabric을 활성화하고 사용하는 방법, 그리고 Copilot이 지능형 AI 지원을 통해 모든 Fabric 워크로드의 생산성을 향상시키는 방법에 대해 알아보았습니다.