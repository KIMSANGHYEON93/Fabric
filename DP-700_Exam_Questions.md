# DP-700 실전 문제 모음 (DP-700 Practice Questions Collection)

이 문서는 Microsoft Fabric DP-700 시험 대비를 위한 실전 문제와 해설을 모아놓은 자료입니다. 각 섹션은 특정 모듈의 평가 문제(Module Assessment) 또는 실전 모의고사(Exam) 내용을 포함하고 있습니다.

## 목차 (Table of Contents)

1. [Fabric 레이크하우스 시작하기 (Lakehouse)](#1-fabric-레이크하우스-시작하기-lakehouse)
2. [End-to-End 분석 탐색 (End-to-End Analytics)](#2-end-to-end-분석-탐색-end-to-end-analytics)
3. [Apache Spark 사용하기 (Apache Spark)](#3-apache-spark-사용하기-apache-spark)
4. [CI/CD 및 배포 파이프라인 (CI/CD & Deployment Pipelines)](#4-cicd-및-배포-파이프라인-cicd--deployment-pipelines)
5. [Eventstream 사용 (Real-Time Intelligence)](#5-eventstream-사용-real-time-intelligence)
6. [활동 모니터링 (Monitoring Activities)](#6-활동-모니터링-monitoring-activities)
7. [Dataflows Gen2 데이터 수집 (Data Integration)](#7-dataflows-gen2-데이터-수집-data-integration)
8. [프로세스 및 데이터 이동 오케스트레이션 (Orchestration)](#8-프로세스-및-데이터-이동-오케스트레이션-orchestration)

---

## 1. Fabric 레이크하우스 시작하기 (Lakehouse)
*(Source: Fabric Data Days Microsoft Fabric에서 레이크하우스 시작하기)*

**1. 귀사에서는 Microsoft Fabric 레이크하우스의 데이터를 사용하여 머신 러닝 모델을 학습할 계획입니다. 이 작업에 가장 적합한 도구는 무엇인가요?**

- **정답: 노트북 (Notebook)**
- **논리:** 머신러닝(ML)은 주로 Python, R, Scala 라이브러리(Scikit-learn, PyTorch 등)를 사용합니다. Fabric에서 **Spark 컴퓨팅**을 활용해 코드를 작성하고 ML 모델을 학습시키는 최적의 장소는 **Notebook**입니다.

**2. Dataflows Gen2는 Microsoft Fabric Lakehouse 내에서 ETL 프로세스를 어떻게 지원합니까?**

- **정답: Power Query를 사용하여 변환의 시각적 표현을 제공합니다.**
- **논리:** Dataflow Gen2는 **Power Query Online**을 기반으로 합니다. 코드를 작성하지 않고(Low-code), 엑셀처럼 시각적인 UI에서 데이터를 변환/가공하는 것이 주 목적입니다.

**3. 어떤 Microsoft Fabric 구성 요소를 사용하면 외부 데이터를 원래 위치에 저장한 채로 레이크하우스에 통합할 수 있습니까?**

- **정답: 단축키 (Shortcuts)**
- **논리:** Fabric의 가장 강력한 기능 중 하나입니다. AWS S3나 Azure ADLS Gen2에 있는 데이터를 OneLake로 복사(Copy)하지 않고, **논리적인 링크**만 걸어 사용하는 기능은 **Shortcut(단축키)**입니다.

**4. Microsoft Fabric 레이크하우스와 관련하여 Data Factory 파이프라인을 사용하는 주요 목적은 무엇입니까?**

- **정답: ETL 프로세스를 조율하고 자동화하려면**
- **논리:** 파이프라인(Pipeline)은 직접 데이터를 변환하기보다는, Notebook, Dataflow, Stored Procedure 등 여러 작업을 순서대로 실행하고 **오케스트레이션(조율/스케줄링)** 하는 도구입니다.

**5. Microsoft Fabric 레이크하우스에서 데이터를 변환할 때 데이터 불일치 문제가 발생합니다. Delta Lake 포맷 테이블의 어떤 기능이 데이터 무결성과 일관성을 보장하는 데 도움이 될까요?**

- **정답: ACID 거래 (ACID Transactions)**
- **논리:** Delta Lake가 Parquet 파일과 차별화되는 점은 데이터베이스처럼 **트랜잭션 로그(Delta Log)**를 남겨, 작업 도중 실패하더라도 데이터가 깨지지 않게 하는 **ACID(원자성, 일관성, 고립성, 지속성)**를 보장한다는 점입니다.

**6. Microsoft Fabric 레이크하우스는 데이터 처리 기능 측면에서 일반적인 데이터 레이크와 어떻게 다릅니까?**

- **정답: 레이크하우스는 고급 데이터 처리를 위해 SQL과 Spark 엔진을 통합합니다.**
- **논리:** 일반적인 '데이터 레이크'는 저장소일 뿐입니다. '레이크하우스'는 저장소 위에 **SQL Endpoint(T-SQL)**와 **Spark Runtime**이라는 컴퓨팅 엔진이 결합되어 분석이 가능한 형태를 말합니다.

**7. Microsoft Fabric 레이크하우스의 스키마-온-리드가 기존 데이터 웨어하우스의 사전 정의된 스키마와 비교했을 때 갖는 주요 이점은 무엇입니까?**

- **정답: 스키마 온 리드(Schema-on-read)를 사용하면 보다 유연한 데이터 수집 및 변환이 가능합니다.**
- **논리:** 데이터 웨어하우스는 테이블 구조(Schema)를 미리 만들어야 데이터를 넣을 수 있습니다(Schema-on-write). 반면 레이크하우스는 일단 파일을 던져 넣고, **읽을 때 구조를 정의**하므로 훨씬 **유연(Flexible)**합니다.

**8. 귀사에서는 구조화된 거래 데이터와 소셜 미디어 피드를 결합하여 분석하고자 합니다. Microsoft Fabric 레이크하우스가 기존 데이터 웨어하우스보다 더 적합한 이유는 무엇일까요?**

- **정답: 레이크하우스는 모든 데이터 형식을 저장하고 SQL 기반 분석을 지원할 수 있습니다.**
- **논리:** 소셜 미디어 피드(JSON, 텍스트 등 비정형 데이터)는 기존 데이터 웨어하우스(DW)에 넣기 어렵습니다. 레이크하우스는 정형(거래) 및 비정형(소셜) 데이터를 모두 수용하며 SQL 분석까지 지원합니다.

**9. Microsoft Fabric 레이크하우스의 시각적 인터페이스를 사용하여 구조화된 데이터를 수집하고 변환하는 데 어떤 도구를 사용해야 합니까?**

- **정답: 데이터 흐름 Gen2 (Dataflow Gen2)**
- **논리:** 키워드는 **"시각적 인터페이스(Visual Interface)"**입니다. 코드를 짜지 않고 클릭으로 처리하는 도구는 Dataflow Gen2입니다. (Notebook은 코드 기반입니다.)

---

## 2. End-to-End 분석 탐색 (End-to-End Analytics)
*(Source: Explore end-to-end analytics with Microsoft Fabric)*

**1. 데이터 프로젝트에서 Microsoft Fabric을 사용하는 주요 이점은 무엇입니까?**

- **정답: 데이터 프로젝트에 대한 협업을 위한 단일하고 통합된 환경을 제공합니다.**
- **논리:** 과거의 Silo 현상을 극복하고, **OneLake** 위에서 모든 워크로드(DE, DS, BI)를 통합하여 데이터 복제 없이 실시간 협업이 가능합니다.

**2. Fabric의 OneLake의 기본 저장 형식은 무엇입니까?**

- **정답: 델타-파켓 (Delta-Parquet)**
- **논리:** Fabric의 모든 엔진은 **Delta Lake** (Parquet 파일 + 트랜잭션 로그) 포맷을 표준으로 사용합니다.

**3. 데이터를 이동하고 변환하는 데 어떤 Fabric 경험이 사용됩니까?**

- **정답: 데이터 팩토리 (Data Factory)**
- **논리:** 데이터를 옮기고(Pipeline) 변환하는(Dataflow Gen2) 경험의 집합체는 **Data Factory**입니다.

---

## 3. Apache Spark 사용하기 (Apache Spark)
*(Source: Use Apache Spark in Microsoft Fabric)*

**1. Your organization needs to analyze customer data stored in a lakehouse and visualize demographic distributions using Spark in Microsoft Fabric. Which Spark feature would facilitate this analysis?**

- **정답: Dataframe API for structured data manipulation and Spark SQL for querying.**
- **논리:** 구조화된 데이터 분석에는 **DataFrame**과 **Spark SQL**이 최적입니다. RDD는 구형 방식입니다.

**2. What is the expected result of executing the following PySpark command: `df.groupBy('Category').agg({'SalesAmount': 'sum'})`?**

- **정답: A new dataframe with each category and the sum of sales amounts for each category.**
- **논리:** Spark 연산의 결과는 항상 **DataFrame**입니다. (List나 Scalar가 아님)

**3. When creating a custom environment in Microsoft Fabric, which setting allows you to use a specific version of Apache Spark for your tasks?**

- **정답: Specify the Spark runtime in the environment settings.**
- **논리:** Spark 버전 관리는 **Runtime(런타임)** 설정에서 수행합니다.

**4. You have created a dataframe from a CSV file and want to save it as a Delta table in the Spark catalog for future SQL queries. Which method should you use?**

- **정답: `df.write.format("delta").saveAsTable("table_name")`**
- **논리:** **saveAsTable**을 써야 카탈로그(Metastore)에 등록되어 SQL로 조회 가능합니다.

**5. Which SQL magic command should you use in a Microsoft Fabric notebook to execute SQL queries directly?**

- **정답: `%%sql`**
- **논리:** Notebook 셀에서 SQL을 쓰려면 **%%sql** 매직 커맨드를 사용합니다.

**6. In Microsoft Fabric, what is the purpose of setting a default Spark pool in a workspace?**

- **정답: To automatically assign a Spark pool to jobs when no specific pool is specified.**
- **논리:** 별도 지정이 없을 때 사용할 **기본(Default) 컴퓨팅 자원**을 설정하는 것입니다.

**7. Which Spark Dataframe method is most efficient for finding the maximum value in a column of numerical data?**

- **정답: `agg`**
- **논리:** 최대, 최소, 평균 등 집계 연산은 **agg** 메서드를 사용합니다.

**8. Which practice should be followed to optimize data processing performance in a Spark pool using the native execution engine in Microsoft Fabric?**

- **정답: Enable the native execution engine at the environment level by setting relevant Spark properties.**
- **논리:** Fabric의 고성능 엔진(Native Execution Engine)을 쓰려면 환경 설정에서 활성화해야 합니다.

**9. You have a dataframe with a column named 'Date' in a string format, and you need to convert it to a date format for further analysis. Which PySpark method would you use?**

- **정답: `withColumn`**
- **논리:** 컬럼의 타입이나 값을 변경할 때는 **withColumn**을 사용합니다.

---

## 4. CI/CD 및 배포 파이프라인 (CI/CD & Deployment Pipelines)
*(Source: Microsoft Fabric에서 CICD지속적 통합 및 지속적 배포 구현)*

**1. Fabric의 CI/CD 프로세스에서 Git의 역할은 무엇입니까?**

- **정답: Git을 사용하면 팀이 브랜치를 사용하여 협업하고 버전 관리 기능을 활용할 수 있습니다. 증분 코드 변경 사항을 관리하고 코드 이력을 확인하는 데 도움이 됩니다.**
- **논리:** Git은 배포 도구가 아니라 **소스 코드 저장 및 버전 관리(History)** 도구입니다.

**2. Fabric 작업 공간을 Git 저장소에 연결하는 목적은 무엇입니까?**

- **정답: 작업 공간과 Git 간의 콘텐츠를 동기화하여 동일한 콘텐츠를 보유하도록 합니다.**
- **논리:** 웹(Workspace)과 코드(Git) 상태를 일치시키는 **동기화(Sync)**가 주 목적입니다.

**3. Fabric에서 배포 파이프라인의 주요 기능은 무엇입니까?**

- **정답: 배포 파이프라인은 개발, 테스트, 프로덕션 단계를 거쳐 콘텐츠가 이동하는 과정을 자동화합니다.**
- **논리:** 환경 간(Dev -> Test -> Prod)의 **콘텐츠 이동(Release)**을 담당합니다.

---

## 5. Eventstream 사용 (Real-Time Intelligence)
*(Source: Microsoft Fabric에서 Eventstream 사용)*

**1. What advantage does the 'Derived stream' destination offer in an eventstream setup?**

- **정답: It enables content-based routing to multiple destinations based on data content.**
- **논리:** 파생 스트림은 데이터를 필터링/변환하여 조건에 따라 다른 곳으로 보내는 **라우팅** 역할을 합니다.

**2. Your organization needs to integrate real-time event data with an external system for custom processing. Which eventstream destination should be configured?**

- **정답: Custom endpoint**
- **논리:** Fabric 외부 시스템으로 보내려면 **Custom Endpoint**를 사용합니다.

**3. When configuring an eventstream pipeline, you need to ensure that real-time data from Azure IoT Hub is transformed into a standardized format for downstream compatibility. Which transformation should you use to achieve this?**

- **정답: Manage fields transformation to change data types and rename fields**
- **논리:** 필드 이름 변경, 타입 변경은 **Manage fields**가 담당합니다.

**4. You are troubleshooting an eventstream pipeline where data from Azure Service Bus is being transformed but not reaching the intended destination. What could be the most likely cause of this issue?**

- **정답: Misconfigured destination settings in the eventstream canvas**
- **논리:** 변환까지 성공했다면 남은 원인은 **도착지(Destination)** 설정 오류입니다.

**5. When routing real-time event data to trigger specific actions based on detected patterns, which destination is most appropriate?**

- **정답: Fabric Activator**
- **논리:** 패턴 감지 후 **행동(Action)**을 취하는 것은 **Activator**입니다.

**6. Which transformation should be used to filter out invalid data in an eventstream pipeline?**

- **정답: Filter**
- **논리:** 불필요한 데이터를 버리는 것은 **Filter**입니다.

**7. While setting up an eventstream pipeline, you realize that data is being ingested and stored, but it needs enrichment with additional fields for clarity. Which transformation should you use to add calculated fields to the data?**

- **정답: Manage fields transformation**
- **논리:** 새로운 계산 필드를 추가하는 것도 **Manage fields**입니다.

**8. Your organization needs to standardize the format of incoming data from multiple sources before combining them into a single stream. Which transformation should be used to ensure consistent data structure?**

- **정답: Manage fields transformation**
- **논리:** 서로 다른 소스의 스키마(구조)를 일치시키는 작업도 **Manage fields**입니다.

**9. Which transformation would be most suitable for ensuring that incoming data streams have consistent naming conventions before being routed to their destination?**

- **정답: Manage fields transformation**
- **논리:** 명명 규칙(Naming Convention)을 맞추는(Rename) 작업도 **Manage fields**입니다.

---

## 6. 활동 모니터링 (Monitoring Activities)
*(Source: Microsoft Fabric에서 활동 모니터링)*

**1. Microsoft Fabric에서 Monitor 허브의 주요 기능은 무엇입니까?**

- **정답: 선택된 Fabric 품목과 프로세스에서 데이터를 수집하고 집계하여 다양한 활동을 모니터링하기 위한 공통 인터페이스를 제공합니다.**
- **논리:** 모든 아이템의 실행 상태를 한곳에서 보여주는 **중앙 관제소**입니다.

**2. Microsoft Fabric에서 Activator의 주요 기능은 무엇입니까?**

- **정답: Activator는 작업을 트리거하는 이벤트의 자동 처리를 가능하게 합니다.**
- **논리:** 데이터 이벤트를 감지하여 **자동으로 작업(Trigger Action)을 수행**합니다.

**3. 모범 사례를 모니터링하는 데 있어 중요한 측면은 무엇입니까?**

- **정답: 모니터링할 항목을 식별하고, 정기적으로 데이터를 수집하고 분석하고, 로그와 지표를 정기적으로 검토하고, 편차가 발생하면 조치를 취하고, 모니터링 데이터를 사용하여 성능을 최적화합니다.**
- **논리:** 사후 대응(Reactive)이 아닌, **사전 예방(Proactive) 및 최적화**가 핵심입니다.

---

## 7. Dataflows Gen2 데이터 수집 (Data Integration)
*(Source: Microsoft Fabric의 Dataflows Gen2를 사용하여 데이터 수집)*

**1. Your organization wants to reduce data preparation time by reusing data transformations across multiple projects. How can Dataflows Gen2 facilitate this requirement?**

- **정답: By creating reusable dataflows that apply consistent transformations.**
- **논리:** Dataflow는 다른 Dataflow에서 **참조(Reference)**하여 로직을 재사용할 수 있습니다.

**2. Which of the following is a limitation of using Dataflows Gen2 in Microsoft Fabric?**

- **정답: They are not a replacement for a data warehouse.**
- **논리:** Dataflow는 ETL 도구이지, 영구적 저장소인 **Data Warehouse**를 대체하지 않습니다.

**3. When incorporating a Dataflow Gen2 into a pipeline, what step ensures the dataflow runs automatically without manual intervention?**

- **정답: Configuring a trigger to schedule automatic execution**
- **논리:** 자동화를 위해서는 파이프라인에 **스케줄 트리거**를 설정해야 합니다.

**4. In your data pipeline, you have included a Dataflow Gen2 for transforming raw sales data. What is an advantage of adding this dataflow to your pipeline before other activities?**

- **정답: It allows for data transformations to be completed before executing scripts or stored procedures.**
- **논리:** 후속 작업(Script) 전에 **데이터 정제(Transformation)를 완료**하여 에러를 방지합니다.

**5. To support Power BI reporting, your company needs to transform data closer to the source. Why would Dataflows Gen2 be an ideal solution in this scenario?**

- **정답: They allow transformations to be performed upstream, improving report performance**
- **논리:** 상류(Upstream)에서 미리 변환해두면 리포트 성능이 향상됩니다 (**Shift Left** 전략).

**6. How do Dataflows Gen2 simplify data integration compared to traditional data pipelines?**

- **정답: By providing a low-code interface that ingests data from various sources.**
- **논리:** **Low-code/No-code** 인터페이스로 복잡한 코딩 없이 다양한 소스를 연결합니다.

**7. Your organization wants to expose data to a large group of data analysts without making the data source complexity apparent. How can Dataflows Gen2 assist in this situation?**

- **정답: By simplifying data source complexity and exposing only the dataflows to the analysts.**
- **논리:** 복잡한 원천 소스를 감추고(Abstraction), 정제된 Dataflow만 제공하여 분석가들을 돕습니다.

**8. What is an essential step when configuring a Dataflow Gen2 to ensure it can be reused for different data sources?**

- **정답: Parameterizing the data source connections.**
- **논리:** 접속 정보를 **매개변수(Parameter)**로 설정해야 환경 변경 시 재사용 가능합니다.

**9. Which component is often overlooked but is essential for automating data refresh in a Dataflow Gen2?**

- **정답: Scheduling the dataflow in a pipeline.**
- **논리:** Dataflow는 스스로 돌지 않습니다. **Pipeline 스케줄러**가 필요합니다.

---

## 8. 프로세스 및 데이터 이동 오케스트레이션 (Orchestration)
*(Source: Orchestrate processes and data movement with Microsoft Fabric)*

**1. 데이터 파이프라인이란 무엇인가요?**

- **정답: 데이터 수집 또는 변환 프로세스를 조율하기 위한 일련의 활동 (A sequence of activities to orchestrate data ingestion or transformation processes)**
- **논리:** 파이프라인은 작업을 **조율(Orchestrate)**하는 관리자입니다.

**2. 파이프라인을 사용하여 각 실행마다 지정된 이름의 폴더에 데이터를 복사하려고 합니다. 어떻게 해야 할까요?**

- **정답: 파이프라인에 매개변수를 추가하고 이를 사용하여 각 실행에 대한 폴더 이름을 지정합니다.**
- **논리:** **매개변수(Parameter)**를 사용하여 동적으로 경로를 설정합니다.

**3. 이전에 여러 활동이 포함된 파이프라인을 실행한 적이 있습니다. 각 활동을 완료하는 데 걸린 시간을 확인하는 가장 좋은 방법은 무엇인가요?**

- **정답: 실행 기록에서 실행 세부 정보를 확인하세요.**
- **논리:** **실행 기록(Run History)**에서 각 활동의 소요 시간과 상태를 확인할 수 있습니다.

---

## 9. Web Scraped Exam Questions (ExamTopics)
*(Source: https://www.examtopics.com/exams/microsoft/dp-700/view/ - Partial Scrape due to access limits)*

**Question #1 Topic 1**
Contoso, Ltd. is an online retail company that wants to modernize its analytics platform by moving to Fabric... (Case Study context omitted for brevity)...
You need to ensure that the data analysts can access the gold layer lakehouse. What should you do?

A. Add the DataAnalyst group to the Viewer role for WorkspaceA.
B. Share the lakehouse with the DataAnalysts group and grant the Build reports on the default semantic model permission.
C. Share the lakehouse with the DataAnalysts group and grant the Read all SQL Endpoint data permission.
D. Share the lakehouse with the DataAnalysts group and grant the Read all Apache Spark permission.

**Correct Answer:** C
**Community vote distribution:** C (100%), C (25%), B (20%)

**Question #2 Topic 1**
You have a Fabric workspace. You have semi-structured data. You need to read the data by using T-SQL, KQL, and Apache Spark. The data will only be written by using Spark. What should you use to store the data?

A. a lakehouse
B. an eventhouse
C. a datamart
D. a warehouse

**Correct Answer:** A
**Community vote distribution:** A (50%), B (50%), B (20%)

**Question #3 Topic 1**
You have a Fabric workspace that contains a warehouse named Warehouse1. You have an on-premises Microsoft SQL Server database named Database1 that is accessed by using an on-premises data gateway. You need to copy data from Database1 to Warehouse1. Which item should you use?

A. a Dataflow Gen1 dataflow
B. a data pipeline
C. a KQL queryset
D. a notebook

**Correct Answer:** B
**Community vote distribution:** B (100%), C (25%), B (20%)

**Correct Answer:** B
**Community vote distribution:** B (100%), C (25%), B (20%)

**Question #5 Topic 1**
You have a Fabric F32 capacity that contains a workspace. The workspace contains a warehouse named DW1 that is modelled by using MD5 hash surrogate keys. DW1 contains a single fact table that has grown from 200 million rows to 500 million rows during the past year. You have Microsoft Power BI reports that are based on Direct Lake. The reports show year-over-year values. Users report that the performance of some of the reports has degraded over time and some visuals show errors. You need to resolve the performance issues. The solution must meet the following requirements: Provide the best query performance. Minimize operational costs. Which should you do?

A. Change the MD5 hash to SHA256.
B. Increase the capacity.
C. Enable V-Order.
D. Modify the surrogate keys to use a different data type.
E. Create views.

**Correct Answer:** C

**Question #6 Topic 1**
HOTSPOT - You have a Fabric workspace that contains a warehouse named DW1. DW1 contains the following tables and columns. You need to create an output that presents the summarized values of all the order quantities by year and product. The results must include a summary of the order quantities at the year level for all the products. How should you complete the code? To answer, select the appropriate options in the answer area. NOTE: Each correct selection is worth one point.

*(Options not available due to Hotspot format)*

**Correct Answer:** A

**Question #7 Topic 1**
You have a Fabric workspace that contains a lakehouse named Lakehouse1. Data is ingested into Lakehouse1 as one flat table. The table contains the following columns. You plan to load the data into a dimensional model and implement a star schema. From the original flat table, you create two tables named FactSales and DimProduct. You will track changes in DimProduct. You need to prepare the data. Which three columns should you include in the DimProduct table? Each correct answer presents part of the solution. NOTE: Each correct selection is worth one point.

A. Date
B. ProductName
C. ProductColor
D. TransactionID
E. SalesAmount
F. ProductID

**Correct Answer:** BCF

**Question #8 Topic 1**
You have a Fabric workspace named Workspace1 that contains a notebook named Notebook1. In Workspace1, you create a new notebook named Notebook2. You need to ensure that you can attach Notebook2 to the same Apache Spark session as Notebook1. What should you do?

A. Enable high concurrency for notebooks.
B. Enable dynamic allocation for the Spark pool.
C. Change the runtime version.
D. Increase the number of executors.

**Correct Answer:** A

**Question #9 Topic 1**
You have a Fabric workspace named Workspace1 that contains a lakehouse named Lakehouse1. Lakehouse1 contains the following tables: Orders - Customer - Employee - The Employee table contains Personally Identifiable Information (PII). A data engineer is building a workflow that requires writing data to the Customer table, however, the user does NOT have the elevated permissions required to view the contents of the Employee table. You need to ensure that the data engineer can write data to the Customer table without reading data from the Employee table. Which three actions should you perform? Each correct answer presents part of the solution. NOTE: Each correct selection is worth one point.

A. Share Lakehouse1 with the data engineer.
B. Assign the data engineer the Contributor role for Workspace2.
C. Assign the data engineer the Viewer role for Workspace2.
D. Assign the data engineer the Contributor role for Workspace1.
E. Migrate the Employee table from Lakehouse1 to Lakehouse2.
F. Create a new workspace named Workspace2 that contains a new lakehouse named Lakehouse2.
G. Assign the data engineer the Viewer role for Workspace1.

**Correct Answer:** DEF

**Question #10 Topic 1**
You have a Fabric warehouse named DW1. DW1 contains a table that stores sales data and is used by multiple sales representatives. You plan to implement row-level security (RLS). You need to ensure that the sales representatives can see only their respective data. Which warehouse object do you require to implement RLS?

A. STORED PROCEDURE
B. CONSTRAINT
C. SCHEMA
D. FUNCTION

**Correct Answer:** D

**Question #11 Topic 1**
HOTSPOT - You have a Fabric workspace named Workspace1_DEV that contains the following items: 10 reports Four notebooks - Three lakehouses - Two data pipelines - Two Dataflow Gen1 dataflows - Three Dataflow Gen2 dataflows - Five semantic models that each has a scheduled refresh policy You create a deployment pipeline named Pipeline1 to move items from Workspace1_DEV to a new workspace named Workspace1_TEST. You deploy all the items from Workspace1_DEV to Workspace1_TEST. For each of the following statements, select Yes if the statement is true. Otherwise, select No. NOTE: Each correct selection is worth one point.

*(Options not available due to Hotspot format)*

**Correct Answer:** (N/A)

**Question #12 Topic 1**
You have a Fabric deployment pipeline that uses three workspaces named Dev, Test, and Prod. You need to deploy an eventhouse as part of the deployment process. What should you use to add the eventhouse to the deployment process?

A. GitHub Actions
B. a deployment pipeline
C. an Azure DevOps pipeline

**Correct Answer:** B

**Question #13 Topic 1**
You have a Fabric workspace named Workspace1 that contains a warehouse named Warehouse1. You plan to deploy Warehouse1 to a new workspace named Workspace2. As part of the deployment process, you need to verify whether Warehouse1 contains invalid references. The solution must minimize development effort. What should you use?

A. a database project
B. a deployment pipeline
C. a Python script
D. a T-SQL script

**Correct Answer:** B

**Question #14 Topic 1**
You have a Fabric workspace that contains a Real-Time Intelligence solution and an eventhouse. Users report that from OneLake file explorer, they cannot see the data from the eventhouse. You enable OneLake availability for the eventhouse. What will be copied to OneLake?

A. only data added to new databases that are added to the eventhouse
B. only the existing data in the eventhouse
C. no data
D. both new data and existing data in the eventhouse
E. only new data added to the eventhouse

**Correct Answer:** E

**Question #15 Topic 1**
You have a Fabric workspace named Workspace1. You plan to integrate Workspace1 with Azure DevOps. You will use a Fabric deployment pipeline named deployPipeline1 to deploy items from Workspace1 to higher environment workspaces as part of a medallion architecture. You will run deployPipeline1 by using an API call from an Azure DevOps pipeline. You need to configure API authentication between Azure DevOps and Fabric. Which type of authentication should you use?

A. service principal
B. Microsoft Entra username and password
C. managed private endpoint
D. workspace identity

**Correct Answer:** A

**Question #16 Topic 1**
You have a Google Cloud Storage (GCS) container named storage1 that contains the files shown in the following table. You have a Fabric workspace named Workspace1 that has the cache for shortcuts enabled. Workspace1 contains a lakehouse named Lakehouse1. Lakehouse1 has the shortcuts shown in the following table. You need to read data from all the shortcuts. Which shortcuts will retrieve data from the cache?

A. Stores only
B. Products only
C. Stores and Products only
D. Products, Stores, and Trips
E. Trips only
F. Products and Trips only

**Correct Answer:** D

**Question #17 Topic 1**
You have a Fabric workspace named Workspace1 that contains an Apache Spark job definition named Job1. You have an Azure SQL database named Source1 that has public internet access disabled. You need to ensure that Job1 can access the data in Source1. What should you create?

A. an on-premises data gateway
B. a managed private endpoint
C. an integration runtime
D. a data management gateway

**Correct Answer:** B

**Question #18 Topic 1**
You have an Azure Data Lake Storage Gen2 account named storage1 and an Amazon S3 bucket named storage2. You have the Delta Parquet files shown in the following table. You have a Fabric workspace named Workspace1 that has the cache for shortcuts enabled. Workspace1 contains a lakehouse named Lakehouse1. Lakehouse1 has the following shortcuts: A shortcut to ProductFile aliased as Products, A shortcut to StoreFile aliased as Stores, A shortcut to TripsFile aliased as Trips. The data from which shortcuts will be retrieved from the cache?

A. Trips and Stores only
B. Products and Store only
C. Stores only
D. Products only
E. Products, Stores, and Trips

**Correct Answer:** C

**Question #19 Topic 1**
HOTSPOT - You have a Fabric workspace named Workspace1 that contains the items shown in the following table. For Model1, the Keep your Direct Lake data up to date option is disabled. You need to configure the execution of the items to meet the following requirements: Notebook1 must execute every weekday at 8:00 AM. Notebook2 must execute when a file is saved to an Azure Blob Storage container. Model1 must refresh when Notebook1 has executed successfully. How should you orchestrate each item? To answer, select the appropriate options in the answer area. NOTE: Each correct selection is worth one point.

*(Options not available due to Hotspot format)*

**Correct Answer:** (N/A)

**Question #20 Topic 1**
Your company has a sales department that uses two Fabric workspaces named Workspace1 and Workspace2. The company decides to implement a domain strategy to organize the workspaces. You need to ensure that a user can perform the following tasks: Create a new domain for the sales department. Create two subdomains: one for the east region and one for the west region. Assign Workspace1 to the east region subdomain. Assign Workspace2 to the west region subdomain. The solution must follow the principle of least privilege. Which role should you assign to the user?

A. workspace Admin
B. domain admin
C. domain contributor
D. Fabric admin

**Correct Answer:** D

**Question #21 Topic 1**
You have a Fabric workspace named Workspace1 that contains a warehouse named DW1 and a data pipeline named Pipeline1. You plan to add a user named User3 to Workspace1. You need to ensure that User3 can perform the following actions: View all the items in Workspace1. Update the tables in DW1. The solution must follow the principle of least privilege. You already assigned the appropriate object-level permissions to DW1. Which workspace role should you assign to User3?

A. Admin
B. Member
C. Viewer
D. Contributor

**Correct Answer:** D

**Question #22 Topic 1**
You have a Fabric capacity that contains a workspace named Workspace1. Workspace1 contains a lakehouse named Lakehouse1, a data pipeline, a notebook, and several Microsoft Power BI reports. A user named User1 wants to use SQL to analyze the data in Lakehouse1. You need to configure access for User1. The solution must meet the following requirements: Provide User1 with read access to the table data in Lakehouse1. Prevent User1 from using Apache Spark to query the underlying files in Lakehouse1. Prevent User1 from accessing other items in Workspace1. What should you do?

A. Share Lakehouse1 with User1 directly and select Read all SQL endpoint data.
B. Assign User1 the Viewer role for Workspace1. Share Lakehouse1 with User1 and select Read all SQL endpoint data.
C. Share Lakehouse1 with User1 directly and select Build reports on the default semantic model.
D. Assign User1 the Member role for Workspace1. Share Lakehouse1 with User1 and select Read all SQL endpoint data.

**Correct Answer:** A

**Question #23 Topic 1**
DRAG DROP - You are implementing the following data entities in a Fabric environment: Entity1: Available in a lakehouse and contains data that will be used as a core organization entity Entity2: Available in a semantic model and contains data that meets organizational standards Entity3: Available in a Microsoft Power BI report and contains data that is ready for sharing and reuse Entity4: Available in a Power BI dashboard and contains approved data for executive-level decision making Your company requires that specific governance processes be implemented for the data. You need to apply endorsement badges to the entities based on each entity's use case. Which badge should you apply to each entity? To answer, drag the appropriate badges the correct entities. Each badge may be used once, more than once, or not at all. You may need to drag the split bar between panes or scroll to view content. NOTE: Each correct selection is worth one point.

*(Options not available due to Drag Drop format)*

**Correct Answer:** (N/A)

**Question #24 Topic 1**
HOTSPOT - You have three users named User1, User2, and User3. You have the Fabric workspaces shown in the following table. You have a security group named Group1 that contains User1 and User3. The Fabric admin creates the domains shown in the following table. User1 creates a new workspace named Workspace3. You add Group1 to the default domain of Domain1. For each of the following statements, select Yes if the statement is true. Otherwise, select No. NOTE: Each correct selection is worth one point.

*(Options not available due to Hotspot format)*

**Correct Answer:** (N/A)

**Question #25 Topic 1**
You have two Fabric workspaces named Workspace1 and Workspace2. You have a Fabric deployment pipeline named deployPipeline1 that deploys items from Workspace1 to Workspace2. DeployPipeline1 contains all the items in Workspace1. You recently modified the items in Workspaces1. The workspaces currently contain the items shown in the following table. Items in Workspace1 that have the same name as items in Workspace2 are currently paired. You need to ensure that the items in Workspace1 overwrite the corresponding items in Workspace2. The solution must minimize effort. What should you do?

A. Delete all the items in Workspace2, and then run deployPipeline1.
B. Rename each item in Workspace2 to have the same name as the items in Workspace1.
C. Back up the items in Workspace2, and then run deployPipeline1.
D. Run deployPipeline1 without modifying the items in Workspace2.

**Correct Answer:** D

**Question #26 Topic 1**
You have a Fabric workspace named Workspace1 that contains a data pipeline named Pipeline1 and a lakehouse named Lakehouse1. You have a deployment pipeline named deployPipeline1 that deploys Workspace1 to Workspace2. You restructure Workspace1 by adding a folder named Folder1 and moving Pipeline1 to Folder1. You use deployPipeline1 to deploy Workspace1 to Workspace2. What occurs to Workspace2?

A. Folder1 is created, Pipeline1 moves to Folder1, and Lakehouse1 is deployed.
B. Only Pipeline1 and Lakehouse1 are deployed.
C. Folder1 is created, and Pipeline1 and Lakehouse1 move to Folder1.
D. Only Folder1 is created and Pipeline1 moves to Folder1.

**Correct Answer:** A

**Question #27 Topic 1**
DRAG DROP - Your company has a team of developers. The team creates Python libraries of reusable code that is used to transform data. You create a Fabric workspace name Workspace1 that will be used to develop extract, transform, and load (ETL) solutions by using notebooks. You need to ensure that the libraries are available by default to new notebooks in Workspace1. Which three actions should you perform in sequence? To answer, move the appropriate actions from the list of actions to the answer area and arrange them in the correct order.

*(Options not available due to Drag Drop format)*

**Correct Answer:** (N/A)

**Question #28 Topic 1**
You have a Fabric workspace that contains a lakehouse and a notebook named Notebook1. Notebook1 reads data into a DataFrame from a table named Table1 and applies transformation logic. The data from the DataFrame is then written to a new Delta table named Table2 by using a merge operation. You need to consolidate the underlying Parquet files in Table1. Which command should you run?

A. VACUUM
B. BROADCAST
C. OPTIMIZE
D. CACHE

**Correct Answer:** C

**Question #29 Topic 1**
You have five Fabric workspaces. You are monitoring the execution of items by using Monitoring hub. You need to identify in which workspace a specific item runs. Which column should you view in Monitoring hub?

A. Start time
B. Capacity
C. Activity name
D. Submitter
E. Item type
F. Job type
G. Location

**Correct Answer:** G

**Question #30 Topic 1**
You have a Fabric workspace that contains a warehouse named DW1. DW1 is loaded by using a notebook named Notebook1. You need to identify which version of Delta was used when Notebook1 was executed. What should you use?

A. Real-Time hub
B. OneLake data hub
C. the Admin monitoring workspace
D. Fabric Monitor
E. the Microsoft Fabric Capacity Metrics app

**Correct Answer:** D

**Question #31 Topic 1**
DRAG DROP - You have a Fabric workspace that contains a warehouse named Warehouse1. In Warehouse1, you create a table named DimCustomer by running the following statement. You need to set the Customerkey column as a primary key of the DimCustomer table. Which three code segments should you run in sequence? To answer, move the appropriate code segments from the list of code segments to the answer area and arrange them in the correct order.

*(Options not available due to Drag Drop format)*

**Correct Answer:** (N/A)

**Question #32 Topic 1**
You have a Fabric workspace that contains a semantic model named Model1. You need to dynamically execute and monitor the refresh progress of Model1. What should you use?

A. dynamic management views in Microsoft SQL Server Management Studio (SSMS)
B. Monitoring hub
C. dynamic management views in Azure Data Studio
D. a semantic link in a notebook

**Correct Answer:** D

**Question #33 Topic 1**
*(Note: This question is part of a series of questions that present the same scenario.)*
You have a Fabric eventstream that loads data into a table named Bike_Location in a KQL database. The table contains the following columns: BikepointID, Street, Neighbourhood, No_Bikes, No_Empty_Docks, Timestamp. You need to apply transformation and filter logic to prepare the data for consumption. The solution must return data for a neighbourhood named Sands End when No_Bikes is at least 15. The results must be ordered by No_Bikes in ascending order.
Solution: You use the following code segment: (Code not displayed). Does this meet the goal?

A. Yes
B. No

**Correct Answer:** B

**Question #34 Topic 1**
*(Note: This question is part of a series of questions that present the same scenario.)*
You have a Fabric eventstream that loads data into a table named Bike_Location in a KQL database. The table contains the following columns: BikepointID, Street, Neighbourhood, No_Bikes, No_Empty_Docks, Timestamp. You need to apply transformation and filter logic to prepare the data for consumption. The solution must return data for a neighbourhood named Sands End when No_Bikes is at least 15. The results must be ordered by No_Bikes in ascending order.
Solution: You use the following code segment: (Code not displayed). Does this meet the goal?

A. Yes
B. No

**Correct Answer:** B

**Question #35 Topic 1**
*(Note: This question is part of a series of questions that present the same scenario.)*
You have a Fabric eventstream that loads data into a table named Bike_Location in a KQL database. The table contains the following columns: BikepointID, Street, Neighbourhood, No_Bikes, No_Empty_Docks, Timestamp. You need to apply transformation and filter logic to prepare the data for consumption. The solution must return data for a neighbourhood named Sands End when No_Bikes is at least 15. The results must be ordered by No_Bikes in ascending order.
Solution: You use the following code segment: (Code not displayed). Does this meet the goal?

A. Yes
B. No

**Correct Answer:** A

**Question #36 Topic 1**
*(Note: This question is part of a series of questions that present the same scenario.)*
You have a Fabric eventstream that loads data into a table named Bike_Location in a KQL database. The table contains the following columns: BikepointID, Street, Neighbourhood, No_Bikes, No_Empty_Docks, Timestamp. You need to apply transformation and filter logic to prepare the data for consumption. The solution must return data for a neighbourhood named Sands End when No_Bikes is at least 15. The results must be ordered by No_Bikes in ascending order.
Solution: You use the following code segment: (Code not displayed). Does this meet the goal?

A. Yes
B. No

**Correct Answer:** A

**Question #37 Topic 1**
*(Case Study: Litware, Inc. - Overview: Publishing company with online/retail bookstores. Environment: Fabric workspace with high concurrency, medallion architecture (bronze/silver/gold), sales data in ERP/Dataflow Gen1. Requirements: NRT SEO data, version control with GitHub, cost control.)*
You need to ensure that processes for the bronze and silver layers run in isolation. How should you configure the Apache Spark settings?

A. Disable high concurrency.
B. Create a custom pool.
C. Modify the number of executors.
D. Set the default environment.

**Correct Answer:** B

**Question #38 Topic 1**
*(Case Study: Litware, Inc.)*
DRAG DROP - You need to ensure that the authors can see only their respective sales data. How should you complete the statement? To answer, drag the appropriate values the correct targets. Each value may be used once, more than once, or not at all. You may need to drag the split bar between panes or scroll to view content. NOTE: Each correct selection is worth one point.

*(Options not available due to Drag Drop format)*

**Correct Answer:** (N/A)

**Question #39 Topic 1**
*(Note: This question is part of a series of questions that present the same scenario.)*
You have an Azure key vault named KeyVault1 that contains secrets. You have a Fabric workspace named Workspace1. Workspace contains a notebook named Notebook1 that performs the following tasks: Loads stage data to the target tables in a lakehouse, Triggers the refresh of a semantic model. You plan to add functionality to Notebook1 that will use the Fabric API to monitor the semantic model refreshes. You need to retrieve the registered application ID and secret from KeyVault1 to generate the authentication token.
Solution: You use the following code segment: Use notebookutils.credentials.getSecret and specify the key vault URL and key vault secret. Does this meet the goal?

A. Yes
B. No

**Correct Answer:** A

**Question #40 Topic 1**
*(Note: This question is part of a series of questions that present the same scenario.)*
You have an Azure key vault named KeyVault1 that contains secrets. You have a Fabric workspace named Workspace1. Workspace contains a notebook named Notebook1 that performs the following tasks: Loads stage data to the target tables in a lakehouse, Triggers the refresh of a semantic model. You plan to add functionality to Notebook1 that will use the Fabric API to monitor the semantic model refreshes. You need to retrieve the registered application ID and secret from KeyVault1 to generate the authentication token.
Solution: You use the following code segment: Use notebookutils.credentials.putSecret and specify the key vault URL and key vault secret. Does this meet the goal?

A. Yes
B. No

**Correct Answer:** B

**Question #41 Topic 1**
*(Note: This question is part of a series of questions that present the same scenario.)*
You have an Azure key vault named KeyVault1 that contains secrets. You have a Fabric workspace named Workspace1. Workspace contains a notebook named Notebook1 that performs the following tasks: Loads stage data to the target tables in a lakehouse, Triggers the refresh of a semantic model. You plan to add functionality to Notebook1 that will use the Fabric API to monitor the semantic model refreshes. You need to retrieve the registered application ID and secret from KeyVault1 to generate the authentication token.
Solution: You use the following code segment: Use notebookutils.credentials.getSecret and specify the key vault URL and the name of a linked service. Does this meet the goal?

A. Yes
B. No

**Correct Answer:** B

**Question #42 Topic 1**
DRAG DROP - You have two Fabric notebooks named Load_Salesperson and Load_Orders that read data from Parquet files in a lakehouse. Load_Salesperson writes to a Delta table named dim_salesperson. Load_Orders writes to a Delta table named fact_orders and is dependent on the successful execution of Load_Salesperson. You need to implement a pattern to dynamically execute Load_Salesperson and Load_Orders in the appropriate order by using a notebook. How should you complete the code? To answer, drag the appropriate values the correct targets. Each value may be used once, more than once, or not at all. You may need to drag the split bar between panes or scroll to view content. NOTE: Each correct selection is worth one point.

*(Options not available due to Drag Drop format)*

**Correct Answer:** (N/A)

**Question #43 Topic 1**
HOTSPOT - You have a Fabric workspace named Workspace1 that contains a warehouse named Warehouse2. A team of data analysts has Viewer role access to Workspace1. You create a table by running the following statement. You need to ensure that the team can view only the first two characters and the last four characters of the CreditCard attribute. How should you complete the statement? To answer, select the appropriate options in the answer area. NOTE: Each correct selection is worth one point.

*(Options not available due to Hotspot format)*

**Correct Answer:** (N/A)

**Question #44 Topic 1**
HOTSPOT - You are building a data orchestration pattern by using a Fabric data pipeline named Dynamic Data Copy as shown in the exhibit. (Click the Exhibit tab.) Dynamic Data Copy does NOT use parametrization. You need to configure the ForEach activity to receive the list of tables to be copied. How should you complete the pipeline expression? To answer, select the appropriate options in the answer area. NOTE: Each correct selection is worth one point.

*(Options not available due to Hotspot format)*

**Correct Answer:** (N/A)

**Question #45 Topic 1**
HOTSPOT - You have a Fabric workspace that contains a warehouse named Warehouse1. Warehouse1 contains a table named DimCustomers. DimCustomers contains the following columns: CustomerName, CustomerID, BirthDate, EmailAddress. You need to configure security to meet the following requirements: BirthDate in DimCustomer must be masked and display 1900-01-01. EmailAddress in DimCustomer must be masked and display only the first leading character and the last five characters. How should you complete the statement? To answer, select the appropriate options in the answer area. NOTE: Each correct selection is worth one point.

*(Options not available due to Hotspot format)*

**Correct Answer:** (N/A)

**Question #46 Topic 1**
You have a Fabric workspace named Workspace1. Your company acquires GitHub licenses. You need to configure source control for Workpace1 to use GitHub. The solution must follow the principle of least privilege. Which permissions do you require to ensure that you can commit code to GitHub?

A. Actions (Read and write) and Contents (Read and write)
B. Actions (Read and write) only
C. Contents (Read and write) only
D. Contents (Read) and Commit statuses (Read and write)

**Correct Answer:** C

**Question #47 Topic 1**
You have a Fabric workspace named Workspace1. Your company acquires GitHub licenses. You need to configure source control for Workpace1 to use GitHub. The solution must follow the principle of least privilege. Which permissions do you require to ensure that you can commit code to GitHub?

A. Actions (Read and write) and Contents (Read and write)
B. Actions (Read and write) only
C. Contents (Read and write) only
D. Contents (Read) and Commit statuses (Read and write)

**Correct Answer:** C

**Correct Answer:** A

**Question #49 Topic 1**
You have a Fabric workspace that contains a lakehouse and a semantic model named Model1. You use a notebook named Notebook1 to ingest and transform data from an external data source. You need to execute Notebook1 as part of a data pipeline named Pipeline1. The process must meet the following requirements: Run daily at 07:00 AM UTC. Attempt to retry Notebook1 twice if the notebook fails. After Notebook1 executes successfully, refresh Model1. Which three actions should you perform? Each correct answer presents part of the solution. NOTE: Each correct selection is worth one point.

A. Place the Semantic model refresh activity after the Notebook activity and link the activities by using the On success condition.
B. From the Schedule settings of Pipeline1, set the time zone to UTC.
C. Set the Retry setting of the Notebook activity to 2.
D. From the Schedule settings of Notebook1, set the time zone to UTC.
E. Set the Retry setting of the Semantic model refresh activity to 2.
F. Place the Semantic model refresh activity after the Notebook activity and link the activities by using an On completion condition.

**Correct Answer:** ABC

**Question #50 Topic 1**
You have a Fabric workspace that contains a lakehouse named Lakehouse1. You plan to create a data pipeline named Pipeline1 to ingest data into Lakehouse1. You will use a parameter named param1 to pass an external value into Pipeline1. The param1 parameter has a data type of int. You need to ensure that the pipeline expression returns param1 as an int value. How should you specify the parameter value?

A. "@pipeline().parameters.param1"
B. "@{pipeline().parameters.param1}"
C. "@{pipeline().parameters.[param1]}"
D. "@@{pipeline().parameters.param1}"

**Correct Answer:** A

**Question #51 Topic 1**
You have a Fabric workspace named Workspace1 that contains a lakehouse named Lakehouse1. Workspace1 contains the following items: A Dataflow Gen2 dataflow that copies data from an on-premises Microsoft SQL Server database to Lakehouse1, A notebook that transforms files and loads the data to Lakehouse1, A data pipeline that loads a CSV file to Lakehouse1. You need to develop an orchestration solution in Fabric that will load each item one after the other. The solution must be scheduled to run every 15 minutes. Which type of item should you use?

A. notebook
B. warehouse
C. Dataflow Gen2 dataflow
D. data pipeline

**Correct Answer:** D

**Question #52 Topic 1**
You are building a Fabric notebook named MasterNotebook1 in a workspace. MasterNotebook1 contains the following code. You need to ensure that the notebooks are executed in the following sequence: 1. Notebook_03 2. Notebook_01 3. Notebook_02 Which two actions should you perform? Each correct answer presents part of the solution. NOTE: Each correct selection is worth one point.

A. Move the declaration of Notebook_02 to the bottom of the Directed Acyclic Graph (DAG) definition.
B. Add dependencies to the execution of Notebook_03.
C. Split the Directed Acyclic Graph (DAG) definition into three separate definitions.
D. Add dependencies to the execution of Notebook_02.
E. Change the concurrency to 3.
F. Move the declaration of Notebook_03 to the top of the Directed Acyclic Graph (DAG) definition.

**Correct Answer:** DF

**Question #53 Topic 1**
You have a Fabric workspace that contains a data pipeline named Pipeline1 as shown in the exhibit. (Click the Exhibit tab.) What will occur the next time Pipeline1 runs?

A. Copy_kdi will run first, and then Execute procedure1 will run.
B. Execute procedure1 will run first, and then Copy_kdi will run.
C. Execute procedure1 will run and Copy_kdi will be skipped.
D. Copy_kdi will run and Execute procedure1 will be skipped.
E. Both activities will run simultaneously.
F. Both activities will be skipped.

**Correct Answer:** D

**Question #54 Topic 1**
*(Case Study: Contoso, Ltd. - Overview: Online retail company modernizing analytics with Fabric. Environment: Fabric F64 capacity, POS SQL Server, SaaS marketing app MAR1. Requirements: Medallion architecture, minimize egress costs, source control with Azure Repos.)*
You need to ensure that WorkspaceA can be configured for source control. Which two actions should you perform? Each correct answer presents part of the solution. NOTE: Each correct selection is worth one point.

A. From Tenant setting, set Users can synchronize workspace items with their Git repositories to Enabled.
B. From Tenant setting, set Users can sync workspace items with GitHub repositories to Enabled.
C. Configure WorkspaceA to use a Premium Per User (PPU) license.
D. Assign WorkspaceA to Cap1.

**Correct Answer:** AD

**Question #55 Topic 1**
HOTSPOT - You have a Fabric workspace that contains a warehouse named Warehouse1. Warehouse1 contains a table named Customer. Customer contains the following data. You have an internal Microsoft Entra user named User1 that has an email address of user1@contoso.com. You need to provide User1 with access to the Customer table. The solution must prevent User1 from accessing the CreditCard column. How should you complete the statement? To answer, select the appropriate options in the answer area. NOTE: Each correct selection is worth one point.

*(Options not available due to Hotspot format)*

**Correct Answer:** (N/A)

**Question #56 Topic 1**
You have a Fabric deployment pipeline that uses three workspaces named Dev, Test, and Prod. You need to deploy an Eventhouse as part of the deployment process. What should you use to add the Eventhouse to the deployment process?

A. an Azure DevOps pipeline
B. an eventstream
C. GitHub Actions

**Correct Answer:** A

**Question #57 Topic 1**
You have a Fabric warehouse named DW1. DW1 contains a table that stores sales data and is used by multiple sales representatives. You plan to implement row-level security (RLS). You need to ensure that the sales representatives can see only their respective data. Which warehouse object do you require to implement RLS?

A. TRIGGER
B. SCHEMA
C. FUNCTION
D. DATABASE ROLE

**Correct Answer:** C

**Question #58 Topic 1**
You have a Fabric warehouse named DW1. DW1 contains a table that stores sales data and is used by multiple sales representatives. You plan to implement row-level security (RLS). You need to ensure that the sales representatives can see only their respective data. Which warehouse object do you require to implement RLS?

A. SECURITY POLICY
B. TABLE
C. TRIGGER
D. STORED PROCEDURE

**Correct Answer:** A

**Question #59 Topic 1**
You have a Fabric F32 capacity that contains a workspace. The workspace contains a warehouse named DW1 that is modelled by using MD5 hash surrogate keys. DW1 contains a single fact table that has grown from 200 million rows to 500 million rows during the past year. You have Microsoft Power BI reports that are based on Direct Lake. The reports show year-on-year values. Users report that the performance of some of the reports has degraded over time and some visuals show errors. You need to resolve the performance issues. The solution must meet the following requirements: Provide the best query performance. Minimize operational costs. Which should you do?

A. Create views.
B. Modify the surrogate keys to use a different data type.
C. Change the MD5 hash to SHA256.
D. Increase the capacity.
E. Disable V-Order on the warehouse.

**Correct Answer:** D

**Question #60 Topic 1**
You have a Fabric workspace named Workspace1 that contains a warehouse named Warehouse1. You plan to deploy Warehouse 1 to a new workspace named Workspace2. As part of the deployment process, you need to verify whether Warehouse1 contains invalid references. The solution must minimize development effort and provide detailed information about the invalid references. What should you use?

A. a dbt project
B. a deployment pipeline
C. a Python script
D. a database project

**Correct Answer:** B

---

## Topic 2: Ingest and Transform Data
*(Source: ExamTopics Topic 2)*

**Question #1 Topic 2**
*(Case Study: Litware, Inc. - Overview: Publishing company. Environment: Fabric workspace, medallion architecture (bronze/silver/gold), sales data in ERP/Parquet. Requirements: NRT SEO data, version control, no new Azure resources.)*
You need to implement the solution for the book reviews. Which should you do?

A. Create a Dataflow Gen2 dataflow.
B. Create a shortcut.
C. Enable external data sharing.
D. Create a data pipeline.

**Correct Answer:** B

**Question #2 Topic 2**
*(Case Study: Litware, Inc.)*
You need to resolve the sales data issue. The solution must minimize the amount of data transferred. What should you do?

A. Spilt the dataflow into two dataflows.
B. Configure scheduled refresh for the dataflow.
C. Configure incremental refresh for the dataflow. Set Store rows from the past to 1 Month.
D. Configure incremental refresh for the dataflow. Set Refresh rows from the past to 1 Year.
E. Configure incremental refresh for the dataflow. Set Refresh rows from the past to 1 Month.

**Correct Answer:** E

**Question #3 Topic 2**
*(Case Study: Contoso, Ltd. - Same context as previous Topic 1 Case Study)*
HOTSPOT - You need to recommend a method to populate the POS1 data to the lakehouse medallion layers. What should you recommend for each layer? To answer, select the appropriate options in the answer area. NOTE: Each correct selection is worth one point.

*(Options not available due to Hotspot format)*

**Correct Answer:** (N/A)

**Question #4 Topic 2**
*(Case Study: Contoso, Ltd.)*
You need to ensure that usage of the data in the Amazon S3 bucket meets the technical requirements. What should you do?

A. Create a workspace identity and enable high concurrency for the notebooks.
B. Create a shortcut and ensure that caching is disabled for the workspace.
C. Create a workspace identity and use the identity in a data pipeline.
D. Create a shortcut and ensure that caching is enabled for the workspace.

**Correct Answer:** D

**Question #5 Topic 2**
*(Case Study: Contoso, Ltd.)*
HOTSPOT - You need to create the product dimension. How should you complete the Apache Spark SQL code? To answer, select the appropriate options in the answer area. NOTE: Each correct selection is worth one point.

*(Options not available due to Hotspot format)*

**Correct Answer:** (N/A)

**Question #6 Topic 2**
*(Case Study: Contoso, Ltd.)*
You need to populate the MAR1 data in the bronze layer. Which two types of activities should you include in the pipeline? Each correct answer presents part of the solution. NOTE: Each correct selection is worth one point.

A. ForEach
B. Copy data
C. WebHook
D. Stored procedure

**Correct Answer:** AB

**Question #7 Topic 2**
HOTSPOT - You have a Fabric workspace that contains a warehouse named Warehouse1. Warehouse1 contains the following tables and columns. You need to denormalize the tables and include the ContractType and StartDate columns in the Employee table. The solution must meet the following requirements: Ensure that the StartDate column is of the date data type. Ensure that all the rows from the Employee table are preserved and include any matching rows from the Contract table. Ensure that the result set displays the total number of employees per contract type for all the contract types that have more than two employees. How should you complete the statement? To answer, select the appropriate options in the answer area. NOTE: Each correct selection is worth one point.

*(Options not available due to Hotspot format)*

**Correct Answer:** (N/A)

**Question #8 Topic 2**
HOTSPOT - You have an Azure Event Hubs data source that contains weather data. You ingest the data from the data source by using an eventstream named Eventstream1. Eventstream1 uses a lakehouse as the destination. You need to batch ingest only rows from the data source where the City attribute has a value of Kansas. The filter must be added before the destination. The solution must minimize development effort. What should you use for the data processor and filtering? To answer, select the appropriate options in the answer area. NOTE: Each correct selection is worth one point.

*(Options not available due to Hotspot format)*

**Correct Answer:** (N/A)

**Question #9 Topic 2**
You have a Fabric workspace that contains an eventstream named Eventstream1. Eventstream1 processes data from a thermal sensor by using event stream processing, and then stores the data in a lakehouse. You need to modify Eventstream1 to include the standard deviation of the temperature. Which transform operator should you include in the Eventstream1 logic?

A. Expand
B. Group by
C. Union
D. Aggregate

**Correct Answer:** B

**Question #10 Topic 2**
You have an Azure event hub. Each event contains the following fields: BikepointID, Street, Neighbourhood, Latitude, Longitude, No_Bikes, No_Empty_Docks. You need to ingest the events. The solution must only retain events that have a Neighbourhood value of Chelsea, and then store the retained events in a Fabric lakehouse. What should you use?

A. a KQL queryset
B. an eventstream
C. a streaming dataset
D. Apache Spark Structured Streaming

**Correct Answer:** B

**Question #11 Topic 2**
HOTSPOT - You are building a data loading pattern for Fabric notebook workloads. You have the following code segment: For each of the following statements, select Yes if the statement is true. Otherwise, select No. NOTE: Each correct selection is worth one point.

*(Options not available due to Hotspot format)*

**Correct Answer:** (N/A)

**Question #13 Topic 2**
You have a Fabric workspace that contains a lakehouse named Lakehouse1. In an external data source, you have data files that are 500 GB each. A new file is added every day. You need to ingest the data into Lakehouse1 without applying any transformations. The solution must meet the following requirements: Trigger the process when a new file is added. Provide the highest throughput. Which type of item should you use to ingest the data?

A. Eventstream
B. Dataflow Gen2
C. Streaming dataset
D. Data pipeline

**Correct Answer:** D

**Question #14 Topic 2**
You have a Fabric workspace that contains a lakehouse named Lakehouse1. In an external data source, you have data files that are 500 GB each. A new file is added every day. You need to ingest the data into Lakehouse1 without applying any transformations. The solution must meet the following requirements: Trigger the process when a new file is added. Provide the highest throughput. Which type of item should you use to ingest the data?

A. Data pipeline
B. Environment
C. KQL queryset
D. Dataflow Gen2

**Correct Answer:** A

**Question #15 Topic 2**
You have a Fabric workspace that contains an eventhouse and a KQL database named Database1. Database1 has the following: A table named Table1, A table named Table2, An update policy named Policy1. Policy1 sends data from Table1 to Table2. Recently, the following actions were performed on Table1: An additional element named temperature was added to the StreamData column. The data type of the Timestamp column was changed to date. The data type of the DeviceId column was changed to string. You plan to load additional records to Table2. Which two records will load from Table1 to Table2? Each correct answer presents a complete solution. NOTE: Each correct selection is worth one point.

A. (Record sample A)
B. (Record sample B)
C. (Record sample C)
D. (Record sample D)

**Correct Answer:** AD

**Question #16 Topic 2**
HOTSPOT - You have a Fabric workspace. You are debugging a statement and discover the following issues: Sometimes, the statement fails to return all the expected rows. The PurchaseDate output column is NOT in the expected format of mmm dd, yy. You need to resolve the issues. The solution must ensure that the data types of the results are retained. The results can contain blank cells. How should you complete the statement? To answer, select the appropriate options in the answer area. NOTE: Each correct selection is worth one point.

*(Options not available due to Hotspot format)*

**Correct Answer:** (N/A)

**Question #17 Topic 2**
You are developing a data pipeline named Pipeline1. You need to add a Copy data activity that will copy data from a Snowflake data source to a Fabric warehouse. What should you configure?

A. Degree of copy parallelism
B. Fault tolerance
C. Enable staging
D. Enable logging

**Correct Answer:** C

**Question #18 Topic 2**
*(Note: This question is part of a series of questions that present the same scenario.)*
You have a KQL database that contains two tables named Stream and Reference. Stream contains streaming data. Reference contains reference data. Both tables contain millions of rows. You have a KQL queryset. You need to reduce how long it takes to run the KQL queryset.
Solution: You change the join type to kind=outer. Does this meet the goal?

A. Yes
B. No

**Correct Answer:** B

**Question #19 Topic 2**
*(Note: This question is part of a series of questions that present the same scenario.)*
You have a KQL database that contains two tables named Stream and Reference. Stream contains streaming data. Reference contains reference data. Both tables contain millions of rows. You have a KQL queryset. You need to reduce how long it takes to run the KQL queryset.
Solution: You change project to extend. Does this meet the goal?

A. Yes
B. No

**Correct Answer:** B

**Question #20 Topic 2**
*(Note: This question is part of a series of questions that present the same scenario.)*
You have a KQL database that contains two tables named Stream and Reference. Stream contains streaming data. Reference contains reference data. Both tables contain millions of rows. You have a KQL queryset. You need to reduce how long it takes to run the KQL queryset.
Solution: You move the filter to line 02. Does this meet the goal?

A. Yes
B. No

**Correct Answer:** A

**Question #21 Topic 2**
*(Note: This question is part of a series of questions that present the same scenario.)*
You have a KQL database that contains two tables named Stream and Reference. Stream contains streaming data. Reference contains reference data. Both tables contain millions of rows. You have a KQL queryset. You need to reduce how long it takes to run the KQL queryset.
Solution: You add the make_list() function to the output columns. Does this meet the goal?

A. Yes
B. No

**Correct Answer:** B

**Question #22 Topic 2**
*(Case Study: Litware, Inc. - Overview: Publishing company. Environment: Fabric workspace, high concurrency, sales data from ERP/Dataflow Gen1. Requirements: NRT SEO data, book reviews in lakehouse without copy, new book cover image processing.)*
You need to create a workflow for the new book cover images. Which two components should you include in the workflow? Each correct answer presents part of the solution. NOTE: Each correct selection is worth one point.

A. a time-based schedule
B. a streaming dataflow
C. a blob storage action
D. a data pipeline
E. a notebook that uses Apache Spark Structured Streaming
F. a reflex item

**Correct Answer:** DF

**Question #23 Topic 2**
*(Case Study: Litware, Inc.)*
What should you recommend that the data engineering team use to ingest the SEO data?

A. a streaming dataflow
B. a streaming dataset
C. a notebook that uses Apache Spark Structured Streaming
D. an eventstream

**Correct Answer:** D

**Question #24 Topic 2**
HOTSPOT - You have a Fabric warehouse named DW1 that contains four staging tables named ProductCategory, ProductSubcategory, Product, and SalesOrder. ProductCategory, ProductSubcategory, and Product are used often in analytical queries. You need to implement a star schema for DW1. The solution must minimize development effort. Which design approach should you use? To answer, select the appropriate options in the answer area. NOTE: Each correct selection is worth one point.

*(Options not available due to Hotspot format)*

**Correct Answer:** (N/A)

**Question #25 Topic 2**
HOTSPOT - Your company has three newly created data engineering teams named Team1, Team2, and Team3 that plan to use Fabric. The teams have the following personas: Team1 consists of members who currently use Microsoft Power BI and wants to transform data by using a low-code approach. Team2 consists of members that have a background in Python programming and wants to use PySpark code. Team3 consists of members who currently use Azure Data Factory and wants to move data using the least amount of effort. You need to recommend tools for the teams based on their current personas. What should you recommend for each team? To answer, select the appropriate options in the answer area. NOTE: Each correct selection is worth one point.

*(Options not available due to Hotspot format)*

**Correct Answer:** (N/A)

**Question #26 Topic 2**
HOTSPOT - You plan to process the following three datasets by using Fabric: Dataset1 (unique primary key), Dataset2 (semi-structured, bulk transfer, custom visuals), Dataset3 (lakehouse, bulk loaded, windowing functions). You need to identify which type of item to use for the datasets. The solution must minimize development effort and use built-in functionality, when possible. What should you identify for each dataset? To answer, select the appropriate options in the answer area. NOTE: Each correct selection is worth one point.

*(Options not available due to Hotspot format)*

**Correct Answer:** (N/A)

**Question #27 Topic 2**
HOTSPOT - You have a Fabric workspace that contains a lakehouse named Lakehouse1. Lakehouse1 contains a table named Status_Target. The data source contains a table named Status_Source. In a notebook name Notebook1, you load Status_Source to a DataFrame named sourceDF and Status_Target to a DataFrame named targetDF. You need to implement an incremental loading pattern by using Notebook1. The solution must meet the following requirements: Update matching records, Insert new records, Set status to inactive for old records. How should you complete the statement? To answer, select the appropriate options in the answer area. NOTE: Each correct selection is worth one point.

*(Options not available due to Hotspot format)*

**Correct Answer:** (N/A)

**Question #28 Topic 2**
DRAG DROP - You are building a data loading pattern by using a Fabric data pipeline. The source is an Azure SQL database that contains 25 tables. The destination is a lakehouse. In a warehouse, you create a control table named Control.Object. You need to build a data pipeline that will support the dynamic ingestion of the tables listed in the control table by using a single execution. Which three actions should you perform in sequence? To answer, move the appropriate actions from the list of actions to the answer area and arrange them in the correct order.

*(Options not available due to Drag Drop format)*

**Correct Answer:** (N/A)

**Question #29 Topic 2**
You are implementing a medallion architecture in a Fabric lakehouse. You plan to create a dimension table that will contain the following columns: ID, CustomerCode, CustomerName, CustomerAddress, CustomerLocation, ValidFrom, ValidTo. You need to ensure that the table supports the analysis of historical sales data by customer location at the time of each sale. Which type of slowly changing dimension (SCD) should you use?

A. Type 2
B. Type 0
C. Type 1
D. Type 3

**Correct Answer:** A

**Question #30 Topic 2**
You have a Fabric workspace that contains an eventstream named EventStream1. EventStream1 outputs events to a table named Table1 in a lakehouse. The streaming data is sourced from motorway sensors and represents the speed of cars. You need to add a transformation to EventStream1 to average the car speeds. The speeds must be grouped by non-overlapping and contiguous time intervals of one minute. Each event must belong to exactly one window. Which windowing function should you use?

A. sliding
B. hopping
C. tumbling
D. session

**Correct Answer:** C

**Question #31 Topic 2**
HOTSPOT - You have a table in a Fabric lakehouse that contains the following data. You have a notebook that contains the following code segment. For each of the following statements, select Yes if the statement is true. Otherwise, select No. NOTE: Each correct selection is worth one point.

*(Options not available due to Hotspot format)*

**Correct Answer:** (N/A)

**Question #32 Topic 2**
DRAG DROP - You have a Fabric workspace that contains an eventhouse named Eventhouse1. In Eventhouse1, you plan to create a table named DeviceStreamData in a KQL database. The table will contain data based on the following sample. You need to use a KQL query to develop the solution for Eventhouse1. Which three code segments should you run in sequence? To answer, move the appropriate code segments from the list of code segments to the answer area and arrange them in the correct order.

*(Options not available due to Drag Drop format)*

**Correct Answer:** (N/A)

**Question #33 Topic 2**
You have a Fabric workspace that contains a warehouse named Warehouse1. You have an on-premises Microsoft SQL Server database named Database1 that is accessed by using an on-premises data gateway. You need to copy data from Database1 to Warehouse1. Which item should you use?

A. a data pipeline
B. an Apache Spark job definition
C. a streaming dataflow
D. a notebook

**Correct Answer:** A

**Question #34 Topic 2**
You have a Fabric warehouse named DW1 that contains a Type 2 slowly changing dimension (SCD) dimension table named DimCustomer. DimCustomer contains 100 columns and 20 million rows. The columns are of various data types, including int, varchar, date, and varbinary. You need to identify incoming changes to the table and update the records when there is a change. The solution must minimize resource consumption. What should you use to identify changes to attributes?

A. a hash function to compare the attributes in the source table.
B. a direct attributes comparison across the attributes in the DimCustomer table.
C. a direct attributes comparison for the attributes in the source table.
D. a hash function to compare the attributes in the DimCustomer table.

**Correct Answer:** A

**Question #35 Topic 2**
You have an Azure SQL database named DB1. In a Fabric workspace, you deploy an eventstream named EventStreamDB1 to stream record changes from DB1 into a lakehouse. You discover that events are NOT being propagated to EventStreamDB1. You need to ensure that the events are propagated to EventStreamDB1. What should you do?

A. Create a read-only replica of DB1.
B. Create an Azure Stream Analytics job.
C. Enable Extended Events for DB1.
D. Enable change data capture (CDC) for DB1.

**Correct Answer:** D

**Question #36 Topic 2**
*(Case Study: Contoso, Ltd. - Overview: Online retail company. Environment: Fabric F64, POS SQL Server, SaaS app MAR1. Requirements: Medallion architecture, minimize egress, resolve MAR1 connectivity errors.)*
You need to recommend a solution to resolve the MAR1 connectivity issues. The solution must minimize development effort. What should you recommend?

A. Add a ForEach activity to the data pipeline.
B. Configure retries for the Copy data activity.
C. Call a notebook from the data pipeline.
**Question #37 Topic 2**
*(Case Study: Litware, Inc. - Overview: Publishing company. Environment: Fabric workspace, high concurrency, sales data from ERP/Dataflow Gen1. Requirements: NRT SEO data, book reviews in lakehouse without copy, new book cover image processing.)*
You need to recommend a solution for handling old files. The solution must meet the technical requirements. What should you include in the recommendation?

A. a data pipeline that includes a Copy data activity
B. a data pipeline that includes a Delete data activity
C. a notebook that runs the VACUUM command
D. a notebook that runs the OPTIMIZE command

**Correct Answer:** C

**Question #38 Topic 2**
DRAG DROP - You have a KQL database that contains a table named Readings. You need to build a KQL query to compare the MeterReading value of each row to the previous row base on the Timestamp value. A sample of the expected output is shown in the following table. How should you complete the query? To answer, drag the appropriate values the correct targets. Each value may be used once, more than once, or not at all. You may need to drag the split bar between panes or scroll to view content. NOTE: Each correct selection is worth one point.

*(Options not available due to Drag Drop format)*

**Correct Answer:** (N/A)

**Question #39 Topic 2**
HOTSPOT - You need to recommend a Fabric streaming solution that will use the sources shown in the following table. The solution must minimize development effort. What should you include in the recommendation for each source? To answer, select the appropriate options in the answer area. NOTE: Each correct selection is worth one point.

*(Options not available due to Hotspot format)*

**Correct Answer:** (N/A)

**Question #40 Topic 2**
HOTSPOT - You are building a data loading pattern for Fabric notebook workloads. You have the following code segment. For each of the following statements, select Yes if the statement is true. Otherwise, select No. NOTE: Each correct selection is worth one point.

*(Options not available due to Hotspot format)*

**Correct Answer:** (N/A)

---

## Topic 3: Monitor and Optimize
*(Source: ExamTopics Topic 3)*

**Question #1 Topic 3**
*(Note: Question text not available from scrape)*

**Correct Answer:** (N/A)

**Question #2 Topic 3**
*(Note: Question text not available from scrape)*

**Correct Answer:** (N/A)

**Question #3 Topic 3**
DRAG DROP - You have a Fabric eventhouse that contains a KQL database. The database contains a table named TaxiData. The following is a sample of the data in TaxiData. You need to build two KQL queries. The solution must meet the following requirements: One of the queries must partition RunningTotalAmount by VendorID. The other query must create a column named FirstPickupDateTime that shows the first value of each hour from tpep_pickup_datetime partitioned by payment_type. How should you complete each query? To answer, drag the appropriate values the correct targets. Each value may be used once, more than once, or not at all. You may need to drag the split bar between panes or scroll to view content. NOTE: Each correct selection is worth one point.

*(Options not available due to Drag Drop format)*

**Correct Answer:** (N/A)

**Question #4 Topic 3**
HOTSPOT - You are processing streaming data from an external data provider. You have the following code segment. For each of the following statements, select Yes if the statement is true. Otherwise, select No. NOTE: Each correct selection is worth one point.

*(Options not available due to Hotspot format)*

**Correct Answer:** (N/A)

**Question #5 Topic 3**
You have a Fabric workspace that contains a lakehouse named Lakehouse1. Lakehouse1 contains a Delta table named Table1. You analyze Table1 and discover that Table1 contains 2,000 Parquet files of 1 MB each. You need to minimize how long it takes to query Table1. What should you do?

A. Disable V-Order and run the OPTIMIZE command.
B. Disable V-Order and run the VACUUM command.
C. Run the OPTIMIZE and VACUUM commands.

**Correct Answer:** C

**Question #6 Topic 3**
You have a Fabric workspace that contains a warehouse named Warehouse1. Data is loaded daily into Warehouse1 by using data pipelines and stored procedures. You discover that the daily data load takes longer than expected. You need to monitor Warehouse1 to identify the names of users that are actively running queries. Which view should you use?

A. sys.dm_exec_connections
B. sys.dm_exec_requests
C. queryinsights.long_running_queries
D. queryinsights.frequently_run_queries
E. sys.dm_exec_sessions

**Correct Answer:** E
