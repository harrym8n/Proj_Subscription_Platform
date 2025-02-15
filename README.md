# 로그데이터 분석을 통한 콘텐츠 구독 서비스 전환 개선 프로젝트(기여도 40%)
- 팀원 총 4명과 함께 진행
- 프로젝트 팀장으로 역임하여 전체 분석 흐름 설계 및 일정 관리 수행

## 프로젝트 배경 및 목표

---

> **배경**

가상의 온라인 교육 콘텐츠 구독서비스 **코딩천국**의 2년 기간의 (2022.01.01 - 2023.12.31) 온라인 서비스 유저 행동 데이터를 통해 구독서비스의 유저 행동 패턴을 분석하여 어떤 문제가 서비스의 성장을 저해하고 있는지 규명하고 해결 인사이트를 도출해야한다.

*분석에 활용된 데이터는 실존하는 온라인 교육 콘텐츠 구독 서비스의 로그 데이터이며, 분석에 이해도 제고 및 구체적인 인사이트 제안을 위해 가상의 기업 코딩천국을 대입하여 분석 진행*

> **목표**

1. EDA 과정을 거쳐 해결했을 때 가장 비즈니스 임팩트가 큰 문제를 발굴하고 정의한다.
2. 정의한 문제를 해결했을 때 성장할 것이라 기대되는 지표를 설정하고 해당 지표를 상승시킬 수 있는 해결 인사이트를 제안한다.
<br>

## **사용한 스킬 & 도구**

- **프로그래밍 언어**: Python
- **분석 도구**: Pandas, NumPy, Scikit-learn, Matplotlib, Seaborn
- **데이터 시각화**: Matplotlib, Seaborn
<br>

## 활용한 데이터셋

> **데이터 셋 설명**
- 온라인 교육 콘텐츠 구독 서비스의 **유저 행동 데이터** (2022.01.01 ~ 2023.12.31)
- 프로덕트 분석 솔루션인 **앰플리튜드**(Amplitude)를 통해 수집된 이벤트 로그 데이터
- 유저의 서비스 이용 행태를 파악할 수 있는 이벤트 정보 포함
- 로그 데이터만 존재하며 사용자 특성 데이터, 콘텐츠 특성 데이터 등이 미존재
<br>
> **데이터 구성**

|  | 이벤트명 | 설명 |
| --- | --- | --- |
| 1 | enter.main_page | 서비스 메인페이지 진입 |
| 2 | enter.signup_page | 회원가입 페이지 진입 |
| 3 | complete.signup | 회원가입 완료 |
| 4 | enter.content_page | 콘텐츠 개별 페이지 진입 |
| 5 | click.content_page_start_content_button | 콘텐츠 수강하기 버튼 클릭 |
| 6 | click.content_page_more_review_button | 콘텐츠 후기 더보기 버튼 클릭 |
| 7 | enter.payment_page | 결제 페이지 진입 |
| 8 | complete.subscription | 첫 결제 완료 |
| 9 | renew.subscription | 정기 결제 완료 |
| 10 | resubscribe.subscription | 만료 후 재구독 완료 |
| 11 | start.free_trial | 서비스 무료체험 시작 |
| 12 | start.content | 콘텐츠 수강 시작 |
| 13 | enter.lesson_page | 레슨 시작 |
| 14 | complete.lesson | 레슨 완료 |
| 15 | click_lesson_page_related_question_box | 레슨 페이지 내 질문 목록 클릭 |
| 16 | end.content | 콘텐츠 수강 완료 |
| 17 | click.cancel_plan_button | 구독 취소 버튼 클릭 |
<br>

## 프로젝트 진행 과정(문제 해결 과정)

- **데이터 수집**: Amplitude를 통해 수집된 로그 데이터 활용
- **데이터 전처리**: Pandas를 사용하여 결측치 처리, 데이터 정제(중복치, 이상치 처리, 컬럼 매핑) 진행
- **EDA**: 시계열분석을 통한 사용자 행동 패턴 분석, 서비스 핵심 시나리오 단계를 정의하고 퍼널분석을 통해 이탈율이 높은 구간 확인
- **문제 정의**: `회원가입` → `첫 구독` 단계 전환율 저조 원인 파악하고 이를 완화시킬 수 있는 인사이트 발굴
- **데이터 분석(요인선별)**: Scikit-learn을 사용한 로지스틱 회귀분석으로 구독 전환에 영향을 미치는 요인 선별

  > ✓ 구독 전환에 영향을 미치는 요인을 규명하는 분석이므로, 구독 전 발생한 로그 데이터는 집계에서 제외\
  > ✓ 독립변수 중 수치형 변수에서 0값이 너무 많아 다운 샘플링 진행 *(user_id별 집계되므로 특정 유저가 실행하지 않은 이벤트 모두 0으로 집계)*

- **데이터 분석(해결 인사이트 탐색)**: 문제 해결 인사이트를 얻기 위해 각 요인에 대해서 심층 분석 진행
- **인사이트 도출 및 실행 계획**: 구독 전환 증대를 위한 마케팅 인사이트 도출 및 UI/UX 개선 사항 제안
<br>

## **결과 및 성과**

- 구독 전환에 영향을 미치는 주요 요인으로 ‘`콘텐츠 페이지 진입 횟수`’, ‘`콘텐츠 페이지 리뷰 버튼 클릭 여부`’, ‘`무료체험 여부`’ 확인 및 오즈비를 활용하여 구체적인 확률 도출
- 구독 확률을 최대한으로 증가시키는 최적의 **[콘텐츠 페이지 진입 횟수, 무료 체험 플랜 유형]** 등 디테일한 결과 도출하여 비즈니스 임팩트가 클 것이라 예상되는 마케팅, UI/UX 개선 플랜 제안
<br>

## 소프트 스킬

- **팀워크**: 프로젝트 기간 동안 4명의 팀원과 협력하여 역할을 분담, 매일 미팅을 통해 진행 상황 공유 및 이슈 발생시 공유하여 함께 문제 해결
- **의사소통**: 팀장으로서 전체적인 일정을 계획하고 팀원에 공유, 작업을 분담하고 주기적으로 진행 상황을 공유하는 미팅을 주도하여 팀원 간 데이터 이해도 및 프로젝트 진행에 대한 싱크 동기화
- **일정관리**: 노션 작업 스페이스 구축하여 타임라인 설계, 회의록 기록, 인사이트 기록 등을 통해 체계적으로 일정 관리 진행
<br>

## 러닝 포인트

- 단순 수치 기반으로 문제를 정의하지 않고, 비즈니스 모델과 상황을 고려하여 문제를 정의하는 역량을 성장시켰다.
- 회귀분석, 통계적 가설 검증, 퍼널분석, 시계열분석 등 다양한 방법론으로 분석을 진행함으로써 분석에 대한 하드 스킬을 성장시켰다.
- 본격적인 분석 전에 데이터에 대한 이해도를 높이고 구성원간의 싱크를 맞추는 것이 중요하며, 특히 EDA에서 발굴되는 데이터의 특이점들을 기반으로 꼼꼼하게 전처리하는 것이 작업 효율과 성과를 높이는 데 크게 기여한다는 사실을 배웠다.
<br>

## **🔑 Key Point**

1. 퍼널분석(문제 발굴) → 회귀분석(해당 문제 관련 요인 파악) → 심층 분석(인사이트 도출)의 논리적 분석 과정
2. 로지스틱 회귀분석의 정확한 결과 도출을 위한 꼼꼼한 전처리 과정(0 다운 샘플링, 구독 전 데이터 제외 등)
3. 심층 분석으로 비즈니스 임팩트를 고려한 디테일한 결과 도출 → 실무에 바로 적용할 수 있는 전략 제안
4. 프로젝트 팀장으로서 타임라인 설계하여 효율적 일정 관리, 팀원간 싱크를 맞추는 정기 공유 회의 주도
<br>
---
[👉 분석보고서 보러가기]('https://github.com/harrym8n/Proj_Subscription_Platform/blob/main/%E1%84%8F%E1%85%A9%E1%86%AB%E1%84%90%E1%85%A6%E1%86%AB%E1%84%8E%E1%85%B3%E1%84%80%E1%85%AE%E1%84%83%E1%85%A9%E1%86%A8%E1%84%89%E1%85%A5%E1%84%87%E1%85%B5%E1%84%89%E1%85%B3_%E1%84%87%E1%85%AE%E1%86%AB%E1%84%89%E1%85%A5%E1%86%A8%E1%84%87%E1%85%A9%E1%84%80%E1%85%A9%E1%84%89%E1%85%A5_%E1%84%86%E1%85%AE%E1%86%AB%E1%84%89%E1%85%A1%E1%86%BC%E1%84%92%E1%85%A7%E1%86%A8.pdf')
[👉 발표자료 보러가기]('https://github.com/harrym8n/Proj_Subscription_Platform/blob/main/%E1%84%8F%E1%85%A9%E1%86%AB%E1%84%90%E1%85%A6%E1%86%AB%E1%84%8E%E1%85%B3%E1%84%80%E1%85%AE%E1%84%83%E1%85%A9%E1%86%A8%E1%84%89%E1%85%A5%E1%84%87%E1%85%B5%E1%84%89%E1%85%B3_%E1%84%87%E1%85%A1%E1%86%AF%E1%84%91%E1%85%AD%E1%84%8C%E1%85%A1%E1%84%85%E1%85%AD_%E1%84%86%E1%85%AE%E1%86%AB%E1%84%89%E1%85%A1%E1%86%BC%E1%84%92%E1%85%A7%E1%86%A8.pdf')

