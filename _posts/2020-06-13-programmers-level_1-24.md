---
title: Python으로 푸는 프로그래머스 level_1. 정수 내림차순으로 배치하기
excerpt: 함수 solution은 정수 n을 매개변수로 입력받습니다. n의 각 자릿수를 큰것부터 작은 순으로 정렬한 새로운 정수를 리턴해주세요. 예를들어 n이 118372면 873211을 리턴하면 됩니다.

categories:
  - codingTest

tags:
  - Programmers
  - Python

date: 2020-06-13
last_modified_at: 2020-07-29
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---
`Tag` `연습문제`<br>

**문제 설명**

함수 solution은 정수 n을 매개변수로 입력받습니다. n의 각 자릿수를 큰것부터 작은 순으로 정렬한 새로운 정수를 리턴해주세요. 예를들어 n이 118372면 873211을 리턴하면 됩니다.

**제한 조건**

n은 1이상 8000000000 이하인 자연수입니다.

**입출력 예**

n|	return
--|--
118372|	873211

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/12933)

## 코드
```python
def solution(n):
    return int(''.join(sorted(str(test_n),reverse=True)))
```
