---
title: "Python으로 푸는 프로그래머스 level_1. 2016년"
excerpt: "2016년 1월 1일은 금요일입니다. 2016년 a월 b일은 무슨 요일일까요? 두 수 a ,b를 입력받아 2016년 a월 b일이 무슨 요일인지 리턴하는 함수, solution을 완성하세요. 요일의 이름은 일요일부터 토요일까지 각각 SUN,MON,TUE,WED,THU,FRI,SAT입니다.
예를 들어 a=5, b=24라면 5월 24일은 화요일이므로 문자열 TUE를 반환하세요."

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

2016년 1월 1일은 금요일입니다. 2016년 a월 b일은 무슨 요일일까요? 두 수 a ,b를 입력받아 2016년 a월 b일이 무슨 요일인지 리턴하는 함수, solution을 완성하세요. 요일의 이름은 일요일부터 토요일까지 각각 SUN,MON,TUE,WED,THU,FRI,SAT입니다.
예를 들어 a=5, b=24라면 5월 24일은 화요일이므로 문자열 TUE를 반환하세요.

**제한 조건**

2016년은 윤년입니다.
2016년 a월 b일은 실제로 있는 날입니다. (13월 26일이나 2월 45일같은 날짜는 주어지지 않습니다)

**입출력 예**

a|	b	|result
---|---|---
5|	24|	"TUE"

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/12901)

## 코드

```python
def solution(a, b):
    answer = ''
    num_of_days=0
    day_of_month=[31,29,31,30,31,30,31,31,30,31,30,31]
    for month in range(a-1):
        num_of_days+=day_of_month[month]
    num_of_days+=b

    num_of_days+=4
    day_of_week=num_of_days%7
    if 0==day_of_week:
        answer='SUN'
    elif 1==day_of_week:
        answer='MON'
    elif 2==day_of_week:
        answer='TUE'
    elif 3==day_of_week:
        answer='WED'
    elif 4==day_of_week:
        answer='THU'
    elif 5==day_of_week:
        answer='FRI'
    elif 6==day_of_week:
        answer='SAT'

    return answer

```

## 설명

```python
num_of_days=0
day_of_month=[31,29,31,30,31,30,31,31,30,31,30,31]
for month in range(a-1):
    num_of_days+=day_of_month[month]
num_of_days+=b

num_of_days+=4
day_of_week=num_of_days%7

```
- 월별 날짜를 미리 셋팅한다.(2월은 윤년이므로 29일)
- ```a(몇월)``` 까지 모든 일수를 더한다.
- ```b(몇일)``` 까지 모든 일수를 더한다.
- 1월 1일이 금요일이므로 4를 더한다.**(5가 아닌 4를 더하는 이유는  이 전 계산에서 1월1일 날짜 자체가 한번 포함되므로)**
- ```0:SUN ~ 6:SAT``` 로 나머지 연산자를 활용한다.

```python
if 0==day_of_week:
    answer='SUN'
elif 1==day_of_week:
    answer='MON'
elif 2==day_of_week:
    answer='TUE'
elif 3==day_of_week:
    answer='WED'
elif 4==day_of_week:
    answer='THU'
elif 5==day_of_week:
    answer='FRI'
elif 6==day_of_week:
    answer='SAT'

return answer
```
- 결과 값에 따른 요일을 배정한다.

## 또 다른 풀이

```python
def solution2(a,b):
  day_of_month=[31,29,31,30,31,30,31,31,30,31,30,31]
  days = ['FRI', 'SAT','SUN','MON','TUE', 'WED', 'THU']
  return days[(sum(day_of_month[:a-1])+b-1)%7]
```

## 설명
```python
days = ['FRI', 'SAT','SUN','MON','TUE', 'WED', 'THU']
return days[(sum(day_of_month[:a-1])+b-1)%7]
```
- 1월1일이 금요일이므로 첫 시작은 ```FRI``` 기준으로 나열한다.
- sum을 활용하여 나머지연산자와 인덱싱을 통해 결과값을 반환한다.
