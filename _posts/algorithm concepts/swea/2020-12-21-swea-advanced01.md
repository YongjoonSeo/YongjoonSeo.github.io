---
layout: single
title: "16 : 비트 연산자"
excerpt: "비트마스크(bitmask) 소개 및 활용"
categories: 
- Computer Science
- Algorithm Concepts
tags:
- SWEA
- Bitmask
---
## 비트 연산자

### 1. 비트연산자의 종류

- `&`: 비트 단위로 AND 연산
- `|`: 비트 단위로 OR 연산
- `^`: 비트 단위로 XOR 연산 (같으면 0 다르면 1)
- `~`: 피연산자의 모든 비트 반전
- `<<`: 피연산자의 비트열을 왼쪽으로 이동
- `>>`: 피연산자의 비트 열을 오른쪽으로 이동
- 일반적으로 비트 연산자는 다른 연산자에 비해 실행 시간이 적게 소요된다.

<br>

<br>

### 2. 활용 예시

1. `N & 1`: 홀수, 짝수 판별
   - 마지막 비트 값이 1인지 0인지를 보고 판단한다.
2. `1 << n`: 2<sup>n</sup>의 값을 가짐
   - 원소가 n개일 경우의 모든 부분집합의 수를 의미한다.
3. `i & (1 << j)`: i의 j번째 비트가 1인지 아닌지를 의미
   - 만약 i 가 01001010이고, j가 6이라면 `1<<6`은 01000000을 나타내고, `i&(1<<6)`은 01000000을 나타내어 2<sup>6</sup>의 값을 결과로 낼 것이다. 이 원리를 적용하여 부분집합의 어떤 원소가 존재하는 경우와 그렇지 않은 경우를 판단할 수 있다.
4. `^`: XOR 연산자를 두 번 사용하여 처음 값을 반환
   - XOR 연산자를 사용해서 변환된 값은 다시 XOR 연산자를 이용해서 복구할 수 있다.

<br>

<br>

### 3. 엔디안 (Endianness)

- 컴퓨터의 메모리와 같은 1차원의 공간에 여러 개의 연속된 대상을 배열하는 방법
- HW 아키텍처마다 다르다.
- 빅 엔디안, 리틀 엔디안의 두 가지 방식으로 구분된다.
  1. 빅 엔디안: 보통 큰 단위가 앞에 나온다.
     - 0x1234의 표현: 12 34
     - 네트워크에 사용되는 방식
  2. 리틀 엔디안: 작은 단위가 앞에 나온다.
     - 0x1234의 표현: 34 12
     - 대다수 데스크탑 컴퓨터에 사용되는 방식

<br>

<br>

<br>

<br>

출처: SW Expert Academy - Learn - Course - Programming Advanced

[SW Expert Academy - Programming Advanced Course](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDYSqAAbw5UW6)

