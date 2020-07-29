---
title: Python으로 푸는 프로그래머스 level_1. [1차] 비밀지도
excerpt: 네오는 평소 프로도가 비상금을 숨겨놓는 장소를 알려줄 비밀지도를 손에 넣었다. 그런데 이 비밀지도는 숫자로 암호화되어 있어 위치를 확인하기 위해서는 암호를 해독해야 한다. 다행히 지도 암호를 해독할 방법을 적어놓은 메모도 함께 발견했다.

categories:
  - codingTest

tags:
  - Programmers
  - 2018 KAKAO
  - Python

date: 2020-06-23
last_modified_at: 2020-07-29
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---

`Tag` `2018 KAKAO BLIND RECRUITMENT `<br>


**문제 설명**

**비밀지도**

네오는 평소 프로도가 비상금을 숨겨놓는 장소를 알려줄 비밀지도를 손에 넣었다. 그런데 이 비밀지도는 숫자로 암호화되어 있어 위치를 확인하기 위해서는 암호를 해독해야 한다. 다행히 지도 암호를 해독할 방법을 적어놓은 메모도 함께 발견했다.

1. 지도는 한 변의 길이가 n인 정사각형 배열 형태로, 각 칸은 "공백(" ") 또는"벽"("#") 두 종류로 이루어져 있다.
2. 전체 지도는 두 장의 지도를 겹쳐서 얻을 수 있다. 각각 "지도 1"과 "지도 2"라고 하자. 지도 1 또는 지도 2 중 어느 하나라도 벽인 부분은 전체 지도에서도 벽이다. 지도 1과 지도 2에서 모두 공백인 부분은 전체 지도에서도 공백이다.
3. "지도 1"과 "지도 2"는 각각 정수 배열로 암호화되어 있다.
4. 암호화된 배열은 지도의 각 가로줄에서 벽 부분을 ```1```, 공백 부분을 ```0```으로 부호화했을 때 얻어지는 이진수에 해당하는 값의 배열이다.

![programmers-level_1-34-1](/assets/img/programmers-level_1-34-1.png)

네오가 프로도의 비상금을 손에 넣을 수 있도록, 비밀지도의 암호를 해독하는 작업을 도와줄 프로그램을 작성하라.

**입력 형식**

입력으로 지도의 한 변 크기 ```n``` 과 2개의 정수 배열 ```arr1```, ```arr2```가 들어온다.

- 1 ≦ ```n``` ≦ 16
- ```arr1```, ```arr2```는 길이 ```n```인 정수 배열로 주어진다.
- 정수 배열의 각 원소 ```x```를 이진수로 변환했을 때의 길이는 ```n``` 이하이다. 즉, 0 ≦ ```x``` ≦ 2n - 1을 만족한다.

**출력 형식**

원래의 비밀지도를 해독하여 ```'#'```, ```공백```으로 구성된 문자열 배열로 출력하라.

**입출력 예제**

매개변수|	값
--|--
n|	5
arr1|	[9, 20, 28, 18, 11]
arr2|	[30, 1, 21, 17, 28]
출력	|["#####","# # #", "### #", "# ##", "#####"]

매개변수|	값
--|--
n	|6
arr1|	[46, 33, 33 ,22, 31, 50]
arr2|	[27 ,56, 19, 14, 14, 10]
출력|	["######", "### #", "## ##", " #### ", " #####", "### # "]

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/17681)

## 코드
```python
def solution(n, arr1, arr2):
    answer = []


    for idx in range(n):
        temp=''
        for j in range(n):
            r1=arr1[idx]%2
            arr1[idx]=arr1[idx]//2
            r2=arr2[idx]%2
            arr2[idx]=arr2[idx]//2
            if r1+r2>=1:
                temp+="#"
            else:
                temp+=' '
        answer.append(temp[::-1])

    return answer
```

## 설명
```python
for idx in range(n):
    temp=''
    for j in range(n):
        r1=arr1[idx]%2
        arr1[idx]=arr1[idx]//2
        r2=arr2[idx]%2
        arr2[idx]=arr2[idx]//2
        if r1+r2>=1:
            temp+="#"
        else:
            temp+=' '
    answer.append(temp[::-1])
```
- ```10진수->2진수``` 변환을 위해 ```arr1```,```arr2```의 각 원소를 2로 나눈 몫과 나머지를 업데이트 한다.
- ```비트연산 or ``` 을 계산하기 위해 **2진수의 자릿수 합이 1이상** 이 되는 경우에는 ```벽("#")```, 아닌 경우에는 ```공백(" ")```을 넣는다.
- 마지막 자릿수부터 계산한것을 고려하여 문자열을 뒤집어서 결과를 저장한다.


## 또 다른 풀이
```python

def solution(n, arr1, arr2):
    answer = []
    for i,j in zip(arr1,arr2):
        a12 = str(bin(i|j)[2:])
        a12=a12.rjust(n,'0')
        a12=a12.replace('1','#')
        a12=a12.replace('0',' ')
        answer.append(a12)
    return answer
```
- ```bin()``` 과 ```비트연산 | (or)``` 으로 계산한 결과값 ```0b....```에서 ```0b```를 제외한 값을 가져온다
- 문제에서 주어진 이진수 길이를 맞추기 위해 ```rjust()```를 이용해 비워진곳은 ```0```으로 채운다
- 결과 문자열에서 ```'1'->'#'```, ```'0'->' '```으로 바꾼다.

### N 진수 변환
```python
#10진수 -> 2진수
bin(33)
#0b100001
bin(22)
#0b10110

#10진수 -> 8진수
oct(33)
#0o41
oct(22)
#0o26

#10진수->16진수
hex(33)
#0x21
hex(22)
#0x16
```
### 문자열 패딩
```python
'rjust'.rjust(5)
#' rjust'
'rjust'.rjust(7,'t')
#'ttrjust'
'rjust'.rjust(3)
#'rjust'

'ljust'.ljust(5)
#'ljust '
'ljust'.ljust(7,'t')
#'ljusttt'
'ljust'.rjust(3)
#'ljust'

'rstrip   '.rstrip()
#rstrip
'    lstrip'.lstrip()
#lstrip
'   strip  '.strip()
#strip

```
