# IMBK_Bank_Customer_Churn_ML
깃 레포 이름: IMBK_Bank_Customer_Churn_ML
1. 프로젝트명: 고객 이탈 분류 ML 및 인사이트 분석
2. 기간 : 2026년 4월 10일
3. 주요 기술 스택 (Libraries)
-Data Manipulation: Pandas, NumPy
-Machine Learning: Scikit-learn (sklearn)
-Boosting Algorithms: LightGBM (LGBM)
-Hyperparameter Optimization: Optuna
-Model Interpretation: SHAP
-Visualization: Matplotlib
4. 데이터 출처: 캐글 Bank Customer Churn Dataset (row: 10000, col:12)
5. 데이터 전처리
  1) customer_id 제거 : 단순 식별자로 예측력이 없고 모델이 ID에 과적합될 수 있음
  2) LabelEncoder 적용 : country, gender 모두 순서 의미가 없는 범주형이나,
    트리 기반 모델(RF, GBM, XGB)은 정수 인코딩만으로도 분기점을 스스로 학습하므로
    OneHotEncoding 없이 LabelEncoder 만으로 충분하며 범주 수가 적어 차원 증가 부담도 없음
  3) 결측값 없음 : df.isnull().sum() 전체 0 확인 → 별도 imputation 불필요
6. EDA 및 해석
<img width="1389" height="495" alt="image" src="https://github.com/user-attachments/assets/75eb494a-d745-4314-a784-c10ec092db88" />
  막대그래프: Germany의 이탈률이 약 32%로 France(16%), Spain(17%)에 비해 약 2배 높음
  → 독일 고객 대상 별도 리텐션 전략이 필요함을 시사
  꺾은선그래프: 41-50세 구간에서 이탈률이 급격히 상승(~45%)하며 최고점을 형성
  → 중장년층(40대) 고객이 이탈 리스크가 가장 높으므로, 이 연령대 맞춤형 상품·혜택 설계 필요
7. AutoML – Hyperparameter Tuning – Stacking Pipe – Shap value
8. 인사이트 제안
  1) 이탈의 결정적 트리거 : 나이, 활동 여부, 상품 수
    나이: 그래프에서 가장 상단에 위치하며, 붉은색(높은 나이) 점들이 오른쪽에 밀집해 있음
    → 고연령층일수록 이탈 위험이 급격히 높아지는 가장 강력한 이탈 신호
  2) 활동 여부: 푸른색(비활동) 점들이 오른쪽에 있음 → 활동량이 적은 고객일수록 이탈 가능성이 높음
    상품 수: 상품 이용 수가 특정 임계치를 넘거나 너무 적을 때 이탈에 큰 영향을 미침
  3) 인과관계 해석
    활동성과의 반비례 관계: 단순한 잔고보다 '현재 이 고객이 우리 은행 서비스를 얼마나 자주 쓰는가'가
    이탈을 막는 더 중요한 방어선임을 모델이 증명
    자산 규모의 영향: Balance가 높은 고객(붉은 점) 일부가 이탈 쪽으로 쏠려 있는데,
    이는 고액 자산가들이 타사 우대 금리로 이탈하는 현상
    4) 전략적 제언 : 이탈 방지가 핵심
     타겟 마케팅: 40~50대 고연령 고객군을 위한 전용 자산 관리(WM) 프로그램이나 우대 혜택을 강화해야함
     활동성 개선 캠페인: 비활동 고객을 대상으로 앱 푸시나 자동이체 설정 이벤트를 진행
9. Reference
    1) 데이터 출처
    Kaggle: Bank Customer Churn Prediction Dataset (은행 고객 이탈 예측 데이터셋)
    2) 사용 라이브러리 및 공식 문서
    PyCaret: 머신러닝 워크플로우 자동화 및 상위 모델(Top 4) 선정 활용
    Optuna: 베이지안 최적화 알고리즘을 이용한 모델별 최적 하이퍼파라미터 탐색
    SHAP: 게임 이론 기반의 모델 해석 기법 (이탈 결정 주요 원인 분석)
    Scikit-learn: 데이터 전처리(LabelEncoder, split) 및 앙상블 모델 구현
    LightGBM: 리프 중심(Leaf-wise) 트리 학습 기반의 고성능 분류 모델
    3) 분석 방법론
    EDA (탐색적 데이터 분석): 국가별·연령별 이탈률 비교를 통한 인사이트 도출
    Stacking Ensemble: 개별 모델들의 장점을 결합하여 예측 성능을 극대화하는 앙상블 기법
