---
title: Python으로 푸는 프로그래머스 level_1. 시저암호
excerpt: 어떤 문장의 각 알파벳을 일정한 거리만큼 밀어서 다른 알파벳으로 바꾸는 암호화 방식을 시저 암호라고 합니다. 예를 들어 'AB'는 1만큼 밀면 'BC'가 되고, 3만큼 밀면 'DE'가 됩니다. z는 1만큼 밀면 'a'가 됩니다. 문자열 s와 거리 n을 입력받아 s를 n만큼 민 암호문을 만드는 함수, solution을 완성해 보세요.

categories:
  - codingTest

tags:
  - Programmers
  - Python

date: 2020-06-08
last_modified_at: 2020-07-29
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---
`Tag` `연습문제`<br>

**문제 설명**

어떤 문장의 각 알파벳을 일정한 거리만큼 밀어서 다른 알파벳으로 바꾸는 암호화 방식을 시저 암호라고 합니다. 예를 들어 'AB'는 1만큼 밀면 'BC'가 되고, 3만큼 밀면 'DE'가 됩니다. z는 1만큼 밀면 'a'가 됩니다. 문자열 s와 거리 n을 입력받아 s를 n만큼 민 암호문을 만드는 함수, solution을 완성해 보세요.

**제한 조건**

공백은 아무리 밀어도 공백입니다.
s는 알파벳 소문자, 대문자, 공백으로만 이루어져 있습니다.
s의 길이는 8000이하입니다.
n은 1 이상, 25이하인 자연수입니다.

**입출력 예**

s|	n	|result
--|--|--
'AB'|	1	|'BC'
'z'	|1	|'a'
'a B z'	|4	|'e F d'

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/12926)

## 코드
```python
def solution(s,n):
    upper_encryption=[chr(upper)for upper in range(65,91)]
    lower_encryption=[chr(lower)for lower in range(97,123)]

    answer=''
    for c in s:
        if ' '==c:
            answer+=c
        else:
            if c.isupper():
                answer+=upper_encryption[(ord(c)-65+n)%26]
            elif c.islower():
                answer+=lower_encryption[(ord(c)-97+n)%26]

    return answer

```

## 설명
```python
upper_encryption=[chr(upper)for upper in range(65,91)]
lower_encryption=[chr(lower)for lower in range(97,123)]
```
- ```upper_encryption``` = ['A',...,'Z']
- ```lower_encryption``` = ['a',...,'z']

```python
for c in s:
    if ' '==c:
        answer+=c
    else:
        if c.isupper():
            answer+=upper_encryption[(ord(c)-65+n)%26]
        elif c.islower():
            answer+=lower_encryption[(ord(c)-97+n)%26]

```
- 공백일 경우는 변환없이 추가한다.
- 대문자 일경우에는 ```upper_encryption```에서 ```ASCII CODE``` 를 이용하여 변환한다.
- 소문자 일경우에는 ```lower_encryption```에서 ```ASCII CODE``` 를 이용하여 변환한다.
