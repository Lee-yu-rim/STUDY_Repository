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

<mark>ajax 로 불러온 값 화면에 출력 안될 때</mark>
---

> 오류 상황
- ajax 통신으로 값을 불러와서 화면에 출력하려고 하는데 alert 창은 뜨고 화면 출력은 안됨

> 해결 방법
- 불러오려는 값의 속성값을 id 값 말고 class 값으로 바꿔서 불러와보기