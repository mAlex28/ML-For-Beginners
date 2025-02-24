# 머신러닝의 기술

머신러닝 모델과 이를 사용하는 데이터를 구축, 사용, 그리고 관리하는 프로세스는 많은 타 개발 워크플로우와 매우 다른 프로세스입니다. 이 강의에서, 프로세스를 이해하고, 알아야 할 주요 기술을 간단히 설명합니다:

- 머신러닝을 받쳐주는 프로세스를 고수준에서 이해합니다.
- 'models', 'predictions', 그리고 'training data'와 같은 기초 개념을 탐색합니다.
  
## [강의 전 퀴즈](https://gentle-hill-034defd0f.1.azurestaticapps.net/quiz/7/)

## 소개

고수준에서, 머신러닝 (ML) 프로세스를 만드는 기술은 여러 단계로 구성됩니다:

1. **질문 결정하기**. 대부분 ML 프로세스는 간단 조건 프로그램 또는 룰-베이스 엔진으로 대답할 수 없는 질문을 하는 것으로 시작합니다. 이 질문은 가끔 데이터 셋을 기반으로 한 예측을 중심으로 진행됩니다.
2. **데이터 수집 및 준비하기**. 질문에 대답하려면, 데이터가 필요합니다. 데이터의 품질과, 때때로, 양에 따라 초기 질문에 잘 대답할 수 있는 지 결정됩니다. 데이터 시각화는 이 측면에서 중요합니다. 이 단계에서 데이터를 훈련과 테스트 그룹으로 분할하여 모델을 구축하는 게 포함됩니다.
3. **학습 방식 선택하기**. 질문과 데이터의 특성에 따라, 데이터를 가장 잘 반영하고 정확한 예측을 할 수 있게 훈련하는 방법을 선택해야 합니다. 특정 전문 지식과, 지속적으로, 많은 실험이 필요한 ML 프로세스의 일부분입니다.
4. **모델 학습하기**. 학습 데이터로, 다양한 알고리즘을 사용하여 데이터의 패턴을 인식하게 모델을 학습시킵니다. 모델을 더 좋게 만들기 위하여 데이터의 특정 부분을 타 부분보다 먼저 하도록 조정할 수 있도록 내부 가중치를 활용할 수 있습니다.
5. **모델 평가하기**. 수집한 셋에서 이전에 본 적 없는 데이터 (테스트 데이터)로 모델의 성능을 확인합니다.
6. **파라미터 튜닝하기**. 모델의 성능을 기반해서, 모델 학습으로 알고리즘의 동작을 컨트롤하는 다른 파라미터, 또는 변수를, 사용해서 프로세스를 다시 실행할 수 있습니다.
7. **예측하기**. 모델의 정확성을 새로운 입력으로 테스트합니다.

## 물어볼 질문하기

컴퓨터는 데이터에서 숨겨진 패턴 찾는 것을 잘합니다. 유틸리티는 조건-기반 룰 엔진을 만들어서 쉽게 답할 수 없는 도메인에 대해 질문하는 연구원에게 매우 도움이 됩니다. 예를 들어서, actuarial 작업이 주어지면, 데이터 사이언티스트는 흡연자와 비흡연자의 사망률에 대하여 수작업 룰을 작성할 수 있습니다.

많은 다른 변수가 방정식에 포함되면, ML 모델이 과거 건강기록을 기반으로 미래 사망률을 예측하는 데에 효율적이라고 검증할 수 있습니다. 유쾌한 예시로 위도, 경도, 기후 변화, proximity to the ocean, 제트 기류의 패턴을 포함한 데이터 기반으로 주어진 위치에서 4월의 날씨를 예측하는 것입니다.

✅ 날씨 모델에 대한 [slide deck](https://www2.cisl.ucar.edu/sites/default/files/2021-10/0900%20June%2024%20Haupt_0.pdf)은 날씨 분석에서 ML을 사용한 역사적 관점을 제공합니다.

## 작업 사전-구축하기

모델을 만들기 전에, 완료해야 할 몇가지 작업이 더 있습니다. 질문을 테스트하고 모델 예측을 기반으로 가설 구성하려면, 여러 요소를 식별하고 구성해야 합니다.

### 데이터

어떠한 종류의 질문을 대답하려면, 올바른 타입의 데이터가 필요합니다. 이 포인트에서 필요한 두 가지가 있습니다:

- **데이터 수집**. 데이터 분석의 공정도를 설명한 이전 강의를 기억하고, 데이터를 조심히 수집합니다. 데이터의 출처와, 내재적 편견을 알고, 출처를 문서화합니다.
- **데이터 준비**. 데이터 준비 프로세스는 여러 단계가 있습니다. 데이터가 다양한 소스에서 제공되는 경우에는 정렬하고 노멀라이즈해야 할 수 있습니다. ([Clustering](../../../5-Clustering/1-Visualize/README.md)과 같이) 문자열을 숫자로 바꾸는 방식처럼 다양한 방식을 통하여 데이터의 품질과 양을 향상시킬 수 있습니다. ([Classification](../../../4-Classification/1-Introduction/README.md)과 같이) 원본 기반으로, 새로운 데이터를 생성할 수 있습니다. ([Web App](../../../3-Web-App/README.md) 강의 이전처럼) 데이터를 정리하고 변경할 수 있습니다. 마지막으로, 훈련하는 기술에 따라서, 무작위로 섞어야 할 수 있습니다.

✅ 데이터를 수집하고 처리하면, 그 모양이 의도한 질문을 해결할 수 있는 지 잠시 봅니다. [Clustering](../../5-Clustering/1-Visualize/README.md) 강의에서 본 것처럼, 데이터가 주어진 작업에서 잘 수행하지 못할 수 있습니다!

### Features와 타겟

feature는 데이터의 측정할 수 있는 속성입니다. 많은 데이터셋에서 'date' 'size' 또는 'color'처럼 열 제목으로 표현합니다. 일반적으로 코드에서 X로 보여지는 feature 변수는, 모델을 훈련할 때 사용되는 입력 변수로 나타냅니다.

타겟은 예측하려고 시도한 것입니다. 코드에서 X로 표시하는 보통 타겟은, 데이터에 물어보려는 질문의 대답을 나타냅니다: 12월에, 어떤 색의 호박이 가장 쌀까요? San Francisco 근처의 좋은 토지 실제 거래가는 어디인가요? 가끔은 타겟을 라벨 속성이라고 부르기도 합니다.

### feature 변수 선택하기

🎓 **Feature Selection과 Feature Extraction** 모델을 만들 때 선택할 변수를 어떻게 알 수 있을까요? 가장 성능이 좋은 모델에 올바른 변수를 선택하기 위하여 Feature Selection 또는 Feature Extraction 프로세스를 거치게 됩니다. 그러나, 같은 내용이 아닙니다: "Feature extraction creates new features from functions of the original features, whereas feature selection returns a subset of the features." ([source](https://wikipedia.org/wiki/Feature_selection))

### 데이터 시각화하기

데이터 사이언티스트의 툴킷에서 중요한 측면은 Seaborn 또는 MatPlotLib과 같이 여러가지 뛰어난 라이브러리로 데이터 시각화하는 파워입니다. 데이터를 시각화로 보여주면 숨겨진 correlations를 찾아서 활용할 수 있습니다. ([Classification](../../../4-Classification/2-Classifiers-1/README.md)에서 발견한대로) 시각화는 편향적이거나 균형적이지 않은 데이터를 찾는 데 도움이 될 수 있습니다.

### 데이터셋 나누기

훈련하기 전, 데이터를 잘 나타낼 크기로 2개 이상의 데이터 셋을 나눌 필요가 있습니다.

- **학습**. 데이터셋의 파트는 모델을 학습할 때 적당합니다. 이 셋은 본 데이터셋의 대부분을 차지합니다.
- **테스트**. 테스트 데이터셋은 독립적인 데이터의 그룹이지만, 미리 만들어진 모델의 성능을 확인할 때에, 가끔 본 데이터에서도 수집됩니다.
- **검증**. 검증 셋은 모델을 개선하며 모델의 hyperparameters, 또는 architecture를 튜닝할 때, 사용하는 작은 독립된 예시 그룹입니다. ([Time Series Forecasting](../../../7-TimeSeries/1-Introduction/README.md)에서 언급하듯) 데이터의 크기와 질문에 따라서 세번째 셋을 만들 이유가 없습니다.

## 모델 구축하기

훈련하고 있는 데이터를 사용하여, **학습**할 다양한 알고리즘으로, 모델 또는, 데이터의 통계적 표현을 만드는 게 목표입니다. 모델을 학습하면서 데이터에 노출되면 발견, 검증, 그리고 승인하거나 거부되는 perceived patterns에 대하여 가설을 세울 수 있습니다.

### 학습 방식 결정하기

질문과 데이터의 특성에 따라서, 어떻게 학습할 지 선택합니다. [Scikit-learn's documentation](https://scikit-learn.org/stable/user_guide.html)을 - 이 코스에서 - 단계별로 보면 모델이 학습하는 많은 방식을 찾을 수 있습니다. 숙련도에 따라서, 최고의 모델을 만들기 위하여 다른 방식을 해볼 수 있습니다. 데이터 사이언티스트가 볼 수 없는 데이터를 주고 정확도, 편향적, 품질-저하 이슈를 점검해서, 현재 작업에 가장 적당한 학습 방식을 선택하여 모델의 성능을 평가하는 프로세스를 거치게 될 예정입니다.

### 모델 학습하기

훈련 데이터로 감싸면, 모델을 만들 'fit'이 준비 되었습니다. 많은 ML 라이브러리에서 'model.fit' 코드를 찾을 수 있습니다. - 이 순간에 값의 배열 (보통 'X')과 feature 변수 (보통 'y')로 데이터를 보내게 됩니다.

### 모델 평가하기

훈련 프로세스가 완료되면 (큰 모델을 훈련하기 위해서 많이 반복하거나 'epochs'가 요구), 테스트 데이터로 모델의 성능을 측정해서 품질을 평가할 수 있습니다. 데이터는 모델이 이전에 분석하지 않았던 본 데이터의 서브셋입니다. 모델의 품질에 대한 지표 테이블을 출력할 수 있습니다.

🎓 **모델 피팅**

머신러닝의 컨텍스트에서, 모델 피팅은 친근하지 않은 데이터를 분석하려고 시도하는 순간에 모델 기본 기능의 정확도를 보입니다.

🎓 **Underfitting** 과 **overfitting**은 모델 핏이 충분하지 않거나 너무 많을 때, 모델의 품질이 낮아지는 일반적인 이슈입니다. 이러한 이유는 모델이 훈련 데이터와 너무 근접하게 얼라인되거나 너무 느슨하게 얼라인된 예측을 합니다. overfit 모델은 데이터의 디테일과 노이즈를 너무 잘 배웠기에 훈련 데이터로 너무나 잘 예측합니다. underfit 모델은 훈련 데이터 또는 아직 볼 수 없던 데이터를 잘 분석할 수 없으므로 정확하지 않습니다.

![overfitting model](../images/overfitting.png)
> Infographic by [Jen Looper](https://twitter.com/jenlooper)

## 파라미터 튜닝

초반 훈련이 마무리 될 때, 모델의 품질을 살펴보고 'hyperparameters'를 트윅해서 개선하는 것을 고려합니다. [in the documentation](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-tune-hyperparameters?WT.mc_id=academic-15963-cxa) 프로세스에 대하여 알아봅니다.

## 예측

완전히 새 데이터로 모델의 정확도를 테스트할 수 있는 순간입니다. 프로덕션에서 모델을 쓰기 위해서 웹 어셋을 만들며, '적용한' ML 세팅에, 프로세스는 변수를 설정하고 추론하거나, 평가하고자 사용자 입력(예를 들면, 버튼 입력)을 수집해 모델로 보낼 수 있습니다.

이 강의에서는, 'full stack' ML 엔지니어가 되기 위하여 여행을 떠나는 과정이며, 이 단계에 - 데이터 사이언티스트의 모든 제스쳐가 있으며 준비, 빌드, 테스트, 평가와 예측 방식을 보게 됩니다.

---

## 🚀 도전

ML 실무자의 단계를 반영한 플로우를 그려보세요. 프로세스에서 지금 어디에 있는 지 보이나요? 어려운 내용을 예상할 수 있나요? 어떤게 쉬울까요?

## [강의 후 퀴즈](https://gentle-hill-034defd0f.1.azurestaticapps.net/quiz/8/)

## 검토 & 자기주도 학습

일상 업무를 이야기하는 데이터 사이언티스트 인터뷰를 온라인으로 검색합니다. 여기 [one](https://www.youtube.com/watch?v=Z3IjgbbCEfs) 있습니다.

## 과제

[Interview a data scientist](../assignment.md)
