---
title: "문자열 추가하기(padStart, padEnd)"
layout: single
classes: wide
categories:
  - javascript
tags:
  - [js string, string, padStart, padEnd]
date: 2021-10-29
---

## padStart 
* 현재 문자열의 시작(왼쪽)부터 원하는 문자열(padString)로 추가해, 총 길이가 지정한 길이(targetLength)만큼되는 새로운 문자열을 반환한다.
* 문법: str.padStart(targetLength [, padString])
  * targetLength가 str의 문자열 길이보다 작을 경우 그대로 반환한다.
  * padString의 길이가 targetLength보다 길면 총 길이에 맞게 padString의 앞일부분만 추가된다. 지정하지 않을 경우는 공백(" ")으로 채워진다.
* **IE에서 작동하지 않는다.**

```javascript
"abc".padStart(10, "ABC");  // 'ABCABCAabc'
"abc".padStart(6, "1");     // '111abc'
"abc".padStart(6,"123465"); // '123abc'
"abc".padStart(10);         // '       abc'
"abc".padStart(1);          // 'abc'
```

* 폴리필  
다른 모든 코드 이전에 아래 코드를 포함하면 지원하지 않는 플랫폼에서도 String.prototype.padStart() 메서드를 사용할 수 있다.

```javascript
if (!String.prototype.padStart) {
    String.prototype.padStart = function padStart(targetLength,padString) {
        targetLength = targetLength>>0; //truncate if number or convert non-number to 0;
        padString = String((typeof padString !== 'undefined' ? padString : ' '));
        if (this.length > targetLength) {
            return String(this);
        }
        else {
            targetLength = targetLength-this.length;
            if (targetLength > padString.length) {
                padString += padString.repeat(targetLength/padString.length); //append to original to ensure we are longer than needed
            }
            return padString.slice(0,targetLength) + String(this);
        }
    };
}
```

## padEnd 
* 현재 문자열의 끝(오른쪽)부터 원하는 문자열(padString)로 추가해, 총 길이가 지정한 길이(targetLength)만큼되는 새로운 문자열을 반환한다.
* 문법: str.padEnd(targetLength [, padString])
  * targetLength가 str의 문자열 길이보다 작을 경우 그대로 반환한다.
  * padString의 길이가 targetLength보다 길면 총 길이에 맞게 padString의 앞일부분만 추가된다. 지정하지 않을 경우는 공백(" ")으로 채워진다.
* **IE에서 작동하지 않는다.**

```javascript
"abc".padEnd(10, "ABC");  // 'abcABCABCA'
"abc".padEnd(6, "1");     // 'abc111'
"abc".padEnd(6,"123465"); // 'abc123'
"abc".padEnd(10);         // 'abc       '
"abc".padEnd(1);          // 'abc'
```

* 폴리필  
다른 모든 코드 이전에 아래 코드를 포함하면 지원하지 않는 플랫폼에서도 String.prototype.padStart() 메서드를 사용할 수 있다.

```javascript
if (!String.prototype.padEnd) {
    String.prototype.padEnd = function padEnd(targetLength,padString) {
        targetLength = targetLength>>0; //floor if number or convert non-number to 0;
        padString = String((typeof padString !== 'undefined' ? padString : ' '));
        if (this.length > targetLength) {
            return String(this);
        }
        else {
            targetLength = targetLength-this.length;
            if (targetLength > padString.length) {
                padString += padString.repeat(targetLength/padString.length); //append to original to ensure we are longer than needed
            }
            return String(this) + padString.slice(0,targetLength);
        }
    };
}
```