---
layout: single
title: "15-2 : 트리 (2) - 이진 트리"
excerpt: "이진 트리의 종류 및 구현"
categories: 
- Algorithm Concepts
tags:
- SWEA
- Tree
- Binary Tree
---
## 트리 (2)

### 1. <strong>이진 트리란? (Binary Tree)</strong>

- 모든 노드들이 2개의 서브트리를 갖는 형태의 트리
        (노드가 자식 노드를 최대한 2개 까지만 가질 수 있다.)
- 레벨 i에서 노드의 최대 개수는 2<sup>i</sup>개
- 높이가 h인 이진 트리가 가질 수 있는 노드의 최소 개수는 (h+1)개, 최대 개수는 (2<sup>h+1</sup> - 1)개

<br>

<br>

### 2. <strong>이진 트리의 종류</strong>

- 포화 이진 트리, 완전 이진 트리, 편향 이진 트리

#### a. 포화 이진 트리 (Full Binary Tree)

- 모든 레벨에 노드가 포화 상태로 차 있는 이진 트리

#### b. 완전 이진 트리 (Complete Binary Tree)

- 높이가 h이고 노드 수가 n개일때, 1번부터 n번 노드까지 빈 자리가 없는 이진 트리
  (즉, n번 노드가 배치될 때까지 포화 이진 트리의 모양을 따르는 트리)

#### c. 편향 이진 트리 (Skewed Binary Tree)

- 높이 h에 대한 최소 개수의 노드를 가지면서 한쪽 방향의 자식 노드만을 가진 이진 트리
- 왼쪽 편향, 오른쪽 편향 이진 트리가 있다.

<br>

<br>

### 3. <strong>트리의 순회 (Traversal)</strong>

- 트리의 각 노드를 중복되지 않게 전부 방문하는 것
- 기본적인 순회 방법: 전위 순회, 중위 순회, 후위 순회

#### a. 전위 순회 (Preorder traversal)

- 자손 노드보다 루트 노드를 먼저 방문하는 방법. 왼쪽 오른쪽 순으로 방문한다.

#### b. 중위 순회 (Inorder traversal)

- 왼쪽 자손, 루트, 오른쪽 자손 순으로 방문하는 방법

#### c. 후위 순회 (Postorder traversal)

- 루트 노드보다 자손 노드를 먼저 방문하는 방법. 왼쪽 오른쪽 순으로 방문한다.

<br>

<br>

### 4. <strong>이진 트리 구현</strong>

#### a. 리스트를 이용한 이진 트리 구현

- 노드 번호를 리스트의 인덱스로 사용한다.

![이진 트리](https://i.ibb.co/2d6FVZV/treebinary.jpg)

![리스트 모양](https://i.ibb.co/0Kb7MB7/treetolist.jpg)

  - 루트의 번호를 1로 한다.
  - 레벨 n에 있는 노드에 대해 왼쪽부터 오른쪽으로 2<sup>n</sup>부터 2<sup>n+1</sup> - 1 까지 번호를 매긴다.
    - 노드 번호의 성질
    1. 노드 번호가 i인 노드의 부모 노드 번호: i // 2
      2. 노드 번호가 i인 노드의 자식 노드 번호
         - 왼쪽 자식 노드: 2 * i
         - 오른쪽 자식 노드: 2 * i + 1

<br>

#### b. <strong>리스트로 이진 트리를 구현할 때의 문제점</strong>

- 편향 이진 트리의 경우 사용하지 않는 리스트 원소에 대해 메모리 공간 낭비가 발생한다.
  - 연결 리스트를 통해 트리를 구현할 수 있다.
    - 이진 트리의 모든 노드는 최대 2개의 자식 노드를 가지므로, 각 노드에 왼쪽 자식 노드와 오른쪽 자식 노드로의 링크를 만들어 단순 연결 리스트로 구현할 수 있다.

<br>

<br>

<br>

<br>

출처: SW Expert Academy - Learn - Course - Programming Intermediate

[SW Expert Academy - Programming Intermediate course](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDN86AAXw5UW6)

