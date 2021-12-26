---
title: "<span>프로그래머스</span><span>Lv1</span> 두 개 뽑아서 더하기"
header:
  teaser: /assets/images/algorithm/programmers_teaser.png
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, programers, Level1]
date: 2021-10-24
---

## 문제 설명
정수 배열 numbers가 주어집니다. numbers에서 서로 다른 인덱스에 있는 두 개의 수를 뽑아 더해서 만들 수 있는 모든 수를 배열에 오름차순으로 담아 return 하도록 solution 함수를 완성해주세요.

### 제한 사항
* numbers의 길이는 2 이상 100 이하입니다.
  * numbers의 모든 수는 0 이상 100 이하입니다.

### 입출력 예

|numbers|result|
|-|-|
|[2,1,3,4,1]|[2,3,4,5,6,7]|
|[5,0,2,7]|[2,5,7,9,12]|

### 입출력 예 설명
입출력 예 #1
* 2 = 1 + 1 입니다. (1이 numbers에 두 개 있습니다.)
* 3 = 2 + 1 입니다.
* 4 = 1 + 3 입니다.
* 5 = 1 + 4 = 2 + 3 입니다.
* 6 = 2 + 4 입니다.
* 7 = 3 + 4 입니다.
* 따라서 [2,3,4,5,6,7] 을 return 해야 합니다.  
  
입출력 예 #2
* 2 = 0 + 2 입니다.
* 5 = 5 + 0 입니다.
* 7 = 0 + 7 = 5 + 2 입니다.
* 9 = 2 + 7 입니다.
* 12 = 5 + 7 입니다.
* 따라서 [2,5,7,9,12] 를 return 해야 합니다.

## 답안
#### 나의 풀이
```javascript
function solution(numbers) {
    var answer = [];
    
    for(var i = 0; i < numbers.length; i++) {
        for(var j = 1; j < numbers.length; j++) {
            answer.push(numbers[i] + numbers[j]);
        }
        numbers.shift();
        i--;
    }
    
    return answer.filter((el, index) => answer.indexOf(el) == index).sort((a, b) => a - b);
}
```
shift 해주고 i-- 하는 것보다 옛날에 풀었던 방식처럼 안쪽 for문에 j = i+1 로 하는게 더 나은 것 같다ㅠㅠ

#### 옛날 풀이
```javascript
function solution(numbers) {
    let answer = [];

    for(let i = 0; i < numbers.length-1; i++){
        for(let j = i+1; j < numbers.length; j++){
            answer.push(numbers[i] + numbers[j]);
        }
    }
    
    answer = answer.filter((item, index) => answer.indexOf(item) === index);
    
    return answer.sort((a,b) => a-b);
}
```

#### 다른 사람 풀이
```javascript
function solution(numbers) {
    const temp = []

    for (let i = 0; i < numbers.length; i++) {
        for (let j = i + 1; j < numbers.length; j++) {
            temp.push(numbers[i] + numbers[j])
        }
    }

    const answer = [...new Set(temp)]

    return answer.sort((a, b) => a - b)
}
```
Set으로 중복 제거

```javascript
function solution(numbers) {
    var answer = [];
    numbers = numbers.sort();
    console.log(numbers);
    for(var i = 0; i < numbers.length; i++){
        for(var k = i+1; k < numbers.length; k++){
            if(!answer.includes(numbers[i]+numbers[k])){
                answer.push(numbers[i]+numbers[k]);
            }
        }
    }
    answer = answer.sort(function(a, b){
        return a-b;
    });
    return answer;
}
```
push하기 전에 if문으로 이미 배열에 있는지 체크하였다. 더 효율적인 듯
