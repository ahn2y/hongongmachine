# 혼자 공부하는 머신러닝

## 01-3 마켓과 머신러닝

### 생선 분류 문제
30cm 이상이면 도미
```PYTHON:01-3
if fish_lenght >= 30:
  print("도미")
```

###### 도미 데이터 준비하기
```
bream_length = [25.4, 26.3, 26.5, 29.0, 29.0, 29.7, 29.7, 30.0, 30.0, 30.7, 31.0, 31.0, 31.5, 32.0, 32.0, 32.0, 33.0, 33.0, 33.5, 33.5, 34.0, 34.0, 34.5, 35.0, 35.0, 35.0, 35.0, 36.0, 36.0, 37.0, 38.5, 38.5, 39.5, 41.0, 41.0]
bream_weight = [242.0, 290.0, 340.0, 363.0, 430.0, 450.0, 500.0, 390.0, 450.0, 500.0, 475.0, 500.0, 500.0, 340.0, 600.0, 600.0, 700.0, 700.0, 610.0, 650.0, 575.0, 685.0, 620.0, 680.0, 700.0, 725.0, 720.0, 714.0, 850.0, 1000.0, 920.0, 955.0, 925.0, 975.0, 950.0]
```
리스트에서 첫 번째 도미의 길이는 25.4cm, 무게는 242.0g이고 두 번째 도미의 길이는 26.3cm, 무게는 290.0g과 같은 식이다. 이런 특징을 특성이라 부른다.
두 특성을 숫자로 보는 것보다 그래프로 표현하면 데이터를 잘 이해할 수 있고 앞으로 할 작업에 대한 힌트를 얻을 수도 있다.
