---
title: "Python으로 푸는 프로그래머스 level_1. 나누어 떨어지는 숫자 배열"
excerpt: "array의 각 element 중 divisor로 나누어 떨어지는 값을 오름차순으로 정렬한 배열을 반환하는 함수, solution을 작성해주세요.
divisor로 나누어 떨어지는 element가 하나도 없다면 배열에 -1을 담아 반환하세요.
"

categories:
  - codingTest

tags:
  - Programmers
  - Python

date: 2020-05-30
last_modified_at: 2020-07-29
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---
`Tag` `연습문제`<br>


**문제 설명**

array의 각 element 중 divisor로 나누어 떨어지는 값을 오름차순으로 정렬한 배열을 반환하는 함수, solution을 작성해주세요.
divisor로 나누어 떨어지는 element가 하나도 없다면 배열에 -1을 담아 반환하세요.

**제한사항**

arr은 자연수를 담은 배열입니다.
정수 i, j에 대해 i ≠ j 이면 arr[i] ≠ arr[j] 입니다.
divisor는 자연수입니다.
array는 길이 1 이상인 배열입니다.

**입출력 예**

arr|	divisor|	return
-----|---|-----
[5, 9, 7, 10]	|5|	[5, 10]
[2, 36, 1, 3]|	1	|[1, 2, 3, 36]
[3,2,6]	|10|	[-1]

**입출력 예 설명**

**입출력 예#1**

arr의 원소 중 5로 나누어 떨어지는 원소는 5와 10입니다. 따라서 [5, 10]을 리턴합니다.

**입출력 예#2**

arr의 모든 원소는 1으로 나누어 떨어집니다. 원소를 오름차순으로 정렬해 [1, 2, 3, 36]을 리턴합니다.

**입출력 예#3**

3, 2, 6은 10으로 나누어 떨어지지 않습니다. 나누어 떨어지는 원소가 없으므로 [-1]을 리턴합니다.

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/12910)

## 코드
```python
def solution(arr, divisor):

    answer=[value for value in arr if 0==value%divisor]
    if not(answer):
        answer.append(-1)
    return sorted(answer)
```
