---
layout: single
title: "17 : 완전 검색 - 조합적 문제"
excerpt: "순열과 조합을 이용한 완전 탐색"
categories: 
- Algorithm Concepts
tags:
- SWEA
- Permutation
- Combination
- Subset
- Bitmask
---
## 완전 검색 - 조합적 문제

### 1. 순열

- 순서화된 요소들의 집합에서 최선의 방법을 찾는 것과 관련됨
- 사전식 순서, 최소 변경을 통한 방법 등으로 순열을 만들어낼 수 있다.
- 최소 변경을 통해 순열을 생성하는 대표적인 알고리즘
  - Johnson-Trotter 알고리즘
- 파이썬의 라이브러리를 활용한 순열

  ```python
  import itertools
  mylist = [1,2,3]
  result = itertools.permutations(mylist) 
  # (mylist, 3), r 생략시 기본값 리스트 크기
  print(list(result))
  # 출력
  [(1, 2, 3), (1, 3, 2), (2, 1, 3), (2, 3, 1), (3, 1, 2), (3, 2, 1)]
  ```

- 파이썬의 라이브러리를 활용한 중복순열

  ```python
  import itertools
  mylist = [1,2,3]
  result = itertools.product(mylist, repeat=3)
  print(list(result))
  # 출력
  [(1, 1, 1), (1, 1, 2), (1, 1, 3), (1, 2, 1), (1, 2, 2), (1, 2, 3), 
   (1, 3, 1), (1, 3, 2), (1, 3, 3), (2, 1, 1), (2, 1, 2), (2, 1, 3),
   (2, 2, 1), (2, 2, 2), (2, 2, 3), (2, 3, 1), (2, 3, 2), (2, 3, 3),
   (3, 1, 1), (3, 1, 2), (3, 1, 3), (3, 2, 1), (3, 2, 2), (3, 2, 3),
   (3, 3, 1), (3, 3, 2), (3, 3, 3)]
  ```


<br>

<br>

### 2. 부분집합

- 원소들의 그룹에서 최적의 부분 집합을 찾는 것과 관련됨
- 비트 열을 이용한 부분집합 생성

  ```python
  arr = [2, 3, 4, 5]
  
  for i in range(1 << len(arr)): 
      # 0000, 0001, ... , 1110, 1111 까지 모든 수를 포함
      for j in range(len(arr)): # 이진수(i)의 각 자리 수를 순회
          if i & (1 << j): # i의 j번째 비트가 1인 경우
              print(arr[j], end=',') # arr의 j번째 원소 출력
      print()
      
  # 출력
  		#0000
  2,		#0001
  3,		#0010
  2,3,		#0011
  4,		#0100
  2,4,		#0101
  3,4,		#0110
  2,3,4,		#0111
  5,		#1000
  2,5,		#1001
  3,5,		#1010
  2,3,5,		#1011
  4,5,		#1100
  2,4,5,		#1101
  3,4,5,		#1110
  2,3,4,5,	#1111
  ```

  ```python
  # list comprehension
  arr = [2, 3, 4, 5]
  
  for i in range(1 << len(arr)):
      print([arr[j] for j in range(len(arr)) if i & (1 << j)])
      
  # 출력
  []
  [2]
  [3]
  [2, 3]
  [4]
  [2, 4]
  [3, 4]
  [2, 3, 4]
  [5]
  [2, 5]
  [3, 5]
  [2, 3, 5]
  [4, 5]
  [2, 4, 5]
  [3, 4, 5]
  [2, 3, 4, 5]
  ```


<br>

<br>

### 3. 조합

- 파이썬의 라이브러리를 활용한 조합

  ```python
  import itertools
  mylist = [1,2,3]
  result = itertools.combinations(mylist, r=2) # r 생략 불가
  print(list(result))
  # 출력 
  [(1, 2), (1, 3), (2, 3)]
  ```

- 파이썬의 라이브러리를 활용한 중복조합

  ```python
  import itertools
  mylist = [1,2,3]
  result = itertools.combinations_with_replacement(mylist, r=2) # r 생략 불가
  print(list(result))
  # 출력
  [(1, 1), (1, 2), (1, 3), (2, 2), (2, 3), (3, 3)]
  ```


<br>

<br>

<br>

<br>

출처: SW Expert Academy - Learn - Course - Programming Advanced

[SW Expert Academy - Programming Advanced Course](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDYSqAAbw5UW6)

