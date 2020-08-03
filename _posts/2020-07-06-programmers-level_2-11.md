---
title: Python으로 푸는 프로그래머스 level_2. 위장

excerpt: 스파이들은 매일 다른 옷을 조합하여 입어 자신을 위장합니다. 예를 들어 스파이가 가진 옷이 아래와 같고 오늘 스파이가 동그란 안경, 긴 코트, 파란색 티셔츠를 입었다면 다음날은 청바지를 추가로 입거나 동그란 안경 대신 검정 선글라스를 착용하거나 해야 합니다.


categories:
  - codingTest

tags:
  - Programmers
  - Hash
  - Python

date: 2020-07-06
last_modified_at: 2020-08-03
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---


`Tag` `해시`<br>

**문제 설명**

스파이들은 매일 다른 옷을 조합하여 입어 자신을 위장합니다.

예를 들어 스파이가 가진 옷이 아래와 같고 오늘 스파이가 동그란 안경, 긴 코트, 파란색 티셔츠를 입었다면 다음날은 청바지를 추가로 입거나 동그란 안경 대신 검정 선글라스를 착용하거나 해야 합니다.

종류|	이름
--|--
얼굴|	동그란 안경, 검정 선글라스
상의|	파란색 티셔츠
하의|	청바지
겉옷|	긴 코트

스파이가 가진 의상들이 담긴 2차원 배열 clothes가 주어질 때 서로 다른 옷의 조합의 수를 return 하도록 solution 함수를 작성해주세요.

**제한사항**
- clothes의 각 행은 [의상의 이름, 의상의 종류]로 이루어져 있습니다.
- 스파이가 가진 의상의 수는 1개 이상 30개 이하입니다.
- 같은 이름을 가진 의상은 존재하지 않습니다.
- clothes의 모든 원소는 문자열로 이루어져 있습니다.
- 모든 문자열의 길이는 1 이상 20 이하인 자연수이고  알파벳 소문자 또는 '\_' 로만 이루어져 있습니다.
- 스파이는 하루에 최소 한 개의 의상은 입습니다.

**입출력 예**

clothes|	return
--|--
\[["yellow_hat", "headgear"], ["blue_sunglasses", "eyewear"], ["green_turban", "headgear"]]	|5
\[["crow_mask", "face"], ["blue_sunglasses", "face"], ["smoky_makeup", "face"]]|	3

**입출력 예 설명**

**예제 #1**
headgear에 해당하는 의상이 yellow_hat, green_turban이고 eyewear에 해당하는 의상이 blue_sunglasses이므로 아래와 같이 5개의 조합이 가능합니다.

    1. yellow_hat
    2. blue_sunglasses
    3. green_turban
    4. yellow_hat + blue_sunglasses
    5. green_turban + blue_sunglasses

**예제 #2**

face에 해당하는 의상이 crow_mask, blue_sunglasses, smoky_makeup이므로 아래와 같이 3개의 조합이 가능합니다.

    1. crow_mask
    2. blue_sunglasses
    3. smoky_makeup

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/42578)

## 코드

```python
def solution(clothes):
    answer=1
    n=len(clothes)
    clothes_dict=dict()

    clothes_dict={clothes[idx][1]:[] for idx in range(n)}
    for idx in range(n):
        clothes_dict[clothes[idx][1]].append(clothes[idx][0])

    for key in clothes_dict:
        answer*=len(clothes_dict[key])+1
    return answer-1
```

## 설명

```python
clothes_dict={clothes[idx][1]:[] for idx in range(n)}
```
- **옷의 종류** `clothes[idx][1]` 를 **key** 로 하는 `clothes_dict`를 생성한다.
> ex)
clothes=\[["yellow_hat", "headgear"], ["blue_sunglasses", "eyewear"], ["green_turban", "headgear"]]
clothes_dict={'headgear':[], 'eyewear':[]}

```python
for idx in range(n):
    clothes_dict[clothes[idx][1]].append(clothes[idx][0])
```
- 생성된 `clothes_dict` 에 **옷의 이름** `clohtes[idx][0]`을 **value** 로 가지도록 추가한다.
> ex)
clothes_dict={'headgear':["yellow_hat","green_turban"],'eyewear':["bblue_sunglasses"]}

```python
for key in clothes_dict:
    answer*=len(clothes_dict[key])+1
return answer-1
```
- 모든 조합의 가짓수는 각 **옷의 종류** 에 **+1(옷을 안 입는 경우)** 를 한 수의 곱이다.
- 그 후 **모든 옷을 안 입는 경우** 를 **-1** 한다.

## 또 다른 풀이

```python
from collections import Counter
from functools import reduce
def solution(clothes):
    cnt = Counter([kind for name, kind in clothes])
    answer = reduce(lambda x, y: x*(y+1), cnt.values(), 1) - 1
    return answer
```

## 설명
```python
cnt = Counter([kind for name, kind in clothes])
answer = reduce(lambda x, y: x*(y+1), cnt.values(), 1) - 1
```
- [Counter()](#counter) 를 통해 **옷의 종류** `kind` 갯수를 카운팅한다.
> ex)
clothes=\[["yellow_hat", "headgear"], ["blue_sunglasses", "eyewear"], ["green_turban", "headgear"]]
cnt={'headgear':2, 'eyewear':1}

- [reduce()](#reduce) 를 통해 **초기값** `1`을 기준으로 곱셈한다.
> ex)
cnt.values=dict_values([2,5])
result= 1(초기값) * (2+1)=3
result=3 * (5+1)=18



### Counter
- `collections.Counter([iterable-or-mapping])`
- **hashable** 객체를 계산하기 위한 `dict` 하위 클래스 이다.
- `원소` 는 **key** , `원소의 개수`는 **value** 로 저장된다.
- **value** 는 `0` ,`음의 정수` , `양의 정수` 가 될 수 있다.
- **Create**

```python
>>> c=Counter()
>>> c
Counter()

>>> c=Counter('abcdeffe')
>>> c
Counter({'f': 2, 'e': 2, 'd': 1, 'b': 1, 'c': 1, 'a': 1})

>>> c=Counter({'red':4,'blue':2})
>>> c
Counter({'red': 4, 'blue': 2})

>>> c=Counter(cats=4,dogs=9)
>>> c
Counter({'dogs': 9, 'cats': 4})
>>> c['bird']
0

```
- **Method & Operation**
    - `elements()`

    ```python
    >>> c=Counter(cats=4,dogs=9)
    >>> c.elements()
    <itertools.chain object at 0x000002AEA1B40D68>
    >>> list(c.elements())
    ['dogs', 'dogs', 'dogs', 'dogs', 'dogs', 'dogs', 'dogs', 'dogs', 'dogs', 'cats', 'cats', 'cats', 'cats']
    ```
    - `most_common([n])`

    ```python
    >>> c=Counter(cats=4,dogs=9,bird=5)
    >>> c.most_common(2)
    [('dogs', 9), ('bird', 5)]
    ```
    - `subtract([iterable-or-mapping])`

    ```python
    >>> c=Counter(a=2,b=4)
    >>> d=Counter(a=-5,b=6,c=3)
    >>> c.subtract(d)
    >>> c
    Counter({'a': 7, 'b': -2, 'c': -3})
    ```
    - `update([iterable-or-mapping])`

    ```python
    >>> c=Counter(a=2,b=4)
    >>> c
    Counter({'b': 4, 'a': 2})
    >>> c.update(['bird','test'])
    >>> c
    Counter({'b': 4, 'a': 2, 'bird': 1, 'test': 1})
    ```
    - `operation`

    ```python
    >>> c = Counter(a=3, b=1)
    >>> d = Counter(a=1, b=2)
    >>> c + d                       # add two counters together:  c[x] + d[x]
    Counter({'a': 4, 'b': 3})
    >>> c - d                       # subtract (keeping only positive counts)
    Counter({'a': 2})
    >>> c & d                       # intersection:  min(c[x], d[x])
    Counter({'a': 1, 'b': 1})
    >>> c | d                       # union:  max(c[x], d[x])
    Counter({'a': 3, 'b': 2})

    >>> +c
    Counter({'a': 3, 'b': 1}) # empty Counter + c
    >>> -c
    Counter() # empty Counter - c
    ```

### reduce
- `functools.reduce(fucntion,iterable[,initializer])`
- `iterable` 객체에 **순차적** 으로 `function` 을 **누적적용** 하여 **단일 값** 을 반환한다.

```python
>>> reduce(lambda x,y:x+y,[1,2,3,4,5])
15
```
