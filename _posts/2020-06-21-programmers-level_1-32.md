---
title: Python으로 푸는 프로그래머스 level_1. x만큼 간격이 있는 n개의 숫자
excerpt: 함수 solution은 정수 x와 자연수 n을 입력 받아, x부터 시작해 x씩 증가하는 숫자를 n개 지니는 리스트를 리턴해야 합니다. 다음 제한 조건을 보고, 조건을 만족하는 함수, solution을 완성해주세요.

categories:
  - codingTest

tags:
  - Programmers
  - Python

date: 2020-06-21
last_modified_at: 2020-07-29
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---

`Tag` `연습문제`<br>

**문제 설명**

함수 solution은 정수 x와 자연수 n을 입력 받아, x부터 시작해 x씩 증가하는 숫자를 n개 지니는 리스트를 리턴해야 합니다. 다음 제한 조건을 보고, 조건을 만족하는 함수, solution을 완성해주세요.

**제한 조건**

x는 -10000000 이상, 10000000 이하인 정수입니다.
n은 1000 이하인 자연수입니다.

**입출력 예**

x|	n|	answer
--|--|--
2|	5	|[2,4,6,8,10]
4	|3	|[4,8,12]
-4|	2	|[-4, -8]

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/12954)

## 코드
```python
def solution(x,n):
    answer=[]
    if 0==x:
        answer=[0]*n
    else:
        answer= [i for i in range(x,x*n+x,x)]
    return answer
```
