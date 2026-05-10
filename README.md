# Loan Default Credit Scoring Project

## 1. 프로젝트 개요

본 프로젝트는 Kaggle의 Loan Default Prediction Dataset을 활용하여 대출 신청자의 부도 가능성을 예측하는 머신러닝 모델을 구축하는 프로젝트입니다.

기존 Telco Customer Churn 프로젝트에서는 XGBoost 기반 이진분류 모델을 사용했으므로, 이번 프로젝트에서는 Logistic Regression 기반의 설명 가능한 신용평점 모델을 중심으로 구성합니다.

## 2. 프로젝트 목적

대출 신청자의 인적 정보, 재무 정보, 신용 관련 정보를 바탕으로 대출 부도 가능성을 예측하고, 예측 확률을 활용하여 고객을 저위험, 중위험, 고위험 등급으로 분류합니다.

최종 목표는 단순히 부도 여부를 맞히는 것이 아니라, 여신심사 담당자가 의사결정에 참고할 수 있는 설명 가능한 신용평점 모델을 만드는 것입니다.

## 3. 비즈니스 문제 정의

현재의 대출 심사 방식만으로는 부도 위험 고객을 충분히 식별하지 못해 금융기관의 손실이 발생할 수 있습니다.

따라서 대출 신청자의 특성을 기반으로 부도 위험을 사전에 예측하고, 고위험 고객에 대해 추가 심사, 한도 축소, 보증 요구, 거절 검토 등의 의사결정을 지원하는 모델이 필요합니다.

## 4. 핵심 페르소나

| 항목 | 내용 |
|---|---|
| 페르소나 | 은행 여신심사팀 리스크 매니저 |
| 주요 업무 | 대출 신청자의 부도 위험 평가 |
| 핵심 고민 | 기존 심사 기준만으로 고위험 고객을 충분히 구분하기 어려움 |
| 모델 활용 방식 | 대출 신청자의 정보를 입력하여 부도 확률과 위험등급 확인 |
| 주요 의사결정 | 승인, 추가 심사, 한도 축소, 거절 검토 |

## 5. 데이터셋

| 항목 | 내용 |
|---|---|
| 데이터 출처 | Kaggle Loan Default Prediction Dataset |
| 데이터 파일 위치 | data/Loan_default.csv |
| 문제 유형 | 이진분류 |
| 예측 대상 | 대출 부도 여부 |
| 주요 변수 | Age, Income, LoanAmount, CreditScore, EmploymentType 등 |
| 타깃 변수 | Default |

## 6. 프로젝트 구조

    ml-learning/
    ├─ .venv/
    ├─ .vscode/
    │  ├─ settings.json
    │  └─ extensions.json
    ├─ data/
    │  └─ Loan_default.csv
    ├─ notebooks/
    │  └─ loan_default_credit_scoring.ipynb
    ├─ models/
    ├─ reports/
    ├─ requirements.txt
    ├─ README.md
    └─ .gitignore

## 7. 분석 흐름

| 단계 | 내용 |
|---|---|
| Step 1 | 데이터 로드 및 기본 구조 확인 |
| Step 2 | 컬럼 의미 파악 및 타깃 변수 확인 |
| Step 3 | 결측치, 중복값, 자료형 확인 |
| Step 4 | 수치형 변수 EDA |
| Step 5 | 범주형 변수 EDA |
| Step 6 | 타깃 변수와 입력 변수 관계 분석 |
| Step 7 | 이상치 확인 |
| Step 8 | 전처리 전략 결정 |
| Step 9 | Train, Validation, Test 데이터 분리 |
| Step 10 | Baseline 모델 구축 |
| Step 11 | Logistic Regression 기반 신용평점 모델 구축 |
| Step 12 | 비교 모델 학습 |
| Step 13 | 모델 평가 및 임계값 조정 |
| Step 14 | 부도확률 기반 위험등급 생성 |
| Step 15 | 결론 및 한계 정리 |

## 8. 모델링 방향

이번 프로젝트의 최종 모델 후보는 Logistic Regression입니다.

Logistic Regression을 중심 모델로 선택한 이유는 다음과 같습니다.

| 이유 | 설명 |
|---|---|
| 설명 가능성 | 회귀계수를 통해 각 변수가 부도 위험에 미치는 방향을 해석할 수 있음 |
| 확률 출력 | 부도 여부뿐 아니라 부도 확률을 산출할 수 있음 |
| 신용평점화 가능 | 예측 확률을 점수와 위험등급으로 변환할 수 있음 |
| 이전 프로젝트와 차별화 | XGBoost 중심 성능 최적화가 아니라 해석 가능한 금융 리스크 모델링에 초점 |

## 9. 비교 모델

| 모델 | 목적 |
|---|---|
| DummyClassifier | 최소 기준 성능 확인 |
| Logistic Regression | 최종 신용평점 모델 후보 |
| Linear Discriminant Analysis | 선형 판별 기반 비교 |
| KNN | 거리 기반 비모수 모델 비교 |
| RandomForest | 비선형 트리 기반 비교 |

## 10. 주요 평가 지표

| 지표 | 해석 |
|---|---|
| Accuracy | 전체 예측 중 맞힌 비율 |
| Precision | 부도라고 예측한 고객 중 실제 부도 고객 비율 |
| Recall | 실제 부도 고객 중 모델이 잡아낸 비율 |
| F1-score | Precision과 Recall의 조화평균 |
| ROC-AUC | 모델의 전반적인 분류 변별력 |

부도 예측 문제에서는 실제 부도 고객을 정상 고객으로 잘못 예측하는 것이 금융기관 손실로 이어질 수 있으므로, Accuracy만 보지 않고 Recall, F1-score, ROC-AUC를 함께 확인합니다.

## 11. 결과물

| 결과물 | 저장 위치 |
|---|---|
| 최종 모델 | models/final_logistic_credit_scoring_model.joblib |
| 모델 성능 비교 결과 | reports/model_validation_results.csv |
| 테스트 예측 결과 | reports/test_credit_scoring_predictions.csv |
| 최종 노트북 | notebooks/loan_default_credit_scoring.ipynb |

## 12. 위험등급 설계 방향

모델이 산출한 부도확률을 기반으로 다음과 같은 위험등급을 생성합니다.

| 부도확률 구간 | 위험등급 | 의사결정 예시 |
|---|---|---|
| 낮음 | Low | 승인 가능 |
| 중간 | Medium | 추가 심사 |
| 높음 | High | 한도 축소 또는 보증 요구 |
| 매우 높음 | Critical | 거절 검토 |

구체적인 임계값은 Validation 데이터에서 Precision, Recall, F1-score를 비교한 뒤 결정합니다.

## 13. 실행 환경

| 항목 | 내용 |
|---|---|
| Python | 3.11.9 |
| 가상환경 | venv |
| 개발환경 | VS Code |
| 노트북 | Jupyter Notebook |
| 데이터 설치 방식 | Kaggle에서 직접 다운로드 후 data 폴더에 배치 |

## 14. 실행 순서

1. ml-learning 폴더를 VS Code로 연다.
2. .venv 가상환경이 활성화되었는지 확인한다.
3. data 폴더에 Loan_default.csv 파일이 있는지 확인한다.
4. notebooks/loan_default_credit_scoring.ipynb를 연다.
5. Step 1부터 순서대로 실행한다.
6. 각 단계의 출력 결과를 확인한 뒤 다음 단계로 넘어간다.

## 15. 프로젝트 차별점

이전 Telco Customer Churn 프로젝트는 XGBoost와 Optuna 기반의 성능 최적화에 초점을 맞췄습니다.

이번 프로젝트는 다음 차별점을 가집니다.

| 구분 | 이전 Telco 프로젝트 | 이번 Loan Default 프로젝트 |
|---|---|---|
| 핵심 모델 | XGBoost |
| 모델링 방향 | 성능 중심 이진분류 |
| 이번 핵심 모델 | Logistic Regression |
| 이번 방향 | 설명 가능한 신용평점 모델 |
| 주요 결과 | 이탈 여부 예측 |
| 이번 결과 | 부도확률, 신용점수, 위험등급, 심사 의사결정 |

## 16. 한계

공개 데이터셋을 사용하므로 실제 금융기관의 심사 기준과는 차이가 있을 수 있습니다.

Logistic Regression은 해석 가능성이 높지만 복잡한 비선형 관계를 포착하는 데에는 제한이 있을 수 있습니다.

위험등급 기준은 교육용 분석 목적에 맞춘 기준이며, 실제 업무 적용 시에는 손실비용, 심사비용, 규제 기준을 함께 반영해야 합니다.

## 17. 참고

이 프로젝트는 인공지능개론 수업의 분석 프로젝트 흐름에 맞춰 구성합니다.

수업 기준에 따라 프로젝트는 문제 정의, 데이터 이해, 데이터 준비, 모델링, 평가, 결과 해석의 순서로 진행합니다.
