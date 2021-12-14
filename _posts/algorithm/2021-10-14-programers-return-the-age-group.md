---
title: "<span>프로그래머스</span><span>Lv1</span> 연령대 반환"
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, programers, Level1]
date: 2021-10-14
---

## 문제 설명
나이를 숫자로 입력받고, 10년 단위로 구분된 연령대를 반환하는 함수를 구현해주세요.

### 입력 형식
printAgeGroup의 첫 번째 인자로 나이 그룹을 출력할 연령이 주어집니다.  
연령 age는 number 타입으로 주어지며, 0 이상 120 이하의 정수라고 가정합니다. (0 <= age <= 120)  
* printAgeGroup 함수의 이름을 변경하지 마세요.

### 출력 형식
10년 단위로 구분된 연령대를 문자열로 반환해주세요.  
단, 연령이 10세 미만인 경우, '10대 미만'을 반환해주세요.  
연령이 90세 이상인 경우, '90대 이상'을 반환해주세요.

## 답안
#### 나의 풀이
```javascript
function printAgeGroup(age) {
  return answer < 10 ? "10대 미만" : age >= 90 ? "90대 이상" : (age+"")[0] + "0대";
}
```
이중 삼항 연산자를 사용하였다.

#### 다른사람 풀이
```javascript
function printAgeGroup(age) {
  if(typeof age !== "number" || age < 0 || age > 120 || !Number.isInteger(age)){
    return "Error";
  }

  let num = Math.floor(age/10)*10;
  let answer;

  if (num < 10){
    answer = '10대 미만';
  } else if(num >= 90){
    answer = '90대 이상';
  } else{
    answer = num + '대';
  }

  return answer;
}
```
좋았던 점
1. 입력형식의 가정 상황까지 고려하여 if절을 사용하였다.
2. Math.floor를 이용하여 10의 자리로 내림하여 사용하였다.