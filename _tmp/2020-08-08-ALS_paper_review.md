---
layout: post
title: ALS Paper_review
date : 25 Jul 2020
category : Paper_review
comments : true
---
# Collaborative Filtering for Implicit Feedback Datasets

## 0. Abstract
 : 추천 시스템의 기본적ㅇ니 목표는 사용자가 과거에 생성한 암시적인 피드백 정보를 활용하여 개인화된 추천을 제공해주는 것입니다. 그러나, like & dislike가 명확히 표현되어 있지 않은 데이터에 있어서는 사용자가 어떤 아이템을 싫어하는지를 판단하는 것은 쉬운일이 아니게 됩니다.
 때문에 이 논문에서 제시하는 방법론은, 다양한 신뢰 수준(confidence level)에서 긍정과 부정적 선호를 다루고자 합니다. 이는 특히 긍정&부정 선호가 명확하지 않은 Implicit Feedback Datasets에서 중요한 모델로 활용됩니다.


## 1. Introduction
#### 1) Contents Based
 : 영화의 장르, 감독, 배우, 흥행도 등을 사용해 유사한 작품군을 생성하고, 이를 기반하여 추천 모델을 구축합니다. 그러나 위와 같은 자세한 데이터 자체를 구축하기가 현실적으로 여렵다는 문제를 갖고 있습니다.

#### 2) CF(Collaborative Filtering)
 : 선호가 남아있지 않은 user와 item간의 관계를 파악하기 위해, '고객 유사도'와 '아이템 유사도'를 계산합니다. 과거 거래내역 또는 평가 데이터를 활용하며, 정확도 또한 앞서 Contents Based보다 뛰어나 가장 많이 활용되는 방법입니다.

#### 3) Implicit Data 특징
 : Implicit data는 구매이력, 검색이력, 마우스 클릭 등의 선호가 명확하게 표현되어있지않은 데이터를 말합니다. Implicit data의 주요 특징은 몇가지를 살펴보면 아래와 같습니다.
  - **(1) No Negative feedback**
  : 구매하지 않은 데이터는, 선호하지 않은 것이지 혹은 해당 아이템의 존재를 알지 못한 것인지 알 수 없음.

  - **(2) Implict feedback is inferently noisy**
  : 소비내역을 토대로 '선호' 아이템이라고 단정 지을 수 없습니다. 구매 이후에 해당 제품에 대해서 만족하지 못했을 가능성이 존재.

  - **(3) 명시적 수치 = 선호 / 암시적 수치 = 신뢰성**  
  : 암시적 데이터는 명확하게 선호와 비선호를 확인할 수는 없지만, 단순 binary가 아닌, 수치값으로 동일한 데이터를 중복해서 구매 했다면, 이는 높은 신뢰수준에서 선호.

  - **(4) Evaluation**  
  : explicit data는 MSE를 활용해 선호가 존재하는 데이터에 한하여 정확도를 비교할 수 있으나, implicit data에서는 0으로 남아있는 비구매 데이터를 제외하지 않으며 이를 구매하지 않았다고 싫어한다고 이야기 할 수 없어 단순 MSE를 사용하기 어렵.



## 2. Preliminaries
 - users : u, v
 - items : i, j
 - $r_ui$ : number of times u purchased item


## 3. Previous work
#### 1) Latent factor model
 : 대표적 잠재 요인 모델인 SVD모델은 "유저-유저 잠재요인"과 "아이템-아이템 잠재요인" 행렬을 생성하고, 이 두 행렬을 내적하여 예측결과를 제공합니다.  

 - $x_u$ : user(u) & user factor($x_u$)
 - $y_i$ : item(i) & item factor($y_i$)
 - $\hat r_{ui} = x^T_u y_i$

 **object**
<center>$min_{xy} r_{ui} \sum (r_{ui} - x^T_u y_i)^2 + \lambda(||x_u||^2 + ||y_i||^2)$</center>

: 명시적 데이터 셋에서는 선호가 남아있는 값에 한하여 MSE를 진행하고, 과적합을 피하기 위해에 정규화항을 두었습니다. 이때  $\lambda$ 는 정규화를 위해 사용되는 파라미터로 SGD(stochastic gradient descent)를 활용해 계산합니다.










#### Refernce
[1] [Yifan Hu et al. Collaborative Filtering for Implicit Feedback](http://www.Datasetshttp://yifanhu.net/PUB/cf.pdf)
