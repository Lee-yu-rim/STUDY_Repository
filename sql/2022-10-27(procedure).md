저장 프로시저 
=======
1. 저장 프로시저의 생성
```sql
create or replace procedure 프로시저명 (매개변수)

is / as
    변수정의

begin
    sql 구문
    출력구문
    조건문 / 반복문

end;
/
```
```sql
create table emp01
as
select * from emp;

--생성
create or replace procedure emp01_print
is 
    vempno number(10);
    vename varchar2(10);
begin
    vempno := 1111;
    vename := 'Hong';
    
    dbms_output.put_line(vempno ||' '|| vename);
end;
/
```

2. 저장 프로시저의 실행
```sql
execute / exec 프로시저명
```
```sql
--실행
execute emp01_print; 
```

3. 저장 프로시저의 삭제
```sql
create or replace procedure 프로시저명

is

begin
    delete from 프로시저가 저장된 테이블명

end;
/
```
```sql
--삭제
create or replace procedure emp01_del
is
begin
    delete from emp01;
end;
/
```
```sql 
--원하는 데이터만 삭제
create or replace procedure del_name(vename emp01.ename%type)
is
begin
    delete from emp01
    where ename = vename;
end;
/

exec del_ename('SCOTT');
```

4. 저장 프로시저의 매개변수
- in : 값을 전달 받는 용도 (매개 변수 안에 기본적으로 생략되어 있음)
- out : 프로시저 내부의 실행 결과를 외부(실행을 요청한 곳)로 전달하는 용도
- in out : in 과 out의 기능이 합쳐진 용도
```sql
--emp테이블의 사번을 통해 특정 사원 조회
create or replace procedure sel_empno
(
        vempno in emp.empno%type,
        vename out emp.ename%type,
        vsal out emp.sal%type,
        vjob out emp.job%type
)
is

begin
    select ename,sal,job
    into vename,vsal,vjob
    from emp
    where empno = vempno;
end;
/
--바인드 변수를 생성하여 값 조회
variable var_ename varchar2(15);
variable var_sal number;   --바인드 변수에서 number 타입은 크기를 지정하지 않는다.
variable var_job varchar2(9);

exec sel_empno (7499,:var_ename,:var_sal,var_job);
--in 타입에는 매개변수에 넣을 값을 입력하고, out 타입에는 값을 받아올 수 있는 변수를 입력해준다.

print var_ename;
print var_sal;
print var_job;
```
***
저장 함수
======
- 저장 함수와 저장 프로시저의 차이점 - return 값 유무

1. 저장 함수의 생성
```sql
create or replace function 함수명 (매개변수)
    return 리턴값의타입   --세미콜론 생략
is

begin
    sql구문
    출력함수
    조건문 , 반복문

    return 리턴값;

end;
/
```
```sql
create or replace function cal_bonus(vempno emp.empno%type)
    return number  --타입에 크기 지정 X

is
    vsal number(7,2);
begin
    select sal
    into vsal
    from emp
    where empno = vempno;

    return vsal * 200;   --특정 사원에 보너스 지급

end;
/
```

2. 저장 함수의 실행
```sql
execute / exec 바인드 변수 := 함수명(매개변수값)
```
```sql
--실행
execute :var_res := cal_bonus(7788);  --저장 함수를 실행하기 위해서는 바인드 변수를 생성하여 저장 함수에서 반환되는 값을 변수에 받아주어야 한다.
```

***
커서(cursor) 
====
1. 커서란? 
- 기존 프로시저의 제약을 없애고 사용하기 위한 기능을 가진 명령문
- select 구문이 실행하는 결과를 가리킴

```sql
declare
    cursor 커서명 is sql구문;  --커서 선언

begin
    open 커서명;   --커서를 사용하겠다는 의미
    loop  --반복문을 통해 커서 안에 테이블의 데이터를 하나씩 가져옴
        fetch 커서명 into 변수명;   --테이블로부터 레코드(데이터)를 가져와서 변수에 저장
        exit when 커서명%notfound;  --커서가 가리키는 데이터가 없을 때 반복문 종료
    end loop;
    close 커서명;
end;
/
```

```sql
--emp 테이블에 있는 14개의 행을 커서를 모두 통해 가져오는 방법
declare 
    cursor c1 is select * from emp;
    vemp emp%rowtype;

begin
    open c1;
    loop
        fetch c1 into vemp;
        exit when c1%notfound;
        dems_output.put_line(vemp.empno ||' '|| vemp.ename ... )  --emp 테이블에 있는 컬럼명을 모두 입력
    end loop;
    close c1;
end;
/
```
- for문을 이용한 cursor 사용
```sql
declare 
    cursor c1 is select * from dept;
    vdept emp%rowtype;
begin
    for vdept in c1 loop   --vdept를 c1의 횟수만큼 반복한다.(dept 테이블의 데이터를 전부 조회)
        exit when c1%notfound;
        dems_output.put_line(vemp.empno ||' '|| vemp.ename ... )  
    end loop;
end;
/
```
***
여러가지 방식으로 원하는 데이터를 검색하는 법
-----
***