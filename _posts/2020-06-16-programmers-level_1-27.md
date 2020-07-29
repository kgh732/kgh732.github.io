---
title: Python으로 푸는 프로그래머스 level_1. 최대공약수와 최소공배수
excerpt: 두 수를 입력받아 두 수의 최대공약수와 최소공배수를 반환하는 함수, solution을 완성해 보세요. 배열의 맨 앞에 최대공약수, 그다음 최소공배수를 넣어 반환하면 됩니다. 예를 들어 두 수 3, 12의 최대공약수는 3, 최소공배수는 12이므로 solution(3, 12)는 [3, 12]를 반환해야 합니다.

categories:
  - codingTest

tags:
  - Programmers
  - Python

date: 2020-05-27
last_modified_at: 2020-07-29
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---
`Tag` `연습문제`<br>

**문제 설명**

두 수를 입력받아 두 수의 최대공약수와 최소공배수를 반환하는 함수, solution을 완성해 보세요. 배열의 맨 앞에 최대공약수, 그다음 최소공배수를 넣어 반환하면 됩니다. 예를 들어 두 수 3, 12의 최대공약수는 3, 최소공배수는 12이므로 solution(3, 12)는 [3, 12]를 반환해야 합니다.

**제한 사항**

두 수는 1이상 1000000이하의 자연수입니다.

**입출력 예**

n|	m|	return
--|--|--
3	|12|	[3, 12]
2	|5	|[1, 10]

**입출력 예 설명**

**입출력 예 #1**

위의 설명과 같습니다.

**입출력 예 #2**

자연수 2와 5의 최대공약수는 1, 최소공배수는 10이므로 [1, 10]을 리턴해야 합니다.

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/12940)

## 코드
```python
def solution(n,m):
    a=n
    b=m
    remainder=-1
    answer=[]
    if a<b:
        a,b=b,a
    while remainder != 0 :
        remainder=a%b
        a=b
        b=remainder
    answer.append(a)
    answer.append(n*m//a)

    return answer

```

## 설명
```python
if a<b:
    a,b=b,a
while remainder != 0 :
    remainder=a%b
    a=b
    b=remainder
answer.append(a)
```
- ```The Euclidean Algorithm``` 을 이용하여 **최대공약수(The greatest common divisor)** 를 구한다.
> ***Let a,b be positive integers. If a=qb+r, then gcd(a,b)=(b,r)***

```python

answer.append(n*m//a)
```
- 구해진 ```최대공약수 a```를 이용하여 ```최소공배수 n*m//a``` 를 구한다.
> ***For positive integers a and b, gcd(a,b)*lcm(a,b)=ab***
