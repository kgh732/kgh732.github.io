---
title: "Python으로 푸는 프로그래머스 level_1. 모의고사"
excerpt: "수포자는 수학을 포기한 사람의 준말입니다. 수포자 삼인방은 모의고사에 수학 문제를 전부 찍으려 합니다. 수포자는 1번 문제부터 마지막 문제까지 다음과 같이 찍습니다."

categories:
  - codingTest

tags:
  - Programmers
  - Brute-Force
  - Python

date: 2020-05-23
last_modified_at: 2020-07-29
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---
`Tag` `완전탐색`<br>

**문제 설명**<br>
수포자는 수학을 포기한 사람의 준말입니다. 수포자 삼인방은 모의고사에 수학 문제를 전부 찍으려 합니다. 수포자는 1번 문제부터 마지막 문제까지 다음과 같이 찍습니다.

1번 수포자가 찍는 방식: 1, 2, 3, 4, 5, 1, 2, 3, 4, 5, ...

2번 수포자가 찍는 방식: 2, 1, 2, 3, 2, 4, 2, 5, 2, 1, 2, 3, 2, 4, 2, 5, ...

3번 수포자가 찍는 방식: 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, ...

1번 문제부터 마지막 문제까지의 정답이 순서대로 들은 배열 answers가 주어졌을 때, 가장 많은 문제를 맞힌 사람이 누구인지 배열에 담아 return 하도록 solution 함수를 작성해주세요.

**제한 조건**<br>
- 시험은 최대 10,000 문제로 구성되어있습니다.
- 문제의 정답은 1, 2, 3, 4, 5중 하나입니다.
- 가장 높은 점수를 받은 사람이 여럿일 경우, return하는 값을 오름차순 정렬해주세요.

**입출력 예**

answers|return
:-----:|:------:
[1,2,3,4,5]|[1]
[1,3,2,4,2]|[1,2,3]

**입출력 예 설명**

입출력 예 #1

- 수포자 1은 모든 문제를 맞혔습니다.
- 수포자 2는 모든 문제를 틀렸습니다.
- 수포자 3은 모든 문제를 틀렸습니다.

따라서 가장 문제를 많이 맞힌 사람은 수포자 1입니다.

입출력 예 #2

- 모든 사람이 2문제씩을 맞췄습니다.

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/42840)

## 코드

```python
def solution(answers):
    answer=[]
    math_hater={'first':'12345','second':'21232425','third':'3311224455'}
    first_cycle=len(math_hater['first'])
    second_cycle=len(math_hater['second'])
    third_cycle=len(math_hater['third'])

    correct=dict()
    for i,value in enumerate(answers):
        if(str(value)==math_hater['first'][i%first_cycle]):
            correct[1]=correct.get(1,0)+1

        if (str(value)==math_hater['second'][i%second_cycle]):
            correct[2]=correct.get(2,0)+1

        if (str(value) == math_hater['third'][i%third_cycle]):
            correct[3]=correct.get(3,0)+1


    max_grade=max(correct.values())
    for key in correct:
        if (max_grade == correct[key]):
            answer.append(key)

    return sorted(answer)
```

## 설명

- 1번 수포자는 `12345`,`12345`,... 반복된 구조로 찍는다.
- 2번 수포자는  `21232425`,`21232425`,... 반복된 구조로 찍는다.
- 3번 수포자는 `3311224455`,`3311224455`,... 반복된 구조로 찍는다.



```python
math_hater={'first':'12345','second':'21232425','third':'3311224455'}
first_cycle=len(math_hater['first'])
second_cycle=len(math_hater['second'])
third_cycle=len(math_hater['third'])
```
- 각각 수포자들의 주기를 저장해둔다.


```python
correct=dict()
for i,value in enumerate(answers):
    if(str(value)==math_hater['first'][i%first_cycle]):
        correct[1]=correct.get(1,0)+1

    if (str(value)==math_hater['second'][i%second_cycle]):
        correct[2]=correct.get(2,0)+1

    if (str(value) == math_hater['third'][i%third_cycle]):
        correct[3]=correct.get(3,0)+1

```
- `modulo 연산`을 통해 정답 횟수를 저장한다.

```python
max_grade=max(correct.values())
for key in correct:
    if (max_grade == correct[key]):
        answer.append(key)

return sorted(answer)
```
- 최고석차를 저장한 후 key값을 조회하여 추출한다.
- 오름차순으로 정렬한다.

## 또 다른 풀이
- 기본 dictionary는 key:value 저장시 key삽입이 random 으로 이루어 진다.
- 따라서 `collections.OrderedDict`를 사용하거나, 3개의 element를 가지는 list를 선언하여 구현할 수 있다.

```python
from collections import OrderedDict

def solution(answers):
    answer=[]
    math_hater={'first':'12345','second':'21232425','third':'3311224455'}
    first_cycle=len(math_hater['first'])
    second_cycle=len(math_hater['second'])
    third_cycle=len(math_hater['third'])

    correct=OrderedDict()

    for i,value in enumerate(answers):
        if(str(value)==math_hater['first'][i%first_cycle]):
            correct[1]=correct.get(1,0)+1

        if (str(value)==math_hater['second'][i%second_cycle]):
            correct[2]=correct.get(2,0)+1

        if (str(value) == math_hater['third'][i%third_cycle]):
            correct[3]=correct.get(3,0)+1

    max_grade=max(correct.values())
    for key in correct:
        if (max_grade == correct[key]):
            answer.append(key)

    return answer

```

```python

def solution2(answers):
    answer=[]
    math_hater={'first':'12345','second':'21232425','third':'3311224455'}
    first_cycle=len(math_hater['first'])
    second_cycle=len(math_hater['second'])
    third_cycle=len(math_hater['third'])

    correct=[0,0,0]
    for i,value in enumerate(answers):
        if(str(value)==math_hater['first'][i%first_cycle]):
            correct[0]+=1

        if (str(value)==math_hater['second'][i%second_cycle]):
            correct[1]+=1

        if (str(value) == math_hater['third'][i%third_cycle]):
            correct[2]+=1


    max_grade=max(correct)
    for i in range(3):
        if (max_grade == correct[i]):
            answer.append(i+1)

    return answer


```
