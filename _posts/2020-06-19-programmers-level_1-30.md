---
title: Python으로 푸는 프로그래머스 level_1. 핸드폰 번호 가리기
excerpt: 프로그래머스 모바일은 개인정보 보호를 위해 고지서를 보낼 때 고객들의 전화번호의 일부를 가립니다. 전화번호가 문자열 phone_number로 주어졌을 때, 전화번호의 뒷 4자리를 제외한 나머지 숫자를 전부 * 으로 가린 문자열을 리턴하는 함수, solution을 완성해주세요.

categories:
  - codingTest

tags:
  - Programmers
  - Python

date: 2020-06-19
last_modified_at: 2020-07-29
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---


`Tag` `연습문제`<br>

**문제 설명**

프로그래머스 모바일은 개인정보 보호를 위해 고지서를 보낼 때 고객들의 전화번호의 일부를 가립니다.
전화번호가 문자열 phone_number로 주어졌을 때, 전화번호의 뒷 4자리를 제외한 나머지 숫자를 전부 * 으로 가린 문자열을 리턴하는 함수, solution을 완성해주세요.

**제한 조건**

s는 길이 4 이상, 20이하인 문자열입니다.

**입출력 예**

phone_number	|return
--|--
'01033334444'|	'*******4444'
'027778888'|	'*****8888'

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/12948)

## 코드
```python
def solution(phone_number):
    answer=''
    for idx,number in enumerate(phone_number[::-1]):
        if idx<=3:
            answer+=number
        else:
            answer+='*'

    return answer[::-1]
```

## 또 다른 풀이
```python
def solution(phone_number):
    return '*'*(len(phone_number)-4)+phone_number[-4:]
```
