---
title: Python으로 푸는 프로그래머스 level_2. 구명보트

excerpt: 무인도에 갇힌 사람들을 구명보트를 이용하여 구출하려고 합니다. 구명보트는 작아서 한 번에 최대 2명씩 밖에 탈 수 없고, 무게 제한도 있습니다. 예를 들어, 사람들의 몸무게가 [70kg, 50kg, 80kg, 50kg]이고 구명보트의 무게 제한이 100kg이라면 2번째 사람과 4번째 사람은 같이 탈 수 있지만 1번째 사람과 3번째 사람의 무게의 합은 150kg이므로 구명보트의 무게 제한을 초과하여 같이 탈 수 없습니다. 구명보트를 최대한 적게 사용하여 모든 사람을 구출하려고 합니다. 사람들의 몸무게를 담은 배열 people과 구명보트의 무게 제한 limit가 매개변수로 주어질 때, 모든 사람을 구출하기 위해 필요한 구명보트 개수의 최솟값을 return 하도록 solution 함수를 작성해주세요.

categories:
  - codingTest

tags:
  - Programmers
  - Greedy
  - Python

date: 2020-08-28
last_modified_at: 2020-08-28
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---

`Tag` `탐욕법(Greedy)` <br>

**문제 설명**

무인도에 갇힌 사람들을 구명보트를 이용하여 구출하려고 합니다. 구명보트는 작아서 한 번에 최대 2명씩 밖에 탈 수 없고, 무게 제한도 있습니다.

예를 들어, 사람들의 몸무게가 [70kg, 50kg, 80kg, 50kg]이고 구명보트의 무게 제한이 100kg이라면 2번째 사람과 4번째 사람은 같이 탈 수 있지만 1번째 사람과 3번째 사람의 무게의 합은 150kg이므로 구명보트의 무게 제한을 초과하여 같이 탈 수 없습니다.

구명보트를 최대한 적게 사용하여 모든 사람을 구출하려고 합니다.

사람들의 몸무게를 담은 배열 people과 구명보트의 무게 제한 limit가 매개변수로 주어질 때, 모든 사람을 구출하기 위해 필요한 구명보트 개수의 최솟값을 return 하도록 solution 함수를 작성해주세요.

**제한사항**

- 무인도에 갇힌 사람은 1명 이상 50,000명 이하입니다.
- 각 사람의 몸무게는 40kg 이상 240kg 이하입니다.
- 구명보트의 무게 제한은 40kg 이상 240kg 이하입니다.
- 구명보트의 무게 제한은 항상 사람들의 몸무게 중 최댓값보다 크게 주어지므로 사람들을 구출할 수 없는 경우는 없습니다.

**입출력 예**

people|	limit	|return
--|--|--
[70, 50, 80, 50]|	100	|3
[70, 80, 50]	|100|	3


[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/42885?language=python3)

## 코드

```python
from collections import deque
def solution(people, limit):
    answer = 0
    queue=deque(sorted(people))
    while True:
        max=queue[-1] #max 업데이트
        min=queue[0]  #min 업데이트
        queue.pop()
        if not(queue):
            answer+=1
            break
        if max+min<=limit: # 가장 무게가 작은 인원을 담아본다.
            queue.popleft()
            if not(queue):
                answer+=1
                break

        answer+=1 # 보트 구출

    return answer


if __name__=="__main__":
    test_people=[70,80,50,50]
    test_limit=100
    print(solution(test_people,test_limit))

```

## 설명
- `Greedy Algorithm` 을 통해 구현한다.[why??](#why)
- **오름차순 정렬된** `people`을 `queue`에 담는다.
- 문제 전제조건에서 `limit` 는 항상 `people` 중 가장 큰 무게인 `max` 보다 크므로 `queue.pop()` 를 통해 `max`를 제거한다.
- `queue` 가 아직 다 비워지지 않았다면 `people` 중 가장 작은 무게인 `min`과 `max`의 합을 `limit`와 비교하여 보트에 태울수 있다면(`limit`보다 `min+max` 가 작거나 같다면) `queue.popleft()`를 통해 `min` 을 제거한다.
- `queue` 가 아직 다 비워지지 않았다면 `max` , `min` 업데이트 후 위의 과정을 반복한다.

### why??
1. **탐욕스러운 선택 조건(Greedy choice property)** 을 만족하는가?
>이 전의 선택이 이 후의 선택에 영향을 주지 않아야 한다.

- 각각 보트에 태울수 있는 무게를 체크하는 `max` 와 `min` 은 독립적으로 작용한다.

2. **최적 부분 구조 조건(Optimal Substructure)** 을 만족하는가?
> 문제에 대한 최종 해결방법이 부분문제에 대해서도 또한 최적 문제해결 방법이다.

- **전체 문제 집합에서 최적의 값** 은 **각각 보트 부분집합에서 최적으로 인원을 태워서 이동**하는것이다.
- **각각 보트를 태우는 부분집합에서 최적(최대)의 값** 은 `2`이다.
- 만약 `max+min` 값이 `limit`를 넘는다면 ${min}\leq{k} \leq{max}$ 에서 `k`는 살펴볼 필요가 없으며,**당연하게도 부분 집합에서 얻을 수 있는 최적의 값** 은 `1`이다.
- 만약 넘지 않는다면 **부분집합 최적의 값** `2`를 갖는다.
