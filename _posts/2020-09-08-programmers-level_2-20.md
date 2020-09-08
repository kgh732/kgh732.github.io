---
title: Python으로 푸는 프로그래머스 level_2. 올바른 괄호

excerpt: 괄호가 바르게 짝지어졌다는 것은 '(' 문자로 열렸으면 반드시 짝지어서 ')' 문자로 닫혀야 한다는 뜻입니다. 예를 들어 "()()" 또는 "(())()" 는 올바른 괄호입니다. ")()(" 또는 "(()(" 는 올바르지 않은 괄호입니다. '(' 또는 ')' 로만 이루어진 문자열 s가 주어졌을 때, 문자열 s가 올바른 괄호이면 true를 return 하고, 올바르지 않은 괄호이면 false를 return 하는 solution 함수를 완성해 주세요.


categories:
  - codingTest

tags:
  - Programmers
  - Stack
  - Python

date: 2020-09-08
last_modified_at: 2020-09-08
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---


`Tag` `스택(Stack)` <br>

**문제 설명**

괄호가 바르게 짝지어졌다는 것은 '(' 문자로 열렸으면 반드시 짝지어서 ')' 문자로 닫혀야 한다는 뜻입니다. 예를 들어

- "()()" 또는 "(())()" 는 올바른 괄호입니다.
- ")()(" 또는 "(()(" 는 올바르지 않은 괄호입니다.

'(' 또는 ')' 로만 이루어진 문자열 s가 주어졌을 때, 문자열 s가 올바른 괄호이면 true를 return 하고, 올바르지 않은 괄호이면 false를 return 하는 solution 함수를 완성해 주세요.

**제한사항**

- 문자열 s의 길이 : 100,000 이하의 자연수
- 문자열 s는 '(' 또는 ')' 로만 이루어져 있습니다.

**입출력 예**

s	|answer
--|--
"()()"|	true
"(())()"|	true
")()("|	false
"(()("|	false

**입출력 예 설명**

**입출력 예 #1,2,3,4**

문제의 예시와 같습니다.

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/12909?language=python3)

## 코드

```python
def solution(s):
    stack = []
    answer = True
    for parentheses in s:
        if "(" == parentheses:
            stack.append(parentheses)
        elif ")" == parentheses:
            if stack:
                stack.pop()
            else:
                answer = False

    if stack:
        answer = False
    return answer

if __name__=="__main__":
    test_s="(()("
    print(solution(test_s))

```

## 설명

- `"("` 일 경우 `stack` 에 담아둔다.
- `")"` 일 경우 `stack` 이 비어있지 않았을 경우에만 꺼내고, 그렇지 않은 경우 **잘못된 괄호** 이다.
- 모든 괄호 체크 후 `stack`이 아직 남아 있다면, 이것 역시 **잘못된 괄호** 이다.
