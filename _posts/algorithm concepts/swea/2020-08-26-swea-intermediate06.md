---
layout: single
title: "3-2 : 2차원 List (2)"
excerpt: "2차원 배열 - 전치행렬"
categories: 
- Computer Science
- Algorithm Concepts
tags:
- SWEA
- 2-D Array
---
## 2차원 List (2)

### 전치행렬 

- i,j 성분이 j,i성분으로 바뀐 행렬이다. 2차원 리스트로 구현하면 다음과 같다.

#### a. 새로운 2차원 List에 할당하여 만드는 방법

```python
# python 예시 - 전치행렬(1): 새로운 2차원 List에 할당

A = [['{0:2d}'.format(i) for i in range(j, j+5)] for j in range(1, 26, 5)]

for i in range(5):
    print(*A[i])

transA = [[0 for i in range(5)] for j in range(5)]

for i in range(5):
    for j in range(5):
        transA[j][i] = A[i][j]

for _ in range(5):
    print(*transA[_])

# 출력
 1  2  3  4  5
 6  7  8  9 10
11 12 13 14 15
16 17 18 19 20
21 22 23 24 25 # A
 1  6 11 16 21
 2  7 12 17 22
 3  8 13 18 23
 4  9 14 19 24
 5 10 15 20 25 # transA
```

<br>

#### b. 기존 List에서 자리 재배치 하는 방법

```python
# python 예시 - 전치행렬(2): 기존 List에서 자리 재배치

A = [['{0:2d}'.format(i) for i in range(j, j+5)] for j in range(1, 26, 5)]

for i in range(5):
    print(*A[i])

for i in range(5):
    for j in range(i):
        A[i][j], A[j][i] = A[j][i], A[i][j]

for i in range(5):
    print(*A[i])

# 출력
 1  2  3  4  5
 6  7  8  9 10
11 12 13 14 15
16 17 18 19 20
21 22 23 24 25 # A
 1  6 11 16 21
 2  7 12 17 22
 3  8 13 18 23
 4  9 14 19 24
 5 10 15 20 25 # 변경 후 A
```

<br>

#### c. 내장함수 zip을 사용하는 방법

```python
# python 예시 - 전치행렬(3): zip 함수 사용
  
A = [['{0:2d}'.format(i) for i in range(j, j+5)] for j in range(1, 26, 5)]
  
for i in range(5):
    print(*A[i])
  
transA = list(zip(*A))
  
for i in range(5):
    print(*transA[i])
  
# 출력
 1  2  3  4  5
 6  7  8  9 10
11 12 13 14 15
16 17 18 19 20
21 22 23 24 25 # A
 1  6 11 16 21
 2  7 12 17 22
 3  8 13 18 23
 4  9 14 19 24
 5 10 15 20 25 # transA
```



zip 함수를 통해 A의 각 행이 언패킹되어 zip 함수의 인자로 들어간다.

다시 zip함수에 의해 패킹된 요소는 튜플 형식으로 transA에 들어간다.



```python
# python 예시 - zip 함수 요소 형태
  
A = [['{0:2d}'.format(i) for i in range(j, j+5)] for j in range(1, 26, 5)]
  
for i in range(5):
    print(*A[i])
      
transA = list(zip(*A))
  
print(transA)
  print(type(transA[0]))
  
# 출력
>>> [(' 1', ' 6', '11', '16', '21'), (' 2', ' 7', '12', '17', '22'), (' 3', ' 8', '13', '18', '23'), (' 4', ' 9', '14', '19', '24'), (' 5', '10', '15', '20', '25')]
>>> <class 'tuple'>
```

<br>

<br>

<br>

<br>

출처: SW Expert Academy - Learn - Course - Programming Intermediate

[SW Expert Academy - Programming Intermediate course](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDN86AAXw5UW6)