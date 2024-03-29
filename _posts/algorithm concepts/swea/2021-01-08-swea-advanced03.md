---
layout: single
title: "18 : 탐욕 알고리즘 (그리디 알고리즘)"
excerpt: "탐욕 알고리즘 소개 및 활용 예시"
categories: 
- Computer Science
- Algorithm Concepts
tags:
- SWEA
- Greedy Algorithm
- Prim Algorithm
- Kruskal Algorithm
- Dijkstra Algorithm
---
## 탐욕 알고리즘

### 1. 탐욕(그리디) 알고리즘 이란?

- 최적화 문제를 해결하는 알고리즘
- 그리디 알고리즘의 흐름
  1. 여러 경우 중 하나 선택
  2. 매 순간 최적이라고 생각되는 것을 선택
     - <font color='red'>지역적으로 최적이라는 말이 전체적으로 최적이라는 말은 아니다.</font>
  3. 최종 결론에 도달
- 그리디 알고리즘을 적용하여 전체 문제에 대한 최적해를 찾을 수 있는지 검증해야 한다.

<br>

<br>

### 2. **탐욕 알고리즘의 증명**

- 탐욕 알고리즘이 최적해를 구한다는 것에 대한 증명

1. <font color='red'>탐욕적 선택 속성</font>(Greedy choice property)
   - 탐욕적 선택은 항상 안전하다는 것을 보여야 한다.
     즉, 탐욕적 선택으로 전체 문제의 최적해를 반드시 구할 수 있다는 것을 보여야 한다.
   - 보통 탐욕적 선택을 포함하지 않는 최적해의 존재를 가정하고, 이것을 적절히 조작하여 탐욕적 선택을 포함하는 최적해를 만들어 내는 과정으로 증명하곤 한다.
2. <font color='red'>최적 부분 구조</font>
   - [전체 문제의 최적해 = 탐욕적 선택 + 하위 문제의 최적해] 임을 증명해야 한다.

<br>

<br>

### 3. 탐욕 기법과 동적 계획법의 비교

|                      탐욕 기법                       |                         동적 계획법                         |
| :--------------------------------------------------: | :---------------------------------------------------------: |
|  매 단계에서 가장 좋아보이는 것을 빠르게 선택한다.   | 매 단계의 선택은 <br>해결한 하위 문제의 해를 기반으로 한다. |
| 하위 문제를 풀기 전에 탐욕적 선택이 먼저 이루어진다. |                 하위 문제가 우선 해결된다.                  |
|                  **Top-down 방식**                   |                     **Bottom-up 방식**                      |
|             일반적으로 빠르고 간결하다.              |                   좀 더 느리고 복잡하다.                    |

<br>

<br>

### 4. 대표적인 탐욕 기법의 알고리즘들

- Prim
- Kruskal
- Dijkstra
- Huffman coding

<br>

<br>

### 5. 탐욕 알고리즘 적용 예시

#### a. 동전 거스름돈 문제

- **최소 갯수의 동전으로 거스름돈을 줘야한다.**

1. 800원의 거스름돈을 500원, 100원, 50원, 10원짜리 동전으로 줄 때
   - 가장 단위가 큰 500원짜리 동전부터 사용한다.
   - 500원짜리 1개, 100원짜리 3개로 거슬러 줄 수 있다.
   - 그리디 알고리즘으로 구한 해가 전체 문제에 대한 최적해가 된다.
2. 800원의 거스름돈을 500원, 400원, 100원, 50원, 10원짜리 동전으로 줄 때 (400원짜리 동전이 추가됨)
   - 가장 단위가 큰 500원짜리 동전부터 시작하면 500원짜리 1개, 100원짜리 3개로 거슬러주게 된다.
   - 전체 문제에 대한 최적 해는 400원짜리 동전 2개이므로 그리디 알고리즘으로는 전체 문제에 대한 최적해를 구할 수 없다.
   - 이 문제의 경우엔 완전 탐색으로 전체 문제에 대한 최적해를 구할 수 있다.

<br>

#### b. 배낭 문제

- **배낭에 담은 물건의 가격의 합이 최대가 되도록 한다.**

1. 0-1 배낭 문제: 배낭에 물건을 통째로 담아야 하는 문제
   - 그리디 알고리즘으로 최적 해를 구할 수 없다.
2. Fractional 배낭 문제: 물건의 일부를 잘라서 담을 수 있는 경우
   - 그리디 알고리즘으로 최적해를 구할 수 있다. 이 경우, 최적해는 실제로 가능한 해라기 보다는 이상적으로 구할 수 있는 최대 가치이다.

<br>

#### c. 활동 선택 문제

- **회의실 배정 문제**
- 회의실 하나에서 다수의 회의를 할 때, 가능한 많은 회의가 열리기 위해서 회의들을 어떻게 배정할까?

1. 탐욕 기법 풀이

   1. 종료시간이 빠른 순으로 회의를 모두 정렬한다.
   2. 종료시간이 가장 빠른 회의를 선택하고, 해집합에 포함시킨다.
   3. 2에서 선택한 회의와 겹치지 않는 회의들의 집합에 초점을 맞춘다.
   4. 남은 회의가 없을 때까지 2, 3 과정 반복


2. 그리디 알고리즘이 최적해를 구한다는 증명

   1. 탐욕적 선택 속성

      - 전체 회의의 집합 S에서 최대 크기의 부분집합 A가 있다고 하자.
      - 종료 시간이 가장 빠른 회의 Smin을 선택하고, 집합 A에서 종료 시간이 가장 빠른 회의를 Ak라고 하자.
      - 만약 Ak == Smin이면 최대 크기 부분집합 A에 Smin이 포함된다.
      - 만약 Ak != Smin이면 A에서 Ak를 제거하고 Smin을 추가한다.
        -> Smin은 종료 시간이 가장 빠른 회의이므로, Ak대신 A에 들어간다고 해서 A에 들어있는 다른 회의들과 겹치지 않는다.
      - 따라서 종료 시간이 가장 빠른 회의를 선택하는 건 항상 안전하다. 
        (즉, 항상 전체 문제의 최적해를 구할 수 있다.)

   2. 최적 부분 구조

      - Sij를 i번째 회의의 종료 시간부터 j번째 회의의 시작 시간 사이에 포함된 회의들의 집합이라고 하자.
      - Sij에서 종료 시간이 가장 빠른 회의 Smin을 선택하면 하위 문제 Sim, Smj가 존재한다. (Sm을 기준으로 회의들의 집합이 분리된다.)
      - 만약 Sim이 공집합이 아니라면 Smin보다 종료 시간이 빠른 회의가 있다는 뜻인데, 그건 가장 빠르게 끝나는 Smin이라는 회의를 선택한다는 조건에 반한다.
      - 따라서 Sim은 공집합이며 고려할 활동이 없다. Smj에서 최적해를 구하면 된다.

   3. 정리

      - 탐욕적 선택을 하는 순간마다, 전체 회의의 집합 S의 '종료 시간이 가장 빠른 회의'를 포함하는 최적해가 반드시 존재한다는 것을 입증한다.
      - 종료 시간이 가장 빠른 회의를 골라내고 (탐욕적 선택), 시간이 겹치는 회의를 모두 걸러낸 집합에서 당연히 가장 많은 회의를 선택(하위 문제의 최적해)해야 한다.

<br>

<br>

<br>

<br>

출처: SW Expert Academy - Learn - Course - Programming Advanced

[SW Expert Academy - Programming Advanced Course](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDYSqAAbw5UW6)

