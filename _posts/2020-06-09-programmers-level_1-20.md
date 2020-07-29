---
title: Python으로 푸는 프로그래머스 level_1. 약수의 합
excerpt: 정수 n을 입력받아 n의 약수를 모두 더한 값을 리턴하는 함수, solution을 완성해주세요.

categories:
  - codingTest

tags:
  - Programmers
  - Python

date: 2020-06-09
last_modified_at: 2020-07-29
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---

`Tag` `연습문제`<br>



**문제 설명**

정수 n을 입력받아 n의 약수를 모두 더한 값을 리턴하는 함수, solution을 완성해주세요.

**제한 사항**

n은 0 이상 3000이하인 정수입니다.

**입출력 예**

n	|return
--|--
12|	28
5	|6

**입출력 예 설명**

**입출력 예 #1**

12의 약수는 1, 2, 3, 4, 6, 12입니다. 이를 모두 더하면 28입니다.

**입출력 예 #2**

5의 약수는 1, 5입니다. 이를 모두 더하면 6입니다.

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/12928)

## 코드
```python
def solution(n):
    result=[element for element in range(1,n+1) if 0==n%element]
    return sum(result)
```
