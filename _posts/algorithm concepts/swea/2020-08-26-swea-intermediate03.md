---
layout: single
title: "2-2 : 정렬 (2)"
excerpt: "대표적인 정렬 방식 소개 - 선택 정렬"
categories: 
- Computer Science
- Algorithm Concepts
tags:
- SWEA
- Selection Sort
---
## 정렬 (2)

### 셀렉션 알고리즘

- 저장된 자료로부터 k번째로 크거나 작은 원소를 찾는 방법
- 최소값, 최대값 혹은 중간값을 찾을 수 있는 알고리즘
- 시간복잡도 - O(kn)

<br>

#### 1. k번째로 작은 원소 찾기

```python
# python 예시 - 셀렉션 알고리즘(1): k번째로 작은 원소 찾기

def SelectionMin(lst, k):
    local = lst
    times = 0
    
    for i in range(len(local)-1):
        idx = i
        for j in range(i+1, len(local)):
            if local[idx] > local[j]:
                idx = j
        local[i], local[idx] = local[idx], local[i]
        times += 1
        if times == k:
            break
    
    return local[k-1]


lst = [4, 9, 11, 23, 2, 19, 7]
print(SelectionMin(lst, 3))

# 출력
>>> 7
```

<br>

#### 2. k번째로 큰 원소 찾기

```python
# python 예시 - 셀렉션 알고리즘(2): k번째로 큰 원소 찾기

def SelectionMax(lst, k):
    local = lst
    
    for i in range(k):
        minidx = i
        for j in range(i+1, len(lst)):
            if lst[minidx] < lst[j]:
                minidx = j
        local[minidx], local[i] = local[i], local[minidx]
    
    return local[k-1]
    
lst = [4, 9, 11, 23, 2, 19, 7]
print(SelectionMax(lst, 3))  

# 출력
>>> 11
```

<br>

<br>

### <strong>선택 정렬</strong>

* 자료 내에서 가장 작은 값의 원소부터 차례대로 정렬하는 방식
* 셀렉션 알고리즘을 전체 자료에 적용함
  * 자료 내의 최소값을 찾은 후 그 값을 리스트의 맨 앞의 값과 바꿔준다. 이후 남은 리스트에 대해서 같은 작업을 반복한다.
* 시간복잡도 - O(n<sup>2</sup>)

<br>

#### 1. 반복문을 이용한 선택 정렬

```python
# python 예시 - 선택 정렬(1): 반복문

def SelectionSort(lst):
    result = lst
    idx = 0
    for i in range(len(lst) - 1):
        for j in range(i, len(lst)):
            if result[idx] > result[j]:
                idx = j
        result[i], result[idx] = result[idx], result[i]

    return result

lst = [4, 9, 11, 23, 2, 19, 7]
print(SelectionSort(lst))

# 출력
>>> [2, 4, 7, 9, 11, 19, 23]
```

<br>

#### 2. 재귀를 이용한 선택 정렬

```python
# python 예시 - 선택 정렬(2): 재귀

def SelectionSort(lst, k): # 위치 k부터 정렬
    if k == len(lst) :
        return
    idx = k
    for i in range(k+1, len(lst)):
        if lst[k] > lst[i]:
            idx = i
    lst[idx], lst[k] = lst[k], lst[idx]
    return SelectionSort(lst, k+1)

a = [4, 9, 11, 23, 2, 19, 7]
SelectionSort(a, 0)
print(a)

# 출력
>>> [2, 7, 9, 11, 4, 19, 23]
```

<br>

<br>

<br>

<br>

출처: SW Expert Academy - Learn - Course - Programming Intermediate

[SW Expert Academy - Programming Intermediate course](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDN86AAXw5UW6)