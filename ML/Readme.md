# ML

* 머신러닝이란?
* 학습
  * supervised(지도학습)
  * unsupervised(비지도학습)
* regression
  * regression 이란?
  * Linear regression
  * logsitic regression
* classification
  * classification 이란?
  * 



## 머신러닝이란?

일종의 software (프로그래밍) 종류중에 하나 (explicit programming)

스팸필터, 자율주행 같은 software를  개발한다고 하면 여러가지 변수에 대해 규칙을 정해줘야 한다. 하지만 이것들을 프로그래밍하지 않고 데이터 또는 패턴을 가지고 자동적으로 학습 하는 것으로 목표로 생겨났다. 

**간단하게 말하면 개발자가 규칙들을 세워 만드는 것이 아니라, 특정 데이터의 패턴과 규칙들을 학습하여 자동적으로 처리할수 있는 시스템을 말한다.**



## 학습

**Supervised Learning(지도학습)**

정해져 있는 데이터(labeled 들이 정해져있음 ) - trainset

label 를 보고 학습하여  특정 testset 에 대해서 label 을 예측

**Unsupervised Learning(비지도학습)**

하나하나 label 을 줄수 없는 경우

**데이터를 보고 스스로 학습한다 는 개념**

ex) Google news grouping , Word clustering



## Linear regression

어떤 변수에 다른 변수들이 주는 영향력을 선형적으로 분석하는 방법을 선형 회귀분석이라고 한다.



선형 회귀분석을 하기 위해서는 우선 선형회귀 모델(linear regression model)을 만들어야 하며, 여기서 말하는 모델은 **수학식으로 표현되는 함수**를 의미하는데 영향을 주는 변수와 영향을 받는 변수로 구성되어 있다. 

영향을 주는 변수는 **독립변수(independent variable)** 또는 **설명변수(explanatory variable)** 등으로 불린다. (x)

영향을 받는 변수는 **종속변수(dependent variable)** 또는 **반응변수(response variable)** 등으로 불린다. (yhat)

1. 선형회귀 종류
   * 단변량 선형회귀 모델 : 종속변수가 1개일때
   * 다변량 선형회귀 모델 : 종속 변수가 2개 이상일때
   * 단순 선형 회귀 모델 : 독립변수가 1개일때
   * 다중 선형 회귀 모델 : 독립변수가 2개일때
   * 단변량 다중 선형 회귀모델 : 종속변수 1개 독립변수 2개이상
   * 다변량 다중 선형 회귀모델 : 종속 변수와 독립변수 모두 2개 이상일때

![image-20200809171715532](C:\Users\s_m04\AppData\Roaming\Typora\typora-user-images\image-20200809171715532.png)

2. 매개 변수 학습 방법 : minimize the cost function

   * **Cost Function(비용함수)**

     * Cost Function 이란 **데이터셋** 과 어떤 **가설함수(Hypothesis)** 와의 오차를 계산하는 함수이다. Cost Function의 결과가 작을수록 데이터셋에 더 적합한 **가설함수(Hypothesis)** 라는 의미이며 궁극적인 목표는 **Global Minimun**을 찾는 것이다.

     * 일반적으로 linear regression 의 가설함수(Hypothesis) 식은 `Wx+b` 의 식으로 정의되며 `W`는 **가중치**, `x` 는 **데이터** , `b`는 **절편** 이고.

     * 가설함수의 기반하여 cost 함수는 다음과 같이 정의할수 있다.

       ![image-20200810165706049](https://lh3.googleusercontent.com/proxy/0w8Mweuwke4IgGUdtdHGfTEZ3QhrCYXXyI_IIj95Ur65pmOet7pW5-cdCvry7e0Xvzb2YiJmGPVIN8HJOfv-cvWj1iACEWHoj3SwygCgoij8BpwinBmLk5A4HS_XebGZ06vmIBfpc142vEOUGhx4Wtha5VyCJylaobomMv_-5NTdF_0Qrtp78WPb4FYwPSQ6TBtJ7nai3ONdfyQajpAdNmXKmvZLLrEYBWhd1wEsrKGo2ySnj9XdafosyYjzZcQQF2q4eqhdnA83TJ9aKNGxCQ6mYCHMMbPktn3hfjPIfkTzsHg2wAZZ_mwhC_6-xle_KLWs1QpokzOJMvBHkNQkbekV8rjrFpE9mieHA_8bVtuNjWT8OjRgwRsHBQkcqRejm93urek)

     * 학습은 W 와 b 의 값을 변화하면서 제일 작은cost 값을 찾아 가게되는데 이때 사용된 알고리즘이 **Gradient Descent algorithm** 이다

   * **Gradient Descent Algorithm(경사하강법)**

     ![image-20200810170413629](https://cdn-images-1.medium.com/max/600/1*iNPHcCxIvcm7RwkRaMTx1g.jpeg)

     * 경사도에 따라 내려가는 것으로 learning step 에 따라 한번 움직일때 learning step 만큼 내려가며 Minimum 한 값을 찾아내게 된다.
     * **어느 방향에서 시작해도 상관이 없이 최저점에 도달할수 있으며, 미분을 통해 경사도를 구해서 방향을 정하게 된다.**

     ![image-20200810170822394](https://wikidocs.net/images/page/21670/%EB%AF%B8%EB%B6%84.PNG)

3. Regularization (정규화)

   * 정규화란 : 회귀계수가 가질수 있는 값에 제약조건을 부여하는 방법이다.미래데이터에 대한 오차의 기대값은 모델의 Bias와 variance로 분해할수 있는 **정규화는 variance를 감소시켜 일반화 성능을 높이는 기법**이다.

   > Overfit 을 방지하는 역할

   * 일반 선형회귀 모델은 종소변수(y)의 실제값과 모델의 예측값 사이의 **평균제곱오차(Mean Square Error)** 를 최소화 하는 회귀 계수들의 집합을 가리키는 이러한 회귀계수를 뽑는데 쓰는 기법을 **최소자승법(Least Squares Method)** 라 한다.

   

   **L1(Lasso Regression)** : 특정 계수를 0으로 축소하여 `변수 선택을 수행` 할 수 있다.

   L2 (릿지회귀)와 동일하지만 L1norm을 제약한다는 점이 다르다. 

   ```text
   β^Lasso=minβ{(y−Xβ)T(y−Xβ)+λ∥β∥1}
   ```

   요소 개수가 p 개인 회귀계수 벡터B의 L1norm 은 각 요소에 절대값을 취한 뒤 모두 더해 구한다.

   ```text
    ∥β∥1=∑i=1p|βi|
   ```

   L1norm 은 미분이 불가능하기 때문에 Lasso회귀의 경우 해를 단박에 구할수 없다. 그렇기 때문에 numerial 기법들이 다양하게 제시됨

   

   **라쏘회귀의 기하학적 이해**

   찾아야 하는 최적 회귀계수 벡터 B를 [B1,B2]라고 두고, 그림으로 나타냈을때 다음과 같다.

   ![image-20200810172849635](http://i.imgur.com/xsa2fNQ.png)

   MSE가 동일한 [B1,B2]의 자취는 타원이다. 제약식은 L1norm(절대값)을 썼기 때문에 L2norm 이 동일한 [B1,B2]의 자취는 마름모 꼴이 된다.

   파란색 마름모 꼴의 제약 범위 내에서 MSE가 최소인 점은 B2축 위의 검정색 점인데 이점은 바로 B1=0 인 지점이다. B1이 0이라는 이야기는 그에 대응하는 독립변수 X1이 예측에 중요하지 않다는 말과 같다.

   이처럼 라쏘 회귀는 예측에 중요하지 않은 변수의 회귀계수를 감소시킴으로써 **변수선택(Feature Selection) 하는 효과**를 나타낸다.

   

   **L2(Ridge regression)** : 동일한 비율로 모든 계수를 축소한다. **거의 항상 L1을 능가하는 성과를 보인다.**

   평균제곱오차(MSE)를 최소화 하면서 회귀계수 벡터B의 L2norm을 제한하는 기법이다. 선형회귀 모델의 목적식(MSE최소화)과 회귀계수들에 대한 제약식을 함께 쓰면 다음과 같은데 여기서  **λ는 제약을 얼마나 강하게 걸지 결정해주는 값**으로 사용자가 지정하는 **하이퍼파라메터** 이다.

   ```text
   β^Ridge=argminβ{(y−Xβ)T(y−Xβ)+λβTβ}
   ```

   릿지회귀의 해인 회귀계수 벡터 B는 위 식을 B로 미분한 식을 0으로 높고 풀면 명시적으로 구할수 있다.

   ```text
   β^Ridge=(XTX+λI)−1XTy
   ```

   **평균제곱오차뿐 아니라 B의 L2norm또한 최소화 하는 것이 릿지 회귀의 목적이다**

   <img src="http://i.imgur.com/8qnLAnf.png" alt="image-20200810175314331" style="zoom:50%;" />

   MSE 기준으로는 벡터 B의 첫번째 요소 B1과 두번째 요소 B2가 각각 4,5 여야 최소가 된다. 일반 선형회귀 모델이라면 (4,5)가 회귀계수로 결정되지만

    β1^2+B2^2 이 30 이하라는 제약조건을 가한다면 표의 상단 3개는 제외도 나머지 3개가운데 MSE가 최소인 (2,4)를 회귀계수로 결정하게 된다.

   이 방법이 릿지 회귀의 방식이다.



​		**릿지회귀의 기하학적 이해**

​		우리가 찾아야 하는 최적 회귀계수 벡터 B를 [B1,B2]라고 두면 평균제곱오차		를 식으로 했을때 다음과 같다

```text
MSE(β1,β2)==∑i=1n(yi−β1xi1−β2xi2)2(∑i=1nx2i1)β21+(∑i=1nx2i2)β22+2(∑i=1nxi1xi2)β1β2−2(∑i=1nyixi1)β1−2(∑i=1nyixi2)β2+∑i=1ny2i
```

이식으로 보면 MSE는 형태의 **원추곡선(Conic equation)**이 된다. 타원,쌍곡선,원,포물선은 원추곡선의 특수한 경우에 해당하는데 판별식 B2 - 4AC이 0보다 작으면 타원 형태가 된다고 합니다. 위 식에서 판별식을 계산해 보면 **코시-슈바르츠 부등식** 조건에 의해 0 이하가 된다.

따라서 MSE가 같은 [B1,B2] 의 자취를 그려보면 타원 모양이 된다.

![image-20200810180356298](http://i.imgur.com/RBxwo0D.png)

좌측상단 그림에서 타원 모양의 녹색 실선은 MSE가 동일한 [B1,B2]의 자취이다 B^LS라고 표시된 검정색 점은 일반 선형회귀 모델의 결과로, MSE가 최소가 되는 지점이다. 여기에서 멀리 떨어져 있는 타원일수록 MSE가 점점 커진다고 생각하면 된다. 또한 파란색 원은 B의 L2 norm이 동일한 [B1,B2]의 자취인데 원의 반지름이 작아질수록 L2 norm이 감소하고, 그만큼 제약이 커진다고 이해하면 된다.

하이퍼파라메터 λ가 클수록 B의 L2norm 이 줄어들게 된다.



**엘라스틱넷**

엘라스틱넷은 제약식에 L1, L2 norm을 모두 쓰는 기법이다. 목적식과 제약식을 한번에 쓰면 다음과 같다.

```text
β^enet=minβ{(y−Xβ)T(y−Xβ)+λ1∥β∥1+λ2βTβ}
```

**릿지회귀 vs 라쏘회쉬 vs 엘라스틱넷**

|   구분   |              릿지회귀              |            라쏘회귀            |              엘라스틱넷               |
| :------: | :--------------------------------: | :----------------------------: | :-----------------------------------: |
|  제약식  |              L2 norm               |            L1 norm             |              L1+L2 norm               |
| 변수선택 |               불가능               |              가능              |                 가능                  |
| solution |            closed form             |          명시해 없음           |              명시해 없음              |
|   장점   | 변수간 상관관계가 높아도 좋은 성능 | 변수간 상관관계가 높으면 성능↓ |    변수간 상관관계를 반영한 정규화    |
|   특징   |  크기가 큰 변수를 우선적으로 줄임  | 비중요 변수를 우선적으로 줄임  | 상관관계가 큰 변수를 동시에 선택/배제 |



## Logistic regression

