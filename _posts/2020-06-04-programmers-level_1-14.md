---
title: "Python으로 푸는 프로그래머스 level_1. 문자열 다루기 기본"
excerpt: "문자열 s의 길이가 4 혹은 6이고, 숫자로만 구성돼있는지 확인해주는 함수, solution을 완성하세요. 예를 들어 s가 a234이면 False를 리턴하고 1234라면 True를 리턴하면 됩니다."

categories:
  - codingTest

tags:
  - Programmers
  - Python

date: 2020-06-04
last_modified_at: 2020-07-29
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---
`Tag` `연습문제`<br>

**문제 설명**

문자열 s의 길이가 4 혹은 6이고, 숫자로만 구성돼있는지 확인해주는 함수, solution을 완성하세요. 예를 들어 s가 a234이면 False를 리턴하고 1234라면 True를 리턴하면 됩니다.

**제한 사항**

s는 길이 1 이상, 길이 8 이하인 문자열입니다.

**입출력 예**

s|	return
--|--
"a234"|	False
"1234"|	True

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/12918)

## 코드
```python
def solution(s):
    answer=True
    n=len(s)
    if (4==n or 6==n):
        for element in s:
            if ord(element)<48 or ord(element)>57:
                answer=False
                break
    else:
        answer=False

    return answer

```

## 설명
```python
answer=True
n=len(s)
if (4==n or 6==n):
    for element in s:
        if ord(element)<48 or ord(element)>57:
            answer=False
            break
else:
    answer=False

```
- ```ord()``` 는 ```문자->ASCII```  변환해주며 **문자:0 ~ 9 는 ASCII:48~57** 의 값을 갖는다.
> chr()는 ```ASCII->문자``` 변환

## 또 다른 풀이

```python
def solution(s):
  return s.isdigit() and len(s) in (4,6)
```
- ```isdigit()``` 는 모든 문자열이 숫자일경우 ```True```, 아닐 경우 ```False```를 반환한다.
- 문자열 길이가 4 와 6인지 ```in```을 통해 체크한다.
