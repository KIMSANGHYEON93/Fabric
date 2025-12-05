# 📘 DP-700 핵심 용어 핸드북 & 요점 정리

## 1. Core Platform & Architecture (핵심 플랫폼 및 아키텍처)

Microsoft Fabric의 기본 철학은 "통합(Integration)"과 "단일 저장소(OneLake)"입니다.

| 용어 (약어) | Full Name | 한글 번역 | 핵심 요약 (Exam Point) |
| :--- | :--- | :--- | :--- |
| **OneLake** | OneLake | **원레이크** | • **"데이터를 위한 OneDrive"**. 모든 Fabric 워크로드의 단일 통합 저장소.<br>• 데이터 복제 없이 논리적으로 데이터를 공유함. |
| **SaaS** | Software as a Service | **서비스형 소프트웨어** | • Fabric은 PaaS가 아닌 **SaaS**임.<br>• 사용자가 인프라를 관리할 필요 없이 바로 사용 가능한 완전 관리형 플랫폼. |
| **Capacity** | Fabric Capacity | **Fabric 용량** | • 컴퓨팅 리소스의 통합 단위. 모든 워크로드가 이 용량을 공유함.<br>• 비용 관리와 성능 모니터링의 기준점. |
| **Tenant** | Tenant | **테넌트** | • 조직의 최상위 루트(Root). OneLake는 테넌트 당 하나만 존재함. |
| **Workspace** | Workspace | **작업 공간** | • 협업의 기본 단위이자 권한 관리의 경계.<br>• 도메인(Domain)을 사용하여 논리적으로 그룹화 가능. |

---

## 2. Data Engineering: Lakehouse & Spark (데이터 엔지니어링)

데이터 저장과 처리를 담당하는 핵심 영역입니다. **Delta Lake** 포맷이 표준입니다.

| 용어 (약어) | Full Name | 한글 번역 | 핵심 요약 (Exam Point) |
| :--- | :--- | :--- | :--- |
| **Lakehouse** | Lakehouse | **레이크하우스** | • **Data Lake(유연성) + Data Warehouse(관리)**.<br>• Spark(쓰기)와 SQL(읽기) 엔진을 모두 지원.<br>• 스키마 온 리드(Schema-on-read) 방식. |
| **Shortcut** | Shortcut | **단축키 (바로가기)** | • **★ 시험 빈출**. 외부 데이터(S3, ADLS Gen2)를 복사(Copy)하지 않고 원본 위치 그대로 참조만 하는 기능.<br>• 데이터 이동 비용 "0". |
| **Delta Lake** | Delta Lake | **델타 레이크** | • Parquet 파일에 **ACID 트랜잭션 로그(Log)**를 추가한 오픈 소스 저장 포맷.<br>• 시간 여행(Time Travel) 및 데이터 무결성 보장. |
| **Spark** | Apache Spark | **스파크** | • 대규모 데이터 분산 처리 엔진.<br>• **Notebook**(코드 작성) 또는 **Job Definition**(배치 작업)으로 실행. |
| **V-Order** | V-Order | **V-오더** | • Fabric의 **쓰기 최적화 기술**. Parquet 파일 정렬을 최적화하여 **읽기 속도를 비약적으로 향상**시킴. (기본값: 켜짐) |
| **Starter Pool** | Starter Pool | **스타터 풀** | • Spark 세션을 **"콜드 스타트" 없이** 빠르게 시작(약 5~10초)하게 해주는 미리 예열된 노드 집합. |

---

## 3. Data Integration: Data Factory (데이터 통합)

데이터를 옮기고(Copy) 변환(Transform)하는 ETL 도구입니다.

| 용어 (약어) | Full Name | 한글 번역 | 핵심 요약 (Exam Point) |
| :--- | :--- | :--- | :--- |
| **Pipeline** | Data Pipeline | **데이터 파이프라인** | • **오케스트레이션(조율)** 도구. 작업을 순서대로 실행하고 제어함.<br>• `Copy Data Activity`: 대용량 데이터 복사에 최적화.<br>• 매개변수(Parameter)를 통한 동적 실행 지원. |
| **Dataflow Gen2** | Dataflow Generation 2 | **데이터 흐름 Gen2** | • **Low-code/No-code** 데이터 변환 도구.<br>• **Power Query** 인터페이스 사용 (Excel 사용자와 친화적).<br>• 데이터 스테이징(Staging) 기능 기본 제공. |
| **Staging Lakehouse**| Staging Lakehouse | **스테이징 레이크하우스** | • Dataflow Gen2가 데이터를 변환하는 동안 임시로 사용하는 중간 저장소.<br>• 사용자가 관리할 필요 없음(자동 관리). |

---

## 4. Real-Time Intelligence (실시간 인텔리전스)

스트리밍 데이터를 수집하고 즉각적으로 반응하는 영역입니다.

| 용어 (약어) | Full Name | 한글 번역 | 핵심 요약 (Exam Point) |
| :--- | :--- | :--- | :--- |
| **Eventstream** | Eventstream | **이벤트스트림** | • 실시간 데이터를 수집(Source)하고 변환(Transform)하여 전달(Destination)하는 파이프라인.<br>• **No-code** 캔버스 제공. |
| **KQL DB** | Kusto Query Language Database | **KQL 데이터베이스** | • 시계열(Time-series) 및 로그 데이터 분석에 최적화된 고성능 DB.<br>• **Eventhouse**(이벤트하우스) 안에 포함됨. |
| **Activator** | Fabric Activator (Reflex) | **액티베이터 (리플렉스)** | • 데이터 패턴을 감지하여 **행동(Action)**을 취하는 도구.<br>• 예: "온도가 100도 넘으면 이메일 발송". |
| **Derived Stream**| Derived Stream | **파생 스트림** | • 원본 스트림에서 필터링하거나 변환하여 갈라져 나온 하위 스트림.<br>• 콘텐츠 기반 라우팅에 사용됨. |

---

## 5. Architecture Pattern & Ops (아키텍처 패턴 및 운영)

데이터를 구조화하고 배포를 자동화하는 방법론입니다.

| 용어 (약어) | Full Name | 한글 번역 | 핵심 요약 (Exam Point) |
| :--- | :--- | :--- | :--- |
| **Medallion** | Medallion Architecture | **메달리온 아키텍처** | • 데이터 품질에 따른 3단계 계층 구조.<br>• **Bronze (Raw)**: 원시 데이터 그대로 저장.<br>• **Silver (Validated)**: 정제, 중복 제거, 타입 변환.<br>• **Gold (Enriched)**: 비즈니스 로직 적용, 집계, 리포팅용 (Star Schema). |
| **CI/CD** | Continuous Integration / Continuous Delivery | **지속적 통합 / 지속적 배포** | • 개발 → 테스트 → 운영 환경으로의 자동화된 배포 프로세스. |
| **Deployment Pipeline** | Deployment Pipeline | **배포 파이프라인** | • Fabric 워크스페이스 간(Dev/Test/Prod) 콘텐츠 이동을 자동화하는 도구.<br>• **배포 규칙(Deployment Rules)**: 환경별로 매개변수(DB 연결 문자열 등)를 자동 변경. |
| **Git Integration**| Git Integration | **Git 통합** | • Azure DevOps 또는 GitHub와 연동하여 작업 내용을 코드로 버전 관리.<br>• "소스 제어(Source Control)" 버튼으로 동기화. |

---

## 📝 DP-700 시험 합격을 위한 3줄 요점 정리

1.  **저장은 OneLake, 포맷은 Delta-Parquet:** 모든 데이터는 OneLake에 저장되며, 표준 포맷은 Delta Lake(Parquet + Log)입니다. 외부 데이터는 복사하지 말고 **Shortcut**을 쓰세요.
2.  **변환은 상황에 맞게:** 코드(Python/SQL)가 편하면 **Notebook**, UI(Low-code)가 편하면 **Dataflow Gen2**, 단순 복사 및 스케줄링은 **Pipeline**을 선택하세요.
3.  **아키텍처는 메달리온:** 데이터는 Bronze(원시) → Silver(정제) → Gold(집계) 순서로 흘러야 하며, 이를 관리하기 위해 **Git 연동**과 **배포 파이프라인**을 사용하여 운영 환경을 분리하세요.
