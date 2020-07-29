---
title: Python으로 푸는 프로그래머스 level_1. 이상한 문자 만들기
excerpt: 문자열 s는 한 개 이상의 단어로 구성되어 있습니다. 각 단어는 하나 이상의 공백문자로 구분되어 있습니다. 각 단어의 짝수번째 알파벳은 대문자로, 홀수번째 알파벳은 소문자로 바꾼 문자열을 리턴하는 함수, solution을 완성하세요.

categories:
  - codingTest

tags:
  - Programmers
  - Python

date: 2020-06-10
last_modified_at: 2020-07-29
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---
`Tag` `연습문제`<br>

**문제 설명**

문자열 s는 한 개 이상의 단어로 구성되어 있습니다. 각 단어는 하나 이상의 공백문자로 구분되어 있습니다. 각 단어의 짝수번째 알파벳은 대문자로, 홀수번째 알파벳은 소문자로 바꾼 문자열을 리턴하는 함수, solution을 완성하세요.

**제한 사항**

문자열 전체의 짝/홀수 인덱스가 아니라, 단어(공백을 기준)별로 짝/홀수 인덱스를 판단해야합니다.
첫 번째 글자는 0번째 인덱스로 보아 짝수번째 알파벳으로 처리해야 합니다.

**입출력 예**

s	|return
--|--
try hello world	|TrY HeLlO WoRlD

**입출력 예 설명**

"try hello world"는 세 단어 "try", "hello", "world"로 구성되어 있습니다. 각 단어의 짝수번째 문자를 대문자로, 홀수번째 문자를 소문자로 바꾸면 "TrY", "HeLlO", "WoRlD"입니다. 따라서 "TrY HeLlO WoRlD" 를 리턴합니다.

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/12930)

## 코드
```python
def solution(s) :
    split_strings=s.split(' ')
    result=\
    [''.join([chr.upper() if (0==idx%2) \
    else chr.lower() for idx,chr in enumerate(split_string)])\
    for split_string in split_strings ]

    return ' '.join(result)
```

## 설명
```python
split_strings=s.split(' ')
```
- 공백을 기준으로 ```문자열 -> 리스트``` 변환한다.

```python
result=\
[''.join([chr.upper() if (0==idx%2) \
else chr.lower() for idx,chr in enumerate(split_string)])\
for split_string in split_strings ]
```
- ```list comprehension``` 으로 **공백기준 인덱스가 짝수일경우에는 대문자, 홀수일 경우에는 소문자** 로 변환한다.
- 내부 for문에서 변환된 문자들은 ```join()```을 통해 ```리스트 -> 문자열```로 변환한다
- 위의 코드는 아래의 코드와 동일하다.

 ```python
 result=[]
for split_string in split_strings:
  temp_list=[]
  for idx,chr in enumerate(split_string):
    if (0==idx%2): temp_list.append(chr.upper())
    else: temp_list(chr.lower())
  result.append(''.join(temp_list))

 ```
