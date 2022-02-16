# Database

## SQL (Structured Query Language)
- Database에 있는 정보를 사용할 수 있도록 지원하는 언어
- 모든 DBMS에서 사용 가능
- 대소문자는 구별하지 않음
- SQL구문은 DDL, DCL, DML로 구분

## DCL (Data Definition Language)
- 데이터 정의어
- 데이터베이스 객체의 구조를 정의
- 테이블 생성, 컬럼 추가, 타입변경, 제약조건 지정, 수정 등등
- SQL문
    - `create` - 데이터베이스 객체를 생성
    - `drop` - 데이터베이스 객체를 삭제
    - `alter` - 기존에 존재하는 데이터베이스 객체를 수정

## DML (Data Manipulation Language)
- 데이터 조작어
- Data 조작기능
- 테이블의 레코드를 CRUD(Create, Retrieve, Update, Delete)
- SQL문
    - `insert` - 데이터베이스 객체에 데이터를 입력
    - `select` - 데이터베이스 객체에서 데이터를 조회
    - `update` - 데이터베이스 객체에 데이터를 수정
    - `delete` - 데이터베이스 객체에 데이터를 삭제

## DCL (Data Control Language)
- 데이터 제어어
- DB, Table의 접근권한이나 CRUD 권한을 정의
- 특정 사용자에게 테이블의 검색권한 부여/금지 등.
- SQL문
    - `grant` - 데이터베이스 객체에 권한을 부여
    - `revoke` - 데이터베이스 객체 권한 취소

## TCL (Transaction Control Language)
- 트랜잭션 제어어
    - transaction이란 데이터베이스의 논리적 연산 단위
- SQL문
    - `commit` - 실행한 Query를 최종적으로 적용
    - `rollback` - 실행한 Query를 마지막 commit 전으로 취소시켜 데이터를 복구

## DML - SELECT
- 데이터를 조회할 때 사용
- 구조
```sql
select {ALL | DISITINCT} * | column | expression AS alias ...
from table_name;
```
- 키워드
    - `*` - FROM 절에 나열된 테이블에서 모든 열을 선택
    - `ALL` - 선택된 모든 행을 반환, 생략가능
    - `DISTINCT` - 선택된 모든 행 중에서 중복 행 제거
    - `column` - FROM 절에 나열된 테이블에서 지정된 열을 선택
    - `expression` - 표현식은 값으로 인식되는 하나 이상의 값, 연산자 및 SQL 함수의 조합을 뜻함
    - `alias` - 별칭
- `where` 절 키워드
    - `IN (조건1, 조건2, 조건3)` - 주어지는 조건의 나열에 해당하는 것이 하나라도 있으면 뽑아냄
    - `BETWEEN 조건1 and 조건2` - 조건1부터 조건2사이를 만족하면 뽑아냄
    - `IS NULL`, `IS NOT NULL` - null인 것, null이 아닌 것 (`column = null` 이런식으로 사용 불가 -> `column IS NULL`)
    - `LIKE (wild card: 5, _)` - 특정 키워드가 포함된 문자열을 뽑아냄
- `order by column [asc | desc], column2...`
    - 컬럼을 기준으로 정렬함 (asc - 오름차순 (디폴트), desc - 내림차순)
    - `limit 시작인덱스, 개수` - 갯수를 몇개만 가져옴
    - `limit 개수` - 개수를 몇개만 가져옴

## 내장함수
- MYSQL 내장함수
    - 숫자 관련 함수
        - `ABS(숫자)` - 절대값
        - `CEILING(숫자)` - 값보다 큰 정수 중 가장 작은 수
        - `FLOOR(숫자)` - 값보다 작은 정수 중 가장 큰 수
        - `ROUND(숫자, 자릿수)` - 숫자를 자릿수를 기준으로 반올림
        - `TRUNCATE(숫자, 자릿수)` - 숫자를 자릿수를 기준으로 버림
        - `POW(X, Y) or POWER(X, Y)` - X의 Y승
        - `MOD(분자, 분모)` - 분자를 분모로 나눈 나머지
        - `GREATEST(숫자1, 숫자2, 숫자3, ...)` - 주어진 수에서 가장 큰 수를 반환
        - `LEAST(숫자1, 숫자2, 숫자3, ...)` - 주어진 수에서 가장 작은 수를 반환
    - 문자 관련 함수
        - `ASCII(문자)` - 문자의 아스키 코드 값 리턴
        - `CONCAT(문자열,문자열,문자열...)` - 문자열들을 결합
        - `INSERT(문자열, 시작위치, 길이, 새로운 문자열)` 문자열의 시작위치부터 길이만큼 새로운 문자열로 대치
        - `REPLACE(문자열, 기존문자열, 바뀔 문자열)` - 문자열 중 기존 문자열을 바뀔 문자열로 변경
        - `RPAD(문자열, 바꾸는 자리수, 채울 문자열)` - 왼쪽에 특정 문자를 원하는 자리수만큼 채워서 반환
        - `LPAD(문자열, 바꾸는 자리수, 채울 문자열)` - 오른쪽에 특정 문자를 원하는 자리수만큼 채워서 반환
        - `INSTR(문자열, 찾는 문자열)` - 문자열 중 찾는 문자열의 위치 값을 리턴
        - `MID(문자열, 시작위치, 개수)` - 문자열 중 시작위치부터 개수만큼 리턴
        - `SUBSTRING(문자열, 시작위치, 개수)` - 문자열 중 시작위치부터 개수만큼 리턴
        - `LTRIM(문자열)` - 문자열 중 왼쪽의 공백을 제거
        - `RTRIM(문자열)` - 문자열 중 오른쪽의 공백을 제거
        - `TRIM(문자열)` - 양쪽 모두의 공백을 제거
        - `LCASE(문자열) OR LOWER(문자열)` - 모든 문자를 소문자로 변경
        - `UCASE(문자열) OR UPPER(문자열)` - 모든 문자를 대문자로 변경
        - `LEFT(문자열, 개수)` - 문자열 중 왼쪽에서 개수만큼 추출
        - `RIGHT(문자열, 개수)` - 문자열 중 오른쪽에서 개수만큼 추출
        - `REVERSE(문자열)` - 문자열을 반대로 나열
    - 날짜 관련 함수
        - `NOW()` OR `SYSDATE()` OR `CURRENT_TIMESTAMP()` - 현재 날짜와 시간 리턴
        - `CURDATE()` OR `CURRENT_DATE()` - 현재 날짜 리턴
        - `CURTIME()` OR `CURRENT_TIME()` - 현재 시간 리턴
        - `DATE_ADD(날짜, INTERVAL 기준 값)` - 날짜에서 기준 값만큼 더한다.
        - `DATE_SUB(날짜, INTERVAL 기준 값)` - 날짜에서 기준 값만큼 뺀다.
        - `YEAR(날짜)` - 날짜의 연도 리턴
        - `MONTH(날짜)` - 날짜의 월 리턴
        - `MONTHNAME(날짜)` - 날짜의 월을 영어로 리턴.
        - `DAYNAME(날짜)` - 날짜의 요일을 영어로 리턴.
        - `DAYOFMONTH(날짜)` - 날짜의 월별 일자 리턴
        - `DAYOFWEEK(날짜)` - 날짜의 주별 일자 리턴.
        - `WEEKDAY(날짜)` - 날짜의 주별 일자 리턴
        - `DAYOFYEAR(날짜)` - 일년을 기준으로 한 날짜까지의 일 수.
        - `WEEK(날짜)` - 일년 중 몇 번째 주.
        - `FROM_dAYS(날수)` - 00년 00월 00일부터 날수 만큼 경과한 날의 날짜 리턴 ★
        - `TO_DAYS(날짜)` - 00년 00월 00일부터 날짜까지의 일자 수 리턴.
        - `DATE_FORMAT(날짜, 형식)` - 날짜를 형식에 맞게 리턴.
        - `DATEDIFF(날짜, 기준날짜)` - 기준날짜로부터 날짜가 몇일이 지났는지 리턴.
    - 논리 관련 함수
        - `IF(논리식, 값1, 값2)` - 논리식이 참이면 리턴, 가짓이면 값2 리턴.
        - `IFNULL(값1, 값2)` - 값1이 NULL이면 값2로 대치, NULL이 아니면 값1 리턴
        - `NULLIF(값1, 값2)` - 값1 = 값2이 TRUE이면 NULL이 그렇지 않으면 값1이 리턴
    - 그룹 함수
        - `COUNT(필드명)` - NULL 값이 아닌 레코드 수를 리턴
        - `SUM(필드명)` - 필드명에 해당하는 레코드 값의 합계를 리턴
        - `AVG(필드명)` - 각각의 그룹 안에서 필드명에 해당하는 레코드 값의 평균을 리턴
        - `MAX(필드명)` - 필드명에 해당하는 레코드 값 중 최대값을 리턴
        - `MIN(필드명)` - 필드명에 해당하는 레코드 값 중 최소값을 리턴

## Transaction
- MYSQL Transaction
    - 트랜잭션 - 데이터베이스의 상태를 변화시키는 일종의 작업 단위를 의미
    - 트랜잭션 도구
        - `START TRANSACTION` - COMMIT, ROLLBACK이 나올 때까지 실행되는 모든 SQL.
        - `COMMIT` - 모든 코드를 실행
        - `ROLLBACK` - `START TRANSACTION` 실행 전 상태로 되돌림
        - `SAVEPOINT` - 롤백할 시점을 저장함