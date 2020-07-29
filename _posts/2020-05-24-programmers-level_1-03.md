---
title: "Python으로 푸는 프로그래머스 level_1. k 번째 수"
excerpt: "배열 array의 i번째 숫자부터 j번째 숫자까지 자르고 정렬했을 때, k번째에 있는 수를 구하려 합니다."

categories:
  - codingTest

tags:
  - Programmers
  - Sort
  - Python

date: 2020-05-24
last_modified_at: 2020-07-29
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---
`Tag` `정렬`<br>

**문제 설명**<br>
배열 array의 i번째 숫자부터 j번째 숫자까지 자르고 정렬했을 때, k번째에 있는 수를 구하려 합니다.

예를 들어 array가 [1, 5, 2, 6, 3, 7, 4], i = 2, j = 5, k = 3이라면 array의 2번째부터 5번째까지 자르면 [5, 2, 6, 3]입니다.
1에서 나온 배열을 정렬하면 [2, 3, 5, 6]입니다.
2에서 나온 배열의 3번째 숫자는 5입니다.
배열 array, [i, j, k]를 원소로 가진 2차원 배열 commands가 매개변수로 주어질 때, commands의 모든 원소에 대해 앞서 설명한 연산을 적용했을 때 나온 결과를 배열에 담아 return 하도록 solution 함수를 작성해주세요.

**제한사항**<br>
array의 길이는 1 이상 100 이하입니다.
array의 각 원소는 1 이상 100 이하입니다.
commands의 길이는 1 이상 50 이하입니다.
commands의 각 원소는 길이가 3입니다.

**입출력 예**<br>

array|	commands|	return
:-----:|:-----:|:-----:
[1, 5, 2, 6, 3, 7, 4]	|\[[2, 5, 3], [4, 4, 1], [1, 7, 3]]	|[5, 6, 3]


**입출력 예 설명**<br>
- [1, 5, 2, 6, 3, 7, 4]를 2번째부터 5번째까지 자른 후 정렬합니다. [2, 3, 5, 6]의 세 번째 숫자는 5입니다.
- [1, 5, 2, 6, 3, 7, 4]를 4번째부터 4번째까지 자른 후 정렬합니다. [6]의 첫 번째 숫자는 6입니다.
- [1, 5, 2, 6, 3, 7, 4]를 1번째부터 7번째까지 자릅니다. [1, 2, 3, 4, 5, 6, 7]의 세 번째 숫자는 3입니다.


[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/42748)

## 코드

```python
def solution(array, commands):

    answer=[sorted(array[command[0]-1:command[1]])[command[2]-1] for command in commands]

    return answer

```

## 설명

```python
answer=[sorted(array[command[0]-1:command[1]])[command[2]-1] for command in commands]
```
- `List comprehension`을 사용하는 것이 파이썬 속도 관점에서 일반 for문 보다 더 빠르다.
- `List slicing`을 활용하여 영역 추출 후 정렬된 배열의 목표위치 요소를 가져온다.



## 또 다른 풀이

- `map` 과 `lambda` 를 이용하여 풀 수 있다.

### lambda

`lambda(인자리스트:표현식)`

```python
def func(x,y):
  return x+y

f=lambda(x,y:x+y)
```

### map

`map(function,iterable)`

- iterable의 모든 인자 들에 대해 function을 적용한 뒤 반환.

```python
a=[1,2,3,4]
b=[5,6,7,8]

list(map(lambda x,y : x+y,a,b))
#[6,8,10,12]
```

> 주의할것은 python 2 에서는 map 함수는 list로 결과를 반환하지만, python3 에서는 map object를 반환하기 때문에 동일한 결과를 얻기 위해선 list 화 시켜야한다.


### 코드
```python
def solution(array, commands):
    return list(map(lambda x:sorted(array[x[0]-1:x[1]])[x[2]-1], commands))
```
