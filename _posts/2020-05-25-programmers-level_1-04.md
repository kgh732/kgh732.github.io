---
title: "Python으로 푸는 프로그래머스 level_1. 체육복"
excerpt: "점심시간에 도둑이 들어, 일부 학생이 체육복을 도난당했습니다. 다행히 여벌 체육복이 있는 학생이 이들에게 체육복을 빌려주려 합니다. 학생들의 번호는 체격 순으로 매겨져 있어, 바로 앞번호의 학생이나 바로 뒷번호의 학생에게만 체육복을 빌려줄 수 있습니다. 예를 들어, 4번 학생은 3번 학생이나 5번 학생에게만 체육복을 빌려줄 수 있습니다. 체육복이 없으면 수업을 들을 수 없기 때문에 체육복을 적절히 빌려 최대한 많은 학생이 체육수업을 들어야 합니다."

categories:
  - codingTest

tags:
  - Programmers
  - Greedy
  - Python

date: 2020-05-25
last_modified_at: 2020-07-29
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---
`Tag` `탐욕법(Greedy)`<br>

**문제 설명**<br>
점심시간에 도둑이 들어, 일부 학생이 체육복을 도난당했습니다. 다행히 여벌 체육복이 있는 학생이 이들에게 체육복을 빌려주려 합니다. 학생들의 번호는 체격 순으로 매겨져 있어, 바로 앞번호의 학생이나 바로 뒷번호의 학생에게만 체육복을 빌려줄 수 있습니다. 예를 들어, 4번 학생은 3번 학생이나 5번 학생에게만 체육복을 빌려줄 수 있습니다. 체육복이 없으면 수업을 들을 수 없기 때문에 체육복을 적절히 빌려 최대한 많은 학생이 체육수업을 들어야 합니다.

전체 학생의 수 n, 체육복을 도난당한 학생들의 번호가 담긴 배열 lost, 여벌의 체육복을 가져온 학생들의 번호가 담긴 배열 reserve가 매개변수로 주어질 때, 체육수업을 들을 수 있는 학생의 최댓값을 return 하도록 solution 함수를 작성해주세요.

**제한사항**<br>
전체 학생의 수는 2명 이상 30명 이하입니다.
체육복을 도난당한 학생의 수는 1명 이상 n명 이하이고 중복되는 번호는 없습니다.
여벌의 체육복을 가져온 학생의 수는 1명 이상 n명 이하이고 중복되는 번호는 없습니다.
여벌 체육복이 있는 학생만 다른 학생에게 체육복을 빌려줄 수 있습니다.
여벌 체육복을 가져온 학생이 체육복을 도난당했을 수 있습니다. 이때 이 학생은 체육복을 하나만 도난당했다고 가정하며, 남은 체육복이 하나이기에 다른 학생에게는 체육복을 빌려줄 수 없습니다.

**입출력 예**

n	|lost|reserve|return
--|-----|----|-----
5|	[2, 4]|	[1, 3, 5]|	5
5|	[2, 4]|	[3]	|4
3|	[3]|	[1]|	2

**입출력 예 설명**

**예제 #1**
1번 학생이 2번 학생에게 체육복을 빌려주고, 3번 학생이나 5번 학생이 4번 학생에게 체육복을 빌려주면 학생 5명이 체육수업을 들을 수 있습니다.

**예제 #2**
3번 학생이 2번 학생이나 4번 학생에게 체육복을 빌려주면 학생 4명이 체육수업을 들을 수 있습니다.

**예제 #3**
1번 학생은 어느 누구에도 빌려줄수 없으므로 학생 2명이 체육수업을 들을 수 있습니다.

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/42862)

## 코드

```python
def solution(n,lost,reserve):

    answer=[1]*n

    for lost_element in lost:
        answer[lost_element-1]-=1

    for reserve_element in reserve:
        answer[reserve_element-1]+=1


    for i in range(n):
        left=i-1
        right=i+1
        if left>=0 and answer[i]==0 and answer[left]==2:
            answer[i]+=1
            answer[left]-=1

        if right<n and answer[i]==0 and answer[i+1]==2:
            answer[i]+=1
            answer[right]-=1



    result=[1 for a in answer if a>0]
    return sum(result)
```

## 설명

```python
answer=[1]*n

for lost_element in lost:
    answer[lost_element-1]-=1

for reserve_element in reserve:
    answer[reserve_element-1]+=1
```
- 각 학생들은 체육복을 1벌씩 가지고 있는 상태이다.
- 이때, 체육복을 잃어 버린 학생들의 상황를 기록한다.
- 또한, 여벌을 가지고 있는 학생들의 상황를 기록한다.
- answer 가 가질수 있는 원소값
   - ```0``` (여벌이 필요한 학생)
   - ```1``` (자기 체육복을 가지고 있는 학생 or  ***여벌을 가지고 있었으나 자기 자신의 체육복이 도난당한 학생*** )
   - ```2```(여벌을 가지고 있는 학생)

>  주목해야할것은 제한사항에서 여벌을 가지고 있었으나 자신의 체육복을 도난 당한경우 빌려줄수 없다는 것이다. 이것을 위의 기록을 통해서 미리 처리하였다.

```python
for i in range(n):
    left=i-1
    right=i+1
    if left>=0 and answer[i]==0 and answer[left]==2:
        answer[i]+=1
        answer[left]-=1

    if right<n and answer[i]==0 and answer[i+1]==2:
        answer[i]+=1
        answer[right]-=1

```
- 이제 우리가 해야할것은 인접한 학생에게 체육복을 빌릴수 있는지 확인하는 것이다.
- IndexError와 함께 왼쪽과 오른쪽을 함께 체크하여 학생들의 상태를 기록해준다.

```python
result=[1 for a in answer if a>0]
return sum(result)
```
- 여벌을 가지고 있었으나 인접한 학생이 없어 빌려주지 못한 학생들이 있을 경우가 있다. 즉, ```2``` 의 원소값을 가지고 있는 경우가 있다.
- 그래서 우리가 원하는 결과 값을 체육수업에 참여 할수 있는 인원이므로 ```0```이 아닌 학생들의 수를 체크하여 반환한다.
