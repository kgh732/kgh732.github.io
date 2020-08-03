---
title: Python으로 푸는 프로그래머스 level_2. 스킬트리

excerpt: 선행 스킬이란 어떤 스킬을 배우기 전에 먼저 배워야 하는 스킬을 뜻합니다. 예를 들어 선행 스킬 순서가 ```스파크 → 라이트닝 볼트 → 썬더``` 일때, 썬더를 배우려면 먼저 라이트닝 볼트를 배워야 하고, 라이트닝 볼트를 배우려면 먼저 스파크를 배워야 합니다.

categories:
  - codingTest

tags:
  - Programmers
  - Summer/Winter Coding(~2018)
  - Python

date: 2020-06-26
last_modified_at: 2020-08-03
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---

`Tag` `Summer/Winter Coding(~2018) `<br>

**문제 설명**

선행 스킬이란 어떤 스킬을 배우기 전에 먼저 배워야 하는 스킬을 뜻합니다.

예를 들어 선행 스킬 순서가 ```스파크 → 라이트닝 볼트 → 썬더``` 일때, 썬더를 배우려면 먼저 라이트닝 볼트를 배워야 하고, 라이트닝 볼트를 배우려면 먼저 스파크를 배워야 합니다.

위 순서에 없는 다른 스킬(힐링 등)은 순서에 상관없이 배울 수 있습니다. 따라서 ```스파크 → 힐링 → 라이트닝 볼트 → 썬더``` 와 같은 스킬트리는 가능하지만, ```썬더 → 스파크``` 나 ```라이트닝 볼트 → 스파크 → 힐링 → 썬더``` 와 같은 스킬트리는 불가능합니다.

선행 스킬 순서 skill과 유저들이 만든 스킬트리[^1] 를 담은 배열 skill_trees가 매개변수로 주어질 때, 가능한 스킬트리 개수를 return 하는 solution 함수를 작성해주세요.

**제한 조건**

- 스킬은 알파벳 대문자로 표기하며, 모든 문자열은 알파벳 대문자로만 이루어져 있습니다.
- 스킬 순서와 스킬트리는 문자열로 표기합니다.
   - 예를 들어, ```C → B → D``` 라면 CBD로 표기합니다
- 선행 스킬 순서 skill의 길이는 1 이상 26 이하이며, 스킬은 중복해 주어지지 않습니다.
- skill_trees는 길이 1 이상 20 이하인 배열입니다.
- skill_trees의 원소는 스킬을 나타내는 문자열입니다.
  - skill_trees의 원소는 길이가 2 이상 26 이하인 문자열이며, 스킬이 중복해 주어지지 않습니다.

**입출력 예**

skill|	skill_trees	|return
--|--|--
"CBD"|	["BACDE", "CBADF", "AECB", "BDA"]|	2

**입출력 예 설명**

- "BACDE": B 스킬을 배우기 전에 C 스킬을 먼저 배워야 합니다. 불가능한 스킬트립니다.
- "CBADF": 가능한 스킬트리입니다.
- "AECB": 가능한 스킬트리입니다.
- "BDA": B 스킬을 배우기 전에 C 스킬을 먼저 배워야 합니다. 불가능한 스킬트리입니다.


[^1]:스킬트리 :유저가 스킬을 배울 순서

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/49993#fn1)

## 코드
```python
def solution(skill, skill_trees):
    fail = 0
    mapping_skill={}
    order=[]

    for idx,s in enumerate(skill):
        mapping_skill[s]=idx+1
        order.append(idx+1)

    for skill in skill_trees:
        cursor=0
        for s in skill:
            mapping_skill_value=mapping_skill.get(s)
            if mapping_skill_value:
                if order[cursor]==mapping_skill_value:
                    cursor+=1
                else:
                    fail+=1
                    break

    return len(skill_trees)-fail
```

## 설명
```python
for idx,s in enumerate(skill):
    mapping_skill[s]=idx+1
    order.append(idx+1)
```

- ```skill(선행스킬)``` 에 순서를 부여하는 ```mapping_skill``` 을 생성한다.
- 선행스킬 순서를 체크하기 위해 ```order```를 생성한다.
> Ex)
 skill="CBD"
 mapping_skill={'C':1,'B':2,'D':3}
 ***(dict의 생성은 입력 순서대로 생성되지 않기 때문에 위의 결과는 차이가 있을수는 있으나 구성은 같다)***
 order=[1,2,3]

```python
for skill in skill_trees:
    cursor=0
    for s in skill:
        mapping_skill_value=mapping_skill.get(s)
        if mapping_skill_value:
            if order[cursor]==mapping_skill_value:
                cursor+=1
            else:
                fail+=1
                break
```

- ```skill_trees```에서 각 ```skill```에서 **선행스킬** 에만 주목하면 되므로  ```mapping_skill``` 에 해당 키 값이 있을 경우에만 ```order``` 를 체크한다.
- 만약 ```order``` 가 맞지 않다면(**=선행 스킬순서가 어긋났다면**), 불가능한 스킬트리로 ```fail``` 값은 증가한다.


```python
return len(skill_trees)-fail
```
- ```skill_trees```의 전체 스킬 개수에서 불가능한 스킬트리 ```fail``` 을 뺀 값을 반환한다.

## 또 다른 풀이

```python
from collections import deque

def solution(skill, skill_trees):
    answer = 0

    for skills in skill_trees:
        skill_deque = deque(skill)
        for s in skills:
            if s in skill:
                if s != skill_deque.popleft():
                    break
        else:
            answer += 1

    return answer


```

## 설명
### for-else
- ```for``` 문에서 ```break``` 가 발생하지 않았을 경우의 행동을 ```else``` 문에 적어준다.

```python
data = [2, 4, 5, 9, 3]
for i in data:
    if i > 10:
        break
else:
    print('10 보다 큰 수 없음')
```
