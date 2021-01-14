---
layout: single
title: "21 : 그래프의 기본과 탐색"
excerpt: "그래프를 설명하는 용어 및 그래프 표현 방법"
categories: 
- Algorithm Concepts
tags:
- SWEA
- Graph
- DFS
- BFS
---
## 그래프의 기본과 탐색

### 1. 그래프란?

- 객체들 사이의 연결 관계를 표현하는 방법이다.
- **정점(Vertex)**들의 집합과 정점을 연결하는 **간선(Edge)**들의 집합으로 구성된 자료구조이다.
- 방향성에 따라 **무향 그래프**와 **유향 그래프**로 나눌 수 있고, 간선에 가중치를 나타낸 **가중치 그래프**도 있다.

<br>

<br>

### 2. 그래프 용어

#### a. 인접 (Adjacency)

- 두 개의 정점에 간선이 연결 되어있는 경우 서로 인접해 있다고 한다.
- 방향성을 가지는 경우 방향에 따라 인접 여부가 달라진다.
  - ex) 1 -> 2 인 경우 2번 정점은 1번 정점의 인접 정점이지만 1번 정점은 2번 정점의 인접 정점이 아니다.
- 완전 그래프에 속한 정점들은 모두 인접해있다.

<br>

#### b. 경로

- 간선들을 순서대로 나열한 것
- 단순경로: 경로 중 한 정점을 최대 한 번만 지나는 경로
- 사이클: 시작한 정점에서 끝나는 경로
  - cf. 사이클이 없는 유향 그래프: DAG (Directed Acyclic Graph)

<br>

<br>

### 3. 그래프의 표현

- 인접 행렬과 인접 리스트로 표현하는 방법이 있다.

#### a. 인접 행렬

- 두 정점이 인접하면 1, 아니면 0으로 표현한다.
- 무향 그래프: i번째 행의 합 = i번째 열의 합 = i번째 정점의 차수 (=연결된 간선의 개수)
- 유향 그래프: 진출하는 간선을 행에, 진입하는 간선을 열에 저장한다고 하면
  - i번째 행의 합 = i번째 정점의 진출 차수 (i번째 정점에서 나가는 간선의 개수)
  - i번째 열의 합 = i번째 정점의 진입 차수 (i번째 정점으로 들어오는 간선의 개수)
- 단점:
  1. 정점의 개수 n이 커지면 메모리 크기는 n<sup>2</sup>에 비례해서 커진다.
  2. 어떤 정점의 인접 정점을 찾을 때마다, 불필요한 공간을 탐색하는 횟수가 늘어난다.

```python
# 그래프의 표현 - 인접 행렬
num_vertex = 7
edges = [(0,1), (0,2), (0,6), (0,5), (5,3), (4,3), (5,4), (6,4)]

undirected = [[0 for i in range(num_vertex)] for j in range(num_vertex)]
directed = [[0 for i in range(num_vertex)] for j in range(num_vertex)]

for s, e in edges:
    undirected[s][e] = 1
    undirected[e][s] = 1

for s, e in edges:
    directed[s][e] = 1

print('Undirected Graph')
for _ in range(num_vertex):
    print(undirected[_])
print('Directed Graph')
for _ in range(num_vertex):
    print(directed[_])

# 출력
Undirected Graph
[0, 1, 1, 0, 0, 1, 1]
[1, 0, 0, 0, 0, 0, 0]
[1, 0, 0, 0, 0, 0, 0]
[0, 0, 0, 0, 1, 1, 0]
[0, 0, 0, 1, 0, 1, 1]
[1, 0, 0, 1, 1, 0, 0]
[1, 0, 0, 0, 1, 0, 0]
Directed Graph
[0, 1, 1, 0, 0, 1, 1]
[0, 0, 0, 0, 0, 0, 0]
[0, 0, 0, 0, 0, 0, 0]
[0, 0, 0, 0, 0, 0, 0]
[0, 0, 0, 1, 0, 0, 0]
[0, 0, 0, 1, 1, 0, 0]
[0, 0, 0, 0, 1, 0, 0]
```

<br>

#### b. 인접 리스트

- 하나의 정점에 대한 인접 정점들을 각각 노드로 하여 연결리스트 형태로 저장한다.
- 메모리를 많이 사용하는 인접 행렬의 단점을 보완할 수 있다.

```python
# 그래프의 표현 - 인접 리스트
num_vertex = 7
edges = [(0,1), (0,2), (0,6), (0,5), (5,3), (4,3), (5,4), (6,4)]

undirected = dict()
directed = dict()

for s, e in edges:
    if undirected.get(s):
        undirected.get(s).append(e)
    else:
        undirected[s] = [e]
    if undirected.get(e):
        undirected.get(e).append(s)
    else:
        undirected[e] = [s]

for s, e in edges:
    if directed.get(s):
        directed.get(s).append(e)
    else:
        directed[s] = [e]

print('Undirected Graph')
for key in undirected:
    print(key, undirected.get(key))
print('Directed Graph')
for key in directed:
    print(key, directed.get(key))
    
# 출력
Undirected Graph
0 [1, 2, 6, 5]
1 [0]
2 [0]
6 [0, 4]
5 [0, 3, 4]
3 [5, 4]
4 [3, 5, 6]
Directed Graph
0 [1, 2, 6, 5]
5 [3, 4]
4 [3]
6 [4]
```

<br>

<br>

### 4. 그래프의 탐색


- visited를 활용하여 방문한 정점을 다시 방문하지 않게끔 탐색한다.

1. 깊이 우선 탐색(DFS) - 스택 또는 재귀 호출을 이용한다.
2. 너비 우선 탐색(BFS) - 큐를 이용한다.

<br>

<br>

<br>

<br>

출처: SW Expert Academy - Learn - Course - Programming Advanced

[SW Expert Academy - Programming Advanced Course](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDYSqAAbw5UW6)

