# 혼자 공부하는 머신러닝

## 01-3 마켓과 머신러닝

### 생선 분류 문제
30cm 이상이면 도미
```PYTHON:01-3
if fish_lenght >= 30:
  print("도미")
```

###### 도미 데이터 준비하기
```Python: 손코딩
bream_length = [25.4, 26.3, 26.5, 29.0, 29.0, 29.7, 29.7, 30.0, 30.0, 30.7, 31.0, 31.0, 31.5, 32.0, 32.0, 32.0, 33.0, 33.0, 33.5, 33.5, 34.0, 34.0, 34.5, 35.0, 35.0, 35.0, 35.0, 36.0, 36.0, 37.0, 38.5, 38.5, 39.5, 41.0, 41.0]
bream_weight = [242.0, 290.0, 340.0, 363.0, 430.0, 450.0, 500.0, 390.0, 450.0, 500.0, 475.0, 500.0, 500.0, 340.0, 600.0, 600.0, 700.0, 700.0, 610.0, 650.0, 575.0, 685.0, 620.0, 680.0, 700.0, 725.0, 720.0, 714.0, 850.0, 1000.0, 920.0, 955.0, 925.0, 975.0, 950.0]
```
리스트에서 첫 번째 도미의 길이는 25.4cm, 무게는 242.0g이고 두 번째 도미의 길이는 26.3cm, 무게는 290.0g과 같은 식이다. 이런 특징을 특성이라 부른다.<br>
두 특성을 숫자로 보는 것보다 그래프로 표현하면 데이터를 잘 이해할 수 있고 앞으로 할 작업에 대한 힌트를 얻을 수도 있다. <br>

길이를 x축으로 하고 무게를 y축으로 정해 각 도미를 그래프에 점으로 표시할 수 있다.<br>
이런 그래프를 산점도라고 부른다.

파이썬에서 과학계산용 그래프를 그리는 대표적인 패키지는 맷플롯립이다. 이 패키지를 임포트하고 산점도를 그리는 scatter() 함수를 사용할 수 있다. 임포트란 따로 만들어둔 파이썬 패키지를 사용하기 위해 불러오는 명령이다.
'''
import matplotlib.pyplot as plt

plt.scatter(bream_length, bream_weight)
plt.xlabel('length')
plt.ylabel('weight')
plt.show()
```
2개의 특성을 사용해 그린 그래프이기 때문에 2차원 그래프라고 말한다.<br>
산점도 그래프가 일직선에 가까운 형태로 나타나는 경우를 선형적이라고 말한다.

###### 빙어 데이터 준비하기
```
smelt_length = [9.8, 10.5, 10.6, 11.0, 11.2, 11.3, 11.8, 11.8, 12.0, 12.2, 12.4, 13.0, 14.3, 15.0]
smelt_weight = [6.7, 7.5, 7.0, 9.7, 9.8, 8.7, 10.0, 9.9, 9.8, 12.2, 13.4, 12.2, 19.7, 19.9]
```

맷플롯립에서 2개의 산점도를 한 그래프로 그릴 수 있다.
```
plt.scatter(bream_length, bream_weight)
plt.scatter(smelt_length, smelt_weight)
plt.xlabel('length')
plt.ylabel('weight')
plt.show()
```
맷플롯립은 2개의 산점도를 색깔로 구분해서 나타낸다.<br>
빙어의 산점도도 선형적이지만 도미에 비해 무게가 길이에 영향을 덜 받는다는 걸 그래프로 알 수 있다.


### 첫 번쨰 머신러닝 프로그램
k-최근접 이웃 알고리즘을 사용해 도미와 빙어 데이터를 구분한다.<br>
k-최근접 이웃 알고리즘을 사용하기 전에 앞서 준비했던 도미와 빙어 데이터를 하나의 데이터로 합친다.
```
length = bream_length + smelt_length
weight = bream_weight + smelt_weight
```
이 책에서 사용하는 머신러닝 패키지는 사이킷런이다. 이 패키지를 사용하려면 각 특성의 리스트를 세로 방향으로 늘어뜨린 2차원 리스트를 만들어야 한다.<br>
2차원 리스트로 만드는 가장 쉬운 방법은 파이썬의 zip() 함수와 리스트 내포 구문을 사용하는 것이다.
```
fish_data = [[l,w] for l,w in zip(length, weigth)]
```
이런 리스트를 2차원 리스트 혹은 리스트의 리스트라고 부른다.<br>
컴퓨터를 위해 도미와 빙어를 숫자 1과 0으로 표현하면 첫 번째 생선은 도미이므로 1이고 마지막 생선은 빙어이므로 0이 된다.
```
fish_target = [1] * 35 + [0] * 14
'''
이제 사이킷런 패키지에서 k-최근접 이웃 알고리즘을 구현한 클래스인 KNeighborsClassifier를 임포트한다.
```
from sklearn.neighbors import KNeighborsClassifier
kn = KNeighborsClassifier()
```
이 객체에 fish_data와 fish_target을 전달하여 도미를 찾기 위한 기준을 학습시킨다.<br>
이런 과정을 머신러닝에서는 훈련이라고 부른다. 사이킷런에서는 fit() 메서드가 이런 역할을 한다.
```
kn.fit(fish_data, fish_target)
kn.score(fish_data, fish_target)
```
fit() 메서드는 주어진 데이터로 알고리즘을 훈련한다.<br>
사이킷런에서 모델을 평가하는 메서드는 score() 메서드이다. 이 메서드는 0에서 1 사이의 값을 반환한다.<br>
이 값을 정확도라고 부른다. 즉 이 모델은 정확도가 100%이며 도미와 빙어를 완력하게 분류했다는 뜻이다.

###### k-최근접 이웃 알고리즘
k-최근접 이웃 알고리즘은 어떤 데이터에 대한 답을 구할 때 주위의 다른 데이터를 보고 다수를 차지하는 것을 정답으로 사용한다.
```
kn.predict([[30, 600]])
```
predict() 메서드는 새로운 데이터의 정답을 예측한다.<br>
이 메서드도 fit() 메서드와 마찬가지로 리스트의 리스트를 전달해야 한다.<br>
새로운 데이터에 대해 예측할 때는 가장 가까운 직선거리에 어떤 데이터가 있는지를 살피면 된다.<br>
단점은 k-최근접 이웃 알고리즘의 특징 때문에 데이터가 크면 메모리가 많이 필요하고 직선거리를 계산하는 데 많은 시간이 필요하다.
