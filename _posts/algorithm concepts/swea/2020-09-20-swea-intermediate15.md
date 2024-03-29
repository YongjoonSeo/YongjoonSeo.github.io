---
layout: single
title: "8 : DP(동적 계획법, Dynamic Programming)"
excerpt: "동적 계획법 소개"
categories: 
- Computer Science
- Algorithm Concepts
tags:
- SWEA
- Dynamic Programming
- Fibonacci Sequence
---
## DP (동적 계획법, Dynamic Programming)

- <strong>DP(동적 계획법)</strong>

  - 먼저 입력 크기가 작은 부분 문제들을 모두 해결한 후, 그 결과를 이용하여 단계적으로 더 큰 크기의 부분 문제를 해결하고 최종적으로 원래의 문제를 해결하는 방법.
  
  - 부분 문제의 답으로부터 본 문제의 답을 구할 수 있는 문제에 적용할 수 있다.
  
- DP 적용하기
  
  1. 문제를 부분 문제로 분할
    2. 가장 작은 부분 문제부터 해를 구함
    3. 그 결과를 테이블에 저장하고, 테이블에 저장된 부분 문제의 해를 이용하여 더 큰 크기의 부분 문제의 해를 구함
  
  ```python
    # python 예시 - 피보나치 수열(3): DP (동적 계획법, Dynamic Programming)
    
    def fibo_DP(n):
        table = [0,1]
    
        for i in range(2, n+1):
            table.append(table[i-2] + table[i-1])
        # 재귀처럼 자기 자신을 다시 호출해야만 하는 방법만 있는 건 아니다.
        return table[n]
    
    for i in range(1,11):
        print(fibo_DP(i), end=' ')
        
    # 출력
    >>> 1 1 2 3 5 8 13 21 34 55
  ```
  
  - DP를 재귀적으로, 반복적으로 모두 구현할 수 있지만 반복적 구조로 DP를 구현한 게 성능 면에서 더 효율적이다.
  

<br>

<br>

<br>

<br>

출처: SW Expert Academy - Learn - Course - Programming Intermediate

[SW Expert Academy - Programming Intermediate course](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDN86AAXw5UW6)

