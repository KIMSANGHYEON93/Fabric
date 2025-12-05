이번 모듈 평가는 **"Microsoft Fabric에서 Apache Spark 사용하기"**에 관한 내용입니다.

Data Engineering의 꽃이자, DP-700 시험에서 가장 높은 비중을 차지하는 Spark, PySpark, DataFrame 조작 능력을 검증하는 단계입니다.

단순히 코드를 외우는 것이 아니라, **Spark가 데이터를 처리하는 방식(Lazy Evaluation, Distributed Computing)**을 이해해야 실무에서 대용량 데이터를 다룰 수 있습니다.

바로 해설 들어갑니다.

---

### 1. Your organization needs to analyze customer data stored in a lakehouse and visualize demographic distributions using Spark in Microsoft Fabric. Which Spark feature would facilitate this analysis?

## 1. 🎯 출제 의도 파악 (The Hook)

- **Spark의 데이터 처리 표준**이 무엇인지 묻는 문제입니다.
    
- 과거의 방식(RDD)과 현대적인 방식(DataFrame/SQL)을 구분할 수 있어야 합니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: Dataframe API for structured data manipulation and Spark SQL for querying.**
    
- **논리:**
    
    1. Spark에서 구조화된 데이터(표 형태)를 다루는 가장 최적화된 표준 API는 **DataFrame**입니다.
        
    2. DataFrame은 내부적으로 최적화 엔진(Catalyst Optimizer)을 통해 쿼리 속도를 높여줍니다.
        
    3. 또한, SQL 문법에 익숙한 엔지니어를 위해 **Spark SQL**을 제공하여 분석 및 시각화 준비를 돕습니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **RDDs (Resilient Distributed Datasets):** Spark의 가장 기초적인 로우 레벨(Low-level) API입니다. 비정형 데이터 처리에 강력하지만, 최적화가 덜 되어 있고 코드가 복잡하여 최근 분석 업무에는 잘 쓰이지 않습니다.
    
- **Built-in machine learning algorithms:** '분석 및 분포 시각화'가 주 목적이지, '예측 모델링'이 아니므로 ML 알고리즘은 정답이 아닙니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **실무 Tip:** RDD를 직접 쓸 일은 거의 없습니다. 99%의 업무는 `DataFrame`이나 `Spark SQL`로 처리하세요. 그래야 Fabric의 최적화 엔진(V-Order 등)의 혜택을 받습니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **구조화된 데이터 분석은 무조건 DataFrame API와 Spark SQL이 정답입니다.**
    

---

### 2. What is the expected result of executing the following PySpark command: `df.groupBy('Category').agg({'SalesAmount': 'sum'})`?

## 1. 🎯 출제 의도 파악 (The Hook)

- PySpark의 **집계(Aggregation) 함수 동작 원리**와 **리턴 타입**을 묻는 문제입니다.
    
- 코드가 실행된 후 결과물이 '리스트'인지 '데이터프레임'인지 헷갈리게 만듭니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: A new dataframe with each category and the sum of sales amounts for each category.**
    
- **논리:**
    
    1. `groupBy('Category')`: 카테고리별로 그룹을 묶습니다.
        
    2. `.agg({'SalesAmount': 'sum'})`: SalesAmount 컬럼의 합계(sum)를 계산합니다.
        
    3. Spark의 트랜스포메이션(Transformation) 결과는 항상 **새로운 DataFrame**입니다. (Python의 List나 Dictionary가 아님)
        

## 3. ❌ 오답 분석 (The Distractors)

- **A list of categories...:** Spark 작업의 결과는 드라이버로 수집(`collect()`)하지 않는 이상 기본적으로 DataFrame 형태를 유지합니다. 리스트가 아닙니다.
    
- **...average sales amounts...:** 코드에 `'sum'`이라고 명시되어 있으므로 평균(average)이 나올 수 없습니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **코드 팁:** `.agg({'SalesAmount': 'sum'})` 방식도 좋지만, 실무에선 `import pyspark.sql.functions as F` 후 `df.groupBy('Category').agg(F.sum('SalesAmount').alias('TotalSales'))` 처럼 컬럼명을 깔끔하게 지정하는 방식을 선호합니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **Spark의 연산 결과는 항상 DataFrame이며, `sum`은 합계를 구합니다.**
    

---

### 3. When creating a custom environment in Microsoft Fabric, which setting allows you to use a specific version of Apache Spark for your tasks?

## 1. 🎯 출제 의도 파악 (The Hook)

- Fabric의 **환경(Environment) 설정**에서 Spark 버전을 어디서 통제하는지 묻습니다.
    
- 키워드는 **"Specific Version"**입니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: Specify the Spark runtime in the environment settings.**
    
- **논리:**
    
    1. Fabric에서 Spark 버전(예: Spark 3.3, Spark 3.4)은 **Runtime(런타임)**이라는 개념으로 관리됩니다.
        
    2. 환경 설정 메뉴에서 'Runtime' 버전을 선택함으로써 사용할 Spark 코어 및 라이브러리(Pandas, Delta Lake 등)의 버전을 고정할 수 있습니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **Node family type:** 이건 하드웨어 스펙(메모리 최적화 vs 컴퓨팅 최적화)을 고르는 것이지, 소프트웨어 버전(Spark Version)과는 무관합니다.
    
- **High concurrency mode:** 동시 접속자가 많을 때 세션을 효율적으로 관리하는 기능일 뿐, 버전 설정이 아닙니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **주의:** 프로젝트 중간에 런타임 버전을 함부로 올리지 마세요. Python 라이브러리 의존성(Dependency)이 깨져서 잘 돌아가던 코드가 에러를 뿜을 수 있습니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **Spark 버전 = Runtime 버전입니다. 환경 설정에서 런타임을 확인하세요.**
    

---

### 4. You have created a dataframe from a CSV file and want to save it as a Delta table in the Spark catalog for future SQL queries. Which method should you use?

## 1. 🎯 출제 의도 파악 (The Hook)

- 단순히 파일로 저장하는 것과, **카탈로그 테이블(Managed Table)**로 저장하는 것의 차이를 묻습니다.
    
- 키워드는 **"Spark catalog"**와 **"SQL queries"**입니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: `df.write.format("delta").saveAsTable("table_name")`**
    
- **논리:**
    
    1. `saveAsTable`: 이 명령어를 써야 데이터가 Lakehouse의 'Tables' 영역에 등록되고, **Hive Metastore(Catalog)**에 메타데이터가 생성됩니다.
        
    2. 그래야 나중에 SQL Endpoint나 Notebook에서 `SELECT * FROM table_name`으로 바로 조회할 수 있습니다.
        
    3. 포맷을 `delta`로 지정하는 것은 Fabric의 표준입니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **df.write.mode("overwrite").parquet("path"):** 이건 단순히 파일 시스템(Files 영역)에 Parquet 파일을 떨구는 것입니다. 카탈로그에 등록되지 않아 테이블 이름으로 조회할 수 없습니다.
    
- **df.createOrReplaceTempView("view_name"):** 이건 **임시 뷰(Temp View)**입니다. 현재 세션이 끝나면 사라지므로 "Future SQL queries(미래의 조회)"를 보장할 수 없습니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **Lakehouse 구조:** `saveAsTable`을 쓰면 **Managed Table**이 되고, `save`로 경로를 지정하면 **External Table**이나 단순 파일이 됩니다. 관리 편의성을 위해 중요 데이터는 `saveAsTable`을 쓰세요.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **SQL로 조회하고 싶다면 반드시 `saveAsTable`로 저장하여 카탈로그에 등록해야 합니다.**
    

---

### 5. Which SQL magic command should you use in a Microsoft Fabric notebook to execute SQL queries directly?

## 1. 🎯 출제 의도 파악 (The Hook)

- Notebook(주로 PySpark 기본) 셀 내에서 언어를 바꿔 **SQL을 실행하는 매직 커맨드**를 아는지 묻습니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: `%%sql`**
    
- **논리:**
    
    1. Jupyter 기반 Notebook에서 셀의 언어를 변경하는 명령어를 매직 커맨드(`%%`)라고 합니다.
        
    2. Spark SQL을 실행하기 위한 표준 매직 커맨드는 `%%sql`입니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **%%pyspark:** Python 코드를 실행할 때 씁니다(기본값이므로 생략 가능).
    
- **%%spark:** 보통 Scala 코드를 실행할 때 쓰이는 경우가 많거나, `%%sql`과 혼동하기 쉬운 오답입니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **꿀팁:** 복잡한 조인(Join)이나 집계는 Python 코드보다 SQL이 더 가독성이 좋을 때가 많습니다. 셀 하나에 `%%sql` 적고 편하게 쿼리 짜세요. 변수 넘기기도 가능합니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **노트북에서 SQL을 쓰고 싶다면 셀 맨 윗줄에 `%%sql`을 입력하세요.**
    

---

### 6. In Microsoft Fabric, what is the purpose of setting a default Spark pool in a workspace?

## 1. 🎯 출제 의도 파악 (The Hook)

- **워크스페이스 레벨의 컴퓨팅 관리** 개념을 묻습니다.
    
- 매번 풀을 설정하는 귀찮음을 어떻게 해결하는지에 대한 문제입니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: To automatically assign a Spark pool to jobs when no specific pool is specified.**
    
- **논리:**
    
    1. 사용자가 Notebook이나 Job을 만들 때 어떤 컴퓨터(Pool)를 쓸지 지정하지 않을 수 있습니다.
        
    2. 이때 워크스페이스에 설정된 **기본(Default) 풀**이 자동으로 할당되어 즉시 실행될 수 있게 합니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **Limit the number of Spark jobs...:** 동시 실행 제한은 'Concurrency' 설정이나 Capacity 제한에 따르는 것이지, Default Pool의 목적이 아닙니다.
    
- **Enforce the use of memory optimized nodes...:** 특정 하드웨어 강제는 Pool의 세부 설정이지, 'Default 지정' 행위 자체의 목적은 아닙니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **운영 팁:** 팀원들이 무심코 너무 큰 Pool을 쓰지 못하도록, **Default Pool은 작은 사이즈(Small Node)**로 설정해두는 것이 비용 절약의 지름길입니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **지정하지 않았을 때 자동으로 끌어다 쓰는 예비 타이어, 그것이 Default Pool입니다.**
    

---

### 7. Which Spark Dataframe method is most efficient for finding the maximum value in a column of numerical data?

## 1. 🎯 출제 의도 파악 (The Hook)

- 데이터프레임의 **집계(Aggregation) 메서드**를 정확히 알고 있는지 묻습니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: `agg`**
    
- **논리:**
    
    1. 전체 데이터셋 혹은 그룹 내에서 최대(Max), 최소(Min), 평균(Avg) 등의 통계값을 계산하는 것을 **Aggregation(집계)**이라고 합니다.
        
    2. PySpark에서는 `.agg()` 메서드 안에 `max()` 함수를 넣어 처리하는 것이 표준입니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **groupBy:** 그룹을 나누는 것이지, 그 자체로 최대값을 찾아내지는 못합니다. (보통 `groupBy().agg()` 형태로 같이 씁니다.)
    
- **filter:** 특정 조건에 맞는 행을 걸러내는 것이지, 최대값을 계산하는 것이 아닙니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **활용:** `df.agg({'price': 'max'}).show()` 한 줄이면 전체 데이터 중 최고가를 바로 확인할 수 있습니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **최대, 최소, 합계, 평균 등 요약 통계는 무조건 `agg` 메서드입니다.**
    

---

### 8. Which practice should be followed to optimize data processing performance in a Spark pool using the native execution engine in Microsoft Fabric?

## 1. 🎯 출제 의도 파악 (The Hook)

- Fabric Spark의 고성능 엔진인 **Native Execution Engine**을 활성화하는 방법을 묻습니다.
    
- Fabric은 오픈소스 Spark보다 빠른 독자적인 엔진(C++ 기반 등)을 탑재하고 있습니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: Enable the native execution engine at the environment level by setting relevant Spark properties.**
    
- **논리:**
    
    1. Native Execution Engine(과거 Photon이나 Velox와 유사한 개념)을 사용하려면 Spark 설정(Conf)이 필요합니다.
        
    2. 이를 개별 코드마다 넣기보다는 **Environment(환경)** 설정에서 속성(Properties)으로 켜두는 것이 모범 사례(Practice)입니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **Use CPU optimized nodes exclusively:** 하드웨어를 바꾼다고 소프트웨어 엔진이 바뀌는 것은 아닙니다. Native Engine은 메모리 최적화 노드에서도 돌아갑니다.
    
- **Disable dynamic allocation:** 동적 할당(Dynamic Allocation)을 끄면 리소스 효율이 떨어져 오히려 성능이나 비용 면에서 손해를 볼 수 있습니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **현황:** 최근 Fabric 업데이트에서는 **Native Execution Engine이 기본값(Default)으로 활성화**되어 가는 추세입니다. 하지만 시험에서는 "환경 설정에서 켠다"는 개념을 알고 있어야 합니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **Fabric의 빠른 속도를 즐기려면 환경 설정에서 'Native Execution Engine' 관련 속성을 활성화하세요.**
    

---

### 9. You have a dataframe with a column named 'Date' in a string format, and you need to convert it to a date format for further analysis. Which PySpark method would you use?

## 1. 🎯 출제 의도 파악 (The Hook)

- 데이터 전처리의 기본인 **형변환(Type Casting)**과 **컬럼 변환** 메서드를 묻습니다.
    
- 문자열(String)을 날짜(Date)로 바꾸는 상황입니다.
    

## 2. ✅ 정답 및 논리적 추론 (The Logic)

- **정답: `withColumn`**
    
- **논리:**
    
    1. PySpark에서 기존 컬럼을 변형하거나 새로운 컬럼을 추가할 때 가장 많이 쓰는 메서드는 `withColumn`입니다.
        
    2. 보통 `df.withColumn("Date", to_date("Date"))` 형태로 사용하여 문자열을 날짜형으로 덮어씌웁니다.
        

## 3. ❌ 오답 분석 (The Distractors)

- **filter:** 행을 삭제하는 것이지 데이터 타입을 바꾸지 못합니다.
    
- **selectExpr:** SQL 표현식을 써서 바꿀 수는 있지만(`df.selectExpr("to_date(Date)")`), `withColumn`이 DataFrame API 스타일의 정석이며 기존 컬럼을 유지하면서 변환하기에 더 적합합니다.
    

## 4. 💡 시니어의 실무 한 마디 (Pro Tip)

- **주의:** 날짜 포맷이 'yyyy-MM-dd'가 아니라면 `to_date` 함수 두 번째 인자에 포맷을 꼭 명시해야 합니다. 예: `to_date("Date", "MM/dd/yyyy")`. 안 그러면 전부 `Null`로 변해버리는 대참사가 일어납니다.
    

## 5. 📝 한 줄 요약 (Takeaway)

- **컬럼의 데이터 타입을 바꾸거나 값을 계산해서 넣을 때는 `withColumn`이 만능 열쇠입니다.**