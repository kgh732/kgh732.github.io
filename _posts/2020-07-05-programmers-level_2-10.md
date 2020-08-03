---
title: Python으로 푸는 프로그래머스 level_2. 소수 찾기

excerpt: 한자리 숫자가 적힌 종이 조각이 흩어져있습니다. 흩어진 종이 조각을 붙여 소수를 몇 개 만들 수 있는지 알아내려 합니다. 각 종이 조각에 적힌 숫자가 적힌 문자열 numbers가 주어졌을 때, 종이 조각으로 만들 수 있는 소수가 몇 개인지 return 하도록 solution 함수를 완성해주세요.

categories:
  - codingTest

tags:
  - Programmers
  - BruteForce
  - Python

date: 2020-07-05
last_modified_at: 2020-08-03
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---

`Tag` `완전 탐색`<br>

**문제 설명**

한자리 숫자가 적힌 종이 조각이 흩어져있습니다. 흩어진 종이 조각을 붙여 소수를 몇 개 만들 수 있는지 알아내려 합니다.

각 종이 조각에 적힌 숫자가 적힌 문자열 numbers가 주어졌을 때, 종이 조각으로 만들 수 있는 소수가 몇 개인지 return 하도록 solution 함수를 완성해주세요.

**제한사항**

- numbers는 길이 1 이상 7 이하인 문자열입니다.
- numbers는 0~9까지 숫자만으로 이루어져 있습니다.
- 013은 0, 1, 3 숫자가 적힌 종이 조각이 흩어져있다는 의미입니다.

**입출력 예**

numbers|	return
--|--
"17"|	3
"011"|	2

**입출력 예 설명**

**예제 #1**

[1, 7]으로는 소수 [7, 17, 71]를 만들 수 있습니다.

**예제 #2**

[0, 1, 1]으로는 소수 [11, 101]를 만들 수 있습니다.

11과 011은 같은 숫자로 취급합니다.

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/42839)


## 코드
```python
from itertools import permutations

def eratosthenes_sieve(n):
    # 에라토스테네스의 체
    numbers = [False, False] + [True] * (n - 1)
    m = int(n ** 0.5)
    for i in range(2, m + 1):
        if numbers[i]:
            for j in range(2 * i, n + 1, i):
                numbers[j] = False

    return [i for i in range(2, n + 1) if numbers[i] == True]


def solution(numbers):
    answer = 0
    permutations_list=set(int(''.join(p)) for i in range(1,len(numbers)+1)\
    for p in permutations(numbers,i))

    n = max(permutations_list)
    prime_list = eratosthenes_sieve(n)
    for p in permutations_list:
        if prime_list.count(p):
            answer += 1

    return answer
```

## 설명
```python
answer=0
permutations_list=set(int(''.join(p)) for i in range(1,len(numbers)+1)\
for p in permutations(numbers,i))
```

- ```permutations_list``` 는 ```itertools.permutations``` 를 이용하여 모든 순열을 생성한다.
($P(n,r),\ for\ n=len(numbers),\ 1\leq r\leq n$)

```python
n = max(permutations_list)
prime_list = eratosthenes_sieve(n)
for p in permutations_list:
    if prime_list.count(p):
        answer += 1

return answer
```
- 생성된 ```permutations_list``` 의 가장 큰 값 ```n```을 기준으로 ```eratosthenes_sieve()``` 를 통해 ```n```까지 가능한 소수 리스트 ```prime_list``` 를 생성한다.
-  ```permutations_list```의 수가 ```prime_list```에 존재한다면 ```answer```값을 늘려준다.

## 또 다른 풀이

```python
from itertools import permutations

def solution(n):
    a = set()
    for i in range(len(n)):
        a |= set(map(int, map("".join, permutations(n, i + 1))))
    a -= set(range(0, 2))
    for i in range(2, int(max(a) ** 0.5) + 1):
        a -= set(range(i * 2, max(a) + 1, i))
    return len(a)
```

## 설명
```python
a = set()
for i in range(len(n)):
    a |= set(map(int, map("".join, permutations(n, i + 1))))
```
- ```set``` 의 ```OR``` 연산자는 **Union 연산** 이다.
- ```itertools.permutations``` 을 이용한 순열 결과에 대해 ```''.join```으로 ```리스트 - > 문자열``` 로 변환후 ```int()``` 를 통해 ```문자열 -> int``` 한다.

```python
a -= set(range(0, 2))
for i in range(2, int(max(a) ** 0.5) + 1):
    a -= set(range(i * 2, max(a) + 1, i))
return len(a)
```
- ```set```의  ```-``` 연산자는 **Difference 연산** 이다.
- **0** 과 **1** 은 소수가 아니기 때문에 ```a-=set(range(0,2))```  한다. **차집합 연산** 이므로 혹시 ```a``` 에 **0**과 **1** 이 없어도 된다.
- **에라토스테네스의 체** 를 이용하여 ```a```에서 소수가 아닌 수를 제거한다.

## Permutation & Combination
### Permutation
```python
import copy
def permutation_method_1(iterable):
    lst=list(iterable)
    def generate(lst,start=0):
        ret=[]
        n=(len(lst))-start
        if 1==n:
            return [copy.copy(lst)]
        else:
            for move in range(n):
                lst[start],lst[start+move]=lst[start+move],lst[start]
                ret.extend(generate(lst, start + 1))
                lst[start+move], lst[start] = lst[start ], lst[start+move]

            return ret
    return generate(lst)

```
- [Nested function](#nested-function) 으로 구현.
- 첫 시작 인덱스 ```start```와  이것을 기준으로 ```move``` 한 만큼의 위치를 스왑한다.
- ```start``` 를 한칸 밀어서 재귀호출 한다.
- 재귀 호출이 끝난 후 빠져나올때 다시 스왑해서 부모 노드로 돌아온다.  
- ```start``` 가 마지막 위치에 도달할경우 기존 리스트를 copy하여 이중 리스트를 만들어 반환한다.[(why?)](#shallow-copy-vs-deep-copy)
- [DFS(Depth-First-Search)](#dfsdepth-first-search) 방식과 같은 순서로 재귀 호출이 일어난다.


![programmers-level_2-10-2](/assets/img/programmers-level_2-10-2.jpg)

```python
import copy
def permutation_method_2(arr, r):
    used = [0]*len(arr)

    def generate(chosen, used):
        ret=[]        
        if len(chosen) == r:
            return [copy.copy(chosen)]

        for i in range(len(arr)):
            if not used[i]:
                chosen.append(arr[i])
                used[i] = 1
                ret.extend(generate(chosen, used))
                used[i] = 0
                chosen.pop()
        return ret

    return generate([], used)
```
- [Nested function](#nested-function) 으로 구현.
- ```used```변수는 i 번째 값을 사용하였는지 체크한다.
- ```chosen``` 변수는 순열의 원소를 저장하는 변수로 하나씩 추가하다가 그 개수가 r이 되는 순간 반환한다.
- 모든 순열은 arr의 0부터 i-1 번째 값으로 시작한다.
- ```chosen```에 원소를 담고, ```used``` 체크한다.
- ```generate()``` 을 재귀호출하여 반복하며 순열 생성후 ```used```를 다시 uncheck 하며 ```chosen```에서 꺼내준다.

### Combination
```python
def combination(iterable,r):
    def generate(chosen):
        ret=[]
        if len(chosen) == r:
            return [copy.copy(chosen)]

        start=iterable.index(chosen[-1])+1 if chosen else 0
        for idx in range(start,len(iterable)):
            chosen.append(iterable[idx])
            ret.extend(generate(chosen))
            chosen.pop()
        return ret

    return generate([])
```
- [Nested function](#nested-function) 으로 구현.
- ```chosen``` 변수는 조합의 원소를 저장하는 변수로 하나씩 추가하다가 그 개수가 r이 되는 순간 반환한다.
- 조합은 순서 상관없이 뽑는 것으로, ```start```를 **+1** 갱신시켜주며, 뽑힌```chosen```이 비어있다면 아직 뽑지 않은것으로 ```0```이다.
- ```generate()``` 을 재귀호출하여 반복하며 조합 생성후 ```chosen```에서 꺼내준다.

## DFS(Depth-First-Search)
- 탐색을 함에 있어서 보다 깊은것을 우선적으로 하여 탐색하는 방식이다.
- 맹목적으로 각 노드를 탐색할 때 주로 사용한다.
- 빠르게 모든 경우의 수를 탐색하고자 할 때 쉽게 사용할 수 있다.
- **BFS(Breadth-First-Search)** 에서는 **큐(Queue)** 가 사용된다면 **DFS(Depth-First-Search)** 에서는 **스택(Stack)** 이 사용된다.
- 스택을 사용하지 않더라도 컴퓨터는 구조적으로 스택 프레임을 사용하기 때문에 **재귀적** 으로 구현 가능하다.
- **DFS 과정**
  1. 탐색 시작 노드를 스택에 삽입하고 방문 처리한다.
  2. 스택의 최상단 노드에게 방문하지 않은 인접노드가 하나라도 있으면 그 노드를 스택에 넣고 방문 처리한다. 방문하지 않은 인접노드가 없으면 스택에서 최상단 노드를 꺼낸다.
  3. 2번의 과정을 더 이상 수행할 수 없을 때까지 반복한다.

![programmers-level_2-10-1](/assets/img/programmers-level_2-10-1.png)

- **코드**

```python
def DFS_simulator(graph,root):

    # 1. 탐색 시작 노드를 스택에 삽입하고 방문 처리 한다.
    stack=[root]
    visited={root:True}

    while stack:
        # 2. 스택의 최상단 노드에게 방문하지 않은 인접노드가 하나라도 있으면 스택에 넣고 방문 처리한다.
        print('stack: ',stack)
        current_node=stack.pop()
        print('currect_node: ',current_node)
        print('\n')
        adjacent_nodes=graph.get(current_node,False)
        if adjacent_nodes : # 인접 노드가 있을 경우
            for node in adjacent_nodes:
                if not(visited.get(node,False)): # 방문한적이 없을경우에만
                    visited[node]=True
                    stack.append(node)


if __name__=="__main__":            
  graph = {
  'A': ('X',),
  'X': ('G', 'H'),
  'H': ('G', 'E', 'P'),
  'E': ('M', 'Y'),
  'M': ('J',)
  }
  DFS_simulator(graph,'A')
```


## Nested function
- 함수 안에 정의된 또 다른 함수
- 중첩함수는 자기가 속한 원래 함수의 매개변수를 받아서 사용할 수 있다.
- 중첩함수는 자신이 속한 원래 함수 안에서만 역할을 하고, 원래 함수의 밖에서는 호출이 불가능하다.
- 함수 안에 선언된 로컬 변수는 함수안에서만 사용 가능한 원리와 동일

```python

#Ex)
def outer(num):
  def inner(n): #Nested function
  inner_result=n+1
  return result

  outer_result=inner(num)**2
  return outer_result

outer(9) # (9+1)**2=100
```

## Mutable vs Immutable
- **Mutable**
   - 생성 후 그 상태를 바꿀 수 있는 객체
   - 값을 변경하여도 똑같은 메모리 주소```id()``` 값을 가진다.
   - **call by reference** 속성
   ```python
    #Ex)
    >>> x=[1,2,3]
    >>> y=x
    >>> id(x)
    2958444672264
    >>> id(y)
    2958444672264
    >>> y.append(4)
    >>> y
    [1, 2, 3, 4]
    >>> id(y)
    2958444672264
    >>> x
    [1, 2, 3, 4]
    >>> id(x)
    2958444672264
    ```
- **Immutable**
    - 생성 후 그 상태를 바꿀 수 없는 객체
    - 값을 변경하면 다른 메모리 주소 ```id()```값으 가진다.
    - **Call by value** 속성

    ```python
    #Ex)
    >>> x=4
    >>> id(x)
    1803899776
    >>> y=x
    >>> id(y)
    1803899776
    >>> y=y+1
    >>> y
    5
    >>> id(y)
    1803899808
    >>> id(x)
    1803899776
    ```

Mutable | Immutable
---|---
list,set,dict|bool,int,float,tuple,str,frozenset


## Shallow copy vs Deep copy
**1. 단순 복제**
- 변수만 복사하므로 동일한 메모리 주소를 가리키고 있따.
- 즉, 두개의 변수 중 하나만 변경되어도 같은 메모리 주소를 가리키기 때문에 나머지도 동일하게 수정되는 현상 발생

```python
>>> mutable
[1, [2, 10, 7]]
>>> copied
[1, [2, 10, 7]]
>>> mutable[0]=4
>>> mutable
[4, [2, 10, 7]]
>>> copied
[4, [2, 10, 7]]
>>> mutable=[1,[1,2,3]]
>>> copied=mutable
>>> copied
[1, [1, 2, 3]]
>>> copied[0]=4
>>> copied
[4, [1, 2, 3]]
>>> mutable
[4, [1, 2, 3]]
>>> mutable[1]=[2,4,3]
>>> mutable
[4, [2, 4, 3]]
>>> copied
[4, [2, 4, 3]]
```

**2. Shallow copy**
- ```list()```, ```a[:]```, ```copy.copy()```를 통한 새로운 객체 복사
- **리스트 안에 리스트** 일 경우 주의해야 한다.
- 얕은 복사를 통해 다른 객체 주소를 가지고 있지만 **리스트 안의 리스트는 동일한 주소를 가지고 있어서 값 변경이 다른 변수에도 영향을 끼친다.**
- 리스트 안의 mutable 객체를 재 할당 하는 경우에는 상관없다.

```python
>>> mutable=[1,[2,10,7]]
>>> shallow_copied=mutable[:]
>>> id(mutable)
2958444671816
>>> id(shallow_copied)
2958444672904
>>> mutable[0]=4
>>> mutable
[4, [2, 10, 7]]
>>> shallow_copied
[1, [2, 10, 7]]
>>> mutable[1][2]=100
>>> mutable
[4, [2, 10, 100]]
>>> shallow_copied
[1, [2, 10, 100]]
>>> mutable[1]=[2]
>>> mutable
[4, [2]]
>>> shallow_copied
[1, [2, 10, 100]]
```

**3.Deep copy**
- Mutable 한 내부객체(내부리스트)의 문제를 해결하기 위해서 **deep copy** 를 해야한다.
- **shallow copy** 는 복합객체(리스트)만 복사되고 그 안의 내용은 동일한 객체를 참조한다면, **deep copy** 는복합객체를 새로 생성하고 그 안의 내용 까지 재귀적으로 새롭게 생성한다.

```python
>>> mutable=[1,[1,2,3]]
>>> import copy
>>> deep_copied=copy.deepcopy(mutable)
>>> deep_copied
[1, [1, 2, 3]]
>>> mutable[1][2]=4
>>> mutable
[1, [1, 2, 4]]
>>> deep_copied
[1, [1, 2, 3]]
```

## Reference
- [Permutation, Combination - https://shoark7.github.io/programming/algorithm/Permutations-and-Combinations](https://shoark7.github.io/programming/algorithm/Permutations-and-Combinations)
- [DFS - https://www.zerocho.com/category/Algorithm/post/5870153c37e1c80018b64eb0](https://www.zerocho.com/category/Algorithm/post/5870153c37e1c80018b64eb0)
