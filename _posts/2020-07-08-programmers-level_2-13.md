---
title: Python으로 푸는 프로그래머스 level_2. H-Index

excerpt: H-Index는 과학자의 생산성과 영향력을 나타내는 지표입니다. 어느 과학자의 H-Index를 나타내는 값인 h를 구하려고 합니다. 위키백과에 따르면, H-Index는 다음과 같이 구합니다. 어떤 과학자가 발표한 논문 `n` 편 중, `h` 번 이상 인용된 논문이 `h` 편 이상이고 나머지 논문이 `h` 번 이하 인용되었다면 `h` 의 최댓값이 이 과학자의 H-Index입니다. 어떤 과학자가 발표한 논문의 인용 횟수를 담은 배열 citations가 매개변수로 주어질 때, 이 과학자의 H-Index를 return 하도록 solution 함수를 작성해주세요.

categories:
  - codingTest

tags:
  - Programmers
  - Sorting
  - Python

date: 2020-07-08
last_modified_at: 2020-08-03
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---

`Tag` `정렬`<br>

**문제 설명**

H-Index는 과학자의 생산성과 영향력을 나타내는 지표입니다. 어느 과학자의 H-Index를 나타내는 값인 h를 구하려고 합니다. 위키백과에 따르면, H-Index는 다음과 같이 구합니다.

어떤 과학자가 발표한 논문 `n` 편 중, `h` 번 이상 인용된 논문이 `h` 편 이상이고 나머지 논문이 `h` 번 이하 인용되었다면 `h` 의 최댓값이 이 과학자의 H-Index입니다.

어떤 과학자가 발표한 논문의 인용 횟수를 담은 배열 citations가 매개변수로 주어질 때, 이 과학자의 H-Index를 return 하도록 solution 함수를 작성해주세요.

**제한사항**

- 과학자가 발표한 논문의 수는 1편 이상 1,000편 이하입니다.
- 논문별 인용 횟수는 0회 이상 10,000회 이하입니다.

 **입출력 예**

citations|	return
--|--
[3, 0, 6, 1, 5]|	3

**입출력 예 설명**

이 과학자가 발표한 논문의 수는 5편이고, 그중 3편의 논문은 3회 이상 인용되었습니다. 그리고 나머지 2편의 논문은 3회 이하 인용되었기 때문에 이 과학자의 H-Index는 3입니다.

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/42747)

## 코드
```python
def solution(citations):
    citations.sort(reverse=True)
    h=1
    for citation in citations:
        if citation>=h:
            h+=1
        else:
            h-=1
            break

    if len(citations)<h:
        h=len(citations)

    return h
```
## 설명

```python
citations.sort(reverse=True)
h=1
for citation in citations:
    if citation>=h:
        h+=1
    else:
        h-=1
        break
```
- `h`번 이상 인용된 횟수가 핵심 포인트.
- 논문의 인용 횟수 `citations` 를 **내림 차순 정렬** 하여 `h`를 늘려가면서 최댓값을 찾는다.
- **내림차순 정렬** 되어 이전의 원소들은 항상 `h` 이상이므로, 각각의 원소들만 비교하면 된다.
- H-Index `h` 이상 인용 되었을 경우에만 **+1** 한다.
- H-Index를 만족하지 못할 경우 **-1** 한다.
> ex)
citations=[3,0,6,1,5]
citations.sort() # [6,5,3,1,0]

citation|h|bool|operation
--|--|--|--
6|1|True|+1
5|2|True|+1
3|3|True|+1
1|4|False|-1
0||
return|3|


```python
if len(citations)<h:
    h=len(citations)
```
- 모든 **논문의 인용횟수** **>** **논문의 수** 인 경우 `h` 는 **논문의  수** 이다.
>ex)
citations=[24,25,26]

citation|h|bool|operation
--|--|--|--
26|1|True|+1
25|2|True|+1
24|3|True|+1
return|4|
