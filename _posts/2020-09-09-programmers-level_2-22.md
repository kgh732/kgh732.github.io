---
title: Python으로 푸는 프로그래머스 level_2. 땅따먹기

excerpt: 땅따먹기 게임을 하려고 합니다. 땅따먹기 게임의 땅(land)은 총 N행 4열로 이루어져 있고, 모든 칸에는 점수가 쓰여 있습니다. 1행부터 땅을 밟으며 한 행씩 내려올 때, 각 행의 4칸 중 한 칸만 밟으면서 내려와야 합니다. 단, 땅따먹기 게임에는 한 행씩 내려올 때, 같은 열을 연속해서 밟을 수 없는 특수 규칙이 있습니다.


categories:
  - codingTest

tags:
  - Programmers
  - DP(Dynamic Programming)
  - Python

date: 2020-09-09
last_modified_at: 2020-09-09
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---

`Tag` `DP(Dynamic Programming)` <br>

**문제 설명**

땅따먹기 게임을 하려고 합니다. 땅따먹기 게임의 땅(land)은 총 N행 4열로 이루어져 있고, 모든 칸에는 점수가 쓰여 있습니다. 1행부터 땅을 밟으며 한 행씩 내려올 때, 각 행의 4칸 중 한 칸만 밟으면서 내려와야 합니다. 단, 땅따먹기 게임에는 한 행씩 내려올 때, 같은 열을 연속해서 밟을 수 없는 특수 규칙이 있습니다.

예를 들면,

| 1 | 2 | 3 | 5 |

| 5 | 6 | 7 | 8 |

| 4 | 3 | 2 | 1 |

로 땅이 주어졌다면, 1행에서 네번째 칸 (5)를 밟았으면, 2행의 네번째 칸 (8)은 밟을 수 없습니다.

마지막 행까지 모두 내려왔을 때, 얻을 수 있는 점수의 최대값을 return하는 solution 함수를 완성해 주세요. 위 예의 경우, 1행의 네번째 칸 (5), 2행의 세번째 칸 (7), 3행의 첫번째 칸 (4) 땅을 밟아 16점이 최고점이 되므로 16을 return 하면 됩니다.

**제한사항**

- 행의 개수 N : 100,000 이하의 자연수
- 열의 개수는 4개이고, 땅(land)은 2차원 배열로 주어집니다.
- 점수 : 100 이하의 자연수

**입출력 예**

land|	answer
--|--
\[[1,2,3,5],[5,6,7,8],[4,3,2,1]]	|16

**입출력 예 설명**

**입출력 예 #1**

문제의 예시와 같습니다.

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/12913)

## 코드
```python


def solution(land):
    answer = 0
    tabulation = [land[0] if 0 == row else [0, 0, 0, 0]
                   for row in range(len(land))]
    for row_index in range(1, len(land)):
        for c1 in range(4):
            tabulation[row_index][c1] = land[row_index][c1] + \
                max(tabulation[row_index - 1][:c1] +
                    tabulation[row_index - 1][c1 + 1:])

    return max(tabulation[-1])


if __name__ == "__main__":
    test_land = [[1, 2, 3, 5],
                 [5, 6, 7, 100],
                 [4, 3, 2, 1]]

    print(solution(test_land))


```

## 설명

- [DP(Dynamic Programming)](https://kgh732.github.io/codingtest/programmers-level_2-18/#dpdynamic-programming) 를 이용하여 푼다.

1. 주어진 문제에 대한 **순환식** 을 정의한다.

	![programmers-level_2-22-1](/assets/img/programmers-level_2-22-1.jpg)

	- $tabulation[i][j]=land[i][j]+max(tabulation[i-1][0],tabulation[i-1][1],\ldots,tabulation[i-1][j-1],tabulation[i-1][j+1],\ldots)$
	$(1\leq{i}\lt{n},0\leq{j}\lt{4},n=len(land))$

	- **전체 문제의 최적해의 일부분이 부분문제의 최적해** 인지 확인한다

2. **순환식** 을 활용하여 **Tabulation(Bottom-Up)** 으로 푼다.

3. `tabulation` 의 **마지막 행의 최대값 = 전체문제의 최적해** 이다.
