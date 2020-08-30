---
title: Python으로 푸는 프로그래머스 level_2. 카펫

excerpt: Leo는 카펫을 사러 갔다가 아래 그림과 같이 중앙에는 노란색으로 칠해져 있고 테두리 1줄은 갈색으로 칠해져 있는 격자 모양 카펫을 봤습니다. Leo는 집으로 돌아와서 아까 본 카펫의 노란색과 갈색으로 색칠된 격자의 개수는 기억했지만, 전체 카펫의 크기는 기억하지 못했습니다. Leo가 본 카펫에서 갈색 격자의 수 brown, 노란색 격자의 수 yellow가 매개변수로 주어질 때 카펫의 가로, 세로 크기를 순서대로 배열에 담아 return 하도록 solution 함수를 작성해주세요.


categories:
  - codingTest

tags:
  - Programmers
  - BP(Brute-Force)
  - Python

date: 2020-08-30
last_modified_at: 2020-08-30
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---

`Tag` `완전탐색(Brute-Force)` <br>

**문제 설명**

Leo는 카펫을 사러 갔다가 아래 그림과 같이 중앙에는 노란색으로 칠해져 있고 테두리 1줄은 갈색으로 칠해져 있는 격자 모양 카펫을 봤습니다.

![programmers-level_2-16-1](/assets/img/programmers-level_2-16-1.png)

Leo는 집으로 돌아와서 아까 본 카펫의 노란색과 갈색으로 색칠된 격자의 개수는 기억했지만, 전체 카펫의 크기는 기억하지 못했습니다.

Leo가 본 카펫에서 갈색 격자의 수 brown, 노란색 격자의 수 yellow가 매개변수로 주어질 때 카펫의 가로, 세로 크기를 순서대로 배열에 담아 return 하도록 solution 함수를 작성해주세요.

**제한사항**

- 갈색 격자의 수 brown은 8 이상 5,000 이하인 자연수입니다.
- 노란색 격자의 수 yellow는 1 이상 2,000,000 이하인 자연수입니다.
- 카펫의 가로 길이는 세로 길이와 같거나, 세로 길이보다 깁니다.

**입출력 예**

brown	|yellow	|return
--|--|--
10|	2|	[4, 3]
8	|1	|[3, 3]
24	|24	|[8, 6]

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/42842)

## 코드

```python
def solution(brown, yellow):
    inner_width=1 # 내부 노란색 가로 길이
    inner_height=1# 내부 노락색 세로 길이

    for a in range(1,yellow+1):
        if 0==yellow%a: # ab=yellow
            inner_width=a # a
            inner_height=int(yellow/a) # b

            if (2*inner_width)+(2*inner_height)==brown-4: # (a+2)(b+2)=brown
                break

    if inner_width<inner_height: #세로길이가 더 큰 경우
        inner_width,inner_height=inner_height,inner_width # swap

    return [inner_width+2,inner_height+2]

if __name__=="__main__":
    test_brown=24
    test_yellow=24
    print(solution(test_brown,test_yellow))

```
## 설명

![programmers-level_2-16-2](/assets/img/programmers-level_2-16-2.jpg)
- $$
\begin{cases}
    a\cdot b=yellow\\
		(a+2)\cdot(b+2)=brown\\
\end{cases}
(a=inner\_width , b=inner\_height )
$$
을 만족하는 **a** 와 **b** 값을 찾는 것이다.
