---
title: "HTTP 메세지"
header:
  teaser: /assets/images/http/http_teaser.jpg
layout: single
classes: wide
categories:
  - HTTP
tags:
  - [HTTP, HTTP message]
date: 2022-7-25
---

> ⚠️ 김영한님의 '모든 개발자를 위한 HTTP 웹 기본 지식' 강의와 추가 학습을 토대로, 정리한 내용입니다.

## HTTP 메시지 구조

  <img src='{{ "/assets/images/http/2022-07-26-http-message_1.png" | relative_url }}' width="700" alt="http 설명"/>

## 시작 라인 (start-line)

request-line / status-line 두 가지가 있다.

### 요청 메세지

> request-line = method (공백) request-target (공백) HTTP-version (엔터)

<pre class="white-box" style="padding-bottom: 0;">
<strong style="padding: 2px 5px;background: #ededed;">GET /search?q=hello&hl=ko HTTP/1.1</strong>
Host: www.google.com

</pre>

1. HTTP method
   - ex) GET
   - 서버가 수행해야 할 동작 지정
   - 종류: GET, POST, PUT, DELETE..
2. 요청 대상
   - ex) /search?q=hello&hl=ko
   - absolute-path[?query] (절대경로[?쿼리])
   - 절대경로= "/" 로 시작하는 경로
   - 참고: http://...?x=y 와 같이 다른 유형의 경로지정 방법도 있다.
3. HTTP 버전
   - ex) HTTP/1.1
   - HTTP version
   - 종류: …, HTTP/1.1, HTTP/2, HTTP/3

### 응답 메세지

> status-line = HTTP-version (공백) status-code (공백) reason-phrase (엔터)

<pre class="white-box" style="padding-bottom: 0;">
<strong style="padding: 2px 5px;background: #ededed;">HTTP/1.1 200 OK</strong>
Content-Type: text/html;charset=UTF-8
Content=Length: 3423

<<span></span>html>
  <<span></span>body>…</<span></span>body>
</<span></span>html>

</pre>

1. HTTP 버전
   - ex) HTTP/1.1
2. HTTP 상태 코드
   - ex) 200
   - 요청 성공, 실패를 나타낸다.
   - 종류: 200(성공), 4XX(클라이언트 요청 오류), 5XX(서버 내부 오류)
3. 이유 문구: 사람이 이해할 수 있는 짧은 상태 코드 설명 글
   - ex) OK

## 헤더 (header)

- header-field = field-name ":" OWS field-value OWS (OWS:띄어쓰기 허용)
- field-name은 대소문자 구문 상관 없다.
  - Content-Type이나 content-type이나 같다.
  - 그러나 : 뒤의 value는 당연히 대소문자 구분해주어야 한다.
- body에 들어갈 내용 빼고, HTTP 전송에 필요한 <strong>모든 부가정보</strong>가 다 들어간다.
  - ex) 메시지 body의 내용 설명, 메시지 body의 크기, 압축, 인증, 요청 클라이언트(브라우저) 정보, 서버 애플리케이션 정보, 캐시 관리 정보...
- 표준 헤더가 매우 많다.
  - https://en.wikipedia.org/wiki/List_of_HTTP_header_fields
- 필요 시 임의의 헤더를 추가할 수 있다.

### 요청 메세지

<pre class="white-box" style="padding-bottom: 0;">
GET /search?q=hello&hl=ko HTTP/1.1
<strong style="padding: 2px 5px;background: #ededed;">Host: www.google.com</strong>

</pre>

### 응답 메세지

<pre class="white-box" style="padding-bottom: 0;">
HTTP/1.1 200 OK
<strong style="padding: 2px 5px;background: #ededed;">Content-Type: text/html;charset=UTF-8
Content=Length: 3423</strong>

<html>
  <body>…</body>
</html>

</pre>

## 바디 (body)

- 실제 전송할 데이터
- HTML 문서, 이미지, 영상, JSON 등등 byte로 표현할 수 있는 모든 데이터들을 전송 가능하다.
