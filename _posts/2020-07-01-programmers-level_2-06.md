---
title: Python으로 푸는 프로그래머스 level_2. 가장 큰 수

excerpt: 0 또는 양의 정수가 주어졌을 때, 정수를 이어 붙여 만들 수 있는 가장 큰 수를 알아내 주세요. 예를 들어, 주어진 정수가 [6, 10, 2]라면 [6102, 6210, 1062, 1026, 2610, 2106]를 만들 수 있고, 이중 가장 큰 수는 6210입니다.

categories:
  - codingTest

tags:
  - Programmers
  - Sorting
  - Python

date: 2020-07-01
last_modified_at: 2020-08-03
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---

`Tag` `정렬`<br>

**문제 설명**

0 또는 양의 정수가 주어졌을 때, 정수를 이어 붙여 만들 수 있는 가장 큰 수를 알아내 주세요.

예를 들어, 주어진 정수가 [6, 10, 2]라면 [6102, 6210, 1062, 1026, 2610, 2106]를 만들 수 있고, 이중 가장 큰 수는 6210입니다.

0 또는 양의 정수가 담긴 배열 numbers가 매개변수로 주어질 때, 순서를 재배치하여 만들 수 있는 가장 큰 수를 문자열로 바꾸어 return 하도록 solution 함수를 작성해주세요.

**제한 사항**

- numbers의 길이는 1 이상 100,000 이하입니다.
- numbers의 원소는 0 이상 1,000 이하입니다.
- 정답이 너무 클 수 있으니 문자열로 바꾸어 return 합니다.

**입출력 예**

numbers|	return
--|--
[6, 10, 2]|	"6210"
[3, 30, 34, 5, 9]|"9534330"

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/42746)

## 코드
```python
from functools import cmp_to_key
def solution(numbers):

    str_numbers=[str(number) for number in numbers]

    sorted_numbers=sorted(str_numbers,key=cmp_to_key(lambda a,b:int(a+b)-int(b+a)),reverse=True)
    answer=''.join(sorted_numbers)
    if 0==int(answer):
        answer='0'

    return answer
```

## 설명

```python
str_numbers=[str(number) for number in numbers]
```
- 주어진 ```numbers```를 수 그대로 비교한다면 표현범위를 넘어갈 가능성이 있기 때문에 문자열로 변환하여 비교하기 위해 ```str_numbers``` 를 만든다.
> list(map(str,numbers)) 로 대체가능.

```python
sorted_numbers=sorted(str_numbers,key=cmp_to_key(lambda a,b:int(a+b)-int(b+a)),reverse=True)
```
- ```sorted()``` , [```cmp_to_key()```](#cmp_to_key) 그리고 [comparator](#comparator)를 이용하여 sorting 한다.

>Ex)
**str_numbers=['3','30']** 라고 가정하자.
**lambda a,b:int(a+b)-int(b+a)** 에서 **a='3' b'=30'** 을 입력받고, **a+b='330'** , **b+a='303'** 의 결과를 만들어 내며 **int(a+b)=330** , **int(b+a)=303** 의 대소비교를 하여 정렬한다.

```python
answer=''.join(sorted_numbers)
if 0==int(answer):
    answer='0'
```
- ```join()``` 을 통해 ```리스트 -> 문자열``` 로 ```sorted_numbers```를 변환한다.
- 한가지 주의할 것은 ```numbers```의 모든 값이 0 일경우를 대비하여 예외처리를 한다.

### cmp_to_key

- python2.x 에서는 ```cmp()``` 를 지원하지만, python3.x 에서는 지원하지 않는다.
- ```sorted(cmp=) ``` 를 지원하지 않는다.
- 대신 ```functools.cmp_to_key```를 통해 ```comparator -> key``` 후```sorted(key=)```를 활용할수 있다.

### comparator

```python
def comparator(a,b):
  if a<b:
    return -1
  elif a==b:
    return 0
  else:
    return 1
```
