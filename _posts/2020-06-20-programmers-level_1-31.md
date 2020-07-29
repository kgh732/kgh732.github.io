---
title: Python으로 푸는 프로그래머스 level_1. 행렬의 덧셈
excerpt: 행렬의 덧셈은 행과 열의 크기가 같은 두 행렬의 같은 행, 같은 열의 값을 서로 더한 결과가 됩니다. 2개의 행렬 arr1과 arr2를 입력받아, 행렬 덧셈의 결과를 반환하는 함수, solution을 완성해주세요.

categories:
  - codingTest

tags:
  - Programmers
  - Python

date: 2020-06-20
last_modified_at: 2020-07-29
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---
`Tag` `연습문제`<br>

**문제 설명**

행렬의 덧셈은 행과 열의 크기가 같은 두 행렬의 같은 행, 같은 열의 값을 서로 더한 결과가 됩니다. 2개의 행렬 arr1과 arr2를 입력받아, 행렬 덧셈의 결과를 반환하는 함수, solution을 완성해주세요.

**제한 조건**

행렬 arr1, arr2의 행과 열의 길이는 500을 넘지 않습니다.

**입출력 예**

arr1|	arr2|	return
--|--|--
\[[1,2],[2,3]] |	\[[3,4],[5,6]]	|\[[4,6],[7,9]]
\[[1],[2]]	|\[[3],[4]]	|\[[4],[6]]

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/12950)

## 코드
```python
def solution(arr1,arr2):
    return [[sum(elements) for elements in zip(*rows) ]for rows in zip(arr1,arr2)]
```

## 설명
$$
  \begin{bmatrix}
  x & y \\
  z & w \\
  \end{bmatrix}+
  \begin{bmatrix}
  a & b \\
  c & d \\
  \end{bmatrix}=
  \begin{bmatrix}
  x+a & y+b \\
  z+c & w+d \\
  \end{bmatrix}
$$
- ```zip()``` 을 이용하여 arr1과 arr2를 묶는다.
만약 arr1=\[[1,2],[2,3]] , arr2=\[[3,4],[5,6]] 이면 ```zip(arr1,arr2)```=```rows``` =```([1,2],[3,4]), ([2,3],[5,6])``` 이다.
- ```*```을 이용하여 ```rows```를 분해한뒤 다시 ```zip()``` 하여 묶는다.
즉, ```elements```=```(1,3),(2,4),(2,3),(5,6)```이다.
- 마지막으로 각 ```elements```들을 ```sum()``` 결과를 ```list```에 담는다
