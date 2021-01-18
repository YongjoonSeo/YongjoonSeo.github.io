---
layout: single
title: "22 : 상호배타 집합들"
excerpt: "상호배타 집합과 Union-Find 자료구조 설명"
categories: 
- Algorithm Concepts
tags:
- SWEA
- Disjoint Set
- Union-Find
---
## 상호배타 집합들

### 1. 상호배타 집합 (Disjoint Set)

- 서로 중복 포함된 원소가 없는 집합들. (교집합이 없음, 서로소)
- 집합에 속한 하나의 특정 원소를 통해 각 집합들을 구분한다.
  - 특정 원소 - 대표자 (Representative)
- 상호배타 집합을 표현하는 방법
  - 연결 리스트
    - 찾기 연산의 시간복잡도는 O(1)이지만 합치기 연산은 O(n)이다.
  - 트리
    - 이를 **Union-Find** 자료구조라고 한다.

<br>

<br>

### 2. 상호배타 집합의 연산

- Union-Find 자료구조

1. 초기화 - n개의 원소가 자기 자신으로 구성된 집합을 만들도록 한다.
2. 찾기 (find) - 어떤 원소 x가 속한 집합을 반환한다. (집합의 대표자를 알아낸다.)
3. 합치기 (Union) - x 원소가 속한 집합과 y 원소가 속한 집합을 하나의 집합으로 합친다.

<br>

<br>

### 3. 상호배타 집합 연산 최적화

#### a. ranks

- 두 트리를 합칠 때 항상 **높이가 더 낮은 트리를 더 높은 트리 밑에** 집어넣는다.
- 합치기 연산 + 찾기 연산의 시간복잡도가 O(n)에서 **O(logn)**으로 된다.
  - 트리의 높이가 h-1이기 위해 최소 n개의 노드가 필요하다면, 높이가 하나 높아지기 위해서는 최소 2n개의 노드가 필요하기 때문이다.

<br>

#### b. parents

- **경로 압축 (Path Compression)**
- find를 통해 루트까지 올라가는 경로 상에 있는 모든 노드들이 루트 노드(부모 노드)를 가리키게 한다.
- 현실적인 모든 입력에 대해 **상수 시간에 동작**한다.

<br>

<br>

### 4. 상호배타 집합 활용 예시

1. 그래프의 연결성 확인
   - KRUSKAL Minimum Spanning Tree (MST) 알고리즘
2. 가장 큰 집합 추적하기
   - 집합의 노드 개수가 몇 개 이상이 되는 시점 찾기
     (각 트리의 노드의 개수를 담는 배열을 추가해서 값을 갱신하는 방식으로 가능하다.)

<br>

<br>

### 5. 상호배타 집합 구현

#### a. 연결 리스트

```python
class Node:
    def __init__(self, val):
        self.parent = self
        self.next = None
        self.data = val

    def __repr__(self):
        return self.data

class linkedlist:
    def __init__(self, val):
        self.head = Node(val)
        self.length = 1
        self.tail = self.head

    def union(self, llist):
        assert self.length >= llist.length
        self.tail = llist.head
        temphead = llist.head
        while temphead:
            temphead.parent = self.head
            temphead = temphead.next
        self.length += llist.length

    def find(self):
        return self.head.parent

elements1 = ['a', 'd', 'e']
elements2 = ['b', 'f']

linkedlist1 = linkedlist(elements1[0])
linkedlist1.union(linkedlist(elements1[1]))
linkedlist1.union(linkedlist(elements1[2]))

linkedlist2 = linkedlist(elements2[0])
linkedlist2.union(linkedlist(elements2[1]))

print('before union')
print(linkedlist1.find())
print('length:', linkedlist1.length)

linkedlist1.union(linkedlist2)

print('after union')
print(linkedlist1.find())
print('length:', linkedlist1.length)

# 출력
before union
a
length: 3
after union
a
length: 5
```

<br>

#### b. 트리

```python
def Find(x):
    if parents[x] == x:
        return x
    parents[x] = Find(parents[x])
    return parents[x]

def Union(x, y):
    xroot = Find(x)
    yroot = Find(y)
    if ranks[xroot] >= ranks[yroot]:
        parents[yroot] = xroot # y를 루트로 하는 트리를 x를 루트로 하는 트리에 합친다.
    else:
        parents[xroot] = yroot # x를 루트로 하는 트리를 y를 루트로 하는 트리에 합친다.
    if ranks[xroot] == ranks[yroot]:
        ranks[xroot] += 1

parents = [i for i in range(10)]
# 원소가 10개 있는 경우.
# i번째 항목의 값이 i라고 선언하는 것 자체가 각각의 트리를 만든 것이라 보면 된다.
# 인덱스는 각 항목, 값은 부모 노드로 볼 수 있다.
ranks = [0 for i in range(10)]
# 루트 노드가 i인 트리의 랭크 값 저장

print('Initial root nodes and ranks : ')
print(parents)
print(ranks)
print('------------------------------')

Union(2, 3)
Union(4, 5)
Union(2, 4)

print('Root nodes and ranks after Union : ')
print(parents)
print(ranks)
print('------------------------------')

print(Find(5))
print('After find(5) : ')
print(parents)
print('Root node for 5 has been updated')

# 출력
Initial root nodes and ranks : 
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
------------------------------
Root nodes and ranks after Union : 
[0, 1, 2, 2, 2, 4, 6, 7, 8, 9]
[0, 0, 2, 0, 1, 0, 0, 0, 0, 0]
------------------------------
2
After find(5) : 
[0, 1, 2, 2, 2, 2, 6, 7, 8, 9]
Root node for 5 has been updated
```

<br>

<br>

<br>

<br>

출처: SW Expert Academy - Learn - Course - Programming Advanced & <br> 알고리즘 문제 해결 전략

[SW Expert Academy - Programming Advanced Course](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDYSqAAbw5UW6)

