---
layout: single
title: "5 : 검색"
excerpt: "순차 검색, 이진 검색"
categories: 
- Computer Science
- Algorithm Concepts
tags:
- SWEA
- Sequential Search
- Binary Search
---
## 검색

### 1. <strong>순차 검색</strong>

- 일렬로 나열된 자료를 순차적으로 검색하는 방법.
- 정렬된 자료를 검색
- 시간복잡도 - O(n)

<br>

#### a. 정렬되지 않은 자료의 검색

```python
# python 예시 - 순차 검색(1): 정렬되지 않은 자료의 검색

def seq(lst, key):
    for i in range(len(lst)):
        if key == lst[i]:
            return '{0}번째'.format(i+1)
    return '검색 실패'

lst = [4, 9, 11, 23, 2, 19, 7]
print(seq(lst, 2))
print(seq(lst, 10))

# 출력
>>> 5번째
>>> 검색 실패
```

<br>

#### b. 정렬된 자료의 검색

```python
# python 예시 - 순차 검색(2): 정렬된 자료의 검색

def seq2(lst, key):
    for i in range(len(lst)):
        if key == lst[i]:
            return '{0}번째'.format(i+1)
        elif key > lst[i]:
            continue
        else:
            return '검색 실패, 멈춘 단계: {0}'.format(i + 1)
    return '검색 실패'

lst2 = [2, 4, 7, 9, 11, 19, 23]
print(seq2(lst2, 2))
print(seq2(lst2, 10))
print(seq2(lst2, 33))

# 출력
>>> 1번째
>>> 검색 실패, 멈춘 단계: 5
>>> 검색 실패
```

<br>

<br>

### 2. <strong>이진 검색</strong>

- 정렬된 자료를 검색
- 자료의 가운데 값과 찾고자 하는 값을 비교하여 다음 검색의 위치를 정하는 방식
- 시간복잡도 - O(logn)

```python
# python 예시 - 이진 검색

def binarysearch(lst, key):
    s = 0
    e = len(lst) - 1

    while s <= e:
        m = (s + e) // 2
        if lst[m] == key:
            return '{0}번째'.format(m+1)
        elif lst[m] < key:
            s = m+1
        else:
            e = m-1

    return '없습니다'

lst = [2, 4, 7, 9, 11, 19, 23]
print(binarysearch(lst, 2))
print(binarysearch(lst, 10))

# 출력
>>> 1번째
>>> 없습니다
```

<br>

<br>

<br>

<br>

출처: SW Expert Academy - Learn - Course - Programming Intermediate

[SW Expert Academy - Programming Intermediate course](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDN86AAXw5UW6)

