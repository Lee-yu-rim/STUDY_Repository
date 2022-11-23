DQL - 함수
======
1. 문자함수
- upper : 소문자 > 대문자 변환
```sql
select upper('welcome'),upper(ename)
from dual;
```
- lower : 대문자 > 소문자 변환
```sql
select lower(WELCOME),lower(ename)
from emp;
```
- length : 문자열 길이 반환
```sql
select ename,length(ename)
from emp;
```
- substr : 원하는 문자열 반환
```sql
select substr('Welcome to Oracle',2,3)
from dual;
-- 문자열의 2번째부터 3번째까지 가져옴
```
- instr : 문자열의 위치값 반환
```sql
select instr('Welcome to Oracle','r')
from dual;
--r의 위치값 반환

select instr('Welcome to Oracle','e',3,2
from dual;
--3번째 열부터 시작해서 2번째에 나오는 e의 위치값을 반환
```
- replace : 문자열 대체
```sql
select replace('Welcome to Oracle','to','of')
from dual;
--to를 of로 대체
```
- rpad / lpad : 문자열의 오/왼쪽에 공간을 확보해서 문자 대입
```sql
select 
lpad('oracle',10,'#'), --oracle왼쪽에 #을 넣어 10글자 완성
rpad('oracle',10,'*')  --oracle 오른쪽에 *을 넣어 10글자 완성
from dual;
```
- concat : 문자열 연결
```sql
select concat(empno,ename)
from emp;
-- 7369SMITH 두가지 컬럼값이 연결됨
```

2. 숫자함수
- round : 값을 반올림하여 반환
```sql
select 
round(1234.5678.0),   --반올림한 정수값 1235
round(1234.5678,1),   --소수점 첫째자리까지 반올림 1234.6
round(1234.5678,-1)   --정수자리에서 반올림 1230
```
- trunc : 값을 버리고 반환
```sql
select
trunc(1234.5678,0)    --0의 자리까지만 반환 1234