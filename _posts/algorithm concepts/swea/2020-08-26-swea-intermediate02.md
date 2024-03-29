---
layout: single
title: "2-1 : 정렬 (1)"
excerpt: "대표적인 정렬 방식 소개 - 버블 정렬, 카운팅 정렬"
categories: 
- Computer Science
- Algorithm Concepts
tags:
- SWEA
- Bubble Sort
- Counting Sort
---
## 정렬 (1)

### 대표적인 정렬 방식의 종류

- 버블 정렬 (Bubble Sort)
- 카운팅 정렬 (Counting Sort)
- 선택 정렬 (Selection Sort)
- 퀵 정렬 (Quick Sort)
- 삽입 정렬 (Insertion Sort)
- 병합 정렬 (Merge Sort)

<br>

* 시간 복잡도 높은 순서

  n! > 2<sup>n</sup> > n<sup>2</sup> > nlogn > n > logn > 1

  ![big O 시간 복잡도](https://upload.wikimedia.org/wikipedia/commons/thumb/7/7e/Comparison_computational_complexity.svg/768px-Comparison_computational_complexity.svg.png)

<br>

<br>

### <strong>버블 정렬</strong>

* 인접한 두 개의 원소를 비교하며 자리를 계속 교환하는 방식.
* 시간복잡도 - O(n<sup>2</sup>)

```python
# python 예시 - 버블 정렬

def Bubblesort(a):
    for i in range(len(a)-1, 0, -1):
        for j in range(0, i):
            if a[j] > a[j+1]:
                a[j], a[j+1] = a[j+1], a[j]

A = [132, 2, 12, 13 ,1, 9]
a = [0, 4, 1, 3, 1, 2, 4, 1]
Bubblesort(A)
Bubblesort(a)
print(A)
print(a)

# 출력
>>> [1, 2, 9, 12, 13, 132]
>>> [0, 1, 1, 1, 2, 3, 4, 4]
```

<br>

<br>

### <strong>카운팅 정렬</strong>

- 항목들의 순서를 결정하기 위해 집합에 각 항목이 몇 개씩 있는지 세는 작업을 하여, 선형 시간에 정렬하는 효율적인 알고리즘.
  - 정수나 정수로 표현할 수 있는 자료에 대해서만 적용 가능. 각 항목의 발생 회수를 기록하기 위해, 정수 항목으로 인덱스 되는 카운트들의 리스트를 사용하기 때문.

- 시간복잡도 - O(n+k) : n은 리스트의 개수, k는 정수의 최대값

```python
# python 예시 - 카운팅 정렬

def CountingSort(lst, maxn): # lst라는 리스트 내에서 maxn까지의 값을 정렬
    temp = [] # 정렬 가능한 리스트
    temp2 = [] # 남은거반환
    cnt = [0] * (maxn+1)
    
    for i in range(len(lst)):
        if lst[i] <= maxn:
            cnt[lst[i]] += 1
            temp.append(lst[i])
        else:
            temp2.append(lst[i])
    
    for j in range(1, len(cnt)):
        cnt[j] = cnt[j] + cnt[j-1]
    
    result = [0] * len(temp)
    for k in temp:
        cnt[k] -= 1
        result[cnt[k]] = k
    result.extend(temp2)
    
    return result


A = [132, 2, 13, 12 ,1, 9]
a = [0, 4, 1, 3, 1, 2, 4, 1]
print(CountingSort(A, 150)) # A 리스트 내에서 150 이내의 값을 정렬
print(CountingSort(a, 5))	# a 리스트 내에서 5 이내의 값을 정렬
print(CountingSort(A, 12))	# A 리스트 내에서 12 이내의 값을 정렬

# 출력
>>> [1, 2, 9, 12, 13, 132]
>>> [0, 1, 1, 1, 2, 3, 4, 4]
>>> [1, 2, 9, 12, 132, 13]
```

<br>

<br>

<br>

<br>

출처: SW Expert Academy - Learn - Course - Programming Intermediate

[SW Expert Academy - Programming Intermediate course](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDN86AAXw5UW6)