스프링 MVC
===

Controller의 데이터 처리 방식에 사용되는 어노테이션
---

> - @Controller - 스프링에서 객체를 관리해줄 수 있게 함 
> - @RequestMapping - 요청을 관리하는 URI 
>   - @GetMapping / @PostMapping 두가지 속성을 사용

***
<br>

Controller에서 데이터(파라메터)를 전달하는 방식
---

```java
//SampleDTO.java
@Data
public class SampleDTO {
	private String name;
	private int age;
	
}
```

```java
//SampleController.java

@Controller
@RequestMapping("/sample/*")  //대표 uri
@Log4j
public class SampleController {
	@RequestMapping("")  //서브 uri
	public void basic() {
		log.info("basicgogo");
	}
```
<br>

1. get 방식으로 넘어오는 파라메터 값을 받아오는 방식
```java
//SampleController.java

@GetMapping("ex01")
	public String ex01(SampleDTO dto) {  //SampleDTO => 커맨드 객체
		
		log.info("" + dto);
		
		return "ex01";
	}
	//결과값
	//INFO : org.zerock.controller.SampleController - SampleDTO(name=hong, age=10)
```
> 여기서 SampleDTO 는 클라이언트로부터 요청을 전달하는 커맨드 객체가 된다.

> http://localhost:8081/sample/ex01?name=hong&age=10 값을 요청하게 되면 DTO에 있는 set() 메소드가 동작하게 됨   
>	=> DTO에서 내부적으로 스프링 컨테이너를 통해 객체 생성 및 파라메터로 넘겨주는 값을 받아옴 (dto.setName(name))   
>   => 대신 DTO 클래스에는 파라메터로 넘겨주는 매개변수와 동일한 매개변수가 정의되어있어야함

<br>

2. @RequestParam 어노테이션을 사용하여 값을 낱개로 받아오는 방식

```java
//SampleController.java

@GetMapping("ex02")
	public String ex02(@RequestParam("name") String name,@RequestParam("age") int age) {
		
		log.info(name);
		log.info(age);
		
		return "ex02";
	}  
	//결과값
	//INFO : org.zerock.controller.SampleController - hong
	//INFO : org.zerock.controller.SampleController - 10
```

<br>

3. List 형태의 값을 받아오는 방식
```java
//SampleController.java

@GetMapping("ex02List")
	public String ex02List(@RequestParam("ids") ArrayList<String> ids) {
		
		log.info("ids : " + ids);
		
		return "ex02List";
	} 
	//결과값
	//INFO : org.zerock.controller.SampleController - ids : [aaa, bbb, ccc]
```

<br>

4. 객체 리스트 형태의 값을 받아오는 방식
```java
//SampleDTOList.java

@Data
public class SampleDTOList {
	private List<SampleDTO> list;

	public SampleDTOList() {
		list = new ArrayList<>();
	}
	
}
```
```java
//SampleController.java

@GetMapping("ex02Bean")
	public String ex02Bean(SampleDTOList list) {
		
		log.info("list : " + list);
		
		return "ex02Bean";
	} 
	//결과값
	//INFO : org.zerock.controller.SampleController - list : SampleDTOList(list=[SampleDTO(name=aaa, age=0), SampleDTO(name=null, age=0), SampleDTO(name=bbb, age=0)])
```

<br>

5. @DateTimeFormat 어노테이션을 사용하여 날짜 형태의 값을 받아오는 방식
```java
//TodoDTO.java

@Data
public class TodoDTO {
	private String title;
	@DateTimeFormat(pattern = "yyyy/MM/dd")  
	private Date dueDate;  
}
```

```java
//SampleController.java

@GetMapping("ex03")
	public String ex03(TodoDTO todo) {
		
		log.info("todo : " + todo);
		
		return "ex03";
	} 
	//결과값
	//INFO : org.zerock.controller.SampleController - todo : TodoDTO(title=test, dueDate=Wed Dec 21 00:00:00 KST 2022)
```
> 파라메터 값은 문자열로 넘어가기 때문에 날짜 데이터는 형변환이 필요함    
> => @DateTimeFormat 어노테이션을 통해 날짜정보를 문자열로 변환함

<br>

6. @ModelAttribute 어노테이션을 사용하여 EL 형태의 값을 받아오는 방식
```jsp
//ex04.jsp

<body>
	<h2>SAMPLEDTO	${sampleDTO }</h2>  
	<h2>PAGE ${page }</h2>
</body>
```
```java
//SampleController.java

@GetMapping("ex04")
	public String ex04(SampleDTO dto, @ModelAttribute("page")int page) {  //SampleDTO => 커맨드 객체
		
		log.info("dto : " + dto);
		log.info("page : " + page);
		
		return "/sample/ex04";
	} 
	//결과값
	//SAMPLEDTO SampleDTO(name=hong, age=0)
	//PAGE
```
> 파라메터 값은 String 타입으로 전달된다.    

> page 값은 int 타입으로 선언되었으므로 출력되지 않음 => @ModelAttribute 어노테이션을 사용하여 출력

> 커맨드 객체의 역할 및 동작 순서
> 1. 파라메터 자동으로 받기
> 2. 뷰 페이지로 커맨드 객체의 정보 전달(넘길 때 클래스의 첫 글자를 소문자로 구성해서 전달)
> 	 => sampleDTO
> 3. 기본형 매개변수의 값을 뷰페이지로 전달하기 위헤 @ModelAttribute를 적용
>	 => Model 객체에 담겨서 전달됨

<br>

7. json 형식으로 값을 받아오는 방식들

- @ResponseBody 어노테이션을 이용한 방식
```java
//SampleController.java

@GetMapping("/ex06") 
	public @ResponseBody SampleDTO ex06() { 
		
		SampleDTO dto = new SampleDTO();
		dto.setName("hong");
		dto.setAge(10);

		return dto;
	} 
	//결과값
	//{"name":"hong", "age":10}
```
> @ResponseBody : 원하는 형식의 데이터 타입으로 값을 전달해줌 => json 형태로 데이터가 넘어가게됨

<br>

- header 영역을 이용한 방식
```java
//SampleController.java

@GetMapping("/ex07") 
	public ResponseEntity<String> ex07() {   
		
		String msg = "{\"name\":\"홍길동\"}";   //속성과 값이 문자열로 이루어진 json 형태의 객체를 클라이언트로 보냄 = {"name":"홍길동"}
		HttpHeaders header = new HttpHeaders();  
		header.add("Content-type", "application/json;charset=UTF-8"); //header 영역에 값 넣어주기
		
		return new ResponseEntity<>(msg,header,HttpStatus.OK);
	}
	//결과값
	//{"name":"홍길동"} => 페이지에 값이 출력됨
```

***
<br>

파일 업로드를 처리하는 방식
---

```jsp
//exUpload.jsp

<form action="/sample/exUploadPost" method="post" enctype="multipart/form-data">
	<div>
		<input type='file' name='files'>
	</div>
	<div>
		<input type='file' name='files'>
	</div>
	<div>
		<input type='submit'>
	</div>
</form>
```

```xml
<!-- servlet-context.xml -->

<beans:bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
	<beans:property name="defaultEncoding" value="utf-8"></beans:property>
	<beans:property name="maxUploadSize" value="104857560"></beans:property>
	<beans:property name="maxUploadSizePerFile" value="2097152"></beans:property>
	<beans:property name="uploadTempDir" value="file:/C:/upload/tmp"></beans:property>
	<beans:property name="maxInMemorySize" value="10485756"></beans:property>
</beans:bean>
```

```java
//SampleController.java

@GetMapping("/exUpload") 
	public void exUpload() {   
		
		log.info("/exupload.........");
	}
	
	
//post 방식으로 넘어오는 값 처리
@PostMapping("/exUploadPost") 
public void exUploadPost(ArrayList<MultipartFile> files) {   
	//배열형태로 값이 넘어오므로 for문으로 받아오기
	files.forEach(file -> {
		log.info(".....................");
		log.info("name : " + file.getOriginalFilename());
		log.info("size : " + file.getSize());
		
	});
}
```

***
<br><br>

내용 정리하기
---

- 컨트롤러에서 뷰페이지로 데이터를 전달하는 방식
> 1. Model 겍체
>    - addAttribute(속성,값)

> 2. 커맨드 객체

> 3. @ModelAttribute

> 4. RedirectAttribute - 한 번 사용할 데이터를 이동하는 페이지에 전달 / 그 다음 페이지 이동시에는 데이터 사용 불가
>    - addFlashAttr()
>    => response.sendRedirect("list.jsp?name=hong")

> 5. json 형식으로 데이터를 전달하는 방식
>    - DTO 타입으로 리턴값을 정의하고 @ResponseBody 어노테이션을 사용하여 값 전달

> 6. ResponseEntity 타입으로 json 형식의 데이터 전달하기