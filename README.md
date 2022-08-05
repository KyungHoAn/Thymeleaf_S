## Thymeleaf 문법
1. th: text
- 태그 안의 텍스트를 서버에서 전달 받은 값에 따라 표현하고자 할 때 사용
- <span th:text="${hello}">message</span> => 해당 경우 서버에서 hello 라는 변수가 있을 경우 message의 자리를 변수값으로 대체하게 된다.

2. th:utext
- 변수에서 받은 값에서 html 태그가 있다면 태크값을 반영해서 표시해준다.
- 서버에서 받은 hello값이 <p>Hello World</p>일 때
### th:text의 경우
- [Thymeleaf 탬플릿 내의 코드]
- <span td:text="${hello}">message</span>
- 실제 웹브라우저에 표시되는 내용
- <p>Hello World!</p> => 태크값을 인식하지 않고 그대로 텍스트로 인식해서 출력한다.
### th:utext의 경우
- [Thymeleaf 템플릿 내의 코드]
- <span th:utext="${hello}">message</span>
- 실제 웹 브라우저에 표시되는 내용
- Hello world! => 태그에서 지정한 대로 값이 표시된다.

3. th:value
엘리먼트들의 value값을 지정할 수 있다.

3.1사용 예시
<button th:value=”${hello}”/>
(이런식으로 value값을 서버 값에따라 바꿔줄 수 있다.)

4. th:with
변수 값을 지정해서 사용할 수 있다.
 
4.1 사용 예시
<div th:with=”temp=${hello}” th:text=”${temp}”>
5. th:switch
Switch-case문이 필요할 때 사용한다.
 
th:case에서 case문을 다루고 *로 case문에서 다루지 않은 모든 경우가 처리된다.
(java switch문의 default역할)
 
5.1 사용 예시
<div th:switch="${hello}">
    <p th:case="'admin'">User is an administrator
    <p th:case="#{roles.manager}">User is a manager
    <p th:case="*">User is a manager
</div>
 

 
6. th:if
조건문이 필요할 때 사용한다.  else문이 필요한 경우에는 th:unless를 사용한다.
 
1.1. 사용 예시
<p th:if="${hello}=='web'" th:text="${hello}"></p>
<p th:unless="unless 입니다."></p>

7 th:each
반복문이 필요한 경우에 사용한다.
 
리스트와 같은 collection 자료형을 서버에서 넘겨주면 그에 맞춰 반복적인 작업이 이루어질 때 사용한다.
 
먼저 "반복문 돌릴 객체의 변수명": "리스트 변수 명" (예: th:each="item:${itemList}")와 같이 적어 반복문을 명시하고
반복적인 작업이 필요한 곳에서 "객체명.객체 내 지역변수 명"(예: th:text="${item.itemName}")
 
이런식으로 데이터를 사용하면 된다. 
7.1 사용 예시
  ```
<div class="btn-group" th:each="item:${itemList}">   <button class="btn btn-secondary" th:value="${item.landmarkSn}" th:text="${item.landmarkName}" style="margin: 5px;"></button></div>
  ```
```
 <!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<h6>1. th:text 예시</h6>
<span th:text="${hello}">message</span>
<span>님 안녕하세요!</span>
<br>

<h6>2. th:utext 예시</h6>
<th:block th:utext="${hello}">message</th:block>

<br>

<h6>3. th:value 예시</h6>
<input th:value="${hello}" style="width: 100px; height:30px;">

<h6>4. th:with 예시</h6>
<div th:with="temp=${hello}" th:text="${temp}"></div>
<br>

<h6>5. th:switch 예시</h6>
<div th:switch="${hello}">
    <p th:case="'admin'">admin
    <p th:case="#{hello}=='user'">User
    <p th:case="*">*입니다
</div>
<br>

<h6>6. th:if 예시</h6>
<p th:if="${hello}=='web'" th:text="${hello}"></p>
<p th:unless="${true}" th:text="${hello}">
    unless 입니다
</p>
<br>

<h6>7. th:each 예시</h6>
<div class="btn-group" th:each="item:${itemList}">
    <button class="btn btn-secondary" th:value="${item.landmarkSn}" th:text="${item.landmarkName}"
            style="margin: 5px;"></button>
</div>
<br>
</body>
</html>
```
출처: https://chung-develop.tistory.com/5 [춍춍 블로그:티스토리]

<hr/>

## JWT(JSON WEB TOKEN)
JWT(JSON WEB TOKEN)이란 인증에 필요한 정보들을 암호화시킨 JSON토큰을 의미
- JWT 기반 인증은 JWT 토큰(Access Token)을 HTTP 헤더에 실어 서버가 클라이언트를 식별하는 방식
- 토큰 내부에는 위변조 방지를 위해 개인키를 통한 전자서명도 들어있다
JWT는 .을 구분자로 나누어지는 세 가지 문자열의 조합 Header(헤더), Paylead(내용), Signature(서명)
주요 참고 사이트 - https://inpa.tistory.com/entry/WEB-%F0%9F%93%9A-JWTjson-web-token-%EB%9E%80-%F0%9F%92%AF-%EC%A0%95%EB%A6%AC

JWT 연습 - https://jwt.io/

