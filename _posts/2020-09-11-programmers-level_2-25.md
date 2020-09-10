---
title: Python으로 푸는 프로그래머스 level_2. 최댓값과 최솟값

excerpt: 문자열 s에는 공백으로 구분된 숫자들이 저장되어 있습니다. str에 나타나는 숫자 중 최소값과 최대값을 찾아 이를 (최소값) (최대값)형태의 문자열을 반환하는 함수, solution을 완성하세요.
예를들어 s가 "1 2 3 4"라면 "1 4"를 리턴하고, "-1 -2 -3 -4"라면 "-4 -1"을 리턴하면 됩니다.

categories:
  - codingTest

tags:
  - Programmers
  - Python

date: 2020-09-11
last_modified_at: 2020-09-11
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---


`Tag` `연습문제` <br>


**문제 설명**

문자열 s에는 공백으로 구분된 숫자들이 저장되어 있습니다. str에 나타나는 숫자 중 최소값과 최대값을 찾아 이를 (최소값) (최대값)형태의 문자열을 반환하는 함수, solution을 완성하세요.
예를들어 s가 "1 2 3 4"라면 "1 4"를 리턴하고, "-1 -2 -3 -4"라면 "-4 -1"을 리턴하면 됩니다.

**제한 조건**

s에는 둘 이상의 정수가 공백으로 구분되어 있습니다.

**입출력 예**

s|	return
--|--
"1 2 3 4"|	"1 4"
"-1 -2 -3 -4"	|"-4 -1"
"-1 -1"	|"-1 -1"

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/12939)

## 코드

```python
def solution(s):
    answer = ''
    split_s = s.split(' ')
    max_val = min_val = int(split_s[0])

    for idx in range(1, len(split_s)):
        if max_val < int(split_s[idx]):
            max_val = int(split_s[idx])
        if min_val > int(split_s[idx]):
            min_val = int(split_s[idx])
    return str(min_val) + " " + str(max_val)


if __name__ == "__main__":
    test_s = "1 2 3 4"
    print(solution(test_s))
```
