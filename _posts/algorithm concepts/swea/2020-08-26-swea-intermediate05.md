---
layout: single
title: "3-1 : 2차원 List (1)"
excerpt: "2차원 배열 탐색 방법 소개 - 행 우선 탐색, 열 우선 탐색, 지그재그 탐색, 델타를 이용한 탐색"
categories: 
- Computer Science
- Algorithm Concepts
tags:
- SWEA
- 2-D Array
---
## 2차원 List (1)

* List 탐색
  * 행 우선 탐색, 열 우선 탐색, 지그재그 탐색, 델타를 이용한 탐색

<br>

### 1. 행 우선 탐색

- 행을 차례대로 탐색해 나가는 방법이다.

```python
# python 예시 - 행 우선 탐색

A = [['{0:2d}'.format(i) for i in range(j, j+5)] for j in range(1, 26, 5)]

for i in range(5):
    print(*A[i])

# 행 우선 탐색
for i in range(5):
    for j in range(5):
        print(A[i][j], end=' ')
print()

# 출력
 1  2  3  4  5
 6  7  8  9 10
11 12 13 14 15
16 17 18 19 20
21 22 23 24 25
>>>  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25
```

<br>

<br>

### 2. 열 우선 탐색

- 열을 차례대로 탐색해 나가는 방법이다.

```python
# python 예시 - 열 우선 탐색

A = [['{0:2d}'.format(i) for i in range(j, j+5)] for j in range(1, 26, 5)]

for i in range(5):
    print(*A[i])

# 열 우선 탐색
for i in range(5):
    for j in range(5):
        print(A[j][i], end=' ')
print()

# 출력
 1  2  3  4  5
 6  7  8  9 10
11 12 13 14 15
16 17 18 19 20
21 22 23 24 25
>>>  1  6 11 16 21  2  7 12 17 22  3  8 13 18 23  4  9 14 19 24  5 10 15 20 25
```

<br>

<br>

### 3. 지그재그 탐색

- 지그재그로 행 또는 열을 탐색해 나가는 방법이다.

#### a. 행 우선 지그재그 탐색

```python
# python 예시 - 행 우선 지그재그 탐색

A = [['{0:2d}'.format(i) for i in range(j, j+5)] for j in range(1, 26, 5)]

for i in range(5):
    print(*A[i])
    
# 지그재그 탐색 - 행
for i in range(5):
    for j in range(5):
        print(A[i][j + (5 - 1 - 2 * j) * (i % 2)], end=' ')
        # 5 = 행의 길이
print()

# 출력
 1  2  3  4  5
 6  7  8  9 10
11 12 13 14 15
16 17 18 19 20
21 22 23 24 25
>>>  1  2  3  4  5 10  9  8  7  6 11 12 13 14 15 20 19 18 17 16 21 22 23 24 25
```

<br>

#### b. 열 우선 지그재그 탐색

```python
# python 예시 - 열 우선 지그재그 탐색

A = [['{0:2d}'.format(i) for i in range(j, j+5)] for j in range(1, 26, 5)]

for i in range(5):
    print(*A[i])
    
# 지그재그 탐색 - 열
for i in range(5):
    for j in range(5):
        print(A[j + (5 - 1 - 2 * j) * (i % 2)][i], end=' ')
print()

# 출력
 1  2  3  4  5
 6  7  8  9 10
11 12 13 14 15
16 17 18 19 20
21 22 23 24 25
>>>  1  6 11 16 21 22 17 12  7  2  3  8 13 18 23 24 19 14  9  4  5 10 15 20 25
```

<br>

<br>

### 4. 델타를 이용한 탐색

- x축 방면의 진행 방향과 y축 방면의 진행 방향을 각각 dx, dy로 하여 특정한 조건을 만나면 idx라는 변수를 사용하여 방향을 바꾸도록 설정했다. 그래서 위치 x, y를 조절할 수 있고 이를 이용하여 2차원 배열에서 원하는 위치의 요소에 접근할 수 있다.
- 이 코드에서 +x, +y의 방향은 직교좌표계에서 +x, -y 방향이다.

```python
# python 예시 - 델타를 이용한 탐색: 달팽이 모양으로 출력

def Inbox(lst, y, x, xmax, ymax): 
    # 0 <= x < xmax, 0 <= y < ymax 일때 True 반환. IndexError를 방지할 수 있다.
    if x >= 0 and x < xmax and y >= 0 and y < ymax:
        if lst[y][x] == 0:
            return True
    return False

result = [[0 for i in range(5)] for j in range(5)]

dx = [1, 0, -1, 0]
dy = [0, 1, 0, -1]
idx = 0
x, y = 0, 0

for i in range(1, 26):
    result[y][x] = '{0:2d}'.format(i)
    if not Inbox(result, y+dy[idx], x+dx[idx], 5, 5):
        idx = (idx + 1) % 4
    x, y = x + dx[idx], y + dy[idx]

for _ in range(len(result)):
    print(*result[_])
    
# 출력
 1  2  3  4  5
16 17 18 19  6
15 24 25 20  7
14 23 22 21  8
13 12 11 10  9
```

<br>

<br>

<br>

<br>

출처: SW Expert Academy - Learn - Course - Programming Intermediate

[SW Expert Academy - Programming Intermediate course](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDN86AAXw5UW6)