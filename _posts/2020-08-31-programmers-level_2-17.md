---
title: Python으로 푸는 프로그래머스 level_2. 타겟 넘버

excerpt: n개의 음이 아닌 정수가 있습니다. 이 수를 적절히 더하거나 빼서 타겟 넘버를 만들려고 합니다. 예를 들어 [1, 1, 1, 1, 1]로 숫자 3을 만들려면 다음 다섯 방법을 쓸 수 있습니다.


categories:
  - codingTest

tags:
  - Programmers
  - DFS
  - BFS
  - Python

date: 2020-08-31
last_modified_at: 2020-08-31
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---

`Tag` `깊이/너비 우선 탐색(DFS/BFS)` <br>

**문제 설명**

n개의 음이 아닌 정수가 있습니다. 이 수를 적절히 더하거나 빼서 타겟 넘버를 만들려고 합니다. 예를 들어 [1, 1, 1, 1, 1]로 숫자 3을 만들려면 다음 다섯 방법을 쓸 수 있습니다.

	-1+1+1+1+1 = 3
	+1-1+1+1+1 = 3
	+1+1-1+1+1 = 3
	+1+1+1-1+1 = 3
	+1+1+1+1-1 = 3

사용할 수 있는 숫자가 담긴 배열 numbers, 타겟 넘버 target이 매개변수로 주어질 때 숫자를 적절히 더하고 빼서 타겟 넘버를 만드는 방법의 수를 return 하도록 solution 함수를 작성해주세요.

**제한사항**

주어지는 숫자의 개수는 2개 이상 20개 이하입니다.
각 숫자는 1 이상 50 이하인 자연수입니다.
타겟 넘버는 1 이상 1000 이하인 자연수입니다.

**입출력 예**

numbers|	target	|return
--|--|--
[1, 1, 1, 1, 1]|	3|	5

**입출력 예 설명**

문제에 나온 예와 같습니다.

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/43165)

## 코드

```python
def solution(numbers, target):
    answer = 0
    visited={}
    roots=[numbers[0],-numbers[0]]
    temp_target=0
    for root in roots:
        #DFS
        stack=[(root,0)] # (node value, level)
        while stack: # stack을 다 비울때까지
            current_node=stack.pop() # 현재 방문중인 노드
            value=current_node[0]
            level=current_node[1]
            if visited.get(level,False):
                for i in range(level,len(numbers)):
                    temp_target-=visited.get(i)
                    visited.pop(i)
            temp_target+=value
            visited[level]=value
            if level<len(numbers)-1: # 가장 깊이 도달하기 전까지
                stack.append((numbers[level + 1], level + 1))
                stack.append((-numbers[level + 1], level + 1))

            else: #가장 깊이 도달했을때
                if temp_target==target: #원하는 타겟
                    answer+=1

    return answer

if __name__=="__main__":
    test_numbers=[1,1,1,1,1]
    test_target=3
    print(solution(test_numbers,test_target))
```

## 설명
- $ex)numbers=[1,2,3,4,5], target=2$
![programmers-level_2-17-1](/assets/img/programmers-level_2-17-1.jpg)
- [DFS(Depth-First-Search)](https://kgh732.github.io/codingtest/programmers-level_2-10/#dfsdepth-first-search) 를 통해 모든 결과를 탐색한다.
	1. `stack`에는 각 노드의 **(노드값,노드레벨)** 튜플을 담는다
	2. 가장 깊은 레벨에 도달할때 까지 인접노드를 `stack`에 담아둔다.
	3. 가장 깊은 레벨에 도달했을 경우 `temp_target` 과 `target` 값이 같은지 체크한다.
	4. 가장 깊은곳 도달 후 되돌아 갈때 현재 방문 노드 `current_node` 의 `level` 보다 **깊고 같은 노드들은 제거하며, temp_target 값 또한 업데이트 해준다.**
	5. 위의 과정을 `stack`을 비울때까지 반복한다.


## 문제점

- **input으로 들어오는 `numbers`의 순서가 유지가 되어야 하는지 아닌지** 명확하게 문제에 명시되어 있지 않다.
- 즉, **numbers=[1, 2]** 이라고 할 때 ,
	- **순서를 유지하는 경우:** (+1+2), (+1+2), (-1+2), (-1-2)
	- **순서를 유지하지 않는 경우:** (+2+1), (+2-1), (-2+1), (-2-1)
	중 어느 조건인지 명확하지 않다는 것이다.
- 이 문제에선 하필 또 예시가 **numbers=[1, 1, 1, 1, 1]** 이다.
즉,**`numbers`의 순서를 유지하든 유지하지 않든 결과값이 똑같은 예시가 들어있다.**
- 결론적으론 이 문제에서는 **순서를 유지하는 경우** 로 가정하여 구현한다면 통과할수 있다.**(만약 순서를 유지하지 않는 조건이라면 위의 코드는 통되지 않습니다.)**
