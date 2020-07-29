---
title: "Python으로 푸는 프로그래머스 level_1. 완주하지 못한 선수"
excerpt: "수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다."


categories:
  - codingTest

tags:
  - Programmers
  - Algorithm
  - Hash
  - Python

date: 2020-05-22
last_modified_at: 2020-05-27
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---

`Tag` `해시`<br>

**문제 설명**<br>
수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.

마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.

**제한사항**<br>
마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.
completion의 길이는 participant의 길이보다 1 작습니다.
참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.
참가자 중에는 동명이인이 있을 수 있습니다.

**입출력 예**<br>

participant	| completion | return
:---------:|:----:|:----:
[leo, kiki, eden]|[eden, kiki]|leo
[marina, josipa, nikola, vinko, filipa]|[josipa, filipa, marina, nikola]|	vinko
[mislav, stanko, mislav, ana]|[stanko, ana, mislav]	|mislav

**입출력 예 설명**<br>

**예제 #1**
leo는 참여자 명단에는 있지만, 완주자 명단에는 없기 때문에 완주하지 못했습니다.

**예제 #2**
vinko는 참여자 명단에는 있지만, 완주자 명단에는 없기 때문에 완주하지 못했습니다.

**예제 #3**
mislav는 참여자 명단에는 두 명이 있지만, 완주자 명단에는 한 명밖에 없기 때문에 한명은 완주하지 못했습니다.

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/42576)

## 코드

```python
def solution(participant, completion):
    result=dict()
    for key in participant:
        # 중복처리를 어떻게 할까?
        # key-value = name - count
        result[key]=result.get(key,0)+1 #default, key값이 없으면 0

    for key in completion:
            result[key]=result.get(key)-1 # value count 감소
            if 0==result[key]: #완주한 사람은
                result.pop(key) #꺼내주자

    answer=result.popitem()[0] #남아 있는 key(name)가 완주하지 못한사람!

    return answer
```

## 설명
```python
for key in participant:
    result[key]=result.get(key,0)+1
```
- 해싱을 위해 파이썬의 dictionary를 사용한다.
- 중복 key를 처리하기 위해 counting 값을 value로 활용한다.

```python
for key in completion:
        result[key]=result.get(key)-1 # value count 감소
        if 0==result[key]: #완주한 사람은
            result.pop(key) #꺼내주자

```

- 특정 key 의 value가 0이라는 것은 완주했음을 의미한다.
- 완주한 경우에는 dictionary에서 꺼내준다.

```python
    answer=result.popitem()[0]
```
- 남아 있는 key는 완주하지 못한 사람이다.
- item을 꺼내서 key 값을 가져온다.


## 질문
**아래의 코드는 처음 작성했던 것인데 정확성은 맞았지만, 효율성이 0점이였다. 그렇다면 효율성이 떨어진 이유는 무엇인가?**

```python
def solution(participant, completion):
    for c in completion:
        participant.remove(c)
    answer = participant[0]
    return answer
```
- 파이썬의 `remove()` 는 **O(N)** 이다.
- 즉, 위의 코드는 **O($$N^2$$)** 이다


>따라서 dictionary 구조를 이용하여 시간복잡도를 개선해야했다.
