---
layout: single
title: "4 : 부분집합"
excerpt: "부분 집합의 수를 구하거나 원하는 부분 집합을 구하는 방법"
categories: 
- Computer Science
- Algorithm Concepts
tags:
- SWEA
- Subset
---
## 부분 집합

### 1. 부분 집합 개요 및 비트연산

- 부분 집합의 수
  - 집합의 원소가 n개일 때, 공집합을 포함하면 부분 집합의 수는 2<sup>n</sup>개
  - 집합의 각 원소를 부분 집합에 (포함하는 / 포함하지 않는) 2가지 경우를 모두 고려한 것
  - 비트 연산을 통해 부분 집합의 수를 고려하는 알고리즘을 만들 수 있다.

<br>

- 유용한 비트연산
  - 1 << n 	== 	2<sup>n</sup>  		=> 모든 부분 집합의 수를 구할 때 사용 가능
  - n&1                                => 홀,짝 판별 (n이 홀수라면 1을 반환)
  - i & (1<<j)                        => i~j번째 비트가 1인지 아닌지를 판별

<br>

<br>

### 2. 비트 연산을 활용하여 부분 집합 구하기

#### a. 1부터 5까지 정수의 부분 집합

```python
# python 예시 - 1부터 5까지의 정수의 부분집합을 출력

nums = range(1,6)
idx = len(nums)

for i in range(1 << idx):
    temp = []
    for j in range(idx):
        if i & (1<<j):
            temp.append(nums[j])
    print(temp)
    
# 출력
[]
[1]
[2]
[1, 2]
[3]
[1, 3]
[2, 3]
[1, 2, 3]
[4]
[1, 4]
[2, 4]
[1, 2, 4]
[3, 4]
[1, 3, 4]
[2, 3, 4]
[1, 2, 3, 4]
[5]
[1, 5]
[2, 5]
[1, 2, 5]
[3, 5]
[1, 3, 5]
[2, 3, 5]
[1, 2, 3, 5]
[4, 5]
[1, 4, 5]
[2, 4, 5]
[1, 2, 4, 5]
[3, 4, 5]
[1, 3, 4, 5]
[2, 3, 4, 5]
[1, 2, 3, 4, 5]
```

<br>

#### b. 부분집합의 합이 10이 되는 부분 집합

```python
# python 예시 - 부분집합의 합이 10이 되는 부분집합 출력

nums = range(1,6)
idx = len(nums)

for i in range(1 << idx):
    temp = []
    for j in range(idx):
        if i & (1<<j):
            temp.append(nums[j])
    if sum(temp) == 10:
        print(*temp)
        
# 출력
1 2 3 4
2 3 5
1 4 5
```

<br>

<br>

<br>

<br>

출처: SW Expert Academy - Learn - Course - Programming Intermediate

[SW Expert Academy - Programming Intermediate course](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDN86AAXw5UW6)

