---
layout: single
title: "7-2 : 스택 (2) - 괄호 검사"
excerpt: "스택을 이용한 괄호 검사"
categories: 
- Computer Science
- Algorithm Concepts
tags:
- SWEA
- Data Structure
- Stack
---
## 스택 (2)

### <strong>스택 응용 예시 1 - 괄호검사</strong>

#### a. 개요

- 괄호검사 조건

  1. 왼쪽 괄호 개수 == 오른쪽 괄호 개수
  2. 괄호 종류가 같으면 왼쪽 괄호가 오른쪽 괄호보다 먼저 나와야 함
  3. 괄호 종류가 같은 것 끼리만 서로 열고 닫을 수 있다.
- 괄호 조사 알고리즘 개요
  1. 문자열에 있는 괄호를 차례대로 조사.
  2. 괄호를 만나면
     1. 왼쪽 괄호를 만나면 스택에 삽입
     2. 오른쪽 괄호를 만나면 스택에서 top 괄호를 삭제한 후, 짝이 맞는지 확인
        1. 스택이 비어있으면 --> 조건 1 or 조건 2 위배
        2. 괄호의 짝이 맞지 않으면 --> 조건 3 위배
        3. 문자열 끝까지 조사한 후에도 스택에 괄호가 남아있음 --> 조건 1 위배

<br>

#### b. 구현

```python
# python 예시 - 괄호검사

def BracketCheck(string):
    charlst = [0] * 128
    charlst[ord(')')] = '('
    charlst[ord('}')] = '{'
    charlst[ord(']')] = '['
    stack = []

    for char in string:
        if char == '(' or char == '{' or char =='[':
            stack.append(char) # 2-1
        elif char == ')' or char == '}' or char == ']': # 2-2
            if len(stack) == 0: return False # 2-2-1
            check = stack.pop()
            if check != charlst[ord(char)]: return False # 2-2-2
    
    if len(stack) > 0: return False # 2-2-3
    return True

print(BracketCheck("print('{} {}'.format(1, 2))"))
print(BracketCheck("N, M = map(int, input().split())"))
print(BracketCheck("print('#{} {}'.format(tc, find())"))

# 출력
True
True
False
```

<br>

<br>

<br>

<br>

출처: SW Expert Academy - Learn - Course - Programming Intermediate

[SW Expert Academy - Programming Intermediate course](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDN86AAXw5UW6)

