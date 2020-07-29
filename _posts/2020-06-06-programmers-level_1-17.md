---
title: Python으로 푸는 프로그래머스 level_1. 수박수박수박수박수박수?
excerpt: 길이가 n이고, 수박수박수박수....와 같은 패턴을 유지는 문자열을 리턴하는 함수, solution을 완성하세요. 예를들어 n이 4이면 수박수박을 리턴하고 3이라면 수박수를 리턴하면 됩니다.

categories:
  - codingTest

tags:
  - Programmers
  - Python

date: 2020-06-06
last_modified_at: 2020-07-29
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---
`Tag` `연습문제`<br>

**문제 설명**

길이가 n이고, 수박수박수박수....와 같은 패턴을 유지는 문자열을 리턴하는 함수, solution을 완성하세요. 예를들어 n이 4이면 수박수박을 리턴하고 3이라면 수박수를 리턴하면 됩니다.

**제한 조건**

n은 길이 10,000이하인 자연수입니다.

**입출력 예**

n	|return
--|--
3|	수박수
4	|수박수박

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/12922)

## 코드
```python
def solution(n):

  quotient=n//2
  remainder=n%2
  result=['수박' for i in range(quotient)]
  if remainder==1:
      result.append('수')
  return ''.join(result)
```

## 또 다른 풀이
```python
def solution(n):
  return '수박'*(n//2)+'수'*(n%2)

```
