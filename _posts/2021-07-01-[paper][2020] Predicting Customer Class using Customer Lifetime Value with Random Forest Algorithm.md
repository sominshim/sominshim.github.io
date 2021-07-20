---
layout: post
title: "[paper][2020] Predicting Customer Class using Customer Lifetime Value with Random Forest Algorithm"
# subtitle: "first post"
date: 2021-07-01 22:00:0
background: '/img/posts/02.jpg'
---

## [2020] Predicting Customer Class using Customer Lifetime Value with Random Forest Algorithm


Abstract
내년 고객 등급(CLV)을 예측 → 온라인 소매 업체가 장기 CRM을 얻기 위해 어떤 고객을 투자해야 하는지 결정하는 데 도움을 줌.
- Data: Super Store Retail 4년 간의 거래 내역 데이터. (약 1만 건)
- Random Forest Algorithm 훈련 + Random Search tuning 수행 ⇒ Best Accuracy

### 1. Introduction

신규 고객을 확보하는 데 드는 비용이 기존 고객을 유지하는 것보다 더 비싸기 때문에 온라인 소매 업체는 기존 고객에게 집중해야 한다. 또, 마케팅, 판매 및 서비스 비용이 수익을 초과할 수 있는 고객이 있을 것이다. 따라서 온라인 소매 업체는 long term CRM을 유지하기 위해 비즈니스 가치가 가장 높은 고객에게 집중해야 한다. 고객의 비즈니스 가치는 고객이 평생 동안 비즈니스에 지출할 것으로 예상되는 총 금액을 나타내는 CLV로 표현된다. 

대부분의 연구자들은 CLV 문제를 regression task으로 구현했지만 본 연구는 CLV의 범주(고객 등급)를 예측했다. 분류 분석은 소매업체가 마케팅 비용을 비즈니스 전략에 효과적으로 할당하는 데 도움이 될 수 있는 의사 결정 과정에서 더 많은 정보를 주기(유익하기) 때문이다. 

예측 모델은 RF 분류 알고리즘과 함께 사용 된 소매 거래 데이터 세트를 기반으로 수행되어 내년 고객의 비즈니스 클래스를 예측한다. 학습하는 데 사용된 데이터 세트는 캐글의 4년 (from 2011 to 2014)의 트랜잭션 데이터로 구성된다.

**Process**
1. dataset preprocessing 
    - cleaning the data
    - setting interval (feature and target period for training and testing)
    기간 설정 (학습 및 데이트를 위한 특징 및 목표 기간)
    - aggregating(집계) the data
    - discretizing(이산화) target variables(CLV) and feature extraction (predictor variables)

2. Merge the datasets of Feature and Target period for training and testing respectively.
학습 및 테스트를 위해 각각 기능 및 목표 기간의 데이터 세트를 병합한다.

3. Feature selection is made on the training set 

4. Random Search cross-validating is conducted to find the optimal hyperparameter values of Random Forest to achieve the best accuracy.
Random Forest의 최적 하이퍼 파라미터 값을 찾아 최고의 정확도를 얻기 위해 Random Search 교차 검증을 수행한다.

5. Evaluate model's performance on the test dataset.


### 2. Related work
(Bernat, 2019)는 개별 고객에 대한 CLV를 예측하기 위해 Pareto NBD, Cox 비례 위험 및 Gradient Tree Boosting의 세 가지 모델의 예측력을 비교함. 이 모델은 과거 트랜잭션을 사용하여 내년 고객 지출을 예측하도록 훈련. RFM 변수 외에도 다른 공변량을 사용함. 그 중 Pareto NBD 확장 모델은 다른 모델보다 더 나은 성능을 보였음.

(Jasek P, 2018)은 6 개의 데이터 세트를 기반으로 한 확장 Pareto NBD 모델, Markov 체인 모델 및 Status Quo 모델과 같은 다양한 예측 모델의 성능을 비교함. 모델의 성능은 장단기 모두에 대해 평가됨. EP NBD 모델은 대부분의 평가 지표에서 다른 모델보다 우수했음.

(Chamberlain, 2017)은 RF 회귀 알고리즘을 사용하여 내년 모델링 고객의 순 지출을 예측하기 위해 지난 3 년간의 데이터에 대한 풍부한 기능을 사용하는 영국 기반 글로벌 전자 상거래 회사를 위한 CLV 예측 시스템을 개발함. 두 가지 문제 (CLV 및 이탈 예측)를 해결하고 결과를 평가했음. 그런 다음 기능 학습을 사용하여 로지스틱 회귀와 심층 신경망을 결합하는 하이브리드 모델을 실험하여 모델을 개선시킴.

(Nicolas Glady, 2008) 이탈자를 CLV가 감소하는 사람으로 정의했음. 이 논문은 CLV 감소로 인해 발생한 손실이 고객을 잘못 분류하는 비용을 평가하는 데 사용되는 새로운 손실 함수를 도입했음. 로지스틱 회귀, 다층 퍼셉트론 신경망, 의사 결정 트리, 비용에 민감한 의사 결정 트리 및 AdaCost 부스팅의 다섯 가지 분류기의 성능을 비교함. AdaCost 분류기와 비용에 민감한 트리는 경험적 응용 프로그램에서 최상의 결과를 얻었음. 신경망과 의사 결정 트리는 AUROC에서 최상의 결과를 제공함.

### 3. Model Implementation


<center><img class="img-fluid" src="/img/posts/210701Figure1.png" alt="Demo Image" width="300" height="300" ></center>
<span class="caption text-muted">Figure 1 Overview design of the proposed system development</span>


- **3.1. Description and cleaning of the dataset**

    The global Superstore dataset from Kaggle
    - 51,300 order_line rows (25,000 unique Order transactions & 1,500 customers within a purchase period of 4 years (2011 -2014))

    The original dataset contains the 24 attributes: Row ID, Order ID, Order Date, Ship Date, Ship Mode, Customer ID, Customer Name, Segment, City, State, Country, Postal Code, Market, Region, Product ID, Category, Sub- Category, Product Name, Sales, Quantity, Discount, Profit, Shipping Cost, Order Priority.

    - In order to get a set of customer behavioral features for our model
    drop the order-related attributes such as Order Priority, Category, Product Name, etc. that cannot improve our model performance.
    - Categorical attribute has too many unique values → tree-based algorithms’ predictive power diminished.
        ⇒ Drop high unique values attributes, and are described in Table 1.

        <center><img class="img-fluid" src="/img/posts/210701Figure5.png" alt="Demo Image" width="300" height="300" ></center>
        <span class="caption text-muted">Table 1 Count of unique values of Categoricla attributes</span>

    Drop ‘Country’, ‘City, ‘State’ and ‘Region’ to get more insight into customers’ purchase behavior. 
    - Figure 2: the number of orders increasing slightly every year
    - Figure 3: the number of customers per frequency by customers give more understanding of customer purchase behavior.

        <center><img class="img-fluid" src="/img/posts/210701Figure6.png" alt="Demo Image" width="300" height="300" ></center>
        <span class="caption text-muted">Figure 2 Number of orders per year</span>

        <center><img class="img-fluid" src="/img/posts/210701Figure7.png" alt="Demo Image" width="300" height="300" ></center>
        <span class="caption text-muted">Figure 3 Number of customers per frequency</span>

        Figure 3 Number of customers per frequency


- **3.2. Data pre-processing**
    Order date of the dataset is changed into the DateTime format. (계산하기 위해)

    **Step1) Setting Interval**

    <center><img class="img-fluid" src="/img/posts/210701Figure8.png" alt="Demo Image" width="300" height="300" ></center>
    <span class="caption text-muted">Figure 4 Training and testing period of our model</span>
    

    **Step2) Data Aggregation**

    - For all the four period datasets, we create an ‘Orders’ dataframe (grouping order by Order_Id)
        - Total_Amount(the sum of Sales)
        - Total_Profit(the sum of Profit
        - Total_Discount(sum of Discount)

    - Using the Orders dataset, we create a new dataframe ‘Customers’ by grouping by Customer_ID to get unique customers.

    - Calculate RFM.
        - Recency (the day of a customer’s last purchase) - (the last day of the observation period)
        고객의 마지막 구매 일에서 관찰 기간의 마지막 날을 뺀 총 일수
        - Frequency (the number of orders a customer made during the observation period)
        관찰 기간 동안 고객이 주문한 수
        - Monetary value (the sum of Total_Amount of all orders made by a customer)
        고객이 주문한 모든 주문의 Total_Amount 합계

    **Step3) Feature Encoding**
    
    one-hot encoding (categorical → numerical format)

    **Step3) Discretizing Target variable**

    The dependent variable ‘CLV’ is calculated based on the Customers dataset using the following equations (1) to (7).

    ```
    1. CLV = (고객 가치 / 이탈률) * 이익 마진
    2. 고객 가치 = 평균 주문 가치 * 구매 빈도
    3. 이탈률 = 1 - 반복률
    4. 이익 마진 = 총 수익 * 이윤율(%)
    5. 평균 주문 값 = 총 수익 / 개별 고객의 거래 수
    6. 구매 빈도 = 전체 고객의 총 거래 수 / 고객 수
    7. 반복 비율 = 거리 횟수가 1보다 큰 고객 비율
    ```

    Customer Class 

    - 0: High-Class customer / 1: Low-Class customer

    <center><img class="img-fluid" src="/img/posts/210701Figure9.png" alt="Demo Image" width="300" height="300" ></center>

    <center><img class="img-fluid" src="/img/posts/210701Figure10.png" alt="Demo Image" width="300" height="300" ></center>
    <span class="caption text-muted">Table 2 Three rows with discretization of target variable</span>

    

    **Step4) Merge Feature and Target variable**

    **Step5) Feature Selection**
 
 
    Apply feature importance to rank the most important variables from our features set using the Random Forest feature importance method.

    <center><img class="img-fluid" src="/img/posts/210701Figure11.png" alt="Demo Image" width="300" height="300" ></center>
    <span class="caption text-muted">Table 3 Feature importance of selected features</span>

    

- **3.3. Random Forest**

    Random forest: a supervised machine learning algorithm that can be used for both regression and classification problems. 

    In the Random Forest algorithm, there are two stages: 

    ```
    Random Forest creation pseudocode:
    → k개의 feature를 무작위로 선택
    → k개의 feature 중 the best split point을 이용하여 노드 d를 계산
    → the best split point를 사용하여 하위 노드로 분할
    → 노드의 개수가 I개가 될 때까지 위 세단계를 반복
    → n개의 트리를 만들기 위해 위 단계를 n번 반복
    ```

    ```
    Random forest prediction pseudocode:
    → 무작위로 생성된 의사 결정 트리의 규칙을 사용하여 결과를 예측하고 저장
    → 예측된 target에 투표
    → 투표율이 높은 예측 target = 최종 예측 target
    ```

- **3.4. Hyperparameter tuning**
    - 모델 매개 변수: 입력 데이터를 원하는 출력으로 변환하는 방법을 지정하는 훈련 프로세스 중에 추정된 값.
    - 하이퍼 파라미터: 모델 정확도와 계산 효율성에 영향을 미칠 수 있는 모델의 구조를 정의함.


    ```
    랜덤 포레스트의 하이퍼 파라미터
    - max_samples: 각 의사 결정 트리를 훈련하는 샘플 수
    - max_features: 최적 분할을 찾을 때 고려할 특성 수
    - n_estimators: 포리스트의 트리 수
    - criterion: 분할 품질을 측정하는 기능
    - max_depth: 트리의 최대 깊이
    - min_samples_leaf: 리프 노드에 있어야하는 최소 샘플 수
    - min_samples_split: 분할에 필요한 최소 샘플 수
    ```

    향상된 탐색 능력, 임계 하이퍼 파라미터에 대한 최적값을 찾고 훨씬 더 짧은 시간이 걸리기 때문에 Random Search 사용. (Random Search: 하이퍼 파라미터의 무작위 조합을 사용하여 모델에 가장 적합한 하이퍼 파라미터 세트를 찾는 기술)

    <center><img class="img-fluid" src="/img/posts/210701Figure12.png" alt="Demo Image" width="300" height="300" ></center>
    <span class="caption text-muted">Table 4 Initialized values and optimal hyperparameters values of random search of model</span>

    

### 4. Performance measure and Results

```
classification_report
- 정밀도(Precision): 클래스에 속한다고 출력한 샘플 중 실제로 양성 클래스에 속하는 샘플 수의 비율
- 재현율(Recall): 실제 양성 클래스에 속한 표본 중에 양성 클래스에 속한다고 출력한 표본의 수의 비율
- f1-score: 정밀도와 재현율의 가중조화평균(weight harmonic average)
- Accuracy: 전체 샘플 중 맞게 예측한 샘플 수의 비율
```

<center><img class="img-fluid" src="/img/posts/210701Figure2.png" alt="Demo Image" width="300" height="300" ></center>

<center><img class="img-fluid" src="/img/posts/210701Figure3.png" alt="Demo Image" width="300" height="300" ></center>
<span class="caption text-muted">Table 5 Accuracy of classifier models with different hyperparameters’ sets on testing dataset</span>

Table 5 Accuracy of classifier models with different hyperparameters’ sets on testing dataset

<center><img class="img-fluid" src="/img/posts/210701Figure4.png" alt="Demo Image" width="300" height="300" ></center>
<span class="caption text-muted">Table 6 Resulted precision, recall, and f1-score for each customer class of best model</span>
