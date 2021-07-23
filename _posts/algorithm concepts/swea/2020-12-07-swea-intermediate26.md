---
layout: single
title: "15-1 : 트리 (1)"
excerpt: "트리 소개 및 용어 정리"
categories: 
- Algorithm Concepts
tags:
- SWEA
- Tree
---
## 트리 (1)

### 1. <strong>트리란?</strong>

- 비선형 구조
- 원소들 간에 1: n 관계를 가진다.
- 한 개 이상의 노드로 이루어진 유한 집합
  - 노드 중 최상위 노드를 <strong>루트(Root)</strong>라고 한다.
  - 나머지 노드들은 서브트리(SubTree)로 분리된다.
  (서브트리: 부모 노드와 연결된 간선을 끊었을 때 만들어지는 트리)

<br>

<br>

### 2. <strong>트리의 용어</strong>

#### a. 노드(node), 간선(edge)

- 노드: 트리의 원소
- 간선: 노드를 연결하는 선

<br>

#### b. 노드의 종류

- 루트 노드: 트리의 시작 노드
- 형제 노드: 같은 부모 노드의 자식 노드들
- 조상 노드: 간선을 따라 루트 노드까지 이르는 경로에 있는 모든 노드들
- 자손 노드: 서브트리에 있는 <strong>하위 레벨</strong>의 노드들

<br>

#### c. 차수(degree)

- 차수: 노드에 연결된 <strong>자식 노드</strong>의 수
  (cf. 그래프에서는 노드에 연결된 간선의 개수를 차수라고 한다.)
- 트리의 차수: 트리에 있는 노드의 차수 중에서 가장 큰 값
- 단말 노드(리프 노드, leaf): 차수가 0인 노드 (= 자손 노드가 없는 노드)

<br>

#### d. 깊이 및 높이

- 노드의 깊이(Depth): 루트에서 노드에 이르는 간선의 수
  (높이(height)라는 용어와 혼용하기도 하는 것 같다.)
- 레벨(Level): 같은 깊이 수준을 지칭
- 트리의 높이(Height of tree): 트리에 있는 노드의 높이 중 가장 큰 값, 혹은 트리의 최대 레벨

<br>

<br>

<br>

<br>

출처: SW Expert Academy - Learn - Course - Programming Intermediate

[SW Expert Academy - Programming Intermediate course](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDN86AAXw5UW6)

