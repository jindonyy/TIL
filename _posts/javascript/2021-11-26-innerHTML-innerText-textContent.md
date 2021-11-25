---
title: "innerHTML, innerText, textContent의 차이점"
layout: single
classes: wide
categories:
  - javascript
tags:
  - [innerHTML, innerText, textContent]
date: 2021-11-26
---

```html
<div id='content'>
  안녕하세요?     만나서 반가워요.
  <span style='display:none'>숨겨진 텍스트</span>
</div>
```

## innerHTML
innerHTML은 'Element'의 속성으로, 해당 Element의 HTML, XML을 읽어오거나, 설정할 수 있다.  
선택 요소 안의 tag와 text, style 요소 등을 string으로 모두 출력해준다.  
간단히 html 파일에서 작성한 것을 그대로 출력해준다고 생각하면 된다.
```javascript
console.log(document.querySelector('#content').innerHTML);
/*

안녕하세요?     만나서 반가워요.
<span style='display:none'>숨겨진 텍스트</span>
*/
```
content 안에 있는 HTML 전체 내용을 가져오는 것을 확인 할 수 있다.

## innerText
innerText도 'Element'의 속성으로, 해당 Element 내에서 사용자에게 '보여지는' 텍스트 값을 읽어온다.  
그러나 문자열에서 연속되는 공백이나 앞 뒤의 공백이 있다면 제거하고 그 값을 반환한다.
```javascript
console.log(document.querySelector('#content').innerText);
/*
안녕하세요? 만나서 반가워요.
*/
```
연속된 공백이 1개로 되어 출력되며, 숨겨져 있는 요소의 텍스트는 출력하지 않는다.

## textContent
textContent는 'Node'의 속성으로, innetText와는 달리 &lt;script&gt;나 &lt;style&gt; 태그와 상관없이 해상 노드가 가지고 있는 텍스트 값을 그대로 읽는다.  
textContent가 innerText보다 더 먼저 만들어졌으며, 더 빨리 사용되었습니다. 그런 이유로 브라우저 호환성도 좀 더 높습니다.
```javascript
console.log(document.querySelector('#content').textContent);
/*
안녕하세요?     만나서 반가워요.
숨겨진 텍스트
*/
```
연속된 공백이 그대로 출력되며, 'display:none' 스타일이 적용된 '숨겨진 텍스트' 문자열도 그대로 출력된다.

## 주의
실제로 여러 브라우저에서 테스트를 해보면 그 결과가 많이 달라진다. IE의 경우는 위와 같이 나타나지만 현재의 크롬 버전에서는 둘 다 동일하게 결과가 나타난다.