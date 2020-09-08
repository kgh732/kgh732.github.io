---
title: Python으로 푸는 프로그래머스 level_2. 튜플

excerpt: 셀수있는 수량의 순서있는 열거 또는 어떤 순서를 따르는 요소들의 모음을 튜플(tuple)이라고 합니다. n개의 요소를 가진 튜플을 n-튜플(n-tuple)이라고 하며, 다음과 같이 표현할 수 있습니다.


categories:
  - codingTest

tags:
  - Programmers
  - 2019KAKAO
  - Python

date: 2020-09-08
last_modified_at: 2020-09-08
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---


`Tag` `2019 카카오 개발자 겨울 인턴십` <br>

**문제 설명**

셀수있는 수량의 순서있는 열거 또는 어떤 순서를 따르는 요소들의 모음을 튜플(tuple)이라고 합니다. n개의 요소를 가진 튜플을 n-튜플(n-tuple)이라고 하며, 다음과 같이 표현할 수 있습니다.

- (a1, a2, a3, ..., an)

튜플은 다음과 같은 성질을 가지고 있습니다.

- 중복된 원소가 있을 수 있습니다. ex : (2, 3, 1, 2)
- 원소에 정해진 순서가 있으며, 원소의 순서가 다르면 서로 다른 튜플입니다. ex : (1, 2, 3) ≠ (1, 3, 2)
- 튜플의 원소 개수는 유한합니다.
원소의 개수가 n개이고, **<u>중복되는 원소가 없는</u>** 튜플 `(a1, a2, a3, ..., an)` 이 주어질 때(단, a1, a2, ..., an은 자연수), 이는 다음과 같이 집합 기호 '{', '}'를 이용해 표현할 수 있습니다.

- { {a1}, {a1, a2}, {a1, a2, a3}, {a1, a2, a3, a4}, ... {a1, a2, a3, a4, ..., an} }

예를 들어 튜플이 (2, 1, 3, 4)인 경우 이는

- { {2}, {2, 1}, {2, 1, 3}, {2, 1, 3, 4}}

와 같이 표현할 수 있습니다. 이때, 집합은 원소의 순서가 바뀌어도 상관없으므로

- { {2}, {2, 1}, {2, 1, 3}, {2, 1, 3, 4}}
- { {2, 1, 3, 4}, {2}, {2, 1, 3}, {2, 1}}
- { {1, 2, 3}, {2, 1}, {1, 2, 4, 3}, {2}}

는 모두 같은 튜플 (2, 1, 3, 4)를 나타냅니다.

특정 튜플을 표현하는 집합이 담긴 문자열 s가 매개변수로 주어질 때, s가 표현하는 튜플을 배열에 담아 return 하도록 solution 함수를 완성해주세요.

**[제한사항]**

- s의 길이는 5 이상 1,000,000 이하입니다.
- s는 숫자와 '{', '}', ',' 로만 이루어져 있습니다.
- 숫자가 0으로 시작하는 경우는 없습니다.
- s는 항상 중복되는 원소가 없는 튜플을 올바르게 표현하고 있습니다.
- s가 표현하는 튜플의 원소는 1 이상 100,000 이하인 자연수입니다.
- return 하는 배열의 길이가 1 이상 500 이하인 경우만 입력으로 주어집니다.

**[입출력 예]**

s	|result
--|--
"{ {2},{2,1},{2,1,3},{2,1,3,4}}"	|[2, 1, 3, 4]
"{ {1,2,3},{2,1},{1,2,4,3},{2}}"	|[2, 1, 3, 4]
"{ {20,111},{111}}"|	[111, 20]
"{ {123}}"	|[123]
"{ {4,2,3},{3},{2,3,4,1},{2,3}}"|	[3, 2, 4, 1]

**입출력 예에 대한 설명**

**입출력 예 #1**

문제 예시와 같습니다.

**입출력 예 #2**

문제 예시와 같습니다.

**입출력 예 #3**

(111, 20)을 집합 기호를 이용해 표현하면 { {111}, {111,20}}이 되며, 이는 { {20,111}, {111}}과 같습니다.

**입출력 예 #4**

(123)을 집합 기호를 이용해 표현하면 { {123}} 입니다.

**입출력 예 #5**

(3, 2, 4, 1)을 집합 기호를 이용해 표현하면 { {3},{3,2},{3,2,4},{3,2,4,1}}이 되며, 이는 { {4,2,3},{3},{2,3,4,1},{2,3}}과 같습니다.

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/64065)


## 코드

```python
def solution(s):
    answer = []

    # split
    split_s = []
    temp = set()
    flag = False
    temp_str = ''

    for element in s[1:-1]:
        if "{" == element:
            flag = True
        elif "}" == element:
            flag = False
            temp.add(int(temp_str))
            temp_str = ''
            split_s.append(temp)
            temp=set()
        elif flag:
            if ',' != element:  # 숫자 문자인경우
                temp_str += element
            else:  # ',' 인 경우
                temp.add(int(temp_str))
                temp_str = ''

    # Finally
    for element in sorted(split_s, key=lambda x: len(x)):
        answer.append( list(element - set(answer))[0])

    return answer


if __name__ == "__main__":
    test_s = "{ {20,111},{111} }"

    print(solution(test_s))
```

## 설명

- `'{'` 을 만나면 **새로운 집합이 시작** 하는 것이므로  `flag` 를 설정한다.
	- `flag==True`
		- `','` 를 제외한 숫자 문자인 경우  `temp_str`에 이어붙인다.
		- `','` 인 경우 **(=새로운 원소가 나오는 경우)**  `temp` 집합에 `int(temp_str)` 를 추가하고, `temp_str` 초기화 한다.
- `'}'` 을 만나면 하나의 집합이 끝난 것이므로 `flag` 를 설정한다.
	- 이 전까지 담긴 `temp_str` 을 `temp` 집합에 **int 형변환** 하여 추가하고 `temp` 집합을 `split_s` 에 최종적으로 추가한다. 이 후 `temp_str` ,`temp` 을 초기화 한다.

- 각 집합 별로 분할 된 `split_s` 을 **집합길이를 기준으로 오름차순정렬** 하여 순차적으로 `-` 연산을 이용하여 `answer` 에 담아준다.

	> ex) s="{ {20,111},{111}}"  
	split_s=[{20,111},{111}]  
	sorted(split_s, key=lambda x: len(x))=[{111},{20,111}]  
	answer=[]  
	----------------for loop----------------  
	list(element-set(answer))[0]=list({111}-set([]))[0]=list({111})[0]  
	list(element-set(answer))[0]=list({20,111}-set([111]))[0]=list({20})[0]  
	answer=[111,20]

## 또 다른 풀이

```python
import re
from collections import Counter

def solution(s):
	s = Counter(re.findall('\d+', s))
	return [int(k) for k,v in sorted(s.items(),key=lambda x:x[1],reverse=True)]

```


## 설명

- **각 집합에 속한 원소의 갯수가 많을수록 튜플의 순서가 빠른것이다.**
- ``정규표현식(#regular-expressionregex)`` **'\d+'** 을 이용하여 숫자인 모든 문자를 찾아서 `Counter` 로 갯수를 센다.
- `Counter.items()` 을 통해 **갯수를 기준** 으로 **내림차순정렬** 하여 **int 형변환** 후 리스트에 담는다.
