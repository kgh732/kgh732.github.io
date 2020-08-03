---
title: Python으로 푸는 프로그래머스 level_2. 전화번호 목록

excerpt: 전화번호부에 적힌 전화번호 중, 한 번호가 다른 번호의 접두어인 경우가 있는지 확인하려 합니다. 전화번호가 다음과 같을 경우, 구조대 전화번호는 영석이의 전화번호의 접두사입니다.

categories:
  - codingTest

tags:
  - Programmers
  - Hash
  - Python

date: 2020-07-03
last_modified_at: 2020-08-03
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---


`Tag` `해시`<br>

**문제 설명**

전화번호부에 적힌 전화번호 중, 한 번호가 다른 번호의 접두어인 경우가 있는지 확인하려 합니다.
전화번호가 다음과 같을 경우, 구조대 전화번호는 영석이의 전화번호의 접두사입니다.

- 구조대 : 119
- 박준영 : 97 674 223
- 지영석 : 11 9552 4421

전화번호부에 적힌 전화번호를 담은 배열 phone_book 이 solution 함수의 매개변수로 주어질 때, 어떤 번호가 다른 번호의 접두어인 경우가 있으면 false를 그렇지 않으면 true를 return 하도록 solution 함수를 작성해주세요.

**제한 사항**

- phone_book의 길이는 1 이상 1,000,000 이하입니다.
- 각 전화번호의 길이는 1 이상 20 이하입니다.

**입출력 예제**

phone_book|	return
--|--
["119", "97674223", "1195524421"]|	false
["123","456","789"]|	true
["12","123","1235","567","88"]|	false

**입출력 예 설명**

**입출력 예 #1**

앞에서 설명한 예와 같습니다.

**입출력 예 #2**

한 번호가 다른 번호의 접두사인 경우가 없으므로, 답은 true입니다.

**입출력 예 #3**

첫 번째 전화번호, “12”가 두 번째 전화번호 “123”의 접두사입니다. 따라서 답은 false입니다.

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/42577)

##코드
```python
def solution(phone_book):

    answer=True
    sorted_phone_book=sorted(phone_book)
    break_flag=False

    for i in range(len(phone_book)):
        for j in range(i+1,len(phone_book)):
            if sorted_phone_book[j].startswith(sorted_phone_book[i]):
                answer=False
                break_flag=True
                break
        if True==break_flag:
            break

    return answer
```

## 설명
```python
sorted_phone_book=sorted(phone_book)
```
- 순서대로 접두어를 검사하기 위해서 주어진 전화번호 목록 ```phone_book```을 **문자열 길이를 기준으로 오름차순 정렬한다.**

```python
for i in range(len(phone_book)):
    for j in range(i+1,len(phone_book)):
        if sorted_phone_book[j].startswith(sorted_phone_book[i]):
            answer=False
            break_flag=True
            break
    if True==break_flag:
        break
```
- 순차적으로  ```startswith()``` 를 통해 접두어가 같은게 있다면 ```answer``` 는 ```False``` 이고 ```break_flag``` 를 이용하여 반복문을 빠르게 종료한다.

## 또 다른 풀이

```python
def solution(phone_book):
    answer = True
    hash_map={phone_number:1 for phone_number in phone_book}
    break_flag=False

    for phone_number in phone_book:
        prefix = ""
        for number in phone_number:
            teprefixmp += number
            if prefix in hash_map and prefix != phone_number:
                answer = False
                break_flag=True
        if True==break_flag:
            break

    return answer

```

## 설명
- ```dictionary(내부적으로 hash 를 통해 자료 저장)```를 사용하여 접근한다.
- 효율성 측면에서 이 코드가 좀 더 효율적이다.[(why??)](#why)

```python
hash_map={phone_number:1 for phone_number in phone_book}
break_flag=False
```
- ```phone_book``` 의 원소를 key 로 가지는 ```dictionary```를 생성한다.
- 빠른 ```이중 for문``` 탈출을 위해서  ```break_flag``` 변수 생성한다.

```python
for phone_number in phone_book:
    prefix = ""
    for number in phone_number:
        prefix+= number
        if prefix in hash_map and prefix != phone_number:
            answer = False
            break_flag=True
    if True==break_flag:
        break
```
- ```in``` 연산자를 통해서 ```prefix``` 가 ```hash_map```에 있는지 확인하고 ```prefix!=phone_number``` 를 통해 자기 자신을 ```prefix```로 체크하는것을 막는다.


### why??
- ```in ``` 연산자는  ```list```, ```tuple``` 의 경우 하나하나 순회하기 때문에 데이터의 크기 만큼 ```O(n)``` 시간복잡도를 갖는다.
- ```set```,```dictionary```의 경우  내부적으로 hash를 통해서 자료들을 저장하기 때문에 ```O(1) ``` 시간복잡도가 가능하고, 해시가 성능이 떨어졌을 경우(충돌이 많은 경우)에 ```O(n)``` 시간복잡도를 갖는다.
