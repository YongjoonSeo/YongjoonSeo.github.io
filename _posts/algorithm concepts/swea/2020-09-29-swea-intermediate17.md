---
layout: single
title: "10 : 백트래킹 (Backtracking)"
excerpt: "백트래킹 소개 및 응용"
categories: 
- Computer Science
- Algorithm Concepts
tags:
- SWEA
- Backtracking
---
## 백트래킹(Backtracking)

### <strong>백트래킹(Backtracking) 이란?</strong>

- 정답을 찾는 도중에 막히면 되돌아가서 다시 정답을 찾아가는 방법.
- 일반적으로 DFS 순회를 하다 답을 찾을 수 없게 되는 조건을 만나면 가지치기를 하는 방법을 백트래킹이라고 한다.

<br>

### n-queen 문제

- 크기가 N X N인 체스판 위에 퀸 N개를 서로 공격할 수 없게 놓는 문제.
- 퀸을 하나 놓으면 그 공격 범위 내에 다른 퀸이 들어올 수 없다.

- [백준 9663번 N-Queen](https://www.acmicpc.net/problem/9663)

```python
# python 예시 - N-Queen

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
    
# 입력
>>> 8

# 출력
>>> 92
```

<br>

### Power set (멱집합 구하기)

- Power set (멱집합): 어떤 집합의 모든 부분집합으로 이루어진 집합.
- 어떤 집합의 각 원소가 있거나(1) 없을 때(0)의 모든 경우에 맞는 부분집합을 모아 출력한다.

```python
# python 예시 - Power set

def BT_powerset(times, inp):

    if times == inp:
        result.append(list(target[i] for i in range(inp) if cases[i]))
        return

    for j in range(2):
        cases[times] = j
        BT_powerset(times + 1, inp)
        cases[times] = 0

target = [1,2,3]
N = len(target)
cases = [0] * N
result = []

BT_powerset(0, N)
print(result)

# 출력
>>> [[], [3], [2], [2, 3], [1], [1, 3], [1, 2], [1, 2, 3]]
```

<br>

### 순열 (Permutation)

- 순열: 서로 다른 n개에서 r개를 뽑아 순서를 고려하여 늘어놓는 경우의 수.
- 원하는 리스트(target)의 n개 원소 중 r 개를 뽑아 나열하는 모든 경우의 수를 출력한다.
- target에서 어떤 원소 a를 뽑았다면 그 원소를 다시 뽑는 경우는 가지치기를 해준다.  

```python
# python 예시 - 순열 (Permutation)

def BT_permutation(t, inp):
    times = inp - t

    if t == 0:
        result.append(stack.copy())
        return 
    
    for i in range(inp):
        if target[i] not in stack:
            stack.append(target[i])
            BT_permutation(t - 1, inp)
            stack.remove(target[i])


target = [1, 2, 3, 4]
n = len(target)
stack = []

result = []
BT_permutation(2, n) 
# nPr, n개(4개) 중에서 r개(2개)를 뽑아 순서를 고려하여 늘어놓는 경우의 수
print(result)

result = []
BT_permutation(4, n) 
# n!, n개(4개)를 순서를 고려하여 늘어놓는 경우의 수
print(result)

# 출력
[[1, 2], [1, 3], [1, 4], [2, 1], [2, 3], [2, 4], [3, 1], [3, 2], [3, 4], [4, 1], [4, 2],[4, 3]]
# BT_permutation(2, n) 결과
[[1, 2, 3, 4], [1, 2, 4, 3], [1, 3, 2, 4], [1, 3, 4, 2], [1, 4, 2, 3], [1, 4, 3, 2], [2, 1, 3, 4], [2, 1, 4, 3], [2, 3, 1, 4], [2, 3, 4, 1], [2, 4, 1, 3], [2, 4, 3, 1], [3, 1, 2, 4], [3, 1, 4, 2], [3, 2, 1, 4], [3, 2, 4, 1], [3, 4, 1, 2], [3, 4, 2, 1], [4, 1, 2, 3], [4, 1, 3, 2], [4, 2, 1, 3], [4, 2, 3, 1], [4, 3, 1, 2], [4, 3, 2, 1]]
# BT_permutation(4, n) 결과
```

<br>

<br>

<br>

<br>

출처: SW Expert Academy - Learn - Course - Programming Intermediate

[SW Expert Academy - Programming Intermediate course](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDN86AAXw5UW6)

