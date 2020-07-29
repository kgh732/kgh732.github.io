---
title: " Python으로 푸는 프로그래머스 level_1. 문자열 내 p와 y의 개수"
excerpt: "대문자와 소문자가 섞여있는 문자열 s가 주어집니다. s에 'p'의 개수와 'y'의 개수를 비교해 같으면 True, 다르면 False를 return 하는 solution를 완성하세요. 'p', 'y' 모두 하나도 없는 경우는 항상 True를 리턴합니다. 단, 개수를 비교할 때 대문자와 소문자는 구별하지 않습니다."

categories:
  - codingTest

tags:
  - Programmers
  - Python

date: 2020-06-02
last_modified_at: 2020-07-29
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---
`Tag` `연습문제`<br>


**문제 설명**

대문자와 소문자가 섞여있는 문자열 s가 주어집니다. s에 'p'의 개수와 'y'의 개수를 비교해 같으면 True, 다르면 False를 return 하는 solution를 완성하세요. 'p', 'y' 모두 하나도 없는 경우는 항상 True를 리턴합니다. 단, 개수를 비교할 때 대문자와 소문자는 구별하지 않습니다.

예를 들어 s가 pPoooyY면 true를 return하고 Pyy라면 false를 return합니다.

**제한사항**

문자열 s의 길이 : 50 이하의 자연수
문자열 s는 알파벳으로만 이루어져 있습니다.

**입출력 예**

s|	answer
--|--
"pPoooyY"|	true
"Pyy"|	false

**입출력 예 설명**

**입출력 예 #1**

'p'의 개수 2개, 'y'의 개수 2개로 같으므로 true를 return 합니다.

**입출력 예 #2**

'p'의 개수 1개, 'y'의 개수 2개로 다르므로 false를 return 합니다.

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/12916)

## 코드
```python
def solution(s):
    answer = True
    lower_s=s.lower()
    p_count=lower_s.count('p')
    y_count=lower_s.count('y')
    if (p_count==0 and y_count==0) or (p_count==y_count):
        answer=True
    else:
        answer=False

    return answer
```

## 설명

```python
lower_s=s.lower()
p_count=lower_s.count('p')
y_count=lower_s.count('y')
if (p_count==0 and y_count==0) or (p_count==y_count):
    answer=True
else:
    answer=False

```
- 모든 문자를 소문자로 바꾼후 ```count()```를 이용하여 특정 문자의 갯수를 센 후 조건을 체크한다.

## 또 다른 풀이

```python
def solution(s):
    answer = False
    lower_s=s.lower()
    p_count=lower_s.count('p')
    y_count=lower_s.count('y')
    if p_count==y_count:
      answer=True

    return answer
```
- ```p,y 가 없는 경우``` 는 ```p의 갯수=y의 갯수``` 를 내포하고 있음으로 조건문을 줄일수 있다.
