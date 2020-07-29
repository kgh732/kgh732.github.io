---
title: Python으로 푸는 프로그래머스 level_1. 정수 제곱근 판별
excerpt: 임의의 양의 정수 n에 대해, n이 어떤 양의 정수 x의 제곱인지 아닌지 판단하려 합니다. n이 양의 정수 x의 제곱이라면 x+1의 제곱을 리턴하고, n이 양의 정수 x의 제곱이 아니라면 -1을 리턴하는 함수를 완성하세요.

categories:
  - codingTest

tags:
  - Programmers
  - Python

date: 2020-06-14
last_modified_at: 2020-07-29
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---
`Tag` `연습문제`<br>


**문제 설명**

임의의 양의 정수 n에 대해, n이 어떤 양의 정수 x의 제곱인지 아닌지 판단하려 합니다.
n이 양의 정수 x의 제곱이라면 x+1의 제곱을 리턴하고, n이 양의 정수 x의 제곱이 아니라면 -1을 리턴하는 함수를 완성하세요.

**제한 사항**

n은 1이상, 50000000000000 이하인 양의 정수입니다.

**입출력 예**

n|	return
--|--
121	|144
3|	-1

**입출력 예 설명**

**입출력 예#1**

121은 양의 정수 11의 제곱이므로, (11+1)를 제곱한 144를 리턴합니다.

**입출력 예#2**

3은 양의 정수의 제곱이 아니므로, -1을 리턴합니다.

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/12934)

## 코드
```python
def solution(n):
    answer=-1
    sqrt=n**0.5

    if sqrt == int(sqrt):
        answer=int((sqrt+1)**2)

    return answer
```
