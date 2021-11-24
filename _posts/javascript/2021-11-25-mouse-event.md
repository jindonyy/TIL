---
title: "Mouse Event"
layout: single
classes: wide
categories:
  - javascript
tags:
  - [js mouse event, mouse event, event]
date: 2021-11-25
---

마우스 이벤트는 특정 지점을 가리키는 장치를 통해 발생하는 이벤트를 의미한다.  
마우스 이벤트라고 부르지만 '마우스'라는 장치를 통해서만 생기는 것이 아니라 핸드폰이나 태블릿 같은 다른 장치에서도 생긴다.  
주의할 점은 pc와 모바일 기기에서 발생하는 마우스 이벤트가 다르다는 것을 생각해보고 사용해야 한다.

## 마우스 이벤트의 종류
* click  
마우스 왼쪽 버튼을 사용해 해당 요소 위에서 mousedown 이벤트와 mouseup 이벤트를 연달아 발생시킬 때 실행된다.

* dbclick  
해당 요소 위에서 마우스 왼쪽 버튼을 빠르게 클릭할 때 발생한다.

* contextmenu  
마우스 오른쪽 버튼을 눌렀을 때 발생한다. 참고로 특별한 단축키를 눌러도 마우스 오른쪽 버튼을 눌렀을 때처럼 컨텍스트 메뉴가 나타나게 할 수는 있지만 contextmenu라는 마우스 이벤트와 동일하진 않다.

* mousemove  
마우스를 움직일 때 발생한다.

* mousedown  
요소 위에서 마우스 왼쪽 버튼을 누를 때 발생한다.

* mouseup  
요소 위에서 마우스 왼쪽 버튼 누르고 있다가 뗄 때 발생한다.

* mouseover  
마우스 커서가 요소 바깥에 있다가 요소 안으로 움직일 때 발생한다.

* mouseout  
마우스 커서가 요소 위에 있다가 요소 밖으로 움직일 때 발생한다.

* mouseenter  
마우스 커서가 요소 바깥에 있다가 요소 안으로 움직일 때 발생한다.
mouseover와 달리 버블링이 발생하지 않는다.

* mouseleave  
마우스 커서가 요소 위에 있다가 요소 밖으로 움직일 때 발생한다.
mouseleave와 달리 버블링이 발생하지 않는다.

## 마우스 이벤트 동작 과정
위의 이벤트들이 꼭 하나만 생기는 것은 아니다.  
단순하게 마우스 왼쪽 버튼을 클릭하더라도 클릭을 위해선 mousedown과 mouseup이 발생할 수 밖에 없다.  
mousedown과 mouseup, click 각각 이벤트를 등록했다면 사용자의 클릭한번에 3가지 이벤트가 발생하게 되는 것이다.

## 마우스 버튼
클릭과 연관된 이벤트는 정확히 어떤 버튼에서 이벤트가 발생했는지를 알려주는 button 프로퍼티를 지원한다.  
click 이벤트와 contextmenu 이벤트는 마우스에서 누른 버튼에 따라 발생하기 때문에 보통 button 프로퍼티를 사용하지 않는다.  
반면, mousedown이벤트나 mouseup 이벤트는 해당 이벤트의 핸들러에 event.button을 명시해 줘야 할 때가 있다. 이 이벤트들은 마우스 버튼 어디에서나 발생할 수 있는데 button 프로퍼티를 사용해야 정확히 어떤 버튼에서 이벤트가 발생했는지 알 수 있기 때문이다.

* 문법: `event.button`
* 반환되는 값
  * 0 : 메인 버튼 눌림, 일반적으로 왼쪽 버튼 또는 초기화되지 않은 상태
  * 1 : 보조 버튼 눌림, 일반적으로 휠 버튼 또는 중간 버튼(있는 경우)
  * 2 : 보조 버튼 눌림, 일반적으로 오른쪽 버튼
  * 3 : 네 번째 버튼, 일반적으로 브라우저 뒤로 버튼
  * 4 : 다섯 번째 버튼, 일반적으로 브라우저 앞으로 버튼

```javascript
const button = document.querySelector('#button');
const log = document.querySelector('#log');

function logMouseButton(e) {
  if (typeof e === 'object') {
    switch (e.button) {
      case 0:
        log.textContent = 'Left button clicked.';
        break;
      case 1:
        log.textContent = 'Middle button clicked.';
        break;
      case 2:
        log.textContent = 'Right button clicked.';
        break;
      default:
        log.textContent = `Unknown button code: ${e.button}`;
    }
  }
}

button.addEventListener('mouseup', logMouseButton);
```