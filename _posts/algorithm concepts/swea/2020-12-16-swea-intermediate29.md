---
layout: single
title: "15-4 : 트리 (4) - Heap (힙)"
excerpt: "힙 소개 및 힙을 이용한 우선순위 큐 구현"
categories: 
- Computer Science
- Algorithm Concepts
tags:
- SWEA
- Tree
- Heap
- Priority Queue
---
## 트리 (4)

### 1. <strong>힙이란? (Heap)</strong>

- 완전 이진 트리에 있는 노드 중 값이 가장 큰 노드나 가장 작은 노드를 찾기 위해 만들어진 자료구조
- 우선순위 큐를 구현할 때 사용된다.
- 최대 힙, 최소 힙이 있다.
    - 최대 힙 (Max Heap): 부모 노드의 값 > 자식 노드의 값, 루트 노드는 최대값을 갖는다.
    - 최소 힙 (Min Heap): 부모 노드의 값 < 자식 노드의 값, 루트 노드는 최소값을 갖는다.

<br>

<br>

### 2. <strong>힙의 연산</strong> 

- 최대 힙과 최소 힙은 자료구조 내의 원소 배치만 다르고 연산 과정은 같다.
  최소 힙의 연산 과정을 예시로 살펴보자.

#### a. 삽입 연산

1. 삽입할 자리를 확보하여 원소를 삽입한다.
2. 부모 노드와 비교하여 삽입한 원소가 더 작으면 부모 노드와 자리를 바꾼다.
3. 더이상 비교할 부모 노드가 없을 때까지 2번의 과정을 반복한다.

#### b. 삭제 연산

- 힙의 삭제 연산은 루트 노드의 원소를 삭제하는 것이다.
- 따라서 힙의 종류에 따라 최대값 혹은 최소값을 구할 수 있다.

1. 루트 노드를 삭제한다.
2. 가장 마지막 노드를 루트 노드의 위치로 이동한다.
3. 자식 노드 중 더 작은 쪽과 해당 노드를 교환한다.
4. 교환이 발생되지 않을 때까지 3번의 과정을 반복한다.

<br>

<br>

### 3. <strong>힙을 사용한 우선순위 큐 구현</strong>

- 파이썬 표준 라이브러리 중 heapq를 사용했다.

```python
# python 예시 - 힙: 우선순위 큐

from heapq import heappush, heappop
# 리스트를 힙처럼 사용할 수 있게 하는 함수들이다.

h = []
recipe = [
    (4, '베이컨을 볶는다.'),
    (2, '파기름을 낸다.'),
    (3, '파기름에 계란을 볶는다.'),
    (6, '먹는다.'),
    (1, '대파와 베이컨을 잘게 썬다.'),
    (5, '찬밥을 넣고 볶는다.'),
]

for i in recipe:
    print(i)
print('-------------------------------')
for j in recipe:
    heappush(h, j)

for k in recipe:
    print(heappop(h))
    
# 출력
(4, '베이컨을 볶는다.')
(2, '파기름을 낸다.')
(3, '파기름에 계란을 볶는다.')
(6, '먹는다.')
(1, '대파와 베이컨을 잘게 썬다.')
(5, '찬밥을 넣고 볶는다.')
-------------------------------
(1, '대파와 베이컨을 잘게 썬다.')
(2, '파기름을 낸다.')
(3, '파기름에 계란을 볶는다.')
(4, '베이컨을 볶는다.')
(5, '찬밥을 넣고 볶는다.')
(6, '먹는다.')
```

<br>

<br>

<br>

<br>

출처: SW Expert Academy - Learn - Course - Programming Intermediate

[SW Expert Academy - Programming Intermediate course](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDN86AAXw5UW6)

