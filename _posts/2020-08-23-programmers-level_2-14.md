---
title: Python으로 푸는 프로그래머스 level_2. 조이스틱

excerpt: 조이스틱으로 알파벳 이름을 완성하세요. 맨 처음엔 A로만 이루어져 있습니다. ex) 완성해야 하는 이름이 세 글자면 AAA, 네 글자면 AAA조이스틱을 각 방향으로 움직이면 아래와 같습니다.

categories:
  - codingTest

tags:
  - Programmers
  - Greedy
  - BFS
  - Python

date: 2020-08-23
last_modified_at: 2020-08-23
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---

`Tag` `탐욕법(Greedy)` `BFS(Breadth-First-Search)`<br>

**문제 설명**

조이스틱으로 알파벳 이름을 완성하세요. 맨 처음엔 A로만 이루어져 있습니다.
ex) 완성해야 하는 이름이 세 글자면 AAA, 네 글자면 AAAA

조이스틱을 각 방향으로 움직이면 아래와 같습니다.

```
▲ - 다음 알파벳
▼ - 이전 알파벳 (A에서 아래쪽으로 이동하면 Z로)
◀ - 커서를 왼쪽으로 이동 (첫 번째 위치에서 왼쪽으로 이동하면 마지막 문자에 커서)
▶ - 커서를 오른쪽으로 이동
```

예를 들어 아래의 방법으로 JAZ를 만들 수 있습니다.

```
- 첫 번째 위치에서 조이스틱을 위로 9번 조작하여 J를 완성합니다.
- 조이스틱을 왼쪽으로 1번 조작하여 커서를 마지막 문자 위치로 이동시킵니다.
- 마지막 위치에서 조이스틱을 아래로 1번 조작하여 Z를 완성합니다.
따라서 11번 이동시켜 "JAZ"를 만들 수 있고, 이때가 최소 이동입니다.
```

만들고자 하는 이름 name이 매개변수로 주어질 때, 이름에 대해 조이스틱 조작 횟수의 최솟값을 return 하도록 solution 함수를 만드세요.

**제한 사항**

- name은 알파벳 대문자로만 이루어져 있습니다.
- name의 길이는 1 이상 20 이하입니다.

**입출력 예**

name|	return
--|--
"JEROEN"|	56
"JAN"|	23

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/42860)

## 코드
```python
from collections import deque
def solution(name):
	alphabet_dict={chr(i):i-65 for i in range(65,91)}
	move_list=[-1,1]  # left, right
	name_list=list(name)
	#start=(name_list,idx,count)
	def bfs(start):
		queue=deque([start])
		while queue:
			current_node=queue.popleft()
			name_list,idx,cnt=current_node[0],current_node[1],current_node[2]

			#Step-1 상,하 조이스틱 이동
			if 26-alphabet_dict[name_list[idx]]> alphabet_dict[name_list[idx]]:
				cnt+=alphabet_dict[name_list[idx]]
			else:
				cnt+=(26-alphabet_dict[name_list[idx]])

			name_list[idx]='A' #Update

			if name_list.count('A')==len(name_list): # 종료 조건
				return cnt

			#Step-2 좌,우 조이스틱 이동
			for move in move_list:
				updated_name_list=name_list[:] #Shallow copy
				updated_idx=idx+move
				updated_cnt=cnt+1
				queue.append((updated_name_list,updated_idx,updated_cnt))

	return bfs((name_list,0,0))
```

## 설명

```python
alphabet_dict={chr(i):i-65 for i in range(65,91)}
move_list=[-1,1]
name_list=list(name)
```
- `alphabet_dict` 는 `{'A':0, ... ,'Z':25}` 이다.
- `move_list` 에서 **-1 은 왼쪽 이동**, **1 은 오른쪽 이동** 이다.

```python
def bfs(start):
	queue=deque([start])
	while queue:
		current_node=queue.popleft()
		name_list,idx,cnt=current_node[0],current_node[1],current_node[2]

		#Step-1 상,하 조이스틱 이동
		if 26-alphabet_dict[name_list[idx]]> alphabet_dict[name_list[idx]]:
			cnt+=alphabet_dict[name_list[idx]]
		else:
			cnt+=(26-alphabet_dict[name_list[idx]])

		name_list[idx]='A'

		if name_list.count('A')==len(name_list):
			return cnt

		#Step-2 좌,우 조이스틱 이동
		for move in move_list:
			updated_name_list=name_list[:] #Shallow copy
			updated_idx=idx+move
			updated_cnt=cnt+1
			queue.append((updated_name_list,updated_idx,updated_cnt))
```
- [BFS(Breadth-First-Search)](#bfsbreadth-first-search) 를 이용하여 **최소 좌,우 이동거리** 를 찾는다.
- `queue` 에서 방문할 노드를 꺼낸 후 **상,하 이동** 횟수를 저장한다.
- **상,하 이동** 업데이트 후 , 종료조건을 만족하지 않는다면 **좌,우 이동** 을 한다.
- **좌,우 이동**을 통해 방문할 노드 `(현재 name_list,현재 위치,조이스틱 이동횟수)` 를 `queue`에 담은 후 위의 과정을 반복한다.

-
![programmers-level_2-14-2](/assets/img/programmers-level_2-14-2.jpg)

- `방문순서`:`BAB->AAB(left)->AAB(right)->AAA(left)`

## 문제점

- [프로그래머스](https://programmers.co.kr/learn/courses/30/lessons/42860)에서는 `탐욕법(Greedy Algorithm)`으로 분류되어 `Greedy Algorithm`을 이용하여 제출하여 통과하였지만 테스트케이스에 문제가 있는것으로 판단된다.
- 즉, 아래의 코드는 통과된 코드이나 **최소값을 항상 보장하지는 못한다.**

```python
def solution(name):
    list = [min(ord(s) - ord('A'), ord('Z') - ord(s) + 1) for s in name]
    answer = 0
    locat = 0

    while 1:

        answer += list[locat]
        list[locat] = 0
        if sum(list) == 0: break

        left = 1
        right = 1

        while list[locat + right] == 0:
            right += 1

        while list[locat - left] == 0:
            left += 1

        if left >= right:
            locat += right
            answer += right

        else:
            locat -= left
            answer += left

    return answer

```
- 예를들어, `name="BBABAAB"` 이면 조이스틱의 최소 이동횟수는 `9` 이지만 위의 통과한 코드는 `10`을 반환한다.

## BFS(Breadth-First-Search)

- 탐색을 함에 있어서 **가까운 정점을 먼저 탐색** 하고 멀리 떨어져 있는 정점을 나중에 탐색하는 방식이다.
- 즉, 깊게 탐색하기 전에 **넓게** 탐색하는 것이다.
- **두 노드 사이의 최단 경로** 혹은 **임의의 경로** 를 찾고 싶을때 이 방법을 선택한다.
	- Ex) 지구 상에 존재하는 모든 친구 관계를 그래프로 표현한 후 A와 B 사이에 존재하는 경로를 찾는경우
	- **DFS** -모든 친구 관계를 다 살펴봐야 할지도 모른다.
	- **BFS** - A와 가까운 관계부터 탐색.
- **DFS(Depth-First-Search)** 에서는 **스택(Stack)** 이 사용된다면
**BFS(Breadth-First-Search)** 에서는 **큐(Queue)** 가 사용된다.
- **BFS 과정**
	1. 탐색 시작 노드를 큐에 삽입하고 방문처리한다.
	2. 큐의 최상단 노드에게 방문하지 않은 인접노드가 하나라도 있으면 그 노드를 큐에 넣고 방문 처리한다. 방문하지 않은 인접노드가 없으면 큐에서 최상단 노드를 꺼낸다.
	3. 2번의 과정을 더 이상 수행할 수 없을 때까지 반복한다.

![programmers-level_2-14-1](/assets/img/programmers-level_2-14-1.jpg)

## 코드

```python
from collections import deque
def BFS_simulator(graph,root):

	# 1. 탐색 시작 노드를 스택에 삽입하고 방문 처리 한다.
	queue=deque([root])
	visited={root:True}

	while queue:
		# 2. 큐의 최상단 노드에게 방문하지 않은 인접노드가 하나라도 있으면 스택에 넣고 방문 처리한다.
		print('Queue: ',queue)
		current_node=queue.popleft()
		print('currect_node: ',current_node)
		print('\n')
		adjacent_nodes=graph.get(current_node,False)
		if adjacent_nodes : # 인접 노드가 있을 경우
			for node in adjacent_nodes:
				if not(visited.get(node,False)): # 방문한적이 없을경우에만
					visited[node]=True
					queue.append(node)

if __name__=="__main__":
	graph = {
	'A': ['X'],
	'X': ['A', 'G', 'H'],
	'G': ['X','H','P'],
	'H': ['X', 'G', 'P','E'],
	'P': ['G', 'H'],
	'E': ['H','M','Y'],
	'M': ['E','Y','J'],
	'Y': ['E', 'M'],
	'J': ['M'],
	}
	root='A'
	BFS_simulator(graph,root)
```

## Reference
- [BFS-https://gmlwjd9405.github.io/2018/08/15/algorithm-bfs.html](https://gmlwjd9405.github.io/2018/08/15/algorithm-bfs.html)

- [BFS-https://www.zerocho.com/category/Algorithm/post/5870153c37e1c80018b64eb0](https://www.zerocho.com/category/Algorithm/post/5870153c37e1c80018b64eb0)
