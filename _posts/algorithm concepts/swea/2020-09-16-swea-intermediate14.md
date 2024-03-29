---
layout: single
title: "7-4 : 스택 (4) - 계산기"
excerpt: "중위표기식을 후위표기식으로 바꾸기"
categories: 
- Computer Science
- Algorithm Concepts
tags:
- SWEA
- Data Structure
- Stack
- Infix to Postfix
---
## 스택 (4)

### <strong>스택 응용 예시 3 - 계산기</strong>

- 중위표기식을 후위표기식으로 바꾼 다음, 스택을 활용하여 바꾼 식의 연산을 수행한다.
  

<br>

#### a. 중위표기식 --> 후위표기식

- 스택을 활용하여 <strong><span style="color:red">연산자</span></strong>를 컨트롤한다.
- 괄호로 연산자들을 묶어주고, 우선순위가 높은 연산자부터 pop되도록 한다.
- 우선순위가 같은 연산자는 들어온 순서대로 pop되도록 한다.
- 스택이 비어있거나 스택 내부에 여는 괄호가 없을 때 닫는 괄호가 들어오거나, 문자열을 모두 탐색했는데 스택에 남은 게 있는 경우 "Error"를 출력한다.

```python
# python 예시 - 중위표기식 -> 후위표기식

def ISP(char): # in-stack priority
    lst = ['(', '+-', '*/', 'blank']
    for i in lst:
        if char in i:
            return lst.index(i)

def ICP(char): # in-coming priority
    lst = ['blank', '+-', '*/', '(']
    for i in lst:
        if char in i:
            return lst.index(i)

def Postfix(expression):
    operands = '0123456789'
    result = ''
    stack = []

    for i in expression:
        if i in operands: # 피연산자
            result += i
        else:             # 연산자와 괄호
            if i == ')':    # 연산자와 괄호 중 ')'
                if not stack:
                    return 'Error'
                else:
                    top = stack.pop()
                    while top != '(':
                        result += top
                        if stack: top = stack.pop()
                        if top != '(' and not stack:
                            return 'Error'
            else:           # 연산자와 괄호 중 ')'을 제외한 것들
                if not stack:
                    stack.append(i)
                elif ISP(stack[-1]) <= ICP(i):
                    if ISP(stack[-1]) == ICP(i):
                        result += stack.pop()
                    stack.append(i)
                else:
                    result += i

    if stack: return 'Error'
    return result

expression = '(6+5*(2-8)/2)'
expression2 = '(6+5*(2-8))/2)'
expression3 = ')(6+5*(2-8)/2)'
expression4 = '((6+5*(2-8)/2)'

print(Postfix(expression))
print(Postfix(expression2))
print(Postfix(expression3))
print(Postfix(expression4))

# 출력
>>> 6528-*2/+
>>> Error
>>> Error
>>> Error
```

<br>

#### b. 후위표기식 연산

- 스택을 활용하여 <strong><span style="color:red">피연산자</span></strong>를 컨트롤한다.
- (pop 2번) <연산자> (pop 1번) 과 같은 방식으로 연산을 수행하고, 그 결과 값을 다시 스택에 넣는다.
- 문자열을 모두 읽을 때까지 위의 과정을 수행하고, 다 읽으면 스택에 남아있는 마지막 항목을 반환한다.

```python
# python 예시 - 후위표기식 연산

def add(a, b):
    return a + b
def subtract(a, b):
    return a - b
def multiply(a, b):
    return a * b
def divide(a, b):
    if b: return a // b

def Cal_Postfix(expression):
    stack = []
    operands = '0123456789'

    if expression == 'Error': return '잘못된 입력입니다.'
    else:
        for i in expression:
            if i in operands:
                stack.append(int(i))
            else:
                right = stack.pop()
                left = stack.pop()
                temp = 0
                if i == '+': temp = add(left, right)
                elif i == '-': temp = subtract(left, right)
                elif i == '*': temp = multiply(left, right)
                else: temp = divide(left, right)
                stack.append(temp)
        return stack.pop()

print(Cal_Postfix(Postfix(expression)))
print(Cal_Postfix(Postfix(expression2)))

# 출력
>>> -9
>>> 잘못된 입력입니다.
```

<br>

#### c. <strong>전체 코드</strong>

```python
# python 예시 - 중위표기식 -> 후위표기식 변환 후 연산

def ISP(char): # in-stack priority
    lst = ['(', '+-', '*/', 'blank']
    for i in lst:
        if char in i:
            return lst.index(i)

def ICP(char): # in-coming priority
    lst = ['blank', '+-', '*/', '(']
    for i in lst:
        if char in i:
            return lst.index(i)

def Postfix(expression):
    operands = '0123456789'
    result = ''
    stack = []

    for i in expression:
        if i in operands: # 피연산자
            result += i
        else:             # 연산자와 괄호
            if i == ')':    # 연산자와 괄호 중 ')'
                if not stack:
                    return 'Error'
                else:
                    top = stack.pop()
                    while top != '(':
                        result += top
                        if stack: top = stack.pop()
                        if top != '(' and not stack:
                            return 'Error'
            else:           # 연산자와 괄호 중 ')'을 제외한 것들
                if not stack:
                    stack.append(i)
                elif ISP(stack[-1]) <= ICP(i):
                    if ISP(stack[-1]) == ICP(i):
                        result += stack.pop()
                    stack.append(i)
                else:
                    result += i

    if stack: return 'Error'
    return result

def add(a, b):
    return a + b
def subtract(a, b):
    return a - b
def multiply(a, b):
    return a * b
def divide(a, b):
    if b: return a // b

def Cal_Postfix(expression):
    stack = []
    operands = '0123456789'

    if expression == 'Error': return '잘못된 입력입니다.'
    else:
        for i in expression:
            if i in operands:
                stack.append(int(i))
            else:
                right = stack.pop()
                left = stack.pop()
                temp = 0
                if i == '+': temp = add(left, right)
                elif i == '-': temp = subtract(left, right)
                elif i == '*': temp = multiply(left, right)
                else: temp = divide(left, right)
                stack.append(temp)
        return stack.pop()

expression = '(6+5*(2-8)/2)'
expression2 = '(6+5*(2-8))/2)'
expression3 = ')(6+5*(2-8)/2)'
expression4 = '((6+5*(2-8)/2)'

print(Postfix(expression))
print(Postfix(expression2))
print(Postfix(expression3))
print(Postfix(expression4))
print()
print(Cal_Postfix(Postfix(expression)))
print(Cal_Postfix(Postfix(expression2)))

# 출력
6528-*2/+
Error
Error
Error

-9
잘못된 입력입니다.
```

<br>

<br>

<br>

<br>

출처: SW Expert Academy - Learn - Course - Programming Intermediate

[SW Expert Academy - Programming Intermediate course](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDN86AAXw5UW6)

