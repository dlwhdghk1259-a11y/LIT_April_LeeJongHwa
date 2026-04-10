# 데이터 덩어리들을 패브릭으로 원클릭 파이프라인 구축하기

## 📖 서론: 시선 포커싱
본격적인 내용에 앞서, 재미있는 이야기로 시작합니다.

2004년 뉴욕타임즈는 ‘허리케인’이라는 단어로 아주 흥미로운 기사를 썼습니다. 기사의 주인공은 바로 세계적인 유통 기업 **월마트(Walmart)**였는데요. 월마트는 곧 다가올 '프란시스' 허리케인에 대비해 진열대에 어떤 상품을 전면 배치할지 고민하고 있었습니다.

월마트의 대표는 생각했습니다. *"우리가 가진 460TB의 데이터를 활용하자."*
바로 분석을 강행한 결과, 뜻밖의 답이 나왔습니다. 미국의 인기 디저트인 **“딸기 팝타르트”** (한국으로 치면 **초코파이**와 같은 국민 간식입니다) 였죠.

월마트는 데이터 분석을 통해 이전 허리케인 당시 고객들이 사재기했던 품목을 확인했고, 이 국민 간식의 판매량이 평소보다 무려 7배나 증가한다는 패턴을 발견했습니다. 결국 프란시스 허리케인이 닥쳤을 때 해당 상품을 전면에 진열하여 수십 배의 이익을 얻을 수 있었습니다.

하지만, 당시 이런 결과를 낼 수 있었던 근본적인 배경은 결국 **'막대한 자본과 인력'**이었습니다. 이는 월마트 같은 거대 기업만이 누릴 수 있는 특권에 가까웠죠. 

하지만 지금은 2026년입니다. 돈과 인력으로 찍어 눌렀던 장벽은 이미 허물어졌고, 이제 데이터 분석 시스템만 다룰 줄 안다면 누구나 이런 인사이트를 도출할 수 있습니다. 그 혁신적인 시스템, **“마이크로소프트 Fabric(패브릭)”**에 대해 알려드리겠습니다.

---

## 🛠️ 본론 1: Microsoft Fabric 이란?
**Fabric**은 SaaS이자 LakeHouse 아키텍처를 사용하는 **강력한 데이터 통합 플랫폼**입니다.

### 클라우드 서비스 계층의 이해
패브릭을 이해하기 위해 3가지 클라우드 서비스 계층을 간단히 살펴보겠습니다.
* **IaaS** (Infrastructure-as-a-Service)
* **PaaS** (Platform-as-a-Service)
* **SaaS** (Software-as-a-Service)

IaaS에서 SaaS로 갈수록 사용자가 직접 해야 하는 코딩이 줄어들며, 누구나 쉽게 시작할 수 있습니다. 특히 SaaS는 복잡한 설치 없이 인터넷 브라우저만으로 바로 사용하는 완성형 소프트웨어입니다. **Fabric이 바로 이 SaaS 계층에 속합니다.** (우리가 매일 쓰는 Microsoft 365와 같은 위치입니다.)

또한, 데이터와 관련된 다양한 Azure 시스템(PaaS)들이 이 하나의 플랫폼 안에 모여 있기 때문에 진정한 '데이터 통합 플랫폼'이라고 부릅니다. Fabric 내에서는 이러한 도구들을 **'워크로드(Workload)'**라고 부르며, 다음과 같은 워크로드들을 넘나들며 사용할 수 있습니다.
* Data Engineering
* Data Factory
* Data Science
* Power BI 등

---

## 🗄️ 본론 2: 저장소 아키텍처의 변천사
데이터 플랫폼의 핵심인 '저장소'는 어떻게 발전해 왔을까요?

### 1세대 - Data Warehouse (데이터 웨어하우스)
처음 등장한 저장소 형태입니다. ACID 트랜잭션에 강하고, 고성능 SQL 분석과 BI(비즈니스 인텔리전스)에 최적화되어 있습니다. 하지만 엑셀 같은 정형 데이터 외에 비정형 데이터를 담기 어렵다는 한계가 있었습니다.

### 2세대 - Data Lake (데이터 레이크)
1세대의 단점을 보완하여 등장했습니다. 텍스트는 물론 이미지, 동영상까지 거침없이 담을 수 있어 AI 및 ML 학습에 최적화되었습니다. 하지만 여기에도 치명적인 단점이 있었습니다. 관리 체계 없이 데이터를 계속 붓다 보니, 나중에는 로그 파일들이 뒤죽박죽 섞여 이른바 **'데이터의 늪(쓰레기장)'**이 되어버린다는 점입니다. 거버넌스가 유실되고 데이터의 신뢰도가 하락하는 문제를 해결해야만 했습니다.

### 3세대 - Data LakeHouse (데이터 레이크하우스) ★
현재 Fabric에서 기본적으로 사용하는 최신 저장소 아키텍처입니다. 1세대와 2세대의 장점만을 결합했습니다. 어떤 유형의 자료든 유연하게 저장할 수 있으면서도, 2세대에 없었던 **관리 체계**를 완벽하게 도입했습니다.
* **주요 기능:** 트랜잭션 보장, 스키마 강제 맞춤, 단계별 데이터 품질 관리 등

이를 통해 SQL 분석과 높은 신뢰도를 동시에 갖춘 형태로 발전했습니다.

---

## 🎬 본론 3: 데모 시연 흐름
*(효율적인 진행을 위해 사전 녹화된 영상 자료로 로딩 시간을 스킵하며 설명합니다.)*

* **[1단계] 데이터 적재:** 회사 내부 데이터(판매 기록 CSV)를 Lakehouse에 직접 업로드하고, 회사 외부 데이터(기상 정보)는 URL을 통해 끌어오는 과정을 보여줍니다.
* **[2단계] 파이프라인 및 팩토리 구축:** Lakehouse에 저장된 두 데이터를 결합하기 위해 Data Factory를 활용, 데이터 전처리 및 JOIN 작업을 진행합니다.
* **[3단계] 시각화 (Power BI):** 공정이 완료된 데이터를 바탕으로 꺾은선형 그래프와 슬라이서를 활용해 최종 인사이트를 시각화합니다.
* **⭐ [4단계] 엔드투엔드 자동화 (핵심 포인트):** 앞선 1~3단계는 실무자 입장에서 매일 아침 반복해야 하는 매우 귀찮고 번거로운 과정입니다. **파이프라인 구축 후, 클릭 한 번으로 위 3단계까지의 작업들을 자동화하는 경험**을 보여드립니다.

---

## 💡 결론 및 마무리

세션을 준비하며 마이크로소프트 Fabric을 공부할 때마다 느낀 점은 딱 하나입니다.
**“이 친구, 데이터 분석계의 스마트폰이네?”**

여러분, 누군가에게 '스마트폰'을 설명하라고 하면 어떻게 하시겠습니까? 아마 2시간을 꼬박 설명해도 그 많은 기능을 다 담기엔 부족할 것입니다. Microsoft Fabric도 마찬가지입니다.

Fabric으로 할 수 있는 일은 무궁무진합니다. 
현재 **교육, 산업, 제조, 의료** 등 분야를 막론하고 수많은 기업들이 패브릭을 도입하여 업무 효율성을 극대화하고 수익 증대 효과를 보고 있습니다. *(출처: [Microsoft Fabric 고객 사례](https://www.microsoft.com/ko-kr/customers/search?filters=product%3Aazure%2Fmicrosoft-fabric&sortBy=PublishedDate+Desc))*

스마트폰에서 여러 가지 어플리케이션을 깔아 쓰듯, 여러분도 비즈니스 상황에 맞는 워크로드들을 직접 선택하고 연결해 작업하는 것을 함께 느껴보셨으면 좋겠습니다. 나아가 이 거대한 엔터프라이즈 플랫폼을 회사에 도입한다면, **F64 버전 이상의 유료 구독 시 활성화되는 'Copilot(코파일럿)'**을 통해 여태껏 사용자가 클릭하고 고민하던 수많은 과정들을 AI에게 대신 지시할 수 있는 장점까지 누리실 수 있습니다.

### 🔗 Call To Action (콜 투 액션)
아까 말씀드린 것처럼, 마치 스마트폰 같은 이 친구를 30분 만에 설명하기에는 무리가 있다고 느꼈습니다. 그래서 여러분이 원하는 정보를 챙겨가실 수 있도록 마이크로소프트 공식 가이드라인 사이트를 준비했습니다. 

👉 **[마이크로소프트 Fabric 시작하기](https://bit.ly/fabric-start)**

세션이 끝난 뒤에도 꼭 한 번 접속하셔서 직접 경험해 보시고 느껴보시길 바랍니다. 감사합니다.

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
