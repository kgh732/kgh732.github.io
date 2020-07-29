---
title: Python으로 푸는 프로그래머스 level_1. 자릿수 더하기
excerpt: 자연수 N이 주어지면, N의 각 자릿수의 합을 구해서 return 하는 solution 함수를 만들어 주세요. 예를들어 N = 123이면 1 + 2 + 3 = 6을 return 하면 됩니다.

categories:
  - codingTest

tags:
  - Programmers
  - Python

date: 2020-06-11
last_modified_at: 2020-07-29
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---

`Tag` `연습문제`<br>

**문제 설명**

자연수 N이 주어지면, N의 각 자릿수의 합을 구해서 return 하는 solution 함수를 만들어 주세요.
예를들어 N = 123이면 1 + 2 + 3 = 6을 return 하면 됩니다.

**제한사항**

N의 범위 : 100,000,000 이하의 자연수

**입출력 예**

N|	answer
--|--
123	|6
987	|24

**입출력 예 설명**

**입출력 예 #1**

문제의 예시와 같습니다.

**입출력 예 #2**

9 + 8 + 7 = 24이므로 24를 return 하면 됩니다.

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/12931)

## 코드
```python
def solution(n):
    string_n=str(n)
    answer=0
    for chr in string_n:
        answer+=ord(chr)-48
    return answer
```

## 또 다른 풀이
```python
def solution(n):
  if n<10:
    return n
  return (n%10)+solution(n//10)
```
