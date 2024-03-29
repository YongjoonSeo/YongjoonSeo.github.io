---
layout: single
title: "14-2 : 연결 리스트 (2) - 정렬"
excerpt: "연결 리스트를 이용한 정렬 - 삽입 정렬, 병합 정렬"
categories: 
- Computer Science
- Algorithm Concepts
tags:
- SWEA
- Linked List
- Insertion Sort
- Merge Sort
---
## 연결 리스트 (Linked List) (2) 

### 1. <strong>삽입 정렬</strong>

- 정렬되지 않은 원소들의 집합에서 원소를 하나씩 꺼내 정렬된 집합에 끼워넣는 방식의 정렬
- 시간복잡도 - O(n<sup>2</sup>)

```python
# python 예시 - 삽입 정렬(1): list로 구현

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

```python
# python 예시 - 삽입 정렬(2): 14-1 연결 리스트(1)에서 구현한 연결 리스트로 구현

from LinkedList import *

class LinkedListArgs(LinkedList):

    def __init__(self, *args):
        super().__init__()
        prevnode = None
        for arg in args:
            node = Node(arg)
            if not self.head:
                self.head = node
            else:
                prevnode.next = node
            prevnode = node
            self.count = self.count + 1

lst = LinkedListArgs(69, 10, 30, 2, 16, 8, 31, 22)

for i in range(1, lst.length()):
    idx = i
    while idx >= 0:
        if idx == 0:
            lst.addtoFirst(lst.delete(i))
        elif lst.get(idx-1).data <= lst.get(i).data:
            lst.add(idx, lst.delete(i))
            break
        idx -= 1

print(lst)

# 출력
>>> [2, 8, 10, 16, 22, 30, 31, 69]
```

<br>

<br>

### 2. <strong>병합 정렬</strong>

- 분할 정복 알고리즘 활용
- 정렬이 끝난 두 개의 수열을 병합하는 방식으로 정렬
- 시간복잡도 - O(nlogn)

```python
# python 예시 - 병합 정렬(1): list로 구현

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

```python
# python 예시 - 병합 정렬(2): deque으로 구현
# (deque은 내부적으로 이중 연결 리스트로 구현되어 있다.)

from collections import deque
import itertools

def MergeSort(deck):
    mid = (0 + len(deck)) // 2
    if len(deck) == 1:
        return deck
    elif len(deck) == 2:
        if deck[0] > deck[1]:
            deck.append(deck.popleft())
        return deck
    else:
        resultdeck = deque()
        deck1 = MergeSort(deque(itertools.islice(deck, 0, mid)))
        deck2 = MergeSort(deque(itertools.islice(deck, mid, len(deck))))
        i, j = -len(deck1), -len(deck2)
        while i < 0 or j < 0:
            if i == 0:
                resultdeck.append(deck2[j])
                j += 1
            elif j == 0:
                resultdeck.append(deck1[i])
                i += 1
            else:
                if deck1[i] < deck2[j]:
                    resultdeck.append(deck1[i])
                    i += 1
                else:
                    resultdeck.append(deck2[j])
                    j += 1
        return resultdeck

sample = deque([69, 10, 30, 2, 16, 8, 31, 22])
print(MergeSort(sample))

# 출력
>>> deque([2, 8, 10, 16, 22, 30, 31, 69])
```

<br>

<br>

<br>

<br>

출처: SW Expert Academy - Learn - Course - Programming Intermediate

[SW Expert Academy - Programming Intermediate course](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDN86AAXw5UW6)

