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

## 자잘한 사실
- SQL에서 문자열의 인덱스는 1부터 시작한다
- 하지만 `limit`절에서 데이터 목록을 뽑아올때는 0부터 시작한다 주의!

## Join
- 둘 이상의 테이블에서 데이터가 필요한 경우 조인을 사용
- 일반적으로 조인 조건을 포함하는 where 절을 작성해야 함
- 종류
    - `INNER JOIN`
        - 가장 일반적인 JOIN의 종류이며 교집합
        - 동등 조인(`EQUI-JOIN`)이라고도 하며, N개의 테이블 조인 시 N-1개의 조인 조건이 필요
        - `ON`을 이용한 조건 지정
        - `USING`을 이용한 조건 지정
            - 형식
                ```sql
                select col1, col2, ...
                from table1 join table2
                using (공통column); 
                -- using절에서는 table이름이나 alias를 명시면 에러
                ```
    - `OUTER JOIN`
        - 어느 한쪽 테이블에는 해당하는 데이터가 존재하는데 다른 쪽 테이블에는 데이터가 존재하지 않을 경우 그 데이터가 검색되지 않는 문제점을 해결하기 위해 사용
        - `LEFT OUTER JOIN`
            - 왼쪽 테이블을 기준으로 JOIN 조건에 일치 하지 않는 데이터까지 출력
        - `RIGHT OUTER JOIN`
            - 오른쪽 테이블을 기준으로 JOIN 조건에 일치 하지 않는 데이터까지 출력
        - `FULL OUTER JOIN`
            - 양쪽 테이블을 기준으로 JOIN 조건에 일치 하지 않는 데이터까지 출력
            - MYSQL은 지원하지 않음
    - `SELF JOIN`
        - 같은 테이블끼리 JOIN
    - `NONE-EQUI JOIN`
        - table의 PK, FK가 아닌 일반 column을 JOIN 조건으로 지정
- JOIN 조건의 명시에 따른 구분
    - `NATURAL JOIN`
        - 동일한 타입과 이름을 가진 컬럼을 조인 조건으로 이용하는 방법
        - 반드시 두 테이블 간의 동일한 이름, 타입을 가진 컬럼이 필요
        - 조인에 이용되는 컬럼은 명시하지 않아도 자동으로 조인에 사용
    - `CROSS JOIN`(`FULL JOIN`, `CARTESIAN JOIN`)
- JOIN시 주의
    - 조인의 처리는 어느 테이블을 먼저 읽을지를 결정하는 것이 중요
    - `INNER JOIN` - 어느 테이블을 먼저 읽어도 결과가 달라지지 않아 MySQL 옵티마이저가 조인의 순서를 조절해서 다양한 방법으로 최적화를 수행할 수 있다.
    - `OUTER JOIN` - 반드시 OUTER가 되는 테이블을 먼저 읽어야 하므로 옵티마이저가 조인 순서를 선택할 수 없다.

## SUBQUERY
- 서브 쿼리란 다른 쿼리 내부에 포함되어 있는 SELECT문을 의미
- 서브 쿼리를 포함하고 있는 쿼리를 외부 쿼리(`OUTER QUERY`) 또는 메인 쿼리라고 부르며, 서브 쿼리는 내부 쿼리(`INNER QUERY`)라고도 부른다.
- 서브 쿼리는 비교 연산자의 오른쪽에 기술해야 하고 반드시 괄호로 감싸져 있어야만 한다.
- 종류
    - 중첩 서브 쿼리 (`Nested Subquery`) - where문에 작성하는 서브 쿼리
        - 단일 행
        - 복수 행
        - 다중 컬럼
            - 서브 쿼리의 결과가 다중행을 리턴
                - `IN` - 검색된 값 중에 하나만 일치하면 참
                - `ANY` - 검색된 값 중에 조건에 맞는 것이 하나 이상 있으면 참
                - `ALL` - 모든 검색된 값과 조건에 맞아야 한다.
    - 인라인 뷰 - from 문에 작성하는 서브 쿼리
        - FROM절에 사용되는 서브 쿼리를 인라인 뷰라 한다.
        - 서브 쿼리가 FROM절에 사용되면 뷰처럼 결과가 동적으로 생성된 테이블로 사용 가능.
        - 임시적인 뷰이기 때문에 데이터베이스에는 저장되지 않는다.
        - 동적으로 생성된 테이블이기 때문에 COLUMN을 자유롭게 참조 가능.
    - 스칼라 서브 쿼리(Scalar Subquery) - select문에 작성하는 서브 쿼리
        
- 주의 사항
    - 서브 쿼리는 반드시 `( )`로 감싸야 한다.
    - 서브 쿼리는 단일 행 또는 다중 행 비교 연산자와 함께 사용된다.
- 사용 가능한 곳
    - SELECT
    - FROM
    - WHERE
    - HAVING
    - ORDER BY
    - INSERT문의 VALUES
    - UPDATE문의 SET