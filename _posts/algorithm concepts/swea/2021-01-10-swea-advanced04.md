---
layout: single
title: "19 : 분할 정복"
excerpt: "분할 정복 소개 및 활용 예시"
categories: 
- Algorithm Concepts
tags:
- SWEA
- Divide and Conquer
- Merge Sort
- Quick Sort
---
## 분할 정복

### 1. 분할 정복 알고리즘이란?

1. 분할 (Divide)
   - 해결할 문제를 여러 개의 작은 문제들로 분할
2. 정복 (Conquer)
   - 나눈 작은 문제를 각각 해결
3. 통합 (Combine)
   - 필요하다면 해결된 해답을 모음

- 분할 정복 기법은 문제를 나누어 정복하여 통합하는 흐름의 **Top-down** 방식을 취한다.

<br>

<br>

### 2. 분할 정복 활용 사례

- 병합 정렬
- 퀵 정렬
- 최근접점의 쌍 문제
  - 2차원 평면상의 n개의 점이 입력으로 주어질 때, 거리가 가장 가까운 한 쌍의 점을 찾는 문제.

<br>

#### a. 병합 정렬

- 시간복잡도: O(nlogn)

1. 최소 크기의 부분집합으로 나눈다.
2. 2개의 부분집합을 정렬하면서 하나의 집합으로 병합한다. 
   - 1개의 집합이 남을 때까지 반복한다.

```python
# 병합 정렬
def mergesort(arr):
    if len(arr) == 1: return arr
    mid = len(arr) // 2
    left = mergesort(arr[:mid])
    right = mergesort(arr[mid:])
    result = []
    i = j = 0
    while not (i == len(left) and j == len(right)):
        if i == len(left):
            result.append(right[j])
            j += 1
        elif j == len(right):
            result.append(left[i])
            i += 1
        elif left[i] >= right[j]:
            result.append(right[j])
            j += 1
        else:
            result.append(left[i])
            i += 1
    return result


a = [69, 10, 30, 2, 16, 8, 7, 31, 22]
b = mergesort(a)
print(b)

# 출력
[2, 7, 8, 10, 16, 22, 30, 31, 69]
```

<br>

#### b. 퀵 정렬

- 시간복잡도: O(nlogn), 최악의 경우 O(n<sup>2</sup>)
  - 최악의 경우가 생기는 건 데이터들이 정렬되어 있는 경우이다. (역순으로 정렬될 때 포함)
    - randomized quicksort를 통해 최악의 경우를 피할 수 있다. (피봇을 무작위로 정하는 방법)
  - 일반적으로 O(nlogn)의 복잡도를 가지는 다른 정렬 알고리즘보다도 수행 시간이 빠르다.
    - cache-efficiency: 퀵 정렬은 별도의 저장공간이 필요 없다.
- 병합 정렬과 다른 부분: 각 부분 정렬이 끝난 후 병합하는 작업이 필요 없다.

<br>

##### i. Hoare 파티션 알고리즘

- 정렬하고자 하는 집합의 첫번째 원소를 피봇으로 한다.
- 피봇 값보다 큰 값들은 오른쪽, 작은 값들은 왼쪽 집합에 모은다.
- 피봇을 두 집합의 가운데에 위치시킨다.
- 모두 정렬될 때까지 위의 작업을 반복한다.

```python
# 퀵 정렬 - Hoare 파티션
def partition(arr, s, e):
    pivot = arr[s]
    i = s + 1
    j = e
    while i <= j:
        while i <= j and arr[i] <= pivot: i += 1
        while i <= j and arr[j] >= pivot: j -= 1
        if i < j: 
        # i와 j가 교차하기 전에는 i는 pivot보다 큰 값, 
        # j는 pivot보다 작은 값을 가리키게 된다.
            arr[i], arr[j] = arr[j], arr[i]
        # i와 j가 교차하게 되면 그 지점을 중심으로 왼쪽엔 pivot보다 작은 값, 
        # 오른쪽엔 pivot보다 큰 값이 모인다.
    arr[s], arr[j] = arr[j], arr[s] # pivot을 그 경계에 집어넣는다.
    return j

def quicksort(arr, s, e):
    pivot = partition(arr, s, e)
    if s < pivot-1:
        quicksort(arr, s, pivot-1)
    if e > pivot:
        quicksort(arr, pivot+1, e)


a = [69, 10, 30, 2, 16, 8, 7, 31, 22]
quicksort(a, 0, len(a)-1)
print(a)

# 출력
[2, 7, 8, 10, 16, 22, 30, 31, 69]
```

<br>

##### ii. Lomuto 파티션 알고리즘

- 정렬하고자 하는 집합의 마지막 원소를 피봇으로 한다.
- i는 시작위치 -1, j는 시작위치부터 피봇 바로 앞의 원소까지 순회하도록 한다.
  - i가 가리키는 것은 피봇보다 작은 원소들의 집합의 가장 마지막 원소이고, 
    j가 가리키는 것은 피봇보다 큰 원소들의 집합의 가장 마지막 원소이다.
- j가 가리키는 값이 피봇보다 작을 때 i를 1 증가하고 i번째 값과 j번째 값을 교환한다.
- 피봇을 두 집합의 가운데(i+1)에 위치시킨다.
- 모두 정렬될 때까지 위의 작업을 반복한다.

```python
# 퀵 정렬 - Lomuto 파티션
def partition(arr, s, e):
    pivot = arr[e]
    i = s - 1
    for j in range(s, e):
        if arr[j] < pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]
    arr[i+1], arr[e] = arr[e], arr[i+1]
    return i+1

def quicksort(arr, s, e):
    pivot = partition(arr, s, e)
    if s < pivot-1:
        quicksort(arr, s, pivot-1)
    if e > pivot:
        quicksort(arr, pivot+1, e)


a = [69, 10, 30, 2, 16, 8, 7, 31, 22]
quicksort(a, 0, len(a)-1)
print(a)

# 출력
[2, 7, 8, 10, 16, 22, 30, 31, 69]
```

<br>

<br>

<br>

<br>

출처: SW Expert Academy - Learn - Course - Programming Advanced

[SW Expert Academy - Programming Advanced Course](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDYSqAAbw5UW6)

