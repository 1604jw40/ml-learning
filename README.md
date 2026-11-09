# Loan Default Credit Scoring Project

Kaggle의 Loan Default Prediction Dataset을 이용해 대출 부도 예측과 설명 가능한 신용평점 모델링을 학습하는 프로젝트입니다. 인공지능개론 수업의 문제 정의 → 데이터 이해 → 데이터 준비 → 모델링 → 평가 흐름에 맞춰 진행합니다.

## 현재 구현 상태

**공개 노트북은 Step 1~3 데이터 로드·컬럼 이해·품질 점검까지 구현되어 있습니다.** 총 17개 코드 셀이 있으며, 모델 학습·평가·위험등급 생성은 아직 포함되어 있지 않습니다. 아래 모델과 결과물은 완료 실적이 아니라 후속 계획입니다.

| 단계 | 공개 노트북 상태 |
|---|---|
| Step 1 | 라이브러리·경로 설정, CSV 로드, 샘플 확인 |
| Step 2 | 컬럼 설명·한글명 매핑, 컬럼 일치 확인, 한글 컬럼명 CSV 저장 |
| Step 3 | 결측치·중복·ID·타깃·변수 유형·값 범위 점검 |
| Step 4~8 | EDA, 변수 관계·이상치 확인, 전처리 전략 수립 예정 |
| Step 9~15 | 데이터 분리, 모델 학습·비교, 평가·임계값·위험등급·결론 작성 예정 |

저장된 노트북 출력은 과거 실행 기록이며, 현재 환경에서 재실행해 검증한 결과는 아닙니다.

## 목적과 데이터

최종 목표는 Logistic Regression을 중심으로 부도 가능성을 추정하고 계수와 예측 결과를 해석하는 것입니다. 은행 여신심사팀 리스크 매니저를 가상의 활용 대상으로 설정하지만, 이 저장소는 교육용이며 실제 승인·거절 판단에 사용할 수 있는 검증된 금융 시스템이 아닙니다.

| 항목 | 내용 |
|---|---|
| 데이터 | Kaggle Loan Default Prediction Dataset |
| 로컬 입력 위치 | `data/Loan_default.csv` |
| 문제 유형 | 이진분류 |
| 타깃 | `Default` |
| 입력 변수 예시 | Age, Income, LoanAmount, CreditScore, EmploymentType |
| 식별자 | LoanID 등 ID 후보는 입력 변수 후보에서 제외 |

원본 CSV는 저장소에 포함되어 있지 않습니다. 정확한 Kaggle 데이터 페이지, 버전, 이용 조건과 파일 식별 정보는 추가 기록이 필요합니다. 컬럼 설명의 “사용” 표시는 후보 정의이며, 실제 모델 학습이 끝났다는 의미는 아닙니다.

## 저장소 구조

```text
ml-learning/
├── .gitignore
├── .vscode/
│   ├── settings.json
│   └── extensions.json
├── notebooks/
│   └── loan_default_credit_scoring.ipynb
├── requirements.txt
└── README.md
```

`data/`, `models/`, `reports/`는 노트북 실행 시 생성되는 로컬 폴더입니다. `.venv/`도 로컬에서 별도로 만듭니다. 폴더가 생성되었다고 학습 모델이나 평가 결과가 존재하는 것은 아닙니다.

## 실행 방법

기존 문서의 기준 Python 버전은 3.11.9이며, 패키지 버전은 `requirements.txt`에 기록되어 있습니다.

```bash
python -m venv .venv
# Windows PowerShell: .venv\Scripts\Activate.ps1
# macOS/Linux: source .venv/bin/activate
python -m pip install -r requirements.txt
python -m jupyter lab
```

1. 저장소 루트에서 실행하고 `data/` 폴더에 사용 권한이 있는 `Loan_default.csv`를 준비합니다.
2. `notebooks/loan_default_credit_scoring.ipynb`를 열고 해당 가상환경 커널을 선택합니다.
3. Step 1부터 순서대로 실행합니다. 현재 구현은 Step 3-8에서 끝납니다.
4. Step 1-4의 “사용 데이터 파일”과 Step 2의 컬럼 일치 결과를 확인합니다.

**입력 파일 주의:** 현재 코드는 `data/`의 CSV를 정렬해 첫 번째 파일을 읽습니다. 파일명을 고정해서 선택하는 코드는 아니므로, 해당 폴더에는 의도한 CSV 하나만 두세요. 실행 위치는 저장소 루트 또는 그 안의 `notebooks/`여야 합니다.

**출력 주의:** Step 2-4는 전체 데이터의 컬럼명을 바꾼 `reports/loan_default_korean_columns.csv`를 저장하며, 같은 이름의 기존 파일을 덮어씁니다. 이는 요약 통계가 아닌 행 단위 데이터 사본입니다. 원본과 동일하게 취급하고 공개 업로드하지 마세요. 노트북의 샘플 출력도 공유 전에 검토해야 합니다.

## 후속 모델링 계획

| 모델 후보 | 목적 |
|---|---|
| DummyClassifier | 최소 기준 성능 확인 |
| Logistic Regression | 설명 가능한 중심 모델 후보 |
| Linear Discriminant Analysis | 선형 판별 비교 |
| KNN | 거리 기반 모델 비교 |
| RandomForest | 비선형 트리 모델 비교 |

평가 지표는 Accuracy만이 아니라 Precision, Recall, F1-score, ROC-AUC를 함께 살펴볼 계획입니다. 불균형 정도에 따라 PR-AUC와 혼동행렬을 보완하고, 확률을 위험등급으로 사용할 경우 확률 보정과 비용 기준도 검토해야 합니다.

### 평가 전에 확인할 사항

- Train/Validation/Test를 분리하고 테스트를 모델·임계값 선택에 사용하지 않기
- 결측치 처리, 스케일링, 인코딩, 재표본화는 학습 데이터 안에서만 적합하기
- 중복 ID 또는 같은 대상의 반복 기록이 분할 사이에 섞이지 않는지 확인하기
- InterestRate 등 변수가 실제 예측 시점에 이용 가능한지 확인하기
- 랜덤 시드, 분할 조건, 데이터 버전과 평가 지표를 함께 기록하기
- 교육용 공개 데이터의 한계와 실제 금융 의사결정에 필요한 공정성·규제 검토를 구분하기

이 항목들은 구현 완료가 아닌 후속 검증 기준입니다.

## 결과물 구분

| 구분 | 경로 | 상태 |
|---|---|---|
| 데이터 이해·품질 점검 노트북 | `notebooks/loan_default_credit_scoring.ipynb` | 공개됨 |
| 한글 컬럼명 데이터 사본 | `reports/loan_default_korean_columns.csv` | 실행 시 로컬 생성, 공개 대상 아님 |
| 최종 모델 | `models/final_logistic_credit_scoring_model.joblib` | 예정, 생성 코드·파일 없음 |
| 모델 비교표 | `reports/model_validation_results.csv` | 예정, 생성 코드·파일 없음 |
| 테스트 예측 | `reports/test_credit_scoring_predictions.csv` | 예정, 생성 코드·파일 없음 |

부도확률 기반 위험등급의 임계값과 최종 모델 성능은 아직 확정되지 않았습니다. 계수 해석은 인과관계의 증명이 아니며, 위험등급은 검증 없이 실제 대출 심사에 적용하지 않습니다.
