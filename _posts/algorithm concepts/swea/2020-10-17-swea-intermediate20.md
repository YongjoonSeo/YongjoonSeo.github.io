---
layout: single
title: "12-2 : 큐 (2) - 큐의 종류"
excerpt: "선형 큐, 원형 큐, 연결 큐"
categories: 
- Computer Science
- Algorithm Concepts
tags:
- SWEA
- Queue
---
## 큐 (2)

### 1. <strong>선형 큐</strong>

#### a. 선형 큐의 구조

- 1차원 리스트를 활용한다. (큐의 크기 == 리스트의 크기)
- front - 머리 인덱스 // rear - 꼬리 인덱스
  - 초기: front = rear = -1
  - 공백: front == rear
  - 포화: rear == len(lst) - 1  (꼬리 인덱스가 리스트의 마지막 인덱스가 되면 포화)

<br>

#### b. <strong>선형 큐 구현하기</strong>

1. 기본 세팅
   - 초기화 함수: CreateQueue()
     크기 n인 1차원 리스트를 만들고 front = rear = -1로 설정
     (고정된 크기의 리스트를 사용)
   - 공백 상태 체크 함수: isEmpty()
     front == rear 이면 True를 반환하는 함수
   - 포화 상태 체크 함수: isFull()
     rear == len(lst) - 1이면 True를 반환하는 함수
2. 연산
   - 삽입: enQueue(item)
     - 큐가 포화 상태인 경우 삽입하지 못함
     - rear 값을 +1 한 후 [rear] 자리에 item을 저장
   - 삭제: deQueue()
     - 큐가 공백 상태인 경우 삭제하지 못함
     - front 값을 +1 한 후 [front] 자리의 item을 반환
       (front 값을 +1 해주기 때문에 리스트에서 원소를 별도로 삭제해줄 필요가 없다.)
   - 검색: Qpeek()
     - 큐의 가장 앞에 있는 원소를 찾아서 반환
     - [front + 1] 자리의 item을 반환
       (큐에서 item이 삭제되지 않는 이유는 front 값을 바꾸지 않기 때문이다.)

<br>

#### c. <strong>선형 큐의 문제점</strong>

- 고정된 리스트를 사용하기 때문에 사용할 큐의 크기 만큼의 공간을 미리 확보해야 한다. 이때문에 메모리 낭비가 발생한다.
- 삽입, 삭제를 하다보면 리스트의 앞부분에 활용할 수 있는 공간이 있더라도 꼬리가 len(lst) - 1에 도달하면 큐가 포화된 것으로 인식되어 더이상 큐를 사용할 수 없다.

<br>

<br>

### 2. <strong>원형 큐</strong>

#### a. 원형 큐의 구조

- 선형 큐와 같은 방식이지만, 머리와 꼬리를 붙여 원형을 이룬다고 생각한다.

  - 이 방식을 구현하기 위해 인덱스를 순환해야 하므로 % 연산자를 사용한다.

- front - 머리 인덱스 // rear - 꼬리 인덱스

  - 초기: front = rear = 0
  - 공백: front == rear
  - 포화: (rear + 1) % len(lst) == front  (rear의 다음 위치 == front)

  > 공백, 포화 상태를 쉽게 구분하기 위해 front자리는 항상 비워둠.

<br>

#### b. <strong>원형 큐 구현하기</strong>

1. 기본 세팅
   - 초기화 함수: CreateQueue()
     크기 n인 1차원 리스트를 만들고 front = rear = 0으로 설정
     (고정된 크기의 리스트를 사용)
   - 공백 상태 체크 함수: isEmpty()
     front == rear 이면 True를 반환하는 함수
   - 포화 상태 체크 함수: isFull()
     (rear + 1) % len(lst) == front 이면 True를 반환하는 함수
2. 연산
   - 삽입: enQueue(item)
     - 큐가 포화 상태인 경우 삽입하지 못함
     - rear = (rear + 1) % len(lst) 한 후 [rear] 자리에 item을 저장
   - 삭제: deQueue()
     - 큐가 공백 상태인 경우 삭제하지 못함
     - front = (front + 1) % len(lst) 한 후 [front] 자리의 item을 반환
       (원소가 남아있더라도 rear가 다시 그 위에 정보를 덮어쓰기 때문에 리스트에서 원소를 별도로 삭제해줄 필요가 없다.)

<br>

#### c. <strong>원형 큐의 문제점</strong>

- rear 또는 front가 배열의 끝까지 가면 배열의 앞부분으로 이동해야 한다. 
  이때 rear이나 front를 이동하기 위한 연산이 필요하고, 이를 위해 추가적인 시간이 소모되므로 큐의 효율이 낮아진다.
- 선형 큐와 마찬가지로 포화 상태가 되면 더이상 큐를 사용할 수 없다.

<br>

#### 참고: 파이썬의 리스트를 활용한 큐

- 파이썬의 리스트는 크기를 동적으로 변경할 수 있어서 메모리를 절약할 수 있다.
- 하지만 큐를 구현하는 도중에 정보를 삽입, 삭제, 이동하는 연산을 수행하는 데 많은 시간이 걸린다는 단점이 있다.

<br>

<br>

### 3. <strong>연결 큐</strong>

#### a. 연결 큐의 구조

- 단순 연결 리스트를 활용한다.
  - 큐의 원소: 단순 연결 리스트의 각 노드
  - 큐의 원소 순서: 노드의 연결 순서 (링크로 연결됨)
- front - 첫 번째 노드를 가리키는 링크 // rear - 마지막 노드를 가리키는 링크
  - 초기: front = rear = None
  - 공백: front = rear = None
  - 포화: 없음 (계속 노드를 추가할 수 있기 때문에 연결 큐에서는 포화 상태가 없다.)

<br>

#### b. <strong>연결 큐 구현하기</strong>

1. 기본 세팅
   - 초기화 함수: CreateLinkedQueue()
     front = None, rear = None으로 설정 (포인터 변수만 생성)
   - 공백 상태 체크 함수: isEmpty()
     front = rear = None 이면 True를 반환하는 함수
   - 포화 상태 체크 함수: 필요 없음
2. 연산
   - 삽입: enQueue(item)
     - 새로운 노드를 만들고 데이터로 item을 저장
     - 연결 큐가 공백인 경우: front, rear 모두 해당 노드로 링크한다.
       연결 큐가 공백이 아닌 경우: rear만 해당 노드로 링크한다.
   - 삭제: deQueue()
     - 큐가 공백 상태인 경우 삭제하지 못함
     - front를 다음 노드로 링크시켜준다.
       -> 다음 노드로 링크시키기 전에 기존의 노드를 따로 저장해두고 반환한다.
     - 삭제 후 공백 큐가 되는 경우 rear도 None으로 설정한다.

<br>

#### c. <strong>큐 모듈</strong> - import해서 사용 (import queue)

- 큐 모듈의 클래스

  - queue.Queue(maxsize=0)
    : 선입선출 큐의 생성자. 
    maxsize는 큐에 배치할 수 있는 항목 수의 상한이며 0보다 작거나 같으면 큐의 크기는 무한하다.
  - queue.LifoQueue(maxsize=0)
    : 후입선출 큐의 생성자. (사실상 스택의 개념) maxsize는 위와 동일
  - queue.PriorityQueue(maxsize=0)
    : 우선순위 큐의 생성자. maxsize는 위와 동일
    : 가장 낮은 값을 갖는 항목이 먼저 꺼내진다. 
    --> 항목의 전형적인 패턴은 (priority_number, data) 형식의 튜플이며 가장 낮은 값을 갖는 항목은 sorted(list(entries))[0] 에 의해 반환되는 항목이다.

- 본 클래스들의 메서드

  - qsize()
    : 큐의 크기를 반환
  - put(item, block=True, timeout=None)
    : 큐에 item을 넣는다. (삽입)
  - get(block=True, timeout=None)
    : 큐에서 항목을 제거하고 반환한다. (삭제)
    : 큐 객체 특성에 맞추어 반환한다. 
    (ex. 우선순위 큐와 다른 큐의 get 결과 값은 다를 수 있다.)
  - empty()
    : 큐가 비어 있으면 True, 아니면 False를 반환한다.
  - full()
    : 큐가 가득 차면 True, 아니면 False를 반환한다.

<br>

<br>

<br>

<br>

출처: SW Expert Academy - Learn - Course - Programming Intermediate

[SW Expert Academy - Programming Intermediate course](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDN86AAXw5UW6)

