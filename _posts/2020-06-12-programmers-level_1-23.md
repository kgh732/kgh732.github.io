---
title: Python으로 푸는 프로그래머스 level_1. 자연수 뒤집어 배열로 만들기
excerpt: 자연수 n을 뒤집어 각 자리 숫자를 원소로 가지는 배열 형태로 리턴해주세요. 예를들어 n이 12345이면 [5,4,3,2,1]을 리턴합니다.


categories:
  - codingTest

tags:
  - Programmers
  - Python

date: 2020-06-12
last_modified_at: 2020-07-29
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---

`Tag` `연습문제`<br>

**문제 설명**

자연수 n을 뒤집어 각 자리 숫자를 원소로 가지는 배열 형태로 리턴해주세요. 예를들어 n이 12345이면 [5,4,3,2,1]을 리턴합니다.

**제한 조건**

n은 10,000,000,000이하인 자연수입니다.

**입출력 예**

n|	return
--|--
12345	|[5,4,3,2,1]

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/12932)

## 코드
```python
def solution(n):

    answer=[int(chr) for chr in str(n)[::-1]]

    return answer
```
## 또 다른 풀이
```python

def solution(n):
    return list(map(int, reversed(str(n))))
```
