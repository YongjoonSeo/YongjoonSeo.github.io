---
layout: single
title: "15-3 : 트리 (3) - 이진 탐색 트리"
excerpt: "이진 탐색 트리 소개 및 구현"
categories: 
- Computer Science
- Algorithm Concepts
tags:
- SWEA
- Tree
- Binary Tree
- Binary Search Tree
---
## 트리 (3)

### 1. <strong>이진 탐색 트리 (Binary Search Tree)</strong>

- 탐색 작업을 효율적으로 하기 위한 자료구조
- 모든 원소는 서로 다른 값을 가진다.
- 왼쪽 서브트리 값 < 루트 노드의 값 < 오른쪽 서브트리 값
- 중위 순회하면 오름차순으로 정렬된 값을 얻을 수 있다.
- 시간복잡도: O(logn)  (평균)
  (한쪽으로 치우친 편향 이진 트리의 경우 (최악의 경우): O(n))

<br>

<br>

### 2. <strong>이진 탐색 트리의 연산</strong>

#### a. 탐색 연산

1. 루트에서 시작하여 값을 비교한다.
2. 루트 노드의 값과 찾는 값이 같다면 탐색 성공,
   찾는 값이 더 작다면 루트 노드의 왼쪽 서브트리로 가고,
   찾는 값이 더 크다면 루트 노드의 오른쪽 서브트리로 간다.
3. 2번의 과정을 재귀적으로 반복한다.

<br>

#### b. 삽입 연산

1. 삽입할 원소가 트리에 있는지 확인한다.
   (같은 원소가 트리에 있으면 삽입할 수 없다.)
2. 탐색에서 탐색이 실패하는 위치를 찾는다. 이 위치가 삽입 위치가 된다.
3. 삽입 위치에 원소를 삽입한다.

<br>

#### c. 삭제 연산

1. 삭제할 원소를 트리에서 찾는다.
2. 원소를 삭제하고 자식 노드 중 적절한 값으로 대체한다.
   1. 자식 노드가 없는 경우: 삭제만 하면 작업이 끝난다.
   2. 자식 노드가 한 개: 삭제한 노드의 위치로 자식 노드를 이동한다.
   3. 자식 노드가 두 개: 자식 노드의 왼쪽 가지에서 최대 노드를 찾아 삭제한 노드의 위치로 이동한다.
      (자식 노드의 오른쪽 가지에서 최소 노드를 찾아 이동해도 된다.)

<br>

<br>

### 3. 이진 탐색 트리 구현

#### a. 리스트로 구현

```python
# python 예시 - 이진 탐색 트리의 연산(1) - list로 구현 (탐색, 삽입)

def Searchidx(val):
    i = 1
    while i < len(lst):
        if lst[i] == val:
            return i
        elif lst[i] == None:
            return False, i
        elif lst[i] < val:
            i = i*2 + 1
        else:
            i = i*2
    else:
        return False

def Insertval(val):
    get = Searchidx(val)
    if type(get) == tuple:
        lst[get[1]] = val
# 확보된 리스트 공간 내에서만 삽입 연산이 가능하다.

lst = [None, 15, 9, 23, 3, 12, 17, 28, None, 8]

print(lst[1:])
print(Searchidx(8))
Insertval(1)
print(lst[1:])

# 출력
>>> [15, 9, 23, 3, 12, 17, 28, None, 8]
>>> 9
>>> [15, 9, 23, 3, 12, 17, 28, 1, 8]
```

<br>

#### b. 연결 리스트로 구현

```python
# python 예시 - 이진 탐색 트리의 연산(2) - 연결 리스트로 구현 (탐색, 삽입, 삭제)

class Node:

    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

    def __repr__(self):
        return str(self.data)

class BinarySearchTree:

    def __init__(self, *args):
        self.displst = []
        if args: 
            self.head = Node(args[0])
            self.displst.append(args[0])
        else: self.head = None
        for i in range(1, len(args)):
            self.Insert(args[i])
        
    def Search(self, val):
        node = Node(val)
        temphead = self.head
        while temphead:
            if temphead.data == node.data:
                return temphead
            elif temphead.data < node.data:
                if not temphead.right:
                    return False, temphead
                temphead = temphead.right
            else:
                if not temphead.left:
                    return False, temphead
                temphead = temphead.left
    
    def Insert(self, val):
        node = Node(val)
        temphead = self.Search(val)
        if type(temphead) == tuple: # val값을 가지는 노드를 찾지 못한 경우
            temphead = temphead[1]
        elif temphead:
            raise ValueError # BST에서는 중복된 값을 가질 수 없다.

        if node.data < temphead.data:
            temphead.left = node
            self.displst.append(val)
        else:
            temphead.right = node
            self.displst.append(val)
    
    def Delete(self, val):
        temphead = self.head # temphead: 삭제할 노드
        prevhead = None # prevhead: 삭제할 노드(temphead)의 부모 노드
        while temphead:
            if temphead.data == val: # 제거해야할 때
                if not temphead.left and not temphead.right: 
                    # (1) 자식 노드가 없는 경우
                    temphead = None
                    break
                elif temphead.left and temphead.right:
                    # (2) 자식 노드가 두 개 - 왼쪽 가지에서 최대 노드를 찾는다
                    # 1. 찾은 최대 노드(readj)의 부모 노드와 링크를 끊어준다
                    # 2. 찾은 최대 노드(readj)를 삭제할 노드의 부모, 자식 노드
                    #  	 (temphead의 부모, 자식 노드) 모두와 링크해준다.
                    readj = temphead.left # readj: 삭제 후 트리를 재조정할 최대 노드
                    prevreadj = None # prevreadj: readj의 부모 노드
                    while readj.right:
                        prevreadj = readj
                        readj = readj.right
                    
                    # 1번 과정.
                    # 찾은 최대 노드의 왼쪽 서브트리가 있는 경우 readj의 부모 노드와 연결하고,
                    # 그렇지 않으면 자식 노드가 없는 것이므로 None으로 변경한다.
                    if readj.left: 
                        prevreadj.right = readj.left
                    else:
                        prevreadj.right = None
                    
                    # 2번 과정.
                    if prevhead.data < readj.data:
                        prevhead.right = readj
                    else:
                        prevhead.left = readj
                    readj.left = temphead.left
                    readj.right = temphead.right
                    break

                else:
                    # (3) 자식 노드가 한 개 - 삭제한 노드의 위치로 자식 노드를 이동한다.
                    if temphead.left: childhead = temphead.left
                    elif temphead.right: childhead = temphead.right
                    if prevhead.data < childhead.data:
                        prevhead.right = childhead
                    else:
                        prevhead.left = childhead
                    break
            elif temphead.data < val:
                prevhead = temphead
                temphead = temphead.right
            else:
                prevhead = temphead
                temphead = temphead.left
        else:
            raise ValueError # 트리에 없는 값을 제거할 수 없다.
        self.displst.remove(val)

    def __repr__(self):
        return str(self.displst)

    
    
    
sample = BinarySearchTree(15, 9, 23, 3, 12, 17, 28, 8)
print(sample, end='\n\n')

sample.Insert(1)
print(sample, end='\n\n')

sample.Insert(4)
print(sample, end='\n\n')

sample.Delete(28)
print(sample, end='\n\n')

sample.Delete(8)
print(sample, end='\n\n')

sample.Delete(9)
print(sample)

# 출력
[15, 9, 23, 3, 12, 17, 28, 8]

[15, 9, 23, 3, 12, 17, 28, 8, 1]

[15, 9, 23, 3, 12, 17, 28, 8, 1, 4]

[15, 9, 23, 3, 12, 17, 8, 1, 4]

[15, 9, 23, 3, 12, 17, 1, 4]

[15, 23, 3, 12, 17, 1, 4]
# 출력에서 보여주는 건 단순히 자료가 들어온 순서이다.
```

<br>

<br>

<br>

<br>

출처: SW Expert Academy - Learn - Course - Programming Intermediate

[SW Expert Academy - Programming Intermediate course](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDN86AAXw5UW6)

