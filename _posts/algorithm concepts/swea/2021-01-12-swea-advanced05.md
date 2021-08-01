---
layout: single
title: "20 : 백트래킹"
excerpt: "백트래킹 소개 및 활용 예시"
categories: 
- Computer Science
- Algorithm Concepts
tags:
- SWEA
- Backtracking
- N-Queen
---
## 백트래킹

### 1. 백트래킹이란?

- 해를 찾는 중에 막히면 **되돌아가서** 다시 해를 찾아가는 방법.
- 트리를 깊이 우선 탐색하는 방법이 백트래킹 알고리즘의 기본 형태이다.
- 해를 찾지 못하는 경로를 **가지치기** 하여 불필요한 탐색을 조기에 차단할 수 있다.

<br>

<br>

### 2. 백트래킹을 적용하는 예시

- n-queen 문제
- power set 구하기
- 순열 구하기
- 동전 거스름돈 문제

<br>

#### ex) [N-Queen 문제](https://www.acmicpc.net/problem/9663)

```python
def Bt(y, x):
    global cnt, N
    ny = y+1
    
    for nx in range(N):
        if ny < N and not (ny in row or nx in col or ny+nx in diagplus or nx-ny in diagminus):
            row.append(ny)
            col.append(nx)
            diagplus.append(nx+ny)
            diagminus.append(nx-ny)
            Bt(ny, nx)
            row.pop()
            col.pop()
            diagplus.pop()
            diagminus.pop()
            if ny == N-1: cnt += 1

N = int(input())
cnt = 0
if N == 1:
    print(1)
else:
    for i in range(N):
        row = [0]
        col = [i]
        diagplus = [i]
        diagminus = [i]
        Bt(0, i)
    print(cnt)
```

<br>

<br>

<br>

<br>

출처: SW Expert Academy - Learn - Course - Programming Advanced

[SW Expert Academy - Programming Advanced Course](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDYSqAAbw5UW6)

