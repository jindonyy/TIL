---
title: "<span>프로그래머스</span><span>Lv1</span> 2016년"
layout: single
classes: wide
categories:
  - algorithm
tags:
  - [javascript, algorithm, programers, Level1]
date: 2021-10-24
---

## 문제 설명
2016년 1월 1일은 금요일입니다. 2016년 a월 b일은 무슨 요일일까요? 두 수 a ,b를 입력받아 2016년 a월 b일이 무슨 요일인지 리턴하는 함수, solution을 완성하세요. 요일의 이름은 일요일부터 토요일까지 각각 `SUN,MON,TUE,WED,THU,FRI,SAT`
입니다. 예를 들어 a=5, b=24라면 5월 24일은 화요일이므로 문자열 "TUE"를 반환하세요.

### 제한 조건
* 2016년은 윤년입니다.
* 2016년 a월 b일은 실제로 있는 날입니다. (13월 26일이나 2월 45일같은 날짜는 주어지지 않습니다)

### 입출력 예

|a|b|result|
|-|-|-|
|5|24|"TUE"|

## 답안
#### 나의 풀이
```javascript
function solution(a, b) {
    var date = [31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31];
	var day = ["FRI", "SAT", "SUN", "MON", "TUE", "WED", "THU"];
    var sumDate = b;
    
    for(var i = 0; i < a-1; i++) {
        sumDate += date[i];
    }
    
    return day[(sumDate-1) % 7];
}
```

```javascript
function solution(a, b) {
    return String(new Date(`${a} ${b}, 2016`)).slice(0, 3).toUpperCase();
}
```
new Date도 사용해보았다.  
역시 노가다가 아니라 간편하긴 하나 느리다. (그리고 백틱은 IE 지원이 되지 않는다.)  
둘 다 짜보는게 알고리즘 공부와 메서드 공부 둘 다 될 듯 하다.


#### 옛날 풀이
```javascript
function solution(a, b) {
    var answer = '';
    var month = [31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31];
    var week = ['FRI','SAT','SUN','MON','TUE','WED','THU'];
    var sum = 0;
    
    for( var i = 1; i < a; i++ ){
        sum += month[i-1];
    }
    
    answer = week[(sum+b-1)%7];
    
    return answer;
}
```

#### 다른 사람 풀이
```javascript
function getDayName(a,b){
    var date = new Date(2016, (a - 1), b);
    return date.toString().slice(0, 3).toUpperCase();
}
```
백틱 안쓰고 저렇게 쓸 수도 있구나..  
Date도 정리를 좀 해놔야겠다.
