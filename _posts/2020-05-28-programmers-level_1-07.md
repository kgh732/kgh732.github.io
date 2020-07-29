---
title: "Python으로 푸는 프로그래머스 level_1. 가운데 글자 가져오기"
excerpt: "단어 s의 가운데 글자를 반환하는 함수, solution을 만들어 보세요. 단어의 길이가 짝수라면 가운데 두글자를 반환하면 됩니다.
"

categories:
  - codingTest

tags:
  - Programmers
  - Python

date: 2020-05-28
last_modified_at: 2020-07-29
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---
`Tag` `연습문제`<br>

**문제 설명**

단어 s의 가운데 글자를 반환하는 함수, solution을 만들어 보세요. 단어의 길이가 짝수라면 가운데 두글자를 반환하면 됩니다.

**제한사항**

s는 길이가 1 이상, 100이하인 스트링입니다.

**입출력 예**

s|	return
---|---
"abcde"|	"c"
"qwer"|	"we"

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/12903)

## 코드

```python
def solution(s):
    answer=''
    n=len(s)
    if n%2==0:
        start=n//2-1
        end=start+2
        answer=s[start:end]
    else:
        start=n//2
        answer=s[start]


    return answer

```

## 설명

```python
n=len(s)
if n%2==0:
    start=n//2-1
    end=start+2
    answer=s[start:end]
else:
    start=n//2
    answer=s[start]
```
- 문자열 길이를 가져와서 짝수일 경우는 중간값부터 그다음 글자, 홀수일 경우 중간값을 가져온다.
