---
layout: single
title: "2-3 : 정렬 (3)"
excerpt: "대표적인 정렬 방식 소개 - 퀵 정렬, 삽입 정렬, 병합 정렬"
categories: 
- Computer Science
- Algorithm Concepts
tags:
- SWEA
- Quick Sort
- Insertion Sort
- Merge Sort
---
## 정렬 (3)

### <strong>퀵 정렬</strong>

- 분할 정복 알고리즘 활용
- 기준점(pivot)을 만들어서 그 값보다 작은 값, 큰 값들을 나눈다. 이 작업을 더이상 작은 값과 큰 값으로 나눌 수 없을 때까지 진행하여 각각 정렬을 진행하고, 그 결과 값을 합친다.
- 평균적으로 시간 복잡도가 O(nlogn)이다.

```python
# python 예시 - 퀵 정렬

def Quick(inplst):
    if not inplst: return []
    lst = inplst[:]
    pivot = lst[0]
    left = []
    right = []
    pivots = []

    for char in lst:
        if char < pivot: left.append(char)
        elif char == pivot: pivots.append(char)
        else: right.append(char)
    
    if len(inplst) == 2:
        return left + pivots + right
    elif len(inplst) == 3:
        if len(left) == 2: return Quick(left) + pivots
        elif len(right) == 2: return pivots + Quick(right)
    
    if len(left) == 1: return left + pivots + Quick(right)
    elif len(right) == 1: return Quick(left) + pivots + right

    return Quick(left) + pivots + Quick(right)

target = [69, 10, 30, 2, 16, 8, 31, 22]
print(Quick(target))


# 출력
>>> [2, 8, 10, 16, 22, 30, 31, 69]
```

<br>

<br>

### <strong>삽입 정렬</strong>

- 정렬되지 않은 원소들의 집합에서 원소를 하나씩 꺼내 정렬된 집합에 끼워넣는 방식의 정렬
- 시간복잡도 - O(n<sup>2</sup>)

```python
# python 예시 - 삽입 정렬

lst = [69, 10, 30, 2, 16, 8, 31, 22]

for i in range(1, len(lst)):
    idx = i
    while idx >= 0:
        if idx == 0:
            lst.insert(0, lst.pop(i))
        elif lst[idx-1] <= lst[i]:
            lst.insert(idx, lst.pop(i))
            break
        idx -= 1

print(lst)

# 출력
>>> [2, 8, 10, 16, 22, 30, 31, 69]
```

<br>

<br>

### <strong>병합 정렬</strong>

- 분할 정복 알고리즘 활용
- 정렬이 끝난 두 개의 수열을 병합하는 방식으로 정렬
- 시간복잡도 - O(nlogn)

```python
# python 예시 - 병합 정렬

def MergeSort(lst):
    half = len(lst) // 2
    if len(lst) == 1:
        return lst
    elif len(lst) == 2:
        if lst[0] > lst[1]:
            lst[0], lst[1] = lst[1], lst[0]
        return lst
    else:
        resultlst = []
        lst1 = MergeSort(lst[:half])
        lst2 = MergeSort(lst[half:])
        i, j = -len(lst1), -len(lst2)
        while i < 0 or j < 0:
            if i == 0:
                resultlst.append(lst2[j])
                j += 1
            elif j == 0:
                resultlst.append(lst1[i])
                i += 1
            else:
                if lst1[i] < lst2[j]:
                    resultlst.append(lst1[i])
                    i += 1
                else:
                    resultlst.append(lst2[j])
                    j += 1
        return resultlst

lst = [69, 10, 30, 2, 16, 8, 31, 22]
print(MergeSort(lst))

# 출력
>>> [2, 8, 10, 16, 22, 30, 31, 69]
```

<br>

<br>

<br>

<br>

출처: SW Expert Academy - Learn - Course - Programming Intermediate

[SW Expert Academy - Programming Intermediate course](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDN86AAXw5UW6)