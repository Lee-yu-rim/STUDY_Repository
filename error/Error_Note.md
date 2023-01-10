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