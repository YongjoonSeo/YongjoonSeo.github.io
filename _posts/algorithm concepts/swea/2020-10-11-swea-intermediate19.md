---
layout: single
title: "12-1 : 큐 (1)"
excerpt: "큐의 구조 및 종류"
categories: 
- Computer Science
- Algorithm Concepts
tags:
- SWEA
- Queue
---
## 큐 (1)

### <strong>큐?</strong>

- 스택처럼 삽입, 삭제의 위치가 제한적인 자료구조
- 가장 먼저 삽입된 원소부터 삭제된다: 선입선출 (FIFO, First-In-First-Out)

<br>

### <strong>큐의 구조 및 연산</strong>

- 큐에 저장된 원소 중 첫 번째 원소를 머리(Front)라고 하고, 마지막 원소를 꼬리(Rear)라고 한다.
- 큐 관련 연산
  - enQueue(item): 저장소에 자료 저장 (큐의 꼬리에 원소 삽입)
  - deQueue(): 저장소에서 자료를 꺼냄 (큐의 머리에서 삭제하고 반환, 선입선출)
  - Qpeek: 큐의 머리에서 원소를 삭제하지 않고 반환하는 연산
  - createQueue(): 공백 상태의 큐를 만드는 연산
  - isEmpty(): 큐가 공백인지 확인하는 연산
  - isFull(): 큐가 포화상태인지 확인하는 연산

<br>

### <strong>큐의 종류</strong>

- 선형 큐, 원형 큐, 연결 큐, 우선순위 큐
  - 선형 큐, 원형 큐: 리스트를 사용해서 구현
  - 연결 큐: 연결 리스트를 사용해서 구현

<br>

<br>

<br>

<br>

출처: SW Expert Academy - Learn - Course - Programming Intermediate

[SW Expert Academy - Programming Intermediate course](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDN86AAXw5UW6)

