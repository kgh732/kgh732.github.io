---
title: Python으로 푸는 프로그래머스 level_2. 더 맵게

excerpt: 매운 것을 좋아하는 Leo는 모든 음식의 스코빌 지수를 K 이상으로 만들고 싶습니다. 모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 Leo는 스코빌 지수가 가장 낮은 두 개의 음식을 아래와 같이 특별한 방법으로 섞어 새로운 음식을 만듭니다.

categories:
  - codingTest

tags:
  - Programmers
  - Heap
  - Python

date: 2020-07-02
last_modified_at: 2020-08-03
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---

`Tag` `힙`<br>

**문제 설명**

매운 것을 좋아하는 Leo는 모든 음식의 스코빌 지수를 K 이상으로 만들고 싶습니다. 모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 Leo는 스코빌 지수가 가장 낮은 두 개의 음식을 아래와 같이 특별한 방법으로 섞어 새로운 음식을 만듭니다.

      섞은 음식의 스코빌 지수 = 가장 맵지 않은 음식의 스코빌 지수 + (두 번째로 맵지 않은 음식의 스코빌 지수 * 2)

Leo는 모든 음식의 스코빌 지수가 K 이상이 될 때까지 반복하여 섞습니다.
Leo가 가진 음식의 스코빌 지수를 담은 배열 scoville과 원하는 스코빌 지수 K가 주어질 때, 모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 섞어야 하는 최소 횟수를 return 하도록 solution 함수를 작성해주세요.

**제한 사항**

- scoville의 길이는 2 이상 1,000,000 이하입니다.
- K는 0 이상 1,000,000,000 이하입니다.
- scoville의 원소는 각각 0 이상 1,000,000 이하입니다.
- 모든 음식의 스코빌 지수를 K 이상으로 만들 수 없는 경우에는 -1을 return 합니다.

**입출력 예**

scoville|	K|	return
--|--|--
[1, 2, 3, 9, 10, 12]|	7	|2

**입출력 예 설명**

1. 스코빌 지수가 1인 음식과 2인 음식을 섞으면 음식의 스코빌 지수가 아래와 같이 됩니다.
새로운 음식의 스코빌 지수 = 1 + (2 * 2) = 5
가진 음식의 스코빌 지수 = [5, 3, 9, 10, 12]

2. 스코빌 지수가 3인 음식과 5인 음식을 섞으면 음식의 스코빌 지수가 아래와 같이 됩니다.
새로운 음식의 스코빌 지수 = 3 + (5 * 2) = 13
가진 음식의 스코빌 지수 = [13, 9, 10, 12]

모든 음식의 스코빌 지수가 7 이상이 되었고 이때 섞은 횟수는 2회입니다.

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/42626)


## 코드
```python
import heapq
def solution(scoville, K):
    answer = 0
    heapq.heapify(scoville)
    while scoville[0]<K:
        if 1==len(scoville):
            answer=-1
            break
        smallest_a=heapq.heappop(scoville)
        smallest_b=heapq.heappop(scoville)
        heapq.heappush(scoville,smallest_a+smallest_b*2)
        answer+=1

    return answer
```
## 설명
- [```heapq```](#heapq) 모듈을 이용한다.



```python
heapq.heapify(scoville)
```

- 기존 리스트  ```scoville``` 을 ```heap```으로 만든다.

```python
while scoville[0]<K:
    if 1==len(scoville):
        answer=-1
        break
    smallest_a=heapq.heappop(scoville)
    smallest_b=heapq.heappop(scoville)
    heapq.heappush(scoville,smallest_a+smallest_b*2)
    answer+=1
```
- ```min-heap``` 이므로 **루트노드(인덱스 0)** 는 힙의 최소값이다.
- 주의할것은 ```scoville[1]```이 두번째 최솟값은 아니다.
- ```scoville``` 루트노드의  스코빌 지수```K```값을 넘기기 전까지 반복한다.
- ```smallest_a```는 ```scoville```의 가장 작은 스코빌 값이다.
- ```smallest_b```는 ```scoville```의 두번째로 작은 스코빌 값이다.
- ```heappush``` 를 통해 값을 추가함과 동시에 ```min-heap```의 속성을 유지한다.

### heapq 모듈
- ```heapq``` 는 기본적으로 ```min-heap``` 만 제공한다.

#### heap 이란?
- [완전 이진 트리](#complete-binary-tree)의 일종으로 우선순위 큐를 위하여 만들어진 자료구조이다.
- 여러 개의 값들 중에서 최댓값이나 최솟값을 빠르게 찾아내도록 만들어진 자료구조이다.
- 힙은 일종의 **반정렬 상태(느슨한 정렬 상태)** 를 유지한다.
   - 큰 값(작은값)이 상위 레벨에 있고 작은 값(큰값)이 하위 레벨에 있다는 정도를 표현한다.
   - 즉, 부모 노드의 키 값이 자식 노드의 키 값보다 항상 큰(작은) 이진 트리를 말한다.
   - 힙 트리에서는 중복된 값을 허용한다.

#### heap의 종류
-   최대 힙(max heap)
   부모 노드의 키 값이 자식 노드의 키 값보다 **크거나 같은 완전 이진 트리.**
   key(부모 노드) >= key(자식 노드)

-   최소 힙(min heap)
   부모 노드의 키 값이 자식 노드의 키 값보다 **작거나 같은 완전 이진 트리.**
   key(부모 노드) <= key(자식 노드)

-
![programmers-level_2-07-1](/assets/img/programmers-level_2-07-1.png)

#### heapq 모듈 사용법
**기존 리스트를 힙으로 변환**

- `heapq.heapify()`

```python
heap=[4,1,7,3,8,5]
heapq.heapify(heap)
```

**힙에 원소 추가**

- `heapq.heappush()`

```python
heapq.heappush(heap,1)
heapq.heappush(heap,2)
```

**힙에서 원소 삭제**

- `heapq.heappop()`

```python
heapq.heappop(heap)
heapq.heappop(heap)
```

#### [응용] max-heap
- ```heapq``` 모듈은 ```min-heap``` 기능만을 제공한다는 것에 주목한다.
- tuple 을 원소로 추가하거나 삭제하면, 튜플 내에서 맨 앞에 있는 값을 기준으로 구성이 되는 원리를 활용한다.
- heap으로 만들 리스트의 **모든 값의 반대 부호를 붙여 반전** 시켜 ```max-heap``` 기능을 구현한다
```python
import heapq
nums=[1,2,-2,4,5]
heap=[]
for num in nums:
  heapq.heappush(heap,(-num,num)) #우선순위, 값
while heap:
  print(heapq.heappop(heap)[1])
```
```python
5
4
2
1
-2
```
####[응용] k번째 최소값/최대값
- ```min-heap```, ```max-heap``` 을 사용하여 K번째 최소값 ,최대값을 효율적으로 구할 수 있다.
- ```heapq.nsmallest()```, ```heapq.nlargest()```  을 이용하여도 된다.

```python
import heapq
def kth_smallest(nums, k):
  heap = []
  for num in nums:
    heapq.heappush(heap, num)

  kth_min =0
  for _ in range(k):
    kth_min = heapq.heappop(heap)
  return kth_min

```
####[응용] 힙정렬
```python
def heap_sorting(nums):
  heap=[]
  for num in nums:
    heapq.heappush(heap,num)

  sorted_nums=[]
  while heap:
    sorted_nums.append(heapq.heappop(heap))
  return sorted_nums

```


#### Complete Binary Tree , Full(Perfect) Binary Tree
- 이진트리(Binary tree)는 자식의 갯수가 최대 2개인 tree.

    tree|definition
    ---|--
    Full(Perfect) Binary Tree| 모든 leaf의 레벨이 동일한 이진트리이며, leaf 가 아닌 모든 노드들은 모두 2개의 자식을 가지는 트리
    Complete Binary Tree| 포화이진트리의 leaf에서 오른쪽으에서부터 제거하여 얻어진트리.(=왼쪽노드 부터 순차적으로 추가하여 얻어진 트리)

-
![programmers-level_2-07-2](/assets/img/programmers-level_2-07-2.png)

## Reference
- [heapq 모듈 사용법 - https://www.daleseo.com/python-heapq/](https://www.daleseo.com/python-heapq/)
- [heap 자료구조 - https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html](https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html)
