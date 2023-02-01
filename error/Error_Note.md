<mark>maven repository build 후 서버 오류</mark>
---

> 오류 상황
- maven repository 빌드 후 서버 실행 시 [SEVERE: 필수 항목인 서버 구성요소가 제대로 시작되지 못하여, Tomcat이 시작될 수 없습니다.] 오류 뜨면서 실행 실패하는 경우

> 해결 방법
- 위에 project -> clean 해주기
- 프로젝트 오른쪽 클릭 -> properties -> Deployment Assembly -> library에 Maven Dependencies 있는지 확인 
-> 없으면 Add 눌러서 java Build Path Entried 눌러서 추가
- 서버 restart 해서 돌아가는지 확인
- 그래도 안되면 톰캣 서버 delete 후 다시 생성해주기 -> Module이랑 포트 번호 재설정

***
<br>

<mark>홈페이지 404 출력 및 서버 실행 에러</mark>
---

> 오류 상황
- 주소창에 주소 넣고 실행했는데 404 에러 뜨고 서버오류 발생

> 해결 방법
- 서버 포트번호와 모듈 확인 
- 서버 clean 후 재시작

***
<br>

<mark>SQL Developer 테이블 생성 오류</mark>
---

> 오류 상황
- 테이블 생성 시 '열을 사용할 수 없습니다' 라고 에러 뜨는 경우

> 해결 방법
- 오타 없는지 확인
- default 값 문자열을 작은 따옴표가 아닌 큰 따옴표로 감싸줬을 경우

***
<br>

<mark>SQL Developer에 값 넣을 때 앞자리 0이 안들어가는 경우</mark>
---

> 오류 상황
- 핸드폰 번호 값을 DB에 저장하려는데 01011111111이면 1011111111 이런식으로 저장됨

> 해결 방법
- 핸드폰 번호 컬럼의 타입을 number > varchar2 로 변경

***
<br>

<mark>log 밑줄 에러 뜰 경우</mark>
---

> 오류 상황
- Log4j 어노테이션이 들어가있음에도 불구하고 log.info() 메소드에서 log에 빨간줄이 떠있는 오류 발생
> 해결 방법
- lombok 재설치 후 스프링 재실행
- @Log4j 어노테이션과 import 삭제 후 다시 넣어서 import 해주기
***
<br>

<mark>부적합한 열 1111 (505) 에러</mark>
---

> 오류 상황
- 로그인 페이지에서 값 넣고 로그인 버튼 클릭 시 부적합한 열 1111 ~ 어쩌구 하면서 페이지 505 오류 발생
> 해결 방법
- form 태그에 name 과 id 속성 있는지 확인
- controller 에 return 값 성공 시와 실패 시 각각 구분 잘 되어있는지 확인
- controller 변수명 겹치게 쓰지 않도록 주의하기
- https://weekbook.tistory.com/74 페이지 참고해서 따라하기
***
<br>

<mark>ajax 비동기 통신 이용 시 값 인식 에러</mark>
---

> 오류 상황
- 회원 가입 페이지에서 아이디 중복 확인 버튼 누를 시 DB에 있는 데이터 임에도 사용이 가능한 아이디라고 뜨는 상황
> 해결 방법
- ajax에서 dateType : json 추가해주기
***
<br>

<mark>ajax 통신에서 값 여러개 넘길 시 500 에러</mark>
---

> 오류 상황
- controller에서 RequestParam 어노테이션을 사용하여 여러개의 값을 넘길 경우 "org.apache.ibatis.binding.BindingException: Parameter 'a_apy_position' not found. Available parameters are [0, 1, 2, 3, param3, param4, param1, param2]" 라고 뜨면서 페이지 500 에러 발생
> 해결 방법
- 값을 한번에 VO 클래스로 생성 후 넘겨주면 오류 해결
***
<br>

<mark>ajax 로 불러온 값 화면에 출력 안될 때</mark>
---

> 오류 상황
- ajax 통신으로 값을 불러와서 화면에 출력하려고 하는데 alert 창은 뜨고 화면 출력은 안됨

> 해결 방법
- 불러오려는 값의 속성값을 id 값 말고 class 값으로 바꿔서 불러와보기

***
<br>

<mark>DB에서 값 불러올 때 NullPointException 오류</mark>
---

> 오류 상황
- 게시판에서 목록 불러오기 하는데 nullpointException 에러

> 해결 방법
- Controller에 @AllArgsConstructor 넣어주기

***
<br>