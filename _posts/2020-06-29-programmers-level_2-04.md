---
title: Python으로 푸는 프로그래머스 level_2. 다리를 지나는 트럭

excerpt: 트럭 여러 대가 강을 가로지르는 일 차선 다리를 정해진 순으로 건너려 합니다. 모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 알아내야 합니다. 트럭은 1초에 1만큼 움직이며, 다리 길이는 bridge_length이고 다리는 무게 weight까지 견딥니다.

categories:
  - codingTest

tags:
  - Programmers
  - Stack/Queue
  - Python

date: 2020-06-29
last_modified_at: 2020-08-03
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---

`Tag` `스택/큐`<br>

**문제 설명**

트럭 여러 대가 강을 가로지르는 일 차선 다리를 정해진 순으로 건너려 합니다. 모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 알아내야 합니다. 트럭은 1초에 1만큼 움직이며, 다리 길이는 bridge_length이고 다리는 무게 weight까지 견딥니다.
※ 트럭이 다리에 완전히 오르지 않은 경우, 이 트럭의 무게는 고려하지 않습니다.

예를 들어, 길이가 2이고 10kg 무게를 견디는 다리가 있습니다. 무게가 [7, 4, 5, 6]kg인 트럭이 순서대로 최단 시간 안에 다리를 건너려면 다음과 같이 건너야 합니다.

경과 시간	|다리를 지난 트럭|	다리를 건너는 트럭	|대기 트럭
--|--|--|--
0|	[]	|[]	|[7,4,5,6]
1~2|	[]	|[7]|	[4,5,6]
3	|[7]|	[4]|	[5,6]
4	|[7]|	[4,5]|	[6]
5	|[7,4]|	[5]|	[6]
6~7|	[7,4,5]|	[6]	|[]
8	|[7,4,5,6]|	[]|	[]

따라서, 모든 트럭이 다리를 지나려면 최소 8초가 걸립니다.

solution 함수의 매개변수로 다리 길이 bridge_length, 다리가 견딜 수 있는 무게 weight, 트럭별 무게 truck_weights가 주어집니다. 이때 모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 return 하도록 solution 함수를 완성하세요.

**제한 조건**

- bridge_length는 1 이상 10,000 이하입니다.
- weight는 1 이상 10,000 이하입니다.
- truck_weights의 길이는 1 이상 10,000 이하입니다.
- 모든 트럭의 무게는 1 이상 weight 이하입니다.

**입출력 예**

bridge_length|	weight|	truck_weights|	return
--|--|--|--
2|	10|	[7,4,5,6]|	8
100	|100	|[10]|	101
100|	100|	[10,10,10,10,10,10,10,10,10,10]|	110

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/42583)

## 코드
```python
from collections import deque
def solution(bridge_length, weight, truck_weights):
    time=0
    weight_sum=0

    truck_on_bridge=deque()
    waiting_truck=deque(truck_weights)

    while waiting_truck:
        time+=1
        if len(truck_on_bridge)==bridge_length:
            weight_sum-=truck_on_bridge.pop()

        if (weight_sum + waiting_truck[0] <= weight):
            weight_sum+=waiting_truck[0]
            truck_on_bridge.appendleft(waiting_truck.popleft())
        else:
            truck_on_bridge.appendleft(0)


    if sum(truck_on_bridge) != 0:
        for idx,truck in enumerate(truck_on_bridge):
            if truck!=0:
                time+=bridge_length-idx
                break
    return time

```

## 설명
```python
time=0
weight_sum=0

truck_on_bridge=deque()
waiting_truck=deque(truck_weights)

while waiting_truck:
    time+=1
    if len(truck_on_bridge)==bridge_length:
        weight_sum-=truck_on_bridge.pop()

    if (weight_sum + waiting_truck[0] <= weight):
        weight_sum+=waiting_truck[0]
        truck_on_bridge.appendleft(waiting_truck.popleft())
    else:
        truck_on_bridge.appendleft(0)
```
- ```time```은 트럭이 모두 통과한 시간, ```weight_sum```은 다리 위에 있는 트럭의 무게 합.
- ```truck_on_bridge```는 다리위에 있는 트럭,```waiting_truck```은 대기트럭을 나타내며 [Deque](#deque) 구조.
- ```bridge_length```와 ```truck_on_bridge``` 길이가 같아지면 다음 트럭이 들어갈수 있도록 ```pop()``` 과 동시에 ```weight_sum```업데이트
- 다리위의 트럭 무게 합인 ```weight_sum```과 대기중인 트럭의 무게 ```waiting_truck[0]``` 를 합해서 ```weight```를 넘지 않는다면 트럭이 , 아니라면 0을 ```appendleft()``` 한다.

```python
if sum(truck_on_bridge) != 0:
    for idx,truck in enumerate(truck_on_bridge):
        if truck!=0:
            time+=bridge_length-idx
            break
return time
```
- ```waiting_truck``` 모두 다리 위에 올라간 후 모든 트럭을 ```pop()``` 하는 것을 피하기 위해서 제일 마지막에 올라간 트럭을 체크해서 ```time```에 ```bridge_length-idx```만큼 시간을 추가해준다.
>Ex)
weight=20, bridge_length=1000 ,truck_weights=[2,5,6,8] and truck_on_bridge=[8,6,5,2] 상황을 생각해보자.
그렇다면 truck_on_bridge의 길이가 1000인 [0,...0] 으로 만들려면 약 1000번의 루프를 더 돌아야 한다. 하지만 마지막 트럭이 나가는 시점에만 주목한다면 굳이 1000번의 루프 필요없이 8의 인덱스=0 과 bridge_length=1000의 차이만 계산하여 시간을 추가하면 된다.

### Deque
- **Double Ended Queue** 로 **Queue** 와 비슷하지만 **Queue** 는 front에서만 삭제하고, end에서 삽입하는데, **Deque** 는 front와 end에서 삭제와 삽입이 모두 가능한 자료구조
- **Deque** 는 스택과 큐의 일반화
- 파이썬에서 리스트의 ```pop(idx)```,```insert(idx,value)```가 유사한 연산을 제공하지만 ```O(N)``` 복잡도를 가지고 있는 반면 **Deque** ```popleft()```,```appendleft()``` 연산은 ```O(1)``` 복잡도를 가진다.
- 이 외의 연산은 ```list``` 의 연산과 동일하다.
