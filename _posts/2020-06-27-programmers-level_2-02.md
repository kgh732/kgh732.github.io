---
title: Python으로 푸는 프로그래머스 level_2. 문자열 압축

excerpt: 데이터 처리 전문가가 되고 싶은 어피치는 문자열을 압축하는 방법에 대해 공부를 하고 있습니다. 최근에 대량의 데이터 처리를 위한 간단한 비손실 압축 방법에 대해 공부를 하고 있는데, 문자열에서 같은 값이 연속해서 나타나는 것을 그 문자의 개수와 반복되는 값으로 표현하여 더 짧은 문자열로 줄여서 표현하는 알고리즘을 공부하고 있습니다. 간단한 예로 "aabbaccc"의 경우 "2a2ba3c"(문자가 반복되지 않아 한번만 나타난 경우 1은 생략함)와 같이 표현할 수 있는데, 이러한 방식은 반복되는 문자가 적은 경우 압축률이 낮다는 단점이 있습니다. 예를 들면, "abcabcdede"와 같은 문자열은 전혀 압축되지 않습니다. "어피치"는 이러한 단점을 해결하기 위해 문자열을 1개 이상의 단위로 잘라서 압축하여 더 짧은 문자열로 표현할 수 있는지 방법을 찾아보려고 합니다.

categories:
  - codingTest

tags:
  - Programmers
  - 2020 KAKAO
  - Python

date: 2020-06-27
last_modified_at: 2020-08-03
use_math: true
toc: true # Show table of contents
toc_sticky: true # Fixed table of contents
---

`Tag` `2020 KAKAO BLIND RECRUITMENT`<br>

**문제 설명**

데이터 처리 전문가가 되고 싶은 어피치는 문자열을 압축하는 방법에 대해 공부를 하고 있습니다. 최근에 대량의 데이터 처리를 위한 간단한 비손실 압축 방법에 대해 공부를 하고 있는데, 문자열에서 같은 값이 연속해서 나타나는 것을 그 문자의 개수와 반복되는 값으로 표현하여 더 짧은 문자열로 줄여서 표현하는 알고리즘을 공부하고 있습니다.
간단한 예로 "aabbaccc"의 경우 "2a2ba3c"(문자가 반복되지 않아 한번만 나타난 경우 1은 생략함)와 같이 표현할 수 있는데, 이러한 방식은 반복되는 문자가 적은 경우 압축률이 낮다는 단점이 있습니다. 예를 들면, "abcabcdede"와 같은 문자열은 전혀 압축되지 않습니다. "어피치"는 이러한 단점을 해결하기 위해 문자열을 1개 이상의 단위로 잘라서 압축하여 더 짧은 문자열로 표현할 수 있는지 방법을 찾아보려고 합니다.

예를 들어, "ababcdcdababcdcd"의 경우 문자를 1개 단위로 자르면 전혀 압축되지 않지만, 2개 단위로 잘라서 압축한다면 "2ab2cd2ab2cd"로 표현할 수 있습니다. 다른 방법으로 8개 단위로 잘라서 압축한다면 "2ababcdcd"로 표현할 수 있으며, 이때가 가장 짧게 압축하여 표현할 수 있는 방법입니다.

다른 예로, "abcabcdede"와 같은 경우, 문자를 2개 단위로 잘라서 압축하면 "abcabc2de"가 되지만, 3개 단위로 자른다면 "2abcdede"가 되어 3개 단위가 가장 짧은 압축 방법이 됩니다. 이때 3개 단위로 자르고 마지막에 남는 문자열은 그대로 붙여주면 됩니다.

압축할 문자열 s가 매개변수로 주어질 때, 위에 설명한 방법으로 1개 이상 단위로 문자열을 잘라 압축하여 표현한 문자열 중 가장 짧은 것의 길이를 return 하도록 solution 함수를 완성해주세요.

**제한사항**

- s의 길이는 1 이상 1,000 이하입니다.
- s는 알파벳 소문자로만 이루어져 있습니다.

**입출력 예**

s|	result
--|--
"aabbaccc"|	7
"ababcdcdababcdcd"|	9
"abcabcdede"|	8
"abcabcabcabcdededededede"	|14
"xababcdcdababcdcd"	|17

**입출력 예에 대한 설명**

**입출력 예 #1**

문자열을 1개 단위로 잘라 압축했을 때 가장 짧습니다.

**입출력 예 #2**

문자열을 8개 단위로 잘라 압축했을 때 가장 짧습니다.

**입출력 예 #3**

문자열을 3개 단위로 잘라 압축했을 때 가장 짧습니다.

**입출력 예 #4**

문자열을 2개 단위로 자르면 "abcabcabcabc6de" 가 됩니다.
문자열을 3개 단위로 자르면 "4abcdededededede" 가 됩니다.
문자열을 4개 단위로 자르면 "abcabcabcabc3dede" 가 됩니다.
문자열을 6개 단위로 자를 경우 "2abcabc2dedede"가 되며, 이때의 길이가 14로 가장 짧습니다.

**입출력 예 #5**

문자열은 제일 앞부터 정해진 길이만큼 잘라야 합니다.
따라서 주어진 문자열을 x / ababcdcd / ababcdcd 로 자르는 것은 불가능 합니다.
이 경우 어떻게 문자열을 잘라도 압축되지 않으므로 가장 짧은 길이는 17이 됩니다.

[프로그래머스에서 풀기](https://programmers.co.kr/learn/courses/30/lessons/60057)

## 코드
```python
def solution(s):

    slicing_window_size=1
    s_len=len(s)
    result=[]

    while s_len >=slicing_window_size:
        compressed_string = ''
        slicing_window_string=[s[idx:idx+slicing_window_size] for idx in range(0,s_len,slicing_window_size)]
        prev=slicing_window_string[0]
        count=1
        for idx in range(1,len(slicing_window_string)):
            if prev==slicing_window_string[idx]:
                count+=1
            else:
                if 1==count:
                    compressed_string+=prev
                else:
                    compressed_string+=str(count)+prev
                prev = slicing_window_string[idx]
                count = 1

        if 1 == count:
            compressed_string += prev
        else:
            compressed_string += str(count) + prev

        slicing_window_size+=1
        result.append(compressed_string)

    return min([len(s) for s in result])

```

## 설명
```python

while s_len >=slicing_window_size:
    compressed_string = ''
    slicing_window_string=[s[idx:idx+slicing_window_size] for idx in range(0,s_len,slicing_window_size)]
    prev=slicing_window_string[0]
    count=1
```
- ```slicing_window_size``` 가 주어진 문자열 ```s```와 길이가 같아질때까지 반복하며 모든 길이를 체크한다.
- ```slicing_window_string```은 주어진 문자열 ```s```를 ```slicing_window_size``` 만큼 일정한 길이로 자른 리스트이다.
- ```prev``` 변수를 통해 연속으로 문자열이 반복하는지 체크한다.
- 반복횟수를 ```count``` 를 통해 체크한다.

```python
for idx in range(1,len(slicing_window_string)):
    if prev==slicing_window_string[idx]:
        count+=1
    else:
        if 1==count:
            compressed_string+=prev
        else:
            compressed_string+=str(count)+prev
        prev = slicing_window_string[idx]
        count = 1

```
- 일정 길이로 잘린 ```slicing_window_string``` 를 반복하면서 ```prev```와 현재 문자열이 같은지 체크한다.
- 반복된 문자열이 있다면 ```count``` 를 늘리고, 그렇지 않을 경우에 한번만 반복된다면 문자열 그대로 붙이고, 이 외에는 반복횟수와 문자열을 같이 붙인다. 또한 ```prev```와 ```count``` 를 업데이트 및 초기화 한다.

```python
if 1 == count:
    compressed_string += prev
else:
    compressed_string += str(count) + prev

slicing_window_size+=1
result.append(compressed_string)
```
- 마지막 문자열 단위까지 살펴본후 마지막 결과에 대해서도 위의 과정과 동일하게 문자열을 이어 붙인뒤 ```slicing_window_size``` 와 ```result```를 업데이트 한다.

```python
return min([len(s) for s in result])
```
- 압축된 문자열 모든 경우에 대해서 길이를 체크하여 가장 작은 값을 반환한다.

## 또 다른 풀이

```python
def compress(text, tok_len):
    words = [text[i:i+tok_len] for i in range(0, len(text), tok_len)]
    res = []
    cur_word = words[0]
    cur_cnt = 1
    for a, b in zip(words, words[1:] + ['']):
        if a == b:
            cur_cnt += 1
        else:
            res.append([cur_word, cur_cnt])
            cur_word = b
            cur_cnt = 1
    return sum(len(word) + (len(str(cnt)) if cnt > 1 else 0) for word, cnt in res)

def solution(text):
    return min(compress(text, tok_len) for tok_len in list(range(1, int(len(text)/2) + 1)) + [len(text)])

```
- 반복된 문자열을 체크하기 위해서 ```zip()```을 활용할수도 있다.
