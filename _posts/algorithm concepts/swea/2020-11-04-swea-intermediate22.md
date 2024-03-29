---
layout: single
title: "12-4 : 큐 (4) - 우선순위 큐 개요"
excerpt: "우선순위 큐 소개 및 구현"
categories: 
- Computer Science
- Algorithm Concepts
tags:
- SWEA
- Queue
- Priority Queue
---
## 큐 (4)

### 1. <strong>우선순위 큐란?</strong>

- 우선순위를 가진 항목들을 저장하는 큐
- <strong>우선순위가 높은 것부터</strong> 먼저 나가게 됨 (우선순위가 같은 것 끼리는 선입선출)

<br>

<br>

### 2. <strong>우선순위 큐 구현하기</strong>

#### a. 구현 방법

1. 방법: 리스트를 사용하여 구현 or 우선순위 큐 라이브러리 사용
2. 연산:
   1. 기본 세팅: 큐의 구조랑 같다
   2. 삽입 (enQueue): 우선순위에 맞는 위치에 데이터를 삽입한다.
      삭제 (deQueue): 가장 앞에 있는 원소를 삭제하고 반환한다. (가장 우선순위가 높다.)

<br>

#### b. <strong>리스트를 활용해서 구현할 때의 문제점</strong>

- 데이터를 삽입하거나 삭제할 때 원소를 재배치하며 시간이 많이 걸리고 메모리 낭비가 크다.
- 연결 리스트로 우선순위 큐를 구현하더라도 비교 연산이 많이 필요하다.

<br>

#### c. <strong>문제점 해결방법</strong>

- PriorityQueue(maxsize) 클래스 사용
- 힙 자료구조 사용

<br>

<br>

<br>

<br>

출처: SW Expert Academy - Learn - Course - Programming Intermediate

[SW Expert Academy - Programming Intermediate course](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDN86AAXw5UW6)