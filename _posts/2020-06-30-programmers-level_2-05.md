---
title: Python으로 푸는 프로그래머스 level_2. 프린터

excerpt: 일반적인 프린터는 인쇄 요청이 들어온 순서대로 인쇄합니다. 그렇기 때문에 중요한 문서가 나중에 인쇄될 수 있습니다. 이런 문제를 보완하기 위해 중요도가 높은 문서를 먼저 인쇄하는 프린터를 개발했습니다. 이 새롭게 개발한 프린터는 아래와 같은 방식으로 인쇄 작업을 수행합니다.

categories:
  - codingTest

tags:
  - Programmers
  - Stack/Queue
  - Python

date: 2020-06-30
last_modified_at: 2020-08-03
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---

`Tag` `스택/큐`<br>

**문제 설명**

일반적인 프린터는 인쇄 요청이 들어온 순서대로 인쇄합니다. 그렇기 때문에 중요한 문서가 나중에 인쇄될 수 있습니다. 이런 문제를 보완하기 위해 중요도가 높은 문서를 먼저 인쇄하는 프린터를 개발했습니다. 이 새롭게 개발한 프린터는 아래와 같은 방식으로 인쇄 작업을 수행합니다.

      1. 인쇄 대기목록의 가장 앞에 있는 문서(J)를 대기목록에서 꺼냅니다.
      2. 나머지 인쇄 대기목록에서 J보다 중요도가 높은 문서가 한 개라도 존재하면 J를 대기목록의 가장 마지막에 넣습니다.
      3. 그렇지 않으면 J를 인쇄합니다.
      예를 들어, 4개의 문서(A, B, C, D)가 순서대로 인쇄 대기목록에 있고 중요도가 2 1 3 2 라면 C D A B 순으로 인쇄하게 됩니다.

내가 인쇄를 요청한 문서가 몇 번째로 인쇄되는지 알고 싶습니다. 위의 예에서 C는 1번째로, A는 3번째로 인쇄됩니다.

현재 대기목록에 있는 문서의 중요도가 순서대로 담긴 배열 priorities와 내가 인쇄를 요청한 문서가 현재 대기목록의 어떤 위치에 있는지를 알려주는 location이 매개변수로 주어질 때, 내가 인쇄를 요청한 문서가 몇 번째로 인쇄되는지 return 하도록 solution 함수를 작성해주세요.

**제한사항**

- 현재 대기목록에는 1개 이상 100개 이하의 문서가 있습니다.
- 인쇄 작업의 중요도는 1~9로 표현하며 숫자가 클수록 중요하다는 뜻입니다.
- location은 0 이상 (현재 대기목록에 있는 작업 수 - 1) 이하의 값을 가지며 대기목록의 가장 앞에 있으면 0, 두 번째에 있으면 1로 표현합니다.

**입출력 예**

priorities|	location	|return
--|--|--
[2, 1, 3, 2]|	2	|1
[1, 1, 9, 1, 1, 1]	|0	|5

**입출력 예 설명**

**예제 #1**

문제에 나온 예와 같습니다.

**예제 #2**

6개의 문서(A, B, C, D, E, F)가 인쇄 대기목록에 있고 중요도가 1 1 9 1 1 1 이므로 C D E F A B 순으로 인쇄합니다.

[프로그래머스에서 풀기](#https://programmers.co.kr/learn/courses/30/lessons/42587)

## 코드
```python
from collections import deque
def solution(priorities, location):
    answer=0
    new_priorities=deque([{-1 if idx==location else 0 :priority }  for idx,priority in enumerate(priorities)])
    print_list=[]
    end=len(priorities)
    while new_priorities:
        for idx in range(1,end):
            if list(new_priorities[0].values())[0] < list(new_priorities[idx].values())[0]:
                new_priorities.append(new_priorities.popleft())
                break
        else:
            print_list.append(new_priorities.popleft())
            end-=1
    for idx,element in enumerate(print_list):
        if list(element.keys())[0] == -1:
            answer=idx+1
            break

    return answer
```

## 설명
```python
answer=0
new_priorities=deque([{-1 if idx==location else 0 :priority }  for idx,priority in enumerate(priorities)])
print_list=[]
end=len(priorities)
```
- ```new_priorities```는 인쇄를 요청한 문서를 ```{-1:priority}``` , 이외의 문서들을 ```{0:priority}``` 으로 표현한 리스트.
> Ex)
priorities=[2, 1, 3, 2],	location=2
new_priorities=[{0:2},{0:3},{-1:3},{0:2}]

- ```print_list```는 중요도 순으로 정렬된 출력 리스트.
- ```end```는 중요도 순으로 모든 인쇄 대기문서를 살펴봤는지 체크하는 변수


```python
while new_priorities:
    for idx in range(1,end):
        if list(new_priorities[0].values())[0] < list(new_priorities[idx].values())[0]:
            new_priorities.append(new_priorities.popleft())
            break
    else:
        print_list.append(new_priorities.popleft())
        end-=1
```

- ```new_priorities``` 를 모두 비우고  ```print_list``` 에 중요도 순으로 정렬할때까지 루프를 돈다.
- ```dict.values()``` 는 ```dict.values([])```를 리턴하여 list로 만든다.
- 인쇄 출력 풀에 들어온 ```list(new_priorities[0].values())[0]``` 과 인쇄 대기 풀에 있는 ```list(new_priorities[idx].values())[0]``` 와 중요도를 비교하여 우선순위가 낮다면 다시 대기상태, 높다면 ```print_list```에 담고, 인쇄 대기문서 수 ```end``` 를 줄여준다.

```python
for idx,element in enumerate(print_list):
    if list(element.keys())[0] == -1:
        answer=idx+1
        break

```
-  ```print_list```를 돌면서 요청한 대기 문서의 순서를 파악한다.
- 문제에서 원하는 인덱스로 만들기 위해서 ```idx+1``` 을 한다.
