---
title: "<span>프로그래머스</span><span>Lv1</span> 자릿수 더하기"
header:
  teaser: /assets/images/algorithm/programmers_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, programers, Level1]
date: 2021-10-15
---

## 문제 설명
자연수 N이 주어지면, N의 각 자릿수의 합을 구해서 return 하는 solution 함수를 만들어 주세요.
예를들어 N = 123이면 1 + 2 + 3 = 6을 return 하면 됩니다.

### 제한 조건
* N의 범위 : 100,000,000 이하의 자연수

### 입출력 예

|N|answer|
|-|-|
|123|6|
|987|24|

### 입출력 예 설명
#### 입출력 예 #1
문제의 예시와 같습니다.

#### 입출력 예 #2
9 + 8 + 7 = 24이므로 24를 return 하면 됩니다.

## 답안
#### 나의 풀이
```javascript
function solution(n){
	return (n+"").split("").reduce((acc, cur) => acc += (cur*1), 0);
}
```
1. +"" 을 통해 문자열로 바꾸어 준다.
2. split으로 배열로 바꾸어 준다.
3. 문자열인 숫자이므로 *1로 숫자로 바꾸어주면서 reduce를 이용해 더한다.

```javascript
function solution(n){
	var answer = 0;
	var str = n+"";
	
	for(var i = 0; i < str.length; i++) {
		answer += str[i]*1;
	}

	return answer;
}
```
1. +"" 을 통해 문자열로 바꾸어 준다.
2. 문자열인 숫자이므로 *1로 숫자로 바꾸어주면서 for문을 돌려 더한다.  
(for문으로 할 경우 배열이 아니여도 되므로 []를 통해 더할수 있다.)

#### 옛날 풀이
```javascript
function solution(n){
	var answer = 0;
	for(var i = 0; i < String(n).length; i++){
		answer += Number(String(n)[i]);
	}

	return answer;
}
```