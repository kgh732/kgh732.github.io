---
title: Python으로 푸는 프로그래머스 level_2. 가장 큰 정사각형 찾기

excerpt: 1와 0로 채워진 표(board)가 있습니다. 표 1칸은 1 x 1 의 정사각형으로 이루어져 있습니다. 표에서 1로 이루어진 가장 큰 정사각형을 찾아 넓이를 return 하는 solution 함수를 완성해 주세요. (단, 정사각형이란 축에 평행한 정사각형을 말합니다.)


categories:
  - codingTest

tags:
  - Programmers
  - DP(Dynamic Programming)
  - Python

date: 2020-09-02
last_modified_at: 2020-09-02
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---

`Tag` `DP(Dynamic Programming)` <br>

**문제 설명**

1와 0로 채워진 표(board)가 있습니다. 표 1칸은 1 x 1 의 정사각형으로 이루어져 있습니다. 표에서 1로 이루어진 가장 큰 정사각형을 찾아 넓이를 return 하는 solution 함수를 완성해 주세요. (단, 정사각형이란 축에 평행한 정사각형을 말합니다.)

예를 들어

1|	2|	3|	4
--|--|--|--
0|	1|	1|	1
1|	1|	1|	1
1	|1	|1	|1
0|	0|	1|	0
가 있다면 가장 큰 정사각형은

1|	2|	3|	4
--|--|--|--
0	|`1`|	`1`|	`1`
1|	`1`|	`1`|	`1`
1	|`1`|	`1`	|`1`
0	|0|	1	|0
가 되며 넓이는 9가 되므로 9를 반환해 주면 됩니다.

**제한사항**

- 표(board)는 2차원 배열로 주어집니다.
- 표(board)의 행(row)의 크기 : 1,000 이하의 자연수
- 표(board)의 열(column)의 크기 : 1,000 이하의 자연수
- 표(board)의 값은 1또는 0으로만 이루어져 있습니다.

**입출력 예**

board|	answer
--|--
\[[0,1,1,1],[1,1,1,1],[1,1,1,1],[0,0,1,0]]|	9
\[[0,0,1,1],[1,1,1,1]]|	4

**입출력 예 설명**

**입출력 예 #1**

위의 예시와 같습니다.

**입출력 예 #2**
1|	2|	3|	4
--|--|--|--
 0 | 0 | `1` | `1`
 1 | 1 | `1` | `1`

로 가장 큰 정사각형의 넓이는 4가 되므로 4를 return합니다.

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/12905)

## 코드
```python
def solution(board):
    # 첫행,첫열을 미리 살펴서 max_square_size 초기화
    first_column=[board[y][0]for y in range(len(board))]
    max_square_size=1 if 1 in board[0] or 1 in first_column else 0

    #DP(Dynamic Programming,Tabulation,Bottom-up)
    for y in range(1,len(board)):
        for x in range(1,len(board[0])):
            if 1==board[y][x] :
                current_square_size=min(board[y-1][x],board[y][x-1],board[y-1][x-1])+1 # 상단,좌측,좌측상단
                board[y][x]=current_square_size # Tabulation
                if max_square_size<current_square_size:
                    max_square_size=current_square_size

    return max_square_size**2


if __name__=="__main__":
    test_board=[[0,1,1,1],
                [1,1,1,1],
                [1,1,1,1],
                [0,0,1,0]]
    print(solution(test_board))
```

## 설명

```python
first_column=[board[y][0]for y in range(len(board))]
max_square_size=1 if 1 in board[0] or 1 in first_column else 0
```
- `board` = **\[[1,0],[0,0]]** 또는 **\[[0,0],[0,0]]** 와 같은 경우에 `max_square_size`를 제대로 된 값으로 초기화 하기 위해 **첫행** ,**첫열** 을 확인한다.

```python
for y in range(1,len(board)):
    for x in range(1,len(board[0])):
        if 1==board[y][x] :
            current_square_size=min(board[y-1][x],board[y][x-1],board[y-1][x-1])+1 # 상단,좌측,좌측상단
            board[y][x]=current_square_size # Tabulation
            if max_square_size<current_square_size:
                max_square_size=current_square_size
```
- [DP(Dynamic Programming)](#dpdynamic-programming) 을 이용한다.
- 현 배열의 위치에서 값이 **1** 인 경우에만 **상단,좌측,좌측상단** 을 살펴본다. **(순환식)**
![programmmers-level_2-18-1](/assets/img/programmers-level_2-18-1.jpg)

$$
board[y][x]=min(board[y-1][x-1],board[y-1][x],board[y][x-1])+1, \\
(1\leq{y}\leq{m},1\leq{x}\leq{n},m=len(board),n=len(board[0]))
$$

- **가장 작은 값의 +1** 을 **현 배열의 위치 값을 대체** 한다.**(Tabulation)**
- 위의 과정을 배열의 마지막까지 반복한 후 **가장 큰 값 = 가장 큰 정사각형의 한변의 길이** 이다.**(Solving problem)**
![programmmers-level_2-18-2](/assets/img/programmers-level_2-18-2.png)

## DP(Dynamic Programming)
- **overlapping 되는 부분문제들을 풀어서 원래 문제를 해결하는 방식.**
- **부분문제들을 풀어서 원래 문제를 해결한다는 점** 에서 [분할정복법(Divide & Conquer)](#divide-and-conquer) 과 공통점이 있다.
- **작동 과정**
	1. 주어진 문제에 대한 **순환식** 을 정의한다.
		- **순환식** 은 **optimal substructure** 를 표현한다.
		- 순환식을 세우기 위해서는 **전체 문제의 최적해의 일부분이 부분문제의 최적해인가** 에 대한 확인이 필요하다.
	2. **순환식** 을 이용하여 [Memoization](#memoization) 또는 **Bottom-up(Tabulation)** 으로 푼다.


## Memoization
- **DP(Dynamic Programming)** 와 **동일하게 배열 공간을 활용하고, 이전 동작에서의 데이터를 가져다 쓴다는 점에서 비슷하다.**
- **DP** 와 **Memoization** 은 혼용되어서 사용될 수 있다.
- 그렇지만 엄밀히 말하면,
	- **DP(Tabulation)** : **테이블 작성** 을 통해 문제를 해결해 나가는 **Bottom-Up** 에 해당한다.
	- **Memoization** : 이미 모든 부분문제를 해결한 n차 배열을 가지고 문제를 해결해 나가는 **Top-Bottom** 에 해당한다.
	즉, **최종 문제(Top)까지 모든 계산을 마치고, 이미 완성되어 있는 표에 기반해 모든 부분문제(Bottom)을 해결한다.**



## Divide and Conquer
- **복잡한 문제를 분할하여 부분문제를 품으로써 원래 문제를 정복하는 방식.**
- 그렇다면 **DP** 와 **Divide & Conquer**의 차이점은 무엇인가?
	- **Divide & Conquer** : 분할된 문제들은 서로 **disjoint**.
	분할정복의 대표적인 예인 **Quick sort**의 경우  **pivot** 을 기준으로 두 부분문제로 나뉘며 서로 **disjoint.**
	즉, 오른쪽의 계산결과가 왼쪽에 전혀 영향을 끼치지 않으며, 분할된 문제를 해결함으로써 원래 문제를 해결한다.
	![programmers-level_2-18-3](/assets/img/programmers-level_2-18-3.png)

	- **DP** :  분할된 문제들은 서로 **overlap**.
	대표적인 예인 **최단경로(Shortest-Path)** 의 경우, **(i,j)** 까지 오는 경로를 구할때, **(i-1,j) 와 (i,j-1) 까지 오는 부분문제들이 서로 영향을 끼친다.**
	![programmers-level_2-18-4](/assets/img/programmers-level_2-18-4.png)


## Reference
[DP - https://m.blog.naver.com/aufcl4858/221025533282](https://m.blog.naver.com/aufcl4858/221025533282)
