---
title: Python으로 푸는 프로그래머스 level_2. 큰 수 만들기

excerpt: 어떤 숫자에서 k개의 수를 제거했을 때 얻을 수 있는 가장 큰 숫자를 구하려 합니다. 예를 들어, 숫자 1924에서 수 두 개를 제거하면 [19, 12, 14, 92, 94, 24] 를 만들 수 있습니다. 이 중 가장 큰 숫자는 94 입니다. 문자열 형식으로 숫자 number와 제거할 수의 개수 k가 solution 함수의 매개변수로 주어집니다. number에서 k 개의 수를 제거했을 때 만들 수 있는 수 중 가장 큰 숫자를 문자열 형태로 return 하도록 solution 함수를 완성하세요.

categories:
  - codingTest

tags:
  - Programmers
  - Greedy
  - Python

date: 2020-07-07
last_modified_at: 2020-08-03
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---

`Tag` `탐욕법(Greedy)`<br>

**문제 설명**

어떤 숫자에서 k개의 수를 제거했을 때 얻을 수 있는 가장 큰 숫자를 구하려 합니다.

예를 들어, 숫자 1924에서 수 두 개를 제거하면 [19, 12, 14, 92, 94, 24] 를 만들 수 있습니다. 이 중 가장 큰 숫자는 94 입니다.

문자열 형식으로 숫자 number와 제거할 수의 개수 k가 solution 함수의 매개변수로 주어집니다. number에서 k 개의 수를 제거했을 때 만들 수 있는 수 중 가장 큰 숫자를 문자열 형태로 return 하도록 solution 함수를 완성하세요.

**제한 조건**

- number는 1자리 이상, 1,000,000자리 이하인 숫자입니다.
- k는 1 이상 `number 의 자릿수` 미만인 자연수입니다.

**입출력 예**

number|k|	return
---|---|---
"1924"|2|	"94"
"1231234"|	3|	"3234"
"4177252841"	|4|	"775841"

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/42883)

## 코드
```python
def solution(number, k):
    answer = []
    max_idx=0
    start=-1
    len_target=len(number)-k # 구하고자하는 숫자의 길이
    update_flag=False

    while (len(answer)<len_target):
        #Initialize start, max
        if update_flag: # max 값이 업데이트가 되었을 경우에만
            start=max_idx+1
            update_flag=False

        else: # max값이 업데이트 안된경우= start 자기 자신이 max인경우에는 start를 한칸 밀어준다.
            start+=1

        max=number[start]
        for idx in range(start,k+1+len(answer)):
                # Update max, max_idx
                if max<number[idx]:
                    max=number[idx]
                    max_idx=idx
                    update_flag=True

        answer.append(max)

    return ''.join(answer)
```
## 설명
- K개의 숫자를 제거했을 때 얻을 수 있는 숫자의 길이 `len_target` 을  `len_answer`이 만족할때까지 반복한다.

```python
#Initialize start, max
if update_flag: # max 값이 업데이트가 되었을 경우에만
    start=max_idx+1
    update_flag=False

else: # max값이 업데이트 안된경우= start 자기 자신이 max인경우에는 start를 한칸 밀어준다.
    start+=1
```
- 아래의 예시에서 `max_idx` 가 계속 같은 곳을 가리켜서 `start` 가 제대로 업데이트 되지 않는 경우가 발생하므로, `update_flag`를 통해 체크한다.
> ex)
number='4177252841'
k=4
len_target=6


  loop|n|start|max|max_idx|k+1+len(answer)|
  --|--|--|--|--|--
  1|4|0|4|0|5
  -|1|-|-|-|-
  -|7|-|7|2|-
  -|7|-|-|-|-
  -|2|-|-|-|-

  loop|n|start|max|max_idx|k+1+len(answer)|
  --|--|--|--|--|--
  2|7|3|7|3|6
  -|7|-|-|-|-
  -|2|-|-|-|-
  -|5|-|-|-|-
  -|2|-|-|-|-

- 범위를 한정하지 않으면  아래와 같이 **원하는 숫자 개수를 뽑아 낼수 없는 상황** 이 생기므로  `[start:k+1+len(answer)]` 범위를 한정하여 `max`와 `max_idx` 를 업데이트 한 후 `max` 값을 `answer`에 담아준다.
> ex)
number='12345'
k=2
len_target=3
len_answer=0

loop|n|start|max|max_idx|answer
--|--|--|--|--|--
1|1|0|1|0|
-|2|-|2|1|
-|3|-|3|2|
-|4|-|4|3|
-|5|-|5|4|
-|6|-|6|5|
return|||||[6]


len_target|3|||||
--|--|--|--|--|--
**idx** |0|1|2|3|4
**number** |1|2|3|4|5
**k+1+len(answer)** ||||3
**number[start:k+1+len(answer)]** |1|2|3








- 모든 반복이 끝난 후   `join()` 을 통해 `리스트->문자열` 로 변환하여 반환한다.

## 문제점
- 위의 코드는 **정확성은 통과했지만, 효율성은 통과하지 못했다.**
- **list[a:b]** 의 시간복잡도는 `O(b-a)` 이므로, 반복문마다 `slicing`으로 리스트에 접근하기 때문에 효율적이지 못하다.


## 또 다른 풀이

```python
def solution(number,k):
    answer=[]

    for num in number:
        while answer and answer[-1]<num and k>0:
            answer.pop()
            k-=1
        answer.append(num)
    if 0!=k:
        answer=answer[:-k]

    return ''.join(answer)
```
- [탐욕법(Greedy)](#greedy-algorithm)을 이용하여 **매 순간의 최적의 해** 를 찾는다.
1. 순차적으로 반복하여 앞자리부터 쌓기 시작하여 후보셋을 만들어낸다.
2. 매 순간의 최대값을 쌓기 시작한다.
3. 뒷자리가 그 앞자리보다 큰지 작은지 판별하여 타당성을 체크한다.
4. 뒷자리가 앞자리보다 크다면 선택을 되돌려 앞자리를 제거한다.
5. **number=[4,3,2,1]** ,**k=2** 와 같이 **내림차순** 인 경우 `k!=0`이므로 `answer[:-k]`를 반환한다.

## Greedy Algorithm
- 문제를 해결하는 과정에서 **그 순간순간마다 최적** 이라고 생각되는 결정을 하는 방식으로 진행하여 **최종 해답에 도달하는 문제 해결 방식**
![programmers-level_2-12-1](/assets/img/programmers-level_2-12-1.png)
[이미지 출처](https://velog.io/@cyranocoding/%EB%8F%99%EC%A0%81-%EA%B3%84%ED%9A%8D%EB%B2%95Dynamic-Programming%EA%B3%BC-%ED%83%90%EC%9A%95%EB%B2%95Greedy-Algorithm-3yjyoohia5)

-  **부분집합의 최적의 해**  **!=** **전체집합의 최적의 해**
- 가장 큰 장점은 **계산 속도** 이다.
- 일반적으로 다섯가지의 핵심기능을 가진다.
    1. **A candidate set, from which a solution is created**
    2. **A selection function, which chooses the best candidate to be added to the solution**
    3. **A feasibility function, that is used to determine if a candidate can be used to contribute to a solution**
    4. **An objective function, which assigns a value to a solution, or a partial solution, and**
    5. **A solution function, which will indicate when we have discovered a complete solution**
- 올바르게 작동하기 위해서는 두가지 조건이 필요하다.
    - **탐욕스러운 선택 조건(Greedy choice property)**
    >이 전의 선택이 이 후의 선택에 영향을 주지 않아야 한다.

    - **최적 부분 구조 조건(Optimal Substructure)**
    > 문제에 대한 최종 해결방법이 부분문제에 대해서도 또한 최적 문제해결 방법이다.
