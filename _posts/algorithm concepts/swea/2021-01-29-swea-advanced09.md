---
layout: single
title: "23-2 : 그래프의 최소 비용 문제 (2) - 최단 경로"
excerpt: "최단 경로 문제 알고리즘 소개"
categories: 
- Computer Science
- Algorithm Concepts
tags:
- SWEA
- Dijkstra Algorithm
- Bellman-Ford Algorithm
- Floyd-Warshall Algorithm
---
## 그래프의 최소 비용 문제 (2) - 최단 경로 문제

### 1. 최단 경로 문제

- 간선의 가중치가 있는 유향 그래프에서 두 정점 사이의 경로들 중 간선의 가중치의 합이 최소인 경로.

#### a. 단일 시작점 최단 경로 문제

- 출발점에서 다른 모든 정점들에 이르는 최단 경로를 구하는 문제.
- **다익스트라(Dijkstra)** 알고리즘, **벨만-포드(Bellman-Ford)** 알고리즘이 있다.

<br>

#### b. 모든 쌍 최단 경로 문제

- 모든 정점 쌍 간의 최단경로를 구하는 문제
- **플로이드-워샬(Floyd-Warshall)** 알고리즘이 있다.

<br>

#### c. 음수 간선이 있는 경우

- 음수 사이클이 있는 경우 최단 경로 문제는 정의되지 않는다.
- 음수 간선이 있는 경우엔 최단 경로 문제를 풀 수 있지만, 이 경우 **다익스트라 알고리즘은 적용할 수 없다**.

<br>

#### d. 유향 그래프와 무향 그래프

- 이 최단 경로 알고리즘들은 모두 유향 그래프에서 적용된다.
- 무향 그래프에서 최단 경로 문제를 풀기 위해서는 각각의 양방향 간선을 두 개의 일방 통행 간선으로 쪼개서 유향 그래프로 만든 후 풀어야 한다.

<br>

<br>

### 2. 다익스트라 알고리즘

#### a. 다익스트라 알고리즘이란?

- 시작 정점에서 거리가 최소인 정점부터 선택해 나가면서 최단 경로를 구하는 방식이다.
- 그리디 알고리즘으로 구현되며, 프림 알고리즘과 유사하다.
- 시간복잡도:  O(V² + E) (V: 정점의 개수, E: 간선의 개수)
  (간선 (u, v)는 u가 트리에 추가될 때 한 번, v가 트리에 추가될 때 한 번 검사된다.)
- 우선순위 큐를 활용한다면 O(ElogV)의 시간복잡도로 구현할 수 있다.

<br>

#### b. 다익스트라 알고리즘의 구현

- 최단 경로를 저장하는 배열을 만들고, 최단 경로 트리에 정점을 새로 추가할 때마다 그 정점에 인접한 간선들을 순회하면서 갱신한다.

1. 시작점을 선택해서 시작한다. 최단 경로를 저장하는 배열에서 시작점에 해당하는 곳엔 0을 넣는다.
2. 선택한 정점들과 인접하는 정점들을 순회하며 각 정점까지의 최단 경로를 갱신하고, 그때의 부모 노드를 최단 경로 트리에 기록한다.
3. 모든 정점을 방문할 때까지 2번 과정을 반복한다.

```python
# 다익스트라 알고리즘
def Dijkstra(G, s, N): # G: 그래프, s: 시작 정점, N: 정점의 개수
    visited = [0 for i in range(N+1)] # 정점 방문 여부 초기화
    dist = [float('inf') for i in range(N+1)] # 경로 길이를 무한대로 초기화
    parents = [None for i in range(N+1)] # 트리에서 연결될 부모 정점 초기화.
    # 각 정점이 실제 어떤 간선을 통해 트리와 연결되었는지를 확인하기 위해 사용한다.
    dist[s] = 0 # 시작 정점의 경로 길이를 0으로 설정한다.
    # 또한, 이 설정은 시작 정점을 방문하겠다고 표시하기 위한 장치가 된다.

    for i in range(1, N+1): # 정점의 개수 만큼 반복 (모든 정점을 방문할 때까지)
        minidx, minval = -1, float('inf') # 최소 경로 정점을 찾기 위한 초기화
        # 여기서부터 방문하지 않은 정점 중 최소 경로 정점 찾기
        for j in range(1, N+1): # 새로 추가할 정점 찾기
            if not visited[j] and dist[j] < minval:
                minval = dist[j]
                minidx = j
        visited[minidx] = 1 # 최소 경로 정점 방문 표시
        # 여기서부터 추가한 정점에 인접한 간선에 대해 dist 갱신과정
        if G.get(minidx): # 인접 정점이 있는 경우만 최단 경로 정보 갱신
            for v, val in G.get(minidx): # 새로 추가한 정점 인근의 최단 경로 정보 갱신
                if not visited[v] and dist[minidx] + val < dist[v]:
    # 현재 정점(minidx) 까지의 최단 경로 길이 + 해당 정점(v)와의 거리 <val>의 합이
    # 해당 정점에 저장된 최단 경로 길이 <dist[v]>보다 작으면 
    # dist[v]를 더 작은 값으로 갱신한다.
                    dist[v] = dist[minidx] + val
                    parents[v] = minidx

        print(minidx, minval)  # 새로 추가할 정점과 그 최단 경로 길이
        print(visited[1:], dist[1:], parents[1:])  
        # 정점의 방문 정보, 갱신한 최단 경로 길이 정보, 최단 경로 트리
        print('----------------')

    return parents[1:] # 시작점 s에서의 최단 경로 트리


edges = [(1, 2, 3), (1, 3, 5), (2, 3, 1), (3, 2, 1), (2, 4, 6), (3, 4, 3), 
         (3, 5, 6), (4, 5, 2), (5, 4, 3), (4, 6, 3), (5, 6, 6)]
graph = dict()
for edge in edges:
    s, e, val = edge
    if graph.get(s):
        graph[s].append((e, val))
    else:
        graph[s] = [(e, val)]

for key in graph.keys():
    print(key, graph[key])
print('--------Graph--------')
# 그래프의 인접리스트 표현 (유향 그래프)

print(Dijkstra(graph, 1, 6))

# 출력
1 [(2, 3), (3, 5)]
2 [(3, 1), (4, 6)]
3 [(2, 1), (4, 3), (5, 6)]
4 [(5, 2), (6, 3)]
5 [(4, 3), (6, 6)]
--------Graph--------
1 0
[1, 0, 0, 0, 0, 0] [0, 3, 5, inf, inf, inf] [None, 1, 1, None, None, None]
----------------
2 3
[1, 1, 0, 0, 0, 0] [0, 3, 4, 9, inf, inf] [None, 1, 2, 2, None, None]
----------------
3 4
[1, 1, 1, 0, 0, 0] [0, 3, 4, 7, 10, inf] [None, 1, 2, 3, 3, None]
----------------
4 7
[1, 1, 1, 1, 0, 0] [0, 3, 4, 7, 9, 10] [None, 1, 2, 3, 4, 4]
----------------
5 9
[1, 1, 1, 1, 1, 0] [0, 3, 4, 7, 9, 10] [None, 1, 2, 3, 4, 4]
----------------
6 10
[1, 1, 1, 1, 1, 1] [0, 3, 4, 7, 9, 10] [None, 1, 2, 3, 4, 4]
----------------
[None, 1, 2, 3, 4, 4]
# 최종적으로 프린트된 리스트는 출발 정점 1에서의 최단 경로 트리를 의미한다.
```

<br>

<br>

<br>

<br>


출처: SW Expert Academy - Learn - Course - Programming Advanced / 알고리즘 문제 해결 전략

[SW Expert Academy - Programming Advanced Course](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDYSqAAbw5UW6)

