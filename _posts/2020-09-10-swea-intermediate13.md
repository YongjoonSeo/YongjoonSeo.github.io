---
layout: single
title: "7-3 : 스택 (3) - 함수 호출, 재귀"
excerpt: "스택의 원리를 사용하는 함수 호출, 재귀"
categories: 
- Algorithm Concepts
tags:
- SWEA
- Data Structure
- Stack
- Recursion
- Fibonacci Sequence
---
## 스택 (3)

### <strong>스택 응용 예시 2 - 함수 호출</strong>

- 후입선출 구조로 함수 수행순서 관리
  1. 함수 수행과 관련된 정보를 스택 프레임에 저장
  2. 함수 실행이 끝나면 시스템 스택의 top 원소를 삭제(pop)하면서 프레임에 저장되어있던 복귀주소를 확인하고 복귀
  3. 이 과정이 반복되어 전체 프로그램 수행이 종료되면 시스템 스택은 공백 스택이 됨

<br>

<br>

### 재귀 호출

- 자기 자신을 호출하여 순환 수행되는 것
- 스택 프레임으로 스택에 저장되는 값이 <span style="color:red">입력 값이 다른</span> 같은 함수의 스택 프레임을 저장한다.

```python
# python 예시 - 피보나치 수열(1): 재귀 호출

def fibo(n):
    if n == 1 or n == 2:
        return 1
    else:
        return fibo(n-1) + fibo(n-2)

result = []
for i in range(1,11):
    result.append(fibo(i))

print(*result)

# 출력
>>> 1 1 2 3 5 8 13 21 34 55
```

--> 중복 호출이 많이 일어난다.

<br>

- 참고: <strong>메모이제이션(Memoization)</strong>

  - 이전에 계산한 값을 저장해서 매번 다시 계산하지 않도록 하는 기술
  - DP(동적계획법, Dynamic Programming)의 핵심이 되는 기술

  ```python
  # python 예시 - 피보나치 수열(2): 재귀 호출 + 메모이제이션
  def fibo_memo(n):
      global memo
      if n >= 2 and len(memo) <= n: 
          # 계산 값을 저장한 리스트(memo)의 길이로 제약조건을 걸어 
          # 한 번 계산한 값에 대해 다시 함수를 호출하지 않도록 한다.
          # 부등호를 정할 때, 계산 되기 이전에는 함수를 불러올 수 있도록 한다.
          memo.append(fibo_memo(n-1) + fibo_memo(n-2))
      return memo[n]
  
  memo = [0, 1]
  result = []
  for i in range(1, 11):
      result.append(fibo_memo(i))
  print(*result)
  
  # 출력
  >>> 1 1 2 3 5 8 13 21 34 55
  ```


<br>

<br>

<br>

<br>

출처: SW Expert Academy - Learn - Course - Programming Intermediate

[SW Expert Academy - Programming Intermediate course](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDN86AAXw5UW6)

