액션 태그(Action Tag)
===

> <jsp: inclue> : 외부 파일을 현재 파일에 포함시킴

> <jsp: forward> : 페이지 이동

> <jsp: useBean><jsp: setProperty><jsp: getProperty> : 자바 빈즈 생성

***
<br>

- include 지시어와 <jsp: include> 액션태그의 차이점
> include 지시어
> - 정적 페이지
> - 표현식 사용 불가
> - jsp 파일이 하나로 합쳐짐 -> 포함 시킨 파일의 변수 사용 가능
> - page 영역 / request 영역 모두 공유됨

> <jsp: include> 액션태그
> - 동적 페이지
> - 표현식 사용 가능
> - jsp 파일이 HTML코드로 컴파일 됨 -> 포함시킨 파일의 변수 참조가 불가능 
> - page 영역 공유 불가 / request 영역만 공유 가능(include 되기전에 request 영역의 제어권이 넘어옴)

```jsp
//OuterPage1.jsp
<body>
	<h2>외부 파일 1</h2>
	<%
		String newVar1 = "고구려 세운 동명왕";
	%>
	<ul>
		<li>page 영역 속성 : <%=pageContext.getAttribute("pAttr") %></li>
		<li>request 영역 속성 : <%=request.getAttribute("rAttr") %></li>
	</ul>
</body>
```

```jsp
//OuterPage2.jsp
<body>
	<h2>외부 파일 2</h2>
	<%
		String newVar2 = "백제 온조왕";
	%>
	<ul>
		<li>page 영역 속성 : <%=pageContext.getAttribute("pAttr") %></li>
		<li>request 영역 속성 : <%=request.getAttribute("rAttr") %></li>
	</ul>
</body>
```

```jsp
//IncludeMain.jsp
<%
	//포함할 파일의 경로
	String outerPath1 = "./inc/OuterPage1.jsp";
	String outerPath2 = "./inc/OuterPage2.jsp";
	
	//page 영역과 request 영역에 속성 저장
	pageContext.setAttribute("pAttr", "동명왕");
	request.setAttribute("rAttr", "온조왕");
%>
<body>
	<h2>지시어와 액션태그 동작 방식 비교</h2>
	
	<!-- 지시어 방식 -->
	<h3>지시어로 페이지 포함하기</h3>
	<%@ include file="./inc/OuterPage1.jsp" %>
	<p>외부 파일에 선언한 변수 : <%=newVar1 %></p>  //외부 파일의 변수의 값인 "고구려 세운 동명왕" 이 출력됨
	
	<!-- 액션태그 방식 -->
	<h3>액션태그로 페이지 포함하기</h3>
	<jsp:include page="./inc/OuterPage2.jsp" />  //page 영역 값은 출력되지 않고 request 영역 값만 출력됨
	<jsp:include page="<%=outerPath2 %>" />
	<p>외부 파일에 선언한 변수 : <%--=newVar2 --%></p>  //외부 파일의 변수 사용 불가함
</body>
```

***
<br>

- <jsp: forward> 액션 태그
```jsp
//Forward.jsp
<body>
	<jsp:forward page="./ForwardSub.jsp"></jsp:forward>
</body>

//ForwardSub.jsp
<body>
	<h2>포워드된 페이지</h2>
	<p><%=pageContext.getAttribute("pAttr") %></p>
	<p><%=request.getAttribute("rAttr") %></p>  //request 영역의 제어권이 다음 페이지로 넘어감
</body>
```