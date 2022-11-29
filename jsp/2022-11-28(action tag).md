액션 태그(Action Tag)
===
1. 액션 태그 
- 기존의 스크립틀릿 표현을 간소화 시키기 위해 사용
> <jsp: inclue> : 외부 파일을 현재 파일에 포함시킴

> <jsp: forward> : 페이지 이동 

> <jsp: useBean><jsp: setProperty><jsp: getProperty> : 자바 bean 클래스 생성

> <jsp: param> : include 나 forward를 사용할 때 다른 페이지에 값을 전달

***
<br>

2. <jsp: include> 액션 태그
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

3. <jsp: forward> 액션 태그 

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

***
<br>


4. <jsp: useBean> 액션 태그
- 입력폼의 값을 전송받아서 저장하는 용도
> - <jsp: useBean> : 자바 빈즈 생성
> - <jsp: setProperty> : 멤버 변수 값 설정
> - <jsp: getProperty> : 멤버 변수 값 추출
```jsp
<%
	MemberDAO dao = new MemberDAO();
	dao.getId();
	dao.setId("hong");
%>

<jsp:useBean id="dao(변수명)" class="MemberDAO(패키지 + 클래스명)" scope="(영역객체)">
// = MemberDAO dao = new MemberDAO();
<jsp:setProperty name="dao(변수명)" property="id(호출할 메소드명)" value="hong(매개변수값)">  
// = dao.setId("hong");
<jsp:getProperty name="dao(변수명)" property="id(호출할 메소드명">
// = dao.getId();
```
<br>

- 와일드카드를 이용한 파라메터 값 한번에 가져오기
```jsp
//UseBeanForm.jsp
<body>
	<h2>액션 태그로 폼값 한 번에 받기</h2>
	<form method="post" action="UseBeanAction.jsp">
		이름 : <input type="text" name="name" /><br />
		나이 : <input type="text" name="age" /><br />
		<input type="submit" value="폼값 전송" />
	</form>
</body>
```
```jsp
//UseBeanAction.jsp
<body>
	<h3>액션 태그로 폼값 한 번에 받기</h3>

	<jsp:useBean id="person" class="common.Person"></jsp:useBean>
	
	//<jsp:setProperty property="name" name="person" value="" /> 
	//<jsp:setProperty property="age" name="person" value="" />
	//기존에는 이렇게 작성해야 했던 것을 아래처럼 * 와일드 카드로 한번에 가져올 수 있음
	<jsp:setProperty property="*" name="person" />
	
	
	<ul>
		<li>이름 : <jsp:getProperty property="name" name="person"/></li>
		<li>나이 : <jsp:getProperty property="age" name="person"/></li>
	</ul>
</body>
```

***
<br>

5. <jsp: param> 액션 태그
- <jsp: forward> 태그의 매개변수 값 전달하기
```jsp
//Param.jsp
//포워드되는 페이지로 값 전달
<body>
	<jsp:forward page="ParamForward.jsp">
		<jsp:param name="param1" value="임꺽정" />
		<jsp:param name="param2" value="10"/>
	</jsp:forward>
</body>


//ParamForward.jsp
<body>
	<%=param1 %>
	<%=param2 %>
</body>
```
- <jsp: include> 태그에 포함된 페이지 값 전달하기
```jsp
//Param.jsp
//include 된 페이지의 값을 include 시킨 페이지에 전달
<body>
	<jsp:include page="inc/ParamInclude.jsp">
		<jsp:param value="강원도" name="loc1"/>
		<jsp:param value="부산" name="loc2"/>
	</jsp:include>
</body>

//ParamForward.jsp
<body>
	<%=param1 %>
	<%=param2 %>
</body>
```