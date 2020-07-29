---
title: "Python으로 푸는 프로그래머스 level_1. 문자열 내림차순으로 배치하기"
excerpt: "문자열 s에 나타나는 문자를 큰것부터 작은 순으로 정렬해 새로운 문자열을 리턴하는 함수, solution을 완성해주세요.
s는 영문 대소문자로만 구성되어 있으며, 대문자는 소문자보다 작은 것으로 간주합니다."

categories:
  - codingTest

tags:
  - Programmers
  - Python

date: 2020-06-03
last_modified_at: 2020-07-29
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---
`Tag` `연습문제`<br>


**문제 설명**

문자열 s에 나타나는 문자를 큰것부터 작은 순으로 정렬해 새로운 문자열을 리턴하는 함수, solution을 완성해주세요.
s는 영문 대소문자로만 구성되어 있으며, 대문자는 소문자보다 작은 것으로 간주합니다.

**제한 사항**

str은 길이 1 이상인 문자열입니다.
**입출력 예**

s|	return
--|--
Zbcdefg	|gfedcbZ

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/12917)

## 코드

```python
def solution(s):
    sorted_string=sorted(s,reverse=True)
    return ''.join(sorted_string)
```
- ```reverse=True```를 통해 내림차순정렬한다.
- ```sorted() ``` 는 ```iterable```로 부터 새로운 정렬된 리스트를 만드는 내장함수이다.
- ```join()``` 을 통해 ```리스트->문자열``` 변환한다.
> ```split()``` 함수는 ```문자열->리스트```변환한다.
