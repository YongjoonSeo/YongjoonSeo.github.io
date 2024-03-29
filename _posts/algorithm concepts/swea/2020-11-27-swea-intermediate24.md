---
layout: single
title: "14-1 : 연결 리스트 (1)"
excerpt: "연결 리스트 소개 및 구현"
categories: 
- Computer Science
- Algorithm Concepts
tags:
- SWEA
- Linked List
---
## 연결 리스트 (Linked List)

### 1. <strong>리스트(List)의 종류</strong>

#### a. 순차 리스트

- **배열을 기반으로 구현된 리스트**
- 파이썬의 리스트는 동적 배열로 작성된 순차 리스트다.
- 자료를 삽입하고 삭제할 때 원소를 이동하는 작업이 필요하다.

<br>

#### b. 연결 리스트

- **메모리의 동적 할당을 기반으로 구현된 리스트**
- 파이썬 내에 연결 리스트가 정의된 라이브러리는 없다.

<br>

#### c. 이중 연결 리스트

- **노드의 양쪽에 링크 필드가 있고, 그 사이에 한 개의 데이터 필드가 있음**
- 12-3. 큐 (3) - deque (덱) 에서 소개했던 deque은 
  내부적으로 이중 연결 리스트로 구현되어 있다.
  하지만 deque이 double-ended queue로 만들어졌기 때문에 
  linked list가 필요한 모든 경우에 사용할 수 있는 것은 아니다.

<br>

<br>

### 2. <strong>리스트 복사의 종류</strong>

#### a. 단순히 주소만 참조하는 복사

- 주소를 참조하는 방식. 복사한 리스트의 항목을 바꾸면 원래 리스트의 항목도 함께 바뀐다.

- lst2 = lst1

<br>

#### b. 얕은 복사

- 리스트의 원소를 복사해온다. 리스트가 중첩되어 있을 경우엔 원소로 들어있는 리스트는 주소를 참조하고, 그 리스트들을 담고 있는 전체 리스트만 id가 달라지게 된다.
  (간단히 말해서 한 겹만 복사해 오는 것)

- lst2 = lst1[:]
- lst2 = [] 
  lst2.extend(lst1)
- lst2 = list(lst1)
- lst2 = lst1.copy()
- import copy
  lst2 = copy.copy(lst1)
- lst2 = [i for i in lst1]

<br>

#### c. 깊은 복사

- 리스트 내부의 리스트에 있는 원소도 재귀적으로 모두 복사해오는 방법.
  (중첩 리스트라도 내부의 모든 원소를 복사하는 것)

- import copy
  lst2 = copy.deepcopy(lst1)

<br>

<br>

### 3. <strong>연결 리스트</strong>

#### a. 개요

- 개별적으로 있는 원소의 주소를 연결(링크)하여 하나의 자료구조를 이룬다.
- 노드: 연결 리스트에서 하나의 원소에 필요한 데이터를 가지는 자료단위이며 데이터 필드와 링크 필드로 이루어져 있다.
  - 데이터 필드: 원소의 값을 저장
  - 링크 필드: 다음 노드의 주소를 저장

- 헤드: 연결 리스트의 처음 노드를 가리키는 포인터.

```python
# python 예시 - 연결 리스트: 데이터 저장 및 출력

class Node: # 노드 클래스 안에는 데이터 필드와 링크 필드가 있다.

    def __init__(self, data):
        self.data = data # 데이터 필드
        self.next = None # 링크 필드
    
    def __repr__(self):
        return str(self.data)

class LinkedList:

    def __init__(self):
        self.head = None # 연결 리스트의 초기 헤드는 None이다.
        self.count = 0
   
llist = LinkedList()
first = Node(1)
llist.head = first 
second = Node(2)
third = Node(3)

first.next = second
second.next = third

while llist.head:
    print(llist.head.data)
    llist.head = llist.head.next

# 출력
1
2
3
```

<br>

#### b. <strong>연결 리스트 사용을 위한 함수</strong>

- addtoFirst()
  : 연결리스트의 앞쪽에 원소 추가
- addtoLast()
  : 연결 리스트의 뒤쪽에 원소 추가
- add()
  : 연결 리스트의 특정 위치에 원소 추가
- delete()
  : 연결 리스트의 특정 위치의 원소 삭제
- get
  : 연결 리스트의 특정 위치의 원소 반환

```python
# python 예시 - 연결 리스트: 함수 구현

class LinkedList:

    def __init__(self):
        self.head = None # 연결 리스트의 초기 헤드는 None이다.
        self.count = 0


    def addtoFirst(self, node):
        # 1. head를 추가하는 노드로 옮기고 
        # 2. 추가하는 node를 본래 head 위치로 링크한다.
        temphead = self.head # 2번 과정을 수행하기 위한 준비과정
        self.head = node # 1번 과정 수행 완료
        self.head.next = temphead # 2번 과정 수행 완료
        self.count = self.count + 1
    

    def addtoLast(self, node):
        # 1. 연결 리스트의 마지막 노드에 접근해서 
        # 2. 그 노드를 추가하는 노드에 링크해준다.
        tempcnt = self.count
        temphead = self.head
        while tempcnt > 1:
            temphead = temphead.next
            tempcnt -= 1
        temphead.next = node
        self.count = self.count + 1


    def length(self):
        return self.count


    def get(self, idx):
        assert abs(idx) <= self.count and idx != self.count, IndexError.__name__
        temphead = self.head # 헤드는 바꿔주면 안 된다.
        if idx >= 0:
            while idx > 0:
                temphead = temphead.next
                idx -= 1
        else:
            while idx < -1:
                temphead = self.head
                idx += 1
        return temphead
        # temphead를 들어온 idx만큼 옮겨주고 
        # 그 노드에 저장된 데이터를 반환한다.
    

    def add(self, idx, node):
        if idx == 0 or idx < -self.count:
            # 들어오는 idx 값이 0이거나 리스트의 크기의 음수보다 작으면 
            # 가장 처음에 원소를 추가한다.
            LinkedList.addtoFirst(self, node)
            return
        elif idx >= self.count: 
            # 들어오는 idx 값이 리스트의 크기보다 크거나 같으면 
            # 가장 마지막에 원소를 추가한다.
            LinkedList.addtoLast(self, node)
            return
        else:
            temphead = self.head
            idx -= 1
            if idx >= 0:
                while idx > 0:
                    temphead = temphead.next
                    idx -= 1
            else:
                while idx < -1:
                    temphead = self.head
                    idx += 1
            # 노드를 추가하기 원하는 지점까지 이동한다.
            nextnode = temphead.next 
            # 간단히 말해서 a노드와 b노드 사이에 c노드를 추가하는 상황.
            # a노드: temphead // b노드: nextnode // c노드: node
            temphead.next = node # 이전 노드(a)의 링크를 추가하는 노드(c)로 바꾼다.
            node.next = nextnode # 추가하는 노드(c)의 링크를 이후 노드(b)로 걸어준다.
            self.count = self.count + 1


    def delete(self, idx): 
        # a b c 노드가 있으면 b를 제거한다고 가정했을 때
        # a의 링크를 c로 바꿔주기만 하면 된다.
        assert abs(idx) <= self.count and idx != self.count, IndexError.__name__
        if not self.head:
            print(self.head)
            raise IndexError.__name__
        
        if idx == 0: # idx가 0일 때는 head의 링크만 바꿔주면 된다.
            temp = self.head
            self.head = self.head.next
            self.count = self.count - 1
            return temp

        idx -= 1 # 목표 지점 바로 전 노드를 찾아야 한다.
        temphead = self.head
        if idx >= 0:
            while idx > 0:
                temphead = temphead.next
                idx -= 1
        else:
            while idx < -1:
                temphead = self.head
                idx += 1
        # temphead : a 노드
        temp = temphead.next
        temphead.next = temphead.next.next
        self.count = self.count - 1
        return temp


    def __repr__(self):
        temphead = self.head
        result = []
        while temphead:
            result.append(str(temphead.data))
            temphead = temphead.next
        return '[' + ', '.join(result) + ']'
```

<br>

#### c. <strong>연결 리스트 구현 전체 코드</strong>

```python
# python 예시 - 연결 리스트

class Node: # 노드 클래스 안에는 데이터 필드와 링크 필드가 있다.

    def __init__(self, data):
        self.data = data # 데이터 필드
        self.next = None # 링크 필드
    
    def __repr__(self):
        return str(self.data)

class LinkedList:

    def __init__(self):
        self.head = None # 연결 리스트의 초기 헤드는 None이다. (head)
        self.count = 0


    def addtoFirst(self, node):
        # 1. head를 추가하는 노드로 옮기고 
        # 2. 추가하는 node를 본래 head 위치로 링크한다.
        temphead = self.head # 2번 과정을 수행하기 위한 준비과정
        self.head = node # 1번 과정 수행 완료
        self.head.next = temphead # 2번 과정 수행 완료
        self.count = self.count + 1
    

    def addtoLast(self, node):
        # 1. 연결 리스트의 마지막 노드에 접근해서 
        # 2. 그 노드를 추가하는 노드에 링크해준다.
        tempcnt = self.count
        temphead = self.head
        while tempcnt > 1:
            temphead = temphead.next
            tempcnt -= 1
        temphead.next = node
        self.count = self.count + 1


    def length(self):
        return self.count


    def get(self, idx):
        assert abs(idx) <= self.count and idx != self.count, IndexError.__name__
        temphead = self.head # 헤드는 바꿔주면 안 된다.
        if idx >= 0:
            while idx > 0:
                temphead = temphead.next
                idx -= 1
        else:
            while idx < -1:
                temphead = self.head
                idx += 1
        return temphead
        # temphead를 들어온 idx만큼 옮겨주고 그 노드에 저장된 데이터를 반환한다.
    

    def add(self, idx, node):
        if idx == 0 or idx < -self.count:
            # 들어오는 idx 값이 0이거나 리스트의 크기의 음수보다 작으면 
            # 가장 처음에 원소를 추가한다.
            LinkedList.addtoFirst(self, node)
            return
        elif idx >= self.count: 
            # 들어오는 idx 값이 리스트의 크기보다 크거나 같으면 
            # 가장 마지막에 원소를 추가한다.
            LinkedList.addtoLast(self, node)
            return
        else:
            temphead = self.head
            idx -= 1
            if idx >= 0:
                while idx > 0:
                    temphead = temphead.next
                    idx -= 1
            else:
                while idx < -1:
                    temphead = self.head
                    idx += 1
            # 노드를 추가하기 원하는 지점까지 이동한다.
            nextnode = temphead.next 
            # 간단히 말해서 a노드와 b노드 사이에 c노드를 추가하는 상황.
            # a노드: temphead // b노드: nextnode // c노드: node
            temphead.next = node # 이전 노드(a)의 링크를 추가하는 노드(c)로 바꾼다.
            node.next = nextnode # 추가하는 노드(c)의 링크를 이후 노드(b)로 걸어준다.
            self.count = self.count + 1


    def delete(self, idx): 
        # a b c 노드가 있으면 b를 제거한다고 가정했을 때
        # a의 링크를 c로 바꿔주기만 하면 된다.
        assert abs(idx) <= self.count and idx != self.count, IndexError.__name__
        if not self.head:
            print(self.head)
            raise IndexError.__name__
        
        if idx == 0: # idx가 0일 때는 head의 링크만 바꿔주면 된다.
            temp = self.head
            self.head = self.head.next
            self.count = self.count - 1
            return temp

        idx -= 1 # 목표 지점 바로 전 노드를 찾아야 한다.
        temphead = self.head
        if idx >= 0:
            while idx > 0:
                temphead = temphead.next
                idx -= 1
        else:
            while idx < -1:
                temphead = self.head
                idx += 1
        # temphead : a 노드
        temp = temphead.next
        temphead.next = temphead.next.next
        self.count = self.count - 1
        return temp


    def __repr__(self):
        temphead = self.head
        result = []
        while temphead:
            result.append(str(temphead.data))
            temphead = temphead.next
        return '[' + ', '.join(result) + ']'




first = Node(1)
second = Node('22')
third = Node(3)
fourth = Node('44')
sample = LinkedList()

sample.addtoFirst(first)
print(sample, end='\n\n')

sample.addtoLast(second)
print(sample, end='\n\n')

sample.add(1, third)
print(sample, end='\n\n')

print(f'{sample.delete(2)} 삭제', end='\n\n')

print(sample, end='\n\n')

print(sample.get(1), end='\n\n')

print(sample)


# 출력
[1]

[1, 22]

[1, 3, 22]

22 삭제

[1, 3]

3

[1, 3]
```

<br>

<br>

<br>

<br>

출처: SW Expert Academy - Learn - Course - Programming Intermediate

[SW Expert Academy - Programming Intermediate course](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDN86AAXw5UW6)

