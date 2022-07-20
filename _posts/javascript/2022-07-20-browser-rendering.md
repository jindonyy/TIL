---
title: "브라우저 렌더링 과정"
layout: single
classes: wide
categories:
  - javascript
tags:
  - [browser rendering]
date: 2022-7-20
---

우리가 작성한 HTML, CSS, JavaScript를 브라우저가 어떻게 파싱하여 렌더링 하는지 알아보도록 하자.

## 브라우저 렌더링 과정

1. 브라우저는 HTML, CSS, JavaScript 등 렌더링에 필요한 **리소스를 서버에 요청**하고 **서버로부터 응답**을 받는다.
2. 서버로부터 응답된 HTML과 CSS를 브라우저의 렌더링 엔진이 파싱하여 DOM과 CSSOM을 생성하고, 이들을 결합하여 **렌더 트리**를 생성한다.
3. 브라우저의 자바스크립트 엔진은 서버로부터 응답된 자바스크립트를 파싱하여 AST를 생성하고, 바이트 코드로 변환하여 실행한다. 이 때 **자바스크립트는 DOM API를 통해 DOM이나 CSSOM을 변경**할 수 있다. 변경된 DOM과 CSSOM은 다시 렌더트리로 결합된다.
4. 렌더 트리를 기반으로 HTML 요소의 레이아웃(위치와 크기)을 계산하고, 브라우저 화면에 **HTML 요소를 페인팅**한다.

## 1. 브라우저의 요청과 서버의 응답

렌더링에 필요한 리소스는 모두 서버에 존재한다. 때문에 필요한 리소스를 먼저 서버에 요청해야 한다.  
서버에 요청하기 위해서 브라우저는 주소창을 제공한다. 브라우저의 주소창에 URL을 입력하고 엔터를 누르면 호스트 이름이 DNS를 통해 IP 주소로 변환된다. 그럼 이 IP 주소를 가진 서버에게 요청을 전송하게 되는 것이다.
<img src='{{ "/assets/images/2022-07-20-URL.png" | relative_url }}' style="width: 700px;" title="URL 설명" alt="URL 설명"/>  
주소창에 www.google.com을 입력한 후 엔터를 치면, google.com으로 루트 요청(protocol과 host만 있는 요청)이 가게 된다. 루트 요청은 암묵적으로 index.html을 응답하도록 기본 설정이 되어 있어 index.html이 응답으로 오게 된다.  
만약, 정적 파일을 서버에 요청하려면 www.google.com/data/data.json 과 같이 정적 파일의 경로(path)를 URI의 호스트 뒤에 입력해주면 된다.  
<br>
index.html을 요청하면 응답으로는 HTML만 올까?  
Network 탭을 확인해보면 HTML 외에도 CSS, JavaScript, 이미지, 폰트 등의 정적 파일이 온 것을 확인할 수 있다. 최초 응답으로는 HTML만 오지만, 브라우저의 렌더링 엔진이 HTML을 파싱하는 중에 외부 리소스를 로드하는 태그(link - CSS, img - 이미지, script - JavaScript 등)를 만나면 <u>HTML 파싱을 중단하고 태그들에 적힌 리소스들을 서버에 요청</u>한다.

## 2. HTML 파싱과 DOM 생성

URL을 통해 서버의 응답으로 온 HTML 문서는 문자열로만 이루어진 텍스트 파일이다.  
때문에 이 문자들을 파싱하여 브라우저가 렌더링할 수 있는 자료구조로 변환하여 메모리에 저장해야 한다.

> 💡 파싱(parsing) 이란?  
> 프로그래밍 언어의 문법에 맞게 작성된 텍스트 문서의 문자열을 토큰으로 분해하고, 토큰에 문법적 의미와 구조를 반영하여 **파스 트리를 생성**하는 일련의 과정이

아래의 그림은 브라우저가 HTML을 파싱하여 브라우저가 이해할 수 있는 자료구조인 DOM을 생성하는 과정이다.
<img src='https://velog.velcdn.com/images%2Fdev_jazziron%2Fpost%2Fdceb8a33-ee17-456b-b5fb-738e51c4ece6%2Fimage.png' title="HTML 파싱과 DOM 생성" alt="HTML 파싱과 DOM 생성"/>
<small>이미지 출처 | https://poiemaweb.com/js-dom</small>

1. 브라우저는 서버가 응답한 HTML 문서를 바이트 형태로 응답받는다. 그리고 이 바이트 형태의 HTML 문서는 meta 태그의 charset 속성에 지정된 인코딩 방식(ex: UTF-8)을 기준으로 문자열로 변환된다.  
   (meta 태그에 지정된 인코딩 방식은 content-type: text/html; charset=utf-8과 같이 응답 헤더에 담겨온다. 브라우저는 이를 확인하고 문자열로 변환한다.)
2. 문자열로 변환된 HTML 문서를 읽어 최소 단위인 토큰들로 분해한다.
   > 💡 토큰(token) 이란?  
   > 문법적 의미를 가지며, 문법적으로 더 나눌 수 없는 코드의 기본 요소를 의미
3. HTML 문서는 HTML 요소들로 이루어지며, 이 요소들은 중첩 관계를 갖는다. 즉, HTML 요소의 콘텐츠 영역(시작 태그에서 종료 태그 사이)에는 텍스트 뿐만 아니라 다른 HTML 요소도 포함될 수 있다. 이 중첩 관계에 의해 부자 관계가 형성되어 토큰에 저장된다.
4. 각 토큰들은 객체로 변환하여 [노드(Node)](https://velog.io/@keinn51/HTML%EC%97%90%EC%84%9C-%EB%85%B8%EB%93%9C%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80)들을 생성한다. 토큰의 내용에 따라 문서 노드, 요소 노드, 어트리뷰트 노드, 텍스트 노드가 생성된다. (이 노드들은 DOM을 구성하는 기본 요소이다.)
5. 생성된 노드들의 부자 관계를 반영하여 모든 노드들을 트리 자료 구조로 구성한다. 이 트리 자료 구조를 DOM(Document Object Model)이라 부른다.

## 3. CSS 파싱가 CSSOM 생성

<s>발치한 곳이 아푸다.. 내일 하자 @_@....</s>
