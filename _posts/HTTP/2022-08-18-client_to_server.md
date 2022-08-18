---
title: "HTTP 메서드를 활용하여 클라이언트에서 서버로 데이터 전송"
header:
  teaser: /assets/images/http/http_teaser.jpg
layout: single
classes: wide
categories:
  - HTTP
tags:
  - [HTTP, Client to Server]
date: 2022-8-18
---

> ⚠️ 김영한님의 '모든 개발자를 위한 HTTP 웹 기본 지식' 강의와 추가 학습을 토대로, 정리한 내용입니다.

## GET

- 쿼리 파라미터를 통한 데이터 전송
- 주로 정렬 필터(검색어)

## POST, PUT, PATCH

- 메세지 바디를 통한 데이터 전송
- 회원 가입, 상품 주문, 리소스 등록, 리소스 변경

## 정적 데이터 조회

- 이미지, 정적 텍스트 문서
- 조회는 GET을 사용
- 정적 데이터는 일반적으로 쿼리 파라미터 없이 리소스 경로로 단순하게 조회가 가능

## 동적 데이터 조회

- 주로 검색, 게시판 목록에서 조회 조건을 줄여주는 필터, 조회 결과를 정렬하는 정렬 조건에 주로 사용
- 조회는 GET을 사용
- 쿼리 파라미터를 보내면 쿼리를 기반으로 정렬 또는 필터해서 결과를 동적으로 생성하여 전달

## HTML Form을 통한 데이터 전송

- html에 name을 반드시 지정해야 한다. 그래야 name을 key로 form 태그의 value를 value로 사용하여 전송되기 때문이다.
- HTML Form 전송은 GET, POST만 지원한다.

### [POST](https://developer.mozilla.org/ko/docs/Web/HTTP/Methods/POST)로 전송할 경우

- 회원 가입, 상품 주문, 데이터 변경
- form으로 submit 하여 데이터를 전송할 경우 어떤 데이터를 전송하냐에 따라 웹브라우저가 [Content-Type](https://jw910911.tistory.com/117)을 다르게 지정한다.
- [application/x-www-form-urlencoded](https://blog.naver.com/PostView.naver?blogId=writer0713&logNo=221853596497&redirect=Dlog&widgetTypeCall=true&directAccess=false) 타입
  - urlencoded를 적어주는 이유는 영어가 아닌 문자가 들어올 경우 percent encoded를 통해 변경해주기 위해서이다.
    - ex) abc김 → abc%EA%B9%80
  - 최근에는 RestFul API를 사용하며 json을 많이 사용하게 됨에 따라 해당 타입을 잘 사용하지 않는다. 그러나 form 전송의 default 값이기 때문에 여전히 사용하는 서버가 있다.

  ```html
  // HTML
  <form action="/save" method="post"> // post이므로 저장 action으로
    <input type="text" name="username" />
    <input type="text" name="age" />
    <button type="submit">전송</button>
  </form>

  // 웹브라우저가 생성한 요청 HTTP 메세지
  POST /save HTTP/1.1
  Host: localhost:8080
  Content-Type: application/x-www-form-urlencoded

  username=kim&age=20 // body를 통해 전달
  ```

- multipart/form-data 타입
  - 영어 텍스트 뿐만 아니라 파일 업로드 같은 바이너리 데이터 전송 시 enctype으로 해당 타입을 지정해주야 한다.
  - 영어가 아닌 문자를 사용해주고 싶을 경우에도 사용한다.
    - 이 경우 [accept-charset](https://mieumje.tistory.com/54)을 추가로 지정하여 server와 인코딩 방식을 맞춰야 한다.
  - boundary=----XXX 가 지정되는 이유는 -—-XXX를 경계로 데이터를 구분하기 때문이다.

  ```html
  // HTML
  <form action="/save" method="post" enctype="multipart/form-data" accept-charset="UTF-8"> // enctype을 지정해주어야 한다.
    <input type="text" name="username" />
    <input type="text" name="age" />
    <input type="file" name="file1" />
    <button type="submit">전송</button>
  </form>

  // 웹브라우저가 생성한 요청 HTTP 메세지
  POST /save HTTP/1.1
  Host: localhost:8080
  Content-Type: multipart/form-data; boundary=----XXX
  Content-Length: 10457
  
  ------XXX
  Content-Dispositon: form-data; name="username"
  
  kim
  ------XXX
  Content-Dispositon: form-data; name="age"
  
  20
  ------XXX
  Content-Dispositon: form-data; name="file1"; filtename="intro.png"
  Content-Type: image/png
  
  109238a9o0p3eqwokjasd09ou3oirjwoe9u34ouief... // 이미지에 대한 바이트 정보
  ------XXX--
  ```

### GET으로 조회할 경우

```html
// HTML
<form action="/members" method="get"> // get이므로 조회 action으로
  <input type="text" name="username" />
  <input type="text" name="age" />
  <button type="submit">조회</button>
</form>

// 웹브라우저가 생성한 요청 HTTP 메세지
GET /members?username=kim&age=20 HTTP/1.1 // header를 통해 전달
Host: localhost:8080
```

## HTTP API를 통한 데이터 전송

- 회원 가입, 상품 주문, 데이터 변경
- 서버 to 서버
  - 백엔드끼리 통신할 때
- 앱 클라이언트
  - 아이폰, 안드로이드에서 전송할 때도 자주 사용
- 웹 클라이언트
  - HTML에서 Form 전송 대신 자바스크립트를 통한 통신에 사용 (Ajax)
  - React, VueJS 같은 웹 클라이언트 API 통신
- POST, PUT, PATCH: 메세지 바디를 통해 데이터 전송
- GET: 조회, 쿼리 파라미터로 데이터 전달
- Content-Type: application/json 을 주로 사용 (사실상 표준)
  - TEXT, XML, JSON 등등이 있으나 XML이 읽기 어렵고 열고 닫는 등의 사용이 복잡한 반면, JSON은 사용이 간편하고 데이터 크기도 상대적으로 작으므로 현재는 거의 JSON만 사용하는 추세이다.

```html
POST /members HTTP/1.1
Content-Type: application/json { "username": "kim" "age": 20 }
```

## Reference

- [모든 개발자를 위한 HTTP 웹 기본 지식 - 김영한](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC)
- [MDN POST](https://developer.mozilla.org/ko/docs/Web/HTTP/Methods/POST)
- [HTTP: Content-Type 에 대해 알아보자](https://jw910911.tistory.com/117)
- [Post 요청과 Content-Type의 관계](https://blog.naver.com/PostView.naver?blogId=writer0713&logNo=221853596497&redirect=Dlog&widgetTypeCall=true&directAccess=false)
- [multipart/form-data 한글 깨짐](https://mieumje.tistory.com/54)
