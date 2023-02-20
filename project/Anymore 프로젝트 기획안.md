프로젝트 기획안
===
- 작성일 : 2023.02.20
- 작성자 : 이유림

<br>

프로젝트 명
===
- Anymore Project

<br>

기획의도
===

- 단순 보호소 사이트가 아닌 커뮤니티나 쇼핑몰, 예약과 같은 다양한 서비스를 한 곳에서 이용할 수 있는 사이트를 구현하여, 사용자의 입장에서 편리한 기능을 제공할 수 있는 홈페이지를 개발하고 싶었습니다. 

<br>

홈페이지 설명
===
- 다양한 유기동물을 구조하여 보호하는 보호소 페이지로, 회원제 게시판을 통해 유기 동물을 분양할 수 있도록 하는 역할이 주된 페이지입니다. 더불어 입양 후기나 반려동물 용품 중고거래 등의 회원간의 다양한 의견을 주고 받을 수 있는 커뮤니티와 보호소 내 자체 제작 상품을 판매하는 쇼핑몰, 보호소 방문을 위한 예약 시스템 등의 부가적인 시스템이 결합된 홈페이지입니다.

<br>

주요기능
===

- 회원가입

- 로그인

- 카카오 로그인

- 로그아웃

- 비밀번호 찾기 이메일 발송

- 회원탈퇴

- 회원 마이페이지

- 관리자 마이페이지

- 게시글 작성 / 수정 / 삭제

- 댓글 작성 / 수정 / 삭제

- 게시글 파일 업로드

- 찜 기능

- 카카오 API를 이용한 지도 검색 및 위치 표시

- 공지창 팝업 시스템

- 예약 시스템

- 상품 장바구니

- 아임포트를 이용한 카카오 및 신용카드 결제 시스템

<br>

프로젝트 내 담당 기능
===

- 회원 가입

- 아이디 중복 체크 시스템

- 다음 주소 검색 API를 이용한 주소 검색 시스템

- 회원 로그인

- 카카오 API를 이용한 회원가입 및 로그인

- 로그아웃

- 비밀번호 찾기 이메일 발송

- 메인페이지 공지창 팝업 시스템

- 카카오 API를 이용한 지도 검색 및 위치 표시 시스템

- 상품 목록 및 상세보기 구성

- 장바구니 시스템

- 마이페이지 구매내역 구성

- 보호소 소개 페이지 구성

<br>

프로젝트를 진행하며 변경된 사항
===

1. 회원가입시 아이디 중복체크 및 정규식 사용

2. 네이버 API를 이용한 로그인 구현 제거

3. 비밀번호 찾기를 비밀번호 표시 기능에서 임시비밀번호를 생성하여 이메일로 발송하는 기능으로 변경

4. 공공 데이터 API를 이용한 동물병원 검색 시스템에서 카카오 지도 API를 이용한 동물 병원 검색 시스템으로 변경

5. 메인페이지 공지사항 팝업창 시스템 추가

<br>

<hr>

<br>

DB 정보
---

```sql
CREATE TABLE reservation (
   num   number(10,0)      NOT NULL,
   title   varchar2(50)      NOT NULL,
   sex   varchar2(10)      NULL,
   people_cnt   varchar2(30)      NOT NULL,
   visiter_name   varchar2(20)      NOT NULL,
   phone   varchar2(30)      NOT NULL,
   visit_day   date      NOT NULL,
   reser_time   varchar2(30)      NOT NULL,
   visit_reason   varchar2(2000)      NULL,
   id   varchar2(20)      NULL,
   visit_identify   number(10,0)      NOT NULL
);

CREATE TABLE zzim (
	id	varchar2(20)		NOT NULL,
	board_num	number(10,0)		NULL
);

CREATE TABLE free_board_reply (
	rno	number(10,0)		NOT NULL,
	reply	varchar2(500)		NOT NULL,
	bno	number(10,0)		NOT NULL,
	id	varchar2(30)		NOT NULL,
	replydate	date	DEFAULT sysdate	NOT NULL,
	updatedate	date	DEFAULT sysdate	NOT NULL
);

CREATE TABLE adopt_reservation (
	adoptnum	number(10,0)		NOT NULL,
	name	varchar2(50)		NOT NULL,
	phone	varchar2(20)		NOT NULL,
	birthday_date	varchar2(200)	NOT NULL,
	address	varchar2(200)		NOT NULL,
	board_num	number(10,0)		NULL,
	servey1	varchar2(500)		NOT NULL,
	servey2	varchar2(500)		NOT NULL,
	servey3	varchar2(500)		NOT NULL,
	servey4	varchar2(500)		NOT NULL,
	servey5	varchar2(500)		NOT NULL,
	servey6	varchar2(500)		NOT NULL,
	servey7	varchar2(500)		NOT NULL,
	servey8	varchar2(500)		NOT NULL,
    reg_date date default sysdate not null,
    id	varchar2(20)		NOT NULL
);

CREATE TABLE free_board (
   bno   number(10,0)      NOT NULL,
   title   varchar2(50)      NOT NULL,
   content   varchar2(2000)      NOT NULL,
   regdate   date   DEFAULT sysdate   NULL,
   updatedate   date   DEFAULT sysdate   NULL,
   reply_cnt   number(10,0)      NULL,
   visit_cnt   number(10,0)      NULL,
   field   varchar2(20)      NOT NULL,
   id   varchar2(20)      NOT NULL
);

CREATE TABLE anymore_product (
	product_num	number(10,0)		NOT NULL,
	price	varchar2(50)		NOT NULL,
	discribe	varchar2(2000)		NOT NULL,
    p_amount number(10,0) NULL,
	product_name	varchar2(500)		NOT NULL,
	product_regdate	date	DEFAULT sysdate	NOT NULL,
	product_content	varchar(2000)		NOT NULL
);

CREATE TABLE product_perchase (
	perchase_num	number(10,0)		NOT NULL,
	name	varchar2(50)		NOT NULL,
	perchased_product	varchar2(500)		NOT NULL,
	all_price	varchar2(500)		NOT NULL,
	ordered_date	date	DEFAULT sysdate 	NOT NULL,
	delivery_status	varchar2(50)		NOT NULL,
	product_num	number(10,0)		 NULL,
	payment	varchar2(50)		NOT NULL,
	id	varchar2(20)		NOT NULL
);

CREATE TABLE perchase_info (
	perchase_num	number(10,0)		NOT NULL,
	perchased_pname	varchar2(50)		NOT NULL,
	amount	number(10,0)		NOT NULL,
	product_price	number(10,0)		NOT NULL
);

CREATE TABLE delivery_info (
	perchase_num	number(10,0)		NOT NULL,
	name	varchar2(50)		NOT NULL,
	address	varchar2(100)		NOT NULL,
	phone	varchar2(50)		NOT NULL,
	requests	varchar2(200)		NULL
);

CREATE TABLE animal_info (
	board_num	number(10,0)		NOT NULL,
	animal_name	varchar2(50)		NOT NULL,
	enter_day	date	DEFAULT sysdate 	NOT NULL,
	protect_day	date	DEFAULT sysdate 	NOT NULL,
	variety	varchar2(50)		NOT NULL,
	age	varchar2(50)		NOT NULL,
	sex	varchar2(20)		NOT NULL,
	tnr	varchar2(20)		NOT NULL,
	identity	varchar2(500)		NOT NULL,
	euthanasia_day	varchar2(50)		NOT NULL
);

CREATE TABLE animal_fileupload (
	fno	number(10,0)		NOT NULL,
	fileName	varchar2(100)		NOT NULL,
	uuid	varchar2(100)		NOT NULL,
	uploaddate	date		NOT NULL,
	file_size	number(20,0)		NULL,
	board_num	number(10,0)		NOT NULL,
    uploadpath 	varchar2(200)		NOT NULL,
	fileType	char(1)		NULL
);

CREATE TABLE member (
	id	varchar2(20)		NOT NULL,
	password	varchar2(20)		NOT NULL,
	name	varchar2(10)		NOT NULL,
	staffs	varchar2(2)	DEFAULT 'n'	NOT NULL,
	phone	varchar2(20)		NOT NULL,
	birth	varchar2(20)		NOT NULL,
	email	varchar2(50)		NOT NULL,
	pass_question	number(2, 0)	DEFAULT 1	NULL,
	pass_answer	varchar2(100)		NULL,
	address	varchar2(100)		NOT NULL,
	regdate	date	DEFAULT sysdate	NOT NULL,
	alert_cnt	number(10, 0)		NULL,
    member_num  	number(10,0)	NOT NULL,
    kakao_email     varchar2(50) null
);

CREATE TABLE cart (
	c_num	number(10,0)		NOT NULL,
	quantity	number(10,0)		NOT NULL,
	c_regdate	date	DEFAULT sysdate	NOT NULL,
	id	varchar2(20)		NOT NULL,
	product_num	number(10,0)		NOT NULL
);

CREATE TABLE used_items (
   bno   number(10, 0)      NOT NULL,
   title   varchar2(30)      NOT NULL,
   content   varchar2(1000)      NOT NULL,
   regdate   date   DEFAULT sysdate   NOT NULL,
   updatedate   date   DEFAULT sysdate   NOT NULL,
   reply_cnt   number(10, 0)      NOT NULL,
   visit_cnt   number(10, 0)      NOT NULL,
   field   varchar2(20)      NOT NULL,
   id   varchar2(20)      NOT NULL,
   deal varchar2(20)    null
);

CREATE TABLE used_items_reply (
	rno	number(10,0)		NOT NULL,
	reply	varchar2(500)		NOT NULL,
	bno	number(10, 0)		NOT NULL,
	id	varchar2(30)		NOT NULL,
	replydate	date	DEFAULT sysdate	NOT NULL,
	updatedate	date	DEFAULT sysdate	NOT NULL
);

CREATE TABLE adoption_review (
	bno	number(10,0)		NOT NULL,
	title	varchar2(30)		NOT NULL,
	content	varchar2(1000)		NOT NULL,
	regdate	date	DEFAULT sysdate	NOT NULL,
	updatedate	date	DEFAULT sysdate	NOT NULL,
	reply_cnt	number(10,0)		NOT NULL,
	visit_cnt	number(10,0)		NOT NULL,
	id	varchar2(20)		NOT NULL
);

CREATE TABLE adoption_reply (
	rno	number(10,0)		NOT NULL,
	reply	varchar2(500)		NOT NULL,
	bno	number(10,0)		NOT NULL,
	id	varchar2(30)		NOT NULL,
	replydate	date	DEFAULT sysdate	NOT NULL,
	updatedate	date	DEFAULT sysdate	NOT NULL
);

CREATE TABLE commu_fileupload (
	fno	number(10,0)		NOT NULL,
	fileName	varchar2(100)		NOT NULL,
	uuid	varchar2(100)		NOT NULL,
	uploaddate	date		NOT NULL,
	file_size	number(20,0)		NULL,
	bno	number(10,0)		NOT NULL,
    uploadpath 	varchar2(200)		NOT NULL,
	fileType	char(1)		NULL
);

CREATE TABLE QNA_reply (
	bno	number(10,0)		NOT NULL,
	rno	number(10,0)		NOT NULL,
	reply	varchar2(1000)		NOT NULL,
	replydate	date	DEFAULT sysdate	NOT NULL,
	updatedate	date	DEFAULT sysdate	NOT NULL,
	id	varchar2(20)		NOT NULL
);

CREATE TABLE qna_fileupload (
	fno	number(10,0)		NOT NULL,
	bno	number(10,0)		NOT NULL,
	filename	varchar2(100)		NOT NULL,
	uuid	varchar2(100)		NOT NULL,
	uploaddate	date		NOT NULL,
	file_size	number(20,0)		NULL,
    uploadpath 	varchar2(200)		NOT NULL,
	fileType	char(1)		NULL
);

CREATE TABLE QNA (
	bno	number(10,0)		NOT NULL,
	title	varchar2(100)		NOT NULL,
	content	varchar2(3000)		NOT NULL,
	id	varchar2(30)		NOT NULL,
	regdate	date	DEFAULT sysdate	NOT NULL,
	updatedate	date	DEFAULT sysdate	NOT NULL,
	count	number(10,0)		NOT NULL,
    replycnt number(10,0)  default 0  null 
);

CREATE TABLE notice (
	bno	number(10,0)		NOT NULL,
	title	varchar2(100)		NOT NULL,
	content	varchar2(3000)		NOT NULL,
	id	varchar2(30)		NOT NULL,
	regdate	date	DEFAULT sysdate	NOT NULL,
	updatedate	date	DEFAULT sysdate	NOT NULL,
	count	number(10,0)		NOT NULL
);

CREATE TABLE FAQ (
	bno	number(10,0)		NOT NULL,
	title	varchar2(100)		NOT NULL,
	content	varchar2(3000)		NOT NULL,
	id	varchar2(30)		NOT NULL,
	regdate	date	DEFAULT sysdate	NOT NULL,
	updatedate	date	DEFAULT sysdate	NOT NULL,
	count	number(10,0)		NOT NULL
);

CREATE TABLE notice_fileupload (
	fno	number(10,0)		NOT NULL,
	bno	number(10,0)		NOT NULL,
	fileName	varchar2(100)		NOT NULL, 
	uuid	varchar2(100)		NOT NULL,
	uploaddate	date		NOT NULL,
	file_size	number(20,0)		NULL,
    uploadpath 	varchar2(200)		NOT NULL,
	fileType	char(1)		NULL
);

CREATE TABLE faq_fileupload (
	fno	number(10,0)		NOT NULL,
	bno	number(10,0)		NOT NULL,
	fileName	varchar2(100)		NOT NULL,
	uuid	varchar2(100)		NOT NULL,
	uploaddate	date		NOT NULL,
	file_size	number(20,0)		NULL,
    uploadpath 	varchar2(200)		NOT NULL,
	fileType	char(1)		NULL
);

CREATE TABLE used_item_file_upload (
	fno	number(10,0)		NOT NULL,
	fileName	varchar2(100)		NOT NULL,
	uuid	varchar2(100)		NOT NULL,
	uploaddate	date		NOT NULL,
	file_size	number(20,0)		NULL,
	bno	number(10, 0)		NOT NULL,
    uploadpath 	varchar2(200)		NOT NULL,
	fileType	char(1)		NULL
);

CREATE TABLE anymore_fileupload (
	fno	number(10,0)		NOT NULL,
	fileName	varchar2(100)		NOT NULL,
	uuid	varchar2(100)		NOT NULL,
	uploaddate	date		NOT NULL,
	file_size	number(20,0)		NULL,
	product_num	number(10,0)		NOT NULL,
    uploadpath 	varchar2(200)		NOT NULL,
	fileType	char(1)		NULL
);

CREATE TABLE adopt_fileupload (
	fno	number(10,0)		NOT NULL,
	fileName	varchar2(100)		NOT NULL,
	uuid	varchar2(100)		NOT NULL,
	uploaddate	date		NOT NULL,
	file_size	number(20,0)		NULL,
	bno	number(10,0)		NOT NULL,
    uploadpath 	varchar2(200)		NOT NULL,
	fileType	char(1)		NULL
);
```