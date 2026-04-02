# 허리케인에 품절되는 초코파이의 비밀 
**Microsoft Fabric으로 구축하는 20분 엔드 투 엔드 데이터 파이프라인**

[English Version Below](#english-version)

## 세션 소개 (Session Overview)
회사 내부 데이터만으로는 비즈니스의 원인을 파악하기 어렵고, 외부 데이터와의 결합은 높은 엔지니어링 장벽을 요구합니다. 
본 세션은 복잡한 서버 구축과 코딩 없이, 50만 건의 대규모 내부 데이터와 외부 기상 데이터를 결합하는 **엔터프라이즈급 데이터 파이프라인(ETL)**을 Microsoft Fabric을 통해 20분 만에 즉석에서 구축하는 과정을 라이브 데모로 보여줍니다.

‘미국의 초코파이’라 불리는 팝타르트(Pop-Tarts)가 허리케인 예보 시 왜 가장 먼저 품절되는지, 데이터가 어떻게 숨겨진 상관관계를 찾아내는지 확인해 보세요!

## 핵심 목표 (Key Takeaways)
- **엔지니어링의 간편화:** 파이썬이나 SQL 코딩 없이 시각화된 인터페이스만으로 대용량 데이터를 정제하고 병합합니다.
- **통합 저장소 아키텍쳐:** OneLake라는 단일 저장소 위에서 데이터 수집-가공-적재가 어떻게 하나의 흐름으로 연결되는지 증명합니다.
- **파이프라인 구축:** 가공된 데이터가 물리적 이동 없이 Power BI의 시각화로 즉각 이어지는 E2E(End-to-End)를 경험합니다.

## 아키텍처 및 워크플로우 (Architecture & Workflow)

이 프로젝트는 4단계의 E2E 파이프라인으로 구성되어 있습니다.

1. **Extract (데이터 수집):** - 대구 지점의 50만 행 매출 데이터(로컬 CSV)와 미국 기상청 오픈 데이터(Web/GitHub URL)를 플랫폼으로 호출합니다.
2. **Transform (데이터 팩토리):** - `Data Factory(Dataflow Gen2)`를 활용해 코딩 없이 날짜 형식을 맞추고, 두 거대한 데이터셋을 단 한 번의 클릭으로 JOIN 합니다.
3. **Load (레이크하우스 적재):** - 정제된 통합 데이터를 `OneLake` 기반의 `Lakehouse`에 분석 최적화 포맷인 **Delta Table** 형태로 영구 적재합니다.
4. **Analyze (서빙 및 시각화):** - `Direct Lake` 기술을 활용한 `의미 체계 모델(Semantic Model)`을 통해 원본 데이터를 실시간으로 참조하며, `Power BI`를 사용해 허리케인과 매출 폭증의 상관관계를 시각적으로 증명합니다.

## 🛠️ 사용된 기술 스택 (Tech Stack)
- **Platform:** Microsoft Fabric (SaaS)
- **Workloads:**
  - Data Factory (ETL & Data Integration)
  - Data Engineering (Lakehouse, OneLake Unified Storage)
  - Power BI (Data Visualization & Semantic Model)


---
<br>

<a name="english-version"></a>
# The Secret of Chocopies Sold Out During Hurricanes
**Building a 20-Minute End-to-End Data Pipeline with Microsoft Fabric**

## Session Overview
Internal company data alone often fails to reveal the 'true cause' of business trends, and integrating external data typically requires overcoming a high engineering barrier. 
This session features a live demo of building an **enterprise-grade data pipeline (ETL)** from scratch in just 20 minutes using Microsoft Fabric—without deploying servers or writing complex code.

We will merge 500,000 rows of internal sales data with external weather data to uncover why Pop-Tarts (often compared to "American Chocopies") are the first items to sell out when a hurricane approaches. Discover how seamlessly connected data can independently reveal hidden business insights!

## Key Takeaways
- **Democratization of Engineering:** Clean and merge massive datasets using a visual interface without writing Python or SQL code.
- **The Power of Unified Storage:** See how data ingestion, transformation, and loading flow as a single stream on top of **OneLake**, Fabric's unified storage.
- **Seamless E2E Pipeline:** Experience a true End-to-End workflow where processed data flows instantly into interactive Power BI visualizations without any physical data movement.

## Architecture & Workflow

This project is built on a 4-step E2E pipeline:

1. **Extract (Data Ingestion):** - Import 500,000 rows of local store sales data (CSV) and public US weather data (Web/GitHub URL) into the platform.
2. **Transform (Data Factory):** - Utilize `Data Factory (Dataflow Gen2)` to format dates and JOIN two massive datasets with a single click—entirely no-code.
3. **Load (Lakehouse Storage):** - Load the refined, integrated data into a `Lakehouse` built on `OneLake` as an analytics-optimized **Delta Table**.
4. **Analyze (Serving & Visualization):** - Leverage `Direct Lake` technology via the `Semantic Model` to query raw data in real-time. Finally, use `Power BI`'s interactive charts to visually prove the exact correlation between hurricane events and sales spikes.

## 🛠️ Tech Stack Used
- **Platform:** Microsoft Fabric (SaaS)
- **Workloads:**
  - Data Factory (ETL & Data Integration)
  - Data Engineering (Lakehouse, OneLake Unified Storage)
  - Power BI (Data Visualization & Semantic Model)
