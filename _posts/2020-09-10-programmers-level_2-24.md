---
title: Python으로 푸는 프로그래머스 level_2. 숫자의 표현

excerpt: Finn은 요즘 수학공부에 빠져 있습니다. 수학 공부를 하던 Finn은 자연수 n을 연속한 자연수들로 표현 하는 방법이 여러개라는 사실을 알게 되었습니다. 예를들어 15는 다음과 같이 4가지로 표현 할 수 있습니다. 1 + 2 + 3 + 4 + 5 = 15 4 + 5 + 6 = 15 7 + 8 = 15 15 = 15 자연수 n이 매개변수로 주어질 때, 연속된 자연수들로 n을 표현하는 방법의 수를 return하는 solution를 완성해주세요.


categories:
  - codingTest

tags:
  - Programmers
  - Python

date: 2020-09-10
last_modified_at: 2020-09-10
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---

`Tag` `연습문제` <br>

**문제 설명**

Finn은 요즘 수학공부에 빠져 있습니다. 수학 공부를 하던 Finn은 자연수 n을 연속한 자연수들로 표현 하는 방법이 여러개라는 사실을 알게 되었습니다. 예를들어 15는 다음과 같이 4가지로 표현 할 수 있습니다.

- 1 + 2 + 3 + 4 + 5 = 15
- 4 + 5 + 6 = 15
- 7 + 8 = 15
- 15 = 15

자연수 n이 매개변수로 주어질 때, 연속된 자연수들로 n을 표현하는 방법의 수를 return하는 solution를 완성해주세요.

**제한사항**

n은 10,000 이하의 자연수 입니다.

**입출력 예**

n|	result
--|--
15|	4

**입출력 예 설명**

**입출력 예#1**

문제의 예시와 같습니다.

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/12924)

## 코드

```python
def solution(n):
    answer=0
    consecutive=2
    while True:
        summation=sum([i for i in range(1,consecutive+1)])
        if summation>n:
            break
        elif 0==((n-summation)%consecutive):
            answer+=1

        consecutive+=1


    return answer+1

if __name__ == "__main__":

    test_n=15
    print(solution(test_n))

```

## 설명

- `consecutive` 는 연속된 숫자의 개수를 의미한다.
- 연속된 숫자의 갯수만큼 더한 값을 `summation` 에 저장한다.
- `(n-summation)`  가 `consecutive` 로 나누어 떨어지면 연속된 숫자의 갯수 `consecutive` 로 `n` 을 표현할 수 있다.
	> ex)  
	n=15  
	consecutive=3  
	15-(1+2+3)=9  
	9%consecutive=0  

- `summation` 이 `n` 을 넘지 않는동안 연속된 숫자의 갯수 `consecutive` 를 하나씩 늘려간다.
