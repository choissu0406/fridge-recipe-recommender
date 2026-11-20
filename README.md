# Final Project Task 1 — Data Exploration
**보유 재료 기반 레시피 추천 서비스 (가칭: 냉장고 털이)**
Data Literacy Foundations, 2026 Fall

## 팀원
| 이름 | 학번 | GitHub |
|---|---|---|
| 최승수 | 20260628 | @choissu0406 |
| 조은우 | (학번) | @rvnvunk |
| 장윤우 | (학번) | @20070803-boop |
| 조민혁 | (학번) | @m0n3110 |

## 데이터
| 구분 | 데이터 | 출처 |
|---|---|---|
| 선택 | 식품의약품안전처 「조리식품의 레시피 DB」 (서비스 ID `COOKRCP01`) | 식품안전나라 OpenAPI: https://www.foodsafetykorea.go.kr/api/openApiInfo.do?svc_no=COOKRCP01 · 공공데이터포털: https://www.data.go.kr/data/15060073/openapi.do |
| 비교 후보 | Food.com Recipes and Interactions | https://www.kaggle.com/datasets/shuyangli94/food-com-recipes-and-user-interactions |

- 한 행 = 레시피 1개 (메뉴명, 요리종류, 조리방법, 1인분 영양정보, 재료정보, 조리 단계)
- **데이터 파일은 저장소에 올리지 않습니다.** 아래 방법으로 누구나 같은 데이터를 받을 수 있습니다.
  받은 시각과 전체 건수는 실행 시 `data/download_info.json`에 기록됩니다.

## 실행 방법

### 1. API 키 발급 (무료, 자동 승인)
1. [식품안전나라](https://www.foodsafetykorea.go.kr) 회원가입 및 로그인
2. 「조리식품의 레시피 DB」 서비스 페이지(위 링크)에서 OpenAPI 인증키 신청
3. 발급된 인증키 확인 (사이트 메뉴 구조는 바뀔 수 있으니 페이지 안내를 따르세요)

### 2. 환경 준비
```bash
pip install pandas matplotlib requests jupyter
```

### 3. API 키 설정 후 노트북 실행
API 키는 코드에 직접 적지 말고 환경변수로 넣습니다. (키가 GitHub에 올라가지 않도록)

**Windows (PowerShell)**
```powershell
$env:FOOD_API_KEY="발급받은_키"
jupyter notebook data_exploration.ipynb
```

**macOS / Linux**
```bash
export FOOD_API_KEY="발급받은_키"
jupyter notebook data_exploration.ipynb
```

**Google Colab**: 첫 셀 위에 `import os; os.environ["FOOD_API_KEY"] = "발급받은_키"` 를 추가해 실행한 뒤, 제출 전에는 그 셀을 지우세요.

노트북에서 **Run All** 하면:
1. 첫 실행 시 API에서 전체 레시피를 받아 `data/recipes_raw.csv`로 저장 (이후에는 저장된 파일 사용)
2. 결측·중복·숫자 변환·재료 문자열 품질 점검
3. 요약 표(`figures/summary_by_category.csv`)와 그래프(`figures/top20_ingredients.png`, `figures/ingredients_per_recipe.png`) 생성
4. 재료 입력 → 일치율 기반 레시피 추천 프로토타입 실행
5. 보고서에 쓰는 핵심 숫자 출력

(선택) 비교 후보 점검: Kaggle에서 `RAW_recipes.csv`를 받아 `data/` 폴더에 넣으면 부록 셀이 함께 실행됩니다.

## 파일 구조
```
├── data_exploration.ipynb   # 데이터 수집·점검·EDA·추천 프로토타입
├── README.md
├── .gitignore               # data/ 폴더와 키 파일 제외
├── data/                    # 실행 시 생성 (업로드하지 않음)
└── figures/                 # 실행 시 생성되는 표와 그래프
```

## 이용 조건
식품안전나라 OpenAPI의 이용 조건을 따르며, 출처(식품의약품안전처)를 표시합니다.
원본 데이터는 저장소에 포함하지 않고 공개 API로 다시 받을 수 있게 했습니다.
