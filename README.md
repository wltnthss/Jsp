# Jsp, Servlet

## Jsp, Servlet 개발하면서 궁금한점 기록용

**JSP - c:url**

```jsp
// as-is
<link rel="stylesheet" type="text/css" href="resources/css/Style.css">

// to be
<link rel="stylesheet" type="text/css" href="<c:url value='/css/Style.css'/>">
```

* as-is의 경우로 스스로 게시판 예제를 만들어보던 경우 굳이 c:url 을 사용하는 경로로 사용하는 예제를 많이 보았다.
* 둘의 차이점은 뭘까??

* 검색결과 c:url 은 URL에 자동으로 Context Path 를 붙여주는 일을 하여 컨텍스트 경로를 변경하더라도 URL을 수정 할 필요가 없게되는 것!
* 그렇다면 **전부 c:url 로써 활용하면 되는걸까??**

* **결과는 그렇지 않다.** c:url을 태그를 사용하면 주소창에 jsessionid= 가 생기는 경우가 있는데 이는 클라이언트에서 쿠키를 허용하지 않을 경우 리소스 파일들이 깨지는 단점이 존재한다.
* 따라서 이와 같은 경우에는 2가지 방법으로 해결 가능하다.

```
// <c:url> 태그 대신에 경로 앞에 ${pageContext.request.contextPath}를 붙이면 된다.
${pageContext.request.contextPath}/resources/css/Style.css

// web.xml 파일 session-config 에 설정 추가
    <session-config>        
    <session-timeout>30</session-timeout>        
    <tracking-mode>COOKIE</tracking-mode>    
</session-config>
```

> 위의 2가지 방법으로 해결가능하니 동적으로 컨텍스트 경로를 설정해주는 c:url 태그를 사용하자.