---
layout: single
title: "11 : 분할 정복 (Divide and Conquer)"
excerpt: "분할 정복 소개 및 응용"
categories: 
- Computer Science
- Algorithm Concepts
tags:
- SWEA
- Divide and Conquer
- Quick Sort
---
## 분할 정복 (Divide and Conquer)

### <strong>분할 정복 알고리즘</strong>

- 분할 (Divide): 문제를 여러 개의 자식 문제로 나눈다.
- 정복 (Conquer): 더이상 작은 부분으로 나눌 수 없게 되면 나눈 작은 부분을 각각 해결한다.
- 통합 (Combine): (필요하다면) 각각 해결한 답을 모은다.

<br>

<br>

### 응용1. 거듭 제곱 알고리즘

- a<sup>n</sup>을 구하려고 할 때 a를 n번 곱하는 방법으로 a의 n 거듭제곱을 구할 수 있다. 
  - 시간복잡도: O(n)
- a<sup>n</sup> = (a<sup>n/2</sup>)<sup>2</sup> = (a<sup>n/4</sup>)<sup>2</sup>)<sup>2</sup> 와 같은 식을 사용하여 절반씩 나누고 그 결과값을 구한 뒤 곱해준다.
  - 시간복잡도: O(logn)

```python
# python 예시 - 분할 정복(1): 거듭 제곱 알고리즘

def Power(num, n):
    global cnt1
    cnt1 += 1
    if n == 0: return 1
    return num * Power(num, n-1)

def Power_DC(num, n):
    global cnt2
    cnt2 += 1
    if n // 2:
        prev = Power_DC(num, n//2)
        if n & 1: return prev * prev * num
        else: return prev * prev
    else:
        if n & 1: return num
        else: return 1

cnt1 = 0
print(Power(2, 3))
print(f'세는 횟수: {cnt1}')
cnt1 = 0
print(Power(2, 10))
print(f'세는 횟수: {cnt1}')

cnt2 = 0
print(Power_DC(2, 3))
print(f'세는 횟수: {cnt2}')

cnt2 = 0
print(Power_DC(2, 10))
print(f'세는 횟수: {cnt2}')

# 출력
8
세는 횟수: 4 
1024
세는 횟수: 11 # 이까지 Power(num, n)
8
세는 횟수: 2 
1024
세는 횟수: 4 # 이까지 Power_DC(num, n)
```

<br>

<br>

### 응용2. 퀵 정렬

- 기준점(pivot)을 만들어서 그 값보다 작은 값, 큰 값들을 나눈다. 이 작업을 더이상 작은 값과 큰 값으로 나눌 수 없을 때까지 진행하여 각각 정렬을 진행하고, 그 결과 값을 합친다.
- 최악의 경우 시간 복잡도: O(n<sup>2</sup>) - 합병정렬에 비해 좋지못함
  --> 하지만 평균적으로 시간 복잡도가 <strong>O(nlogn)</strong>이다.

![퀵 정렬의 시간복잡도](https://i.ibb.co/gPC9Cj8/quicksort.jpg)

```python
# python 예시 - 분할 정복(2-1): 퀵 정렬(Quick Sort) <1>

def Quick(inplst):
    lst = inplst[:]
    pivot = lst[0]
    left = []
    right = []
    pivots = []

    for char in lst:
        if char < pivot: left.append(char)
        elif char == pivot: pivots.append(char)
        else: right.append(char)
    
    if len(inplst) <= 2:
        return left + pivots + right
    
    if not left and not right:
        return pivots
    elif not left:
        return pivots + Quick(right)
    elif not right:
        return Quick(left) + pivots

    return Quick(left) + pivots + Quick(right)

target = [3, 5, 8, 1, 2, 9, 4, 7, 6]
print(Quick(target))

# 출력
>>> [1, 2, 3, 4, 5, 6, 7, 8, 9]

```


  - 이 코드는 함수를 호출할 때마다 리스트를 생성하므로 메모리 공간을 많이 쓴다는 단점이 생긴다.

  ```python
  # python 예시 - 분할 정복(2-2): 퀵 정렬(Quick Sort) <2>
  
  def Quick(lst, start, end):
      if start >= end: return
      pivot = start
      L = start + 1
      R = end
  
      # 1 ----------------
      while L < R:        
          while L <= R and lst[L] < lst[pivot]: L += 1
          while L <= R and lst[R] >= lst[pivot]: R -= 1
          if L < R:
              lst[L], lst[R] = lst[R], lst[L]
      # 1 ----------------
      
      # 2 ----------------
      if lst[R] <= lst[pivot]:
          lst[R], lst[pivot] = lst[pivot], lst[R]
          pivot = R
      # 2 ----------------
      
      # 3 ----------------
      Quick(lst, start, pivot - 1)
      Quick(lst, pivot + 1, end)
      # 3 ----------------
  
  target = [3, 5, 8, 1, 2, 9, 4, 7, 6]
  Quick(target, 0, len(target)-1)
  print(target)
  
  # 출력
  >>> [1, 2, 3, 4, 5, 6, 7, 8, 9]
  ```

  - 새로 리스트를 생성하지 않고 이미 존재하는 리스트 내부에서 값을 바꿔주는 방식이므로 메모리 공간을 낭비하지 않고 정렬할 수 있다.
  
    - 1번 블록: Pivot 값보다 작은 것들 // 크거나 같은 것들로 분류
    
      ![1번블록](https://i.ibb.co/ZWbgn6v/quickcode1.jpg)
    
    - 2번 블록: Pivot 값보다 작은 것들 중 가장 마지막으로 찾은 것과 Pivot을 바꿈
      ![2번블록](https://i.ibb.co/pL0dSVf/quickcode2.jpg)
    
    - 3번 블록: Pivot 값보다 작은 것으로 분류된 묶음 // 크거나 같은 것으로 분류된 묶음에 대해 각각 동일한 작업 실행
      ![3번블록](https://i.ibb.co/mS3WT6F/quickcode3.jpg)

<br>

<br>

<br>

<br>


출처: SW Expert Academy - Learn - Course - Programming Intermediate

[SW Expert Academy - Programming Intermediate course](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDN86AAXw5UW6)