---
title: "<span>프로그래머스</span><span>Lv1</span> 소수 찾기"
header:
  teaser: /assets/images/algorithm/programmers_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, programers, Level1]
date: 2021-10-25
---

## 문제 설명
1부터 입력받은 숫자 n 사이에 있는 소수의 개수를 반환하는 함수, solution을 만들어 보세요.  
소수는 1과 자기 자신으로만 나누어지는 수를 의미합니다.  
(1은 소수가 아닙니다.)

### 제한 조건
* n은 2이상 1000000이하의 자연수입니다.

### 입출력 예

|n|result|
|-|-|-|
|10|4|
|5|3|

### 입출력 예 설명
입출력 예 #1  
1부터 10 사이의 소수는 [2,3,5,7] 4개가 존재하므로 4를 반환  
  
입출력 예 #2  
1부터 5 사이의 소수는 [2,3,5] 3개가 존재하므로 3를 반환

## 답안
#### 나의 풀이
```javascript
var answer = [2];

function solution(n) {
    if(n == 2) return 1;
    for(var i = 3; i <= n; i+=2) {
        for(var j = 3; j <= i; j+=2) {
            if(j == i) {
                answer.push(i);
            } else if (i % j == 0) break;
        }
    }
    
    return answer.length;
}
```
테스트 11 시간 초과ㅠㅠ

```javascript
function solution(n) {
    var answer = [2];
    
    for(var i = 3; i <= n; i+=2) answer.push(i);
    
    for(var i = 1; i < answer.length; i++) {
        for(var j = i+1; j < answer.length; j++) {
            if(answer[j] % answer[i] == 0) {
                answer.splice(j, 1);
                j--;
            }
        } 
    }
    
    return answer.length;
}
```
빨라졌지만 여전히 테스트 11 시간 초과..

```javascript

```

#### 옛날 풀이
```javascript
function solution(n) {
    var answer = [2];

    for(var i = 3; i <= n; i+=2){
        var primeNumber = true;

        if(answer.indexOf(i) == -1){
            for(var j = 3; j < i; j+=2){
                if(i % j === 0){
                    primeNumber = false;
                }
            }
        }

        if(primeNumber){
            answer.push(i);
        }
    }

    return answer.length;
}
```
통과X

#### 다른 사람 풀이
```javascript
function getDayName(a,b){
    var date = new Date(2016, (a - 1), b);
    return date.toString().slice(0, 3).toUpperCase();
}
```
백틱 안쓰고 저렇게 쓸 수도 있구나..  
Date도 정리를 좀 해놔야겠다.
