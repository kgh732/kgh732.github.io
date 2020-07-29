---
title: Python으로 푸는 프로그래머스 level_1. 문자열을 정수로 바꾸기
excerpt: 문자열 s를 숫자로 변환한 결과를 반환하는 함수, solution을 완성하세요.

categories:
  - codingTest

tags:
  - Programmers
  - Python

date: 2020-06-07
last_modified_at: 2020-07-29
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---

`Tag` `연습문제`<br>

**문제 설명**

문자열 s를 숫자로 변환한 결과를 반환하는 함수, solution을 완성하세요.

**제한 조건**

s의 길이는 1 이상 5이하입니다.
s의 맨앞에는 부호(+, -)가 올 수 있습니다.
s는 부호와 숫자로만 이루어져있습니다.
s는 0으로 시작하지 않습니다.

**입출력 예**

예를들어 str이 '1234'이면 1234를 반환하고, '-1234'이면 -1234를 반환하면 됩니다.
str은 부호(+,-)와 숫자로만 구성되어 있고, 잘못된 값이 입력되는 경우는 없습니다.

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/12925)

## 코드

```python
def solution(s):
    return int(s)
```

## 설명

**숫자 -> 문자열**

```python
number=123.00001
str(number)
#`123.00001`
```

**문자열 -> 숫자**

```python
float_number=123.00001
float(number)
#123.00001
int_number=-123
int(number)
#-123
```
> Python 3 기준이며, Python 2 에서는 결과물이 다를 수 있다.

## 또 다른 풀이
```python
def solution(s):
  result=0
  for idx,ch in enumerate(s[::-1]):
    if '-'== ch:
      result*=-1
    elif '+'== ch:
        pass
    else:
      result+=(ord(ch)-48)*(10**idx)

  return result

```
## 설명
```python
for idx,ch in enumerate(s[::-1]):
  if '-'== ch:
    result*=-1
  elif '+'== ch:
      pass
  else:
    result+=(ord(ch)-48)*(10**idx)
```
- 주어진 문자열을 ```s[::-1]```으로 역순 접근한다.
- ```ASCII 코드 ```가 ```'0':48 ~ '9':57``` 사실을 이용하여 정수값 추출후 자릿수를 계산해준다.
