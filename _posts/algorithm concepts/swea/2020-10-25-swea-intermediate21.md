---
layout: single
title: "12-3 : 큐 (3) - deque (덱)"
excerpt: "덱(deque) 소개"
categories: 
- Computer Science
- Algorithm Concepts
tags:
- SWEA
- Queue
- Deque
---
## 큐 (3)

### 1. 덱(deque)이란?

- deque = double-ended queue
  덱의 양쪽 어느 방향이든 append, pop의 시간 복잡도가 O(1)이다.
  
  - 고정된 길이 내에서 <strong>접근 (or 검색), 슬라이싱</strong>을 하는 데에는 <strong>list</strong>가 유리하지만, 
    데이터를 <strong>추가 or 삭제</strong>할 땐 <strong>deque</strong>이 유리하다.
  
  <br>
  
  | 시간복잡도 | indexing, slicing | insert, remove, popleft |
  | :---------------: | :--: | :---: |
  | <strong>list</strong>  |       O(1)        |          O(n)           |
  | <strong>deque</strong> | O(n) | O(1) |

<br>

- 파이썬에서의 덱
  - <strong>collections.deque</strong>([iterable[, maxlen]]) (from collections import deque)
- maxlen이 입력되지 않거나 None이면 덱의 길이는 무한히 커질 수 있다.
  maxlen이 입력된다면 덱의 길이는 maxlen 만큼의 상한을 가진다.
  - 덱의 길이가 정해졌을 때 새로운 항목이 추가되면 반대쪽 끝에 있는 항목이 삭제된다.
- iterable의 데이터를 왼쪽에서 오른쪽으로 나열한 덱 객체를 생성한다.
  (iterable가 입력되지 않으면 빈 덱 객체를 생성한다.)

<br>

<br>

### 2. <strong>deque의 메소드</strong>

- list에 사용되는 함수와 같은 역할을 하는 메소드
  - append(x)
  - clear()
  - copy()
  - count(x)
  - extend(iterable)
  - index(x[, start[, stop]])
  - insert(i, x)
  - len(d)
  - pop()
  - remove(value)
  - reverse()
  - reversed(d)
  
- list에 사용되는 함수와 차이 있는 메소드
  - appendleft(x): 덱의 왼쪽 부분에 x를 더한다
  - extendleft(iterable):  덱의 왼쪽 부분에 iterable의 데이터를 항목 별로 추가한다. 이때 iterable 안에서 순서의 역순으로 추가된다.
    ex) a가 빈 덱일 때, a.extendleft([1, 2, 3, 4]) --> deque([4, 3, 2, 1])
  - popleft(): 덱의 왼쪽 부분에서 데이터를 삭제하여 반환한다.
  - rotate(n=1): 덱을 오른쪽으로 n차례 회전시킨다. n이 음수라면 왼쪽으로 회전한다.
  - maxlen: 덱의 최대 크기를 나타낸다. 크기가 정해져있지 않다면 None을 반환한다.
  - 슬라이싱: itertools를 import 해와서 해야 한다.
  
  ```python
  # python 예시 - 덱 슬라이싱
  
  from collections import deque
  import itertools
  
  q = deque([1, 2, 3, 4, 5])
  print(q)
  print(list(itertools.islice(q, 1, 3)))
  
  # islice(iterable, *args)
  # islice('ABCDEFG', 2) --> A B
  # islice('ABCDEFG', 2, 4) --> C D 
  # islice('ABCDEFG', 2, None) --> C D E F G
  # islice('ABCDEFG', 0, None, 2) --> A C E G
  # 슬라이싱 하고 싶은 iterable 변수를 넣어주고, 
  # 그 후 입력되는 인자는 슬라이싱 할 때와 같은 방식으로 한다.
  
  # 출력
  >>> deque([1, 2, 3, 4, 5])
  >>> [2, 3]
  ```

<br>

<br>

<br>

<br>

출처: Python Documentation >> The Python Standard Library >> Data Types

[The Python Standard Library >> collections](https://docs.python.org/3/library/collections.html#collections.deque)