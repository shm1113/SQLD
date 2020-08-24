

## Nologging

>   -   데이터베이스에 데이터를 입력하면 로그파일에 그정보를 기록한다
>   -   Check Point라는 이벤트가 발생하면 로그파일의 데이터를 데이터 파일에 저장한다
>   -   Nologging옵션은 로그파일의 기록을 최소화 시켜서 입력 시 성능을 향상시키는 방법이다
>   -   Nologging 옵션은 Buffer Cache라는 메모리 영역을 생략하고 기록한다



## 테이블 데이터 삭제

>   ### DELETE FROM 테이블명
>
>   -   테이블의 모든 데이터를 삭제한다
>   -   데이터가 삭제되어도 테이블의 용량은 감소하지 않는다
>
>   ### TRUNCATE TABLE 테이블명
>
>   -   테이블의 모든 데이터를 삭제한다
>   -   데이터가 삭제되면 테이블의 **용량은 초기화 된다**



:book: Order by가 정렬하는 시점은 모든 실행이 끝난 후에 데이터를 출력해 주기 바로 전이다.

:book:기본키는 자동으로 오름차순 인덱스가 생성된다

:book: 인덱스 칼럼에 형변환을 수행하면 인덱스를 사용하지 못한다(예외적인 것도 있다)



## NULL함수

| NULL함수   | 설명                                                         |
| ---------- | ------------------------------------------------------------ |
| NVL함수    | - NULL이면 다른 값으로 바꾸는 함수이다<br />-'NVLL(MGR,0)'은 MGR이 NULL이면 0으로 바꾼다 |
| NVL2함수   | -NVL함수와 DECODE함수를 하나로 만든 것이다<br />-'NVL(MGR,1,0)' 은 MGR컬럼이 NULL이 아니면 1을, NULL이면 0을 반환한다 |
| NULLIF함수 | -두 개의 값이 같으면 NULL을, 같지 않으면 첫 번째 값을 반환한다<br />-'NULLIF(exp1,exp2)' 은 exp1과 exp2가 같으면 NULL을, 같지 않으면 exp11을 반환한다 |
| COALESCE   | -NULL이 아닌 최초의 인자 값을 반환한다<br />-'COALESCE(exp1,exp2,exp3...)'은 ex1이 NULL이 아니면 exp1의 값을, 그렇지 않으면 그 뒤에 값의 NULL 여부를 판닪하여 값을 반환한다 |



## 집계함수

| 집계함수      | 설명                       |
| ------------- | -------------------------- |
| COUNT()       | 행 수를 조회한다           |
| SUM()         | 합계를 계산한다            |
| AVG()         | 평균을 계산한다            |
| MAX()와 MIN() | 최댓값과 최솟값을 계산한다 |
| STDDEV()      | 표준편차를 계산한다        |
| VARIAN()      | 분산을 계산한다            |



## 날짜형 함수

| 날짜형 함수                               | 설명                                 |
| ----------------------------------------- | ------------------------------------ |
| SYSDATE                                   | 오늘의 날짜를 날짜 타입으로 알려준다 |
| EXTRACT('YEAR'\|'MONTH'\|'DAY' from dual) | 날짜에서 년,월,일을 조회한다         |



## 숫자형 함수

| 숫자형 함수        | 설명                                                         |
| ------------------ | ------------------------------------------------------------ |
| ABS(숫자)          | 절댓값을 돌려준다                                            |
| SIGN(숫자)         | 양수,음수,0을 구별한다                                       |
| MOD(숫자1,숫자2)   | -숫자1을 숫자2로 나누어 나머지를 계산한다<br />-%를 사용해도 된다 |
| CEIL/CEILING(숫자) | 숫자보다 크거나 같은 최소의 정수를 돌려준다                  |
| FLOOR()            | 숫자보다 작거나 같은 최대의 정수를 돌려준다                  |
| ROUND(숫자,m)      | -소수점 m  자리에 반올림한다<br />-m의 기본값(Default Value)은 0이다 |
| TRUNC(숫자,m)      | -소수점 m 자리에서 절삭한다<br />-m의 기본값(Default Value)은 0이다 |



## DECODE  (=IF문)

>   EMPNO와 1000이 같으면 TRUE 다르면 FALSE를 리턴한다

```mysql
DECODE(EMPNO,1000,'TRUE','FALSE')
```



## CASE문

>   CASE문은 IF~THEN~ELSE -END의 프로그램 언어처럼 조건문을 사용할 수 있다.
>
>   조건을 WHEN구에 사용하고 THEN은 해당 조건이 참이면 실행되고 거짓이면 ELSE구가 실행된다

```mysql
CASE [expression]
	WHEN condition_1 THEN result_1
	WHEN condition_2 THEN result_2
	...
	WHEN condition_n THEN result_n
	ELSE result
END
```



## SELECT 문 실행 순서

1.  FROM
2.  WHERE
3.  GROUP BY
4.  HAVING
5.  SELECT
6.  ORDER BY



## 문자열 함수

| 문자열 함수              | 설명                                                         |
| ------------------------ | ------------------------------------------------------------ |
| ASCII(문자)              | 문자 혹은 숫자를 ASCII 코드값으로 변환한다                   |
| CHAR(ASCII 코드값)       | ASCII 코드값을 문자로 변환한다                               |
| SUBSTR(문자열,m,n)       | 문자열에서 m번째 위치부터 n개를 자른다                       |
| CONCAT(문자열1,문자열2)  | -문자열1번과 문자열2번을 결합한다.<br />_Oracle은 '\|\|',MS-SQL은 '+'를 사용할 수 있다. |
| LOWER(문자열)            | 영문자를 소문자로 변환한다                                   |
| UPPER(문자열)            | 영문자를 대문자로 변환한다                                   |
| LENGTH 혹은 LEN(문자열)  | 공백을 포함해서 문자열의 길이를 알려준다                     |
| LTRIM(문자열,지정문자)   | -왼쪽에서 지정된 문자를 삭제한다<br />-지정된 문자를 생략하면 공백을 삭제한다 |
| RTRIM(문자열,지정문자)   | -오른쪽에서 지정된 문자를 삭제한다<br />-지정된 문자를 생략하면 공백을 삭제한다 |
| TRIM(문자열,지정된 문자) | -왼쪽 및 오른쪽에서 지정된 문자를 삭제한다<br />-지정된 문자를 생략하면 공백을 삭제한다 |



## 인라인뷰(inline view)

>   SELECT문에서 FROM절에 사용되는 서브쿼리(Sub Query)를 의미한다



## ROWNUM과 ROWID

>   ### ROWNUM
>
>   -   ROWNUM은 ORACLE 데이터베이스의 SELECT문ㅇ 결과에 대해서 논리적인 일련번호를 부여한다
>
>   -   ROWNUM은 조회되는 행 수를 제한할 떄 많이 사용된다
>
>   -   ROWNUM은 화면에 데이터를 출력할 때 부여되는 논리적 순번이다. 만약 ROWNUM을 사용해서 페이지 단위 출력을 하기 위해서는 인라인 뷰(Inline view)를 사용해야 한다
>
>       #### SQL Server의 TOP구문과 MYSQL의 limit 구문
>
>       -   Oracle은 ROWNUM을 사용하지만, SQL Server는 TOP문을 사용하고 MySQL은 LIMIT구를 사용한다. 즉 10명만 인출(Fetch)하고자 할 떄에는 다음과 같이 사용한다
>
>           ```mssql
>           --SQL Server
>           SELECT TOP(10) FROM EMP;
>           --MySQL
>           SELECT * FROM EMP LIMIT10;
>           ```
>
>           
>
>   ### ROWID
>
>   -   ROWID는 ORACLE 데이터베이스 내에서 데이터를 구분할 수 있는 유일한 값이다
>   -   ROWID는 "SELECT ROWID,EMPNO FROM EMP" 와 같은 SELECT문으로 확인할 수 있다
>   -   ROWID를 통해서 데이터가 어떤 데이터파일,어느 블록에 저장되어 있는 지 알 수 있다.
>
>   | 구조           | 길이  | 설명                                                         |
>   | -------------- | ----- | ------------------------------------------------------------ |
>   | 오브젝트 번호  | 1~6   | 오브젝트(Object)별로 유일한 값을 가지고 있으며 해당 오브젝트가 속해 있는 값이다. |
>   | 상태 파일 번호 | 7~9   | 테이블스페이스(Tablespace)에 속해 있는 데이터 파일에 대한 상대 파일번호이다. |
>   | 블록 번호      | 10~15 | 데이터 파일 내부에서 어느 블록에 데이터가 있는지 알려준다    |
>   | 데이터 번호    | 16~18 | 데이터 블록에 데이터가 저장되어 있는 순서를 의미한다         |



## WITH구문

>   WITH구문은 서브쿼리(Subquery)를 사용해서 임시 테이블이나 뷰처럼 사용할 수 있는 구문이다
>
>   서브쿼리 블록에 별칭을 지정할 수 있다.
>
>   옵티마이저는 SQL을 인라인 뷰나 임시 테이블로 판단한다
>
>   ```mssql
>   WITH viewData AS
>   (SELECT * FROM EMP
>   	UNION ALL
>    SELECT * FROM EMP)
>    SELECT * FROM viewData WHERE EMPNO=1000;
>   ```





## GRANT

>   ### GRANT문
>
>   ```mssql
>   GRANT 권한 ON 테이블 TO 유저
>   ```
>
>   ### Privileges(권한)
>
>   | 권한       | 설명                                                         |
>   | ---------- | ------------------------------------------------------------ |
>   | SELECT     | SELECT권한                                                   |
>   | INSERT     | INSERT권한                                                   |
>   | UPDATE     | UPDATE권한                                                   |
>   | DELETE     | DELETE권한                                                   |
>   | REFERENCES | 지정된 테이블을 참조하는 제약조건을 생성하는 권한을 부여한다 |
>   | ALTER      | 지정된 테이블에 대해서 수정할 수 있는 권한을 부여한다        |
>   | INDEX      | 지정된 테이블에 대해서 인덱스를 생성할 수 있는 권한을 부여한다 |
>   | ALL        | 테이블에 대한 모든 권한을 부여한다                           |
>
>   
>
>   ### WITH GRANT OPTION
>
>   | GRANT 옵션        | 설명                                                         |
>   | ----------------- | ------------------------------------------------------------ |
>   | WITH GRANT OPTION | -특정 사용자에게 권한을 부여할 수 있는 권한을 부여한다<br />-권한을 A 사용자가 B에 부여하고 B가 다시 C를 부여한 후에 권한을 취소(Revoke)하면 모든 권한이 회수된다 |
>   | WITH ADMIN OPTION | -테이블에 대한 모든 권한을 부여한다<br />-권한을 A 사용자가 B에 부여하고 B가 다시 C에게 부여한 후에 권한을 취소(Revoke)하면 B사용자 권한만 취소된다 |



## REVOKE

>   사용자에게 부여된 권한을 회수한다
>
>   ```mssql
>   REVOKE 권한 ON 테이블 FROM 유저
>   ```



# TCL(Transaction Control Language)

>   ## COMMIT
>
>   -   COMMIT시 변경 전 이전 데이터는 잃어버린다. 즉, A값을 B로 변경하고 COMMIT을 하면 A값은 잃어버리고 B 값을 반영한다
>   -   다른 모든 데이터베이스 사용자는 변경된 데이터를 볼 수 있다
>   -   COMMIT이 완료되면 데이터베이스 변경으로 인한 LOCK이 해제(UNLOCK)된다.
>   -   COMMIT이 완료되면 다른 모든 데이터베이스 사용자는 변경된 데이터를 조작할 수 있다
>   -   COMMIT을 실행하면 하나의 트랜잭션 과정을 종료한다
>
>   **:book: Oracle 데이터베이스는 암시적-트랜잭션-관리를 한다 즉, Oracle 데이터베이스로 트랜잭션을 시작하고 트랜잭션의 종료는 Oracle 데이터베이스 사용자가 COMMIT 혹은 ROLL-BACK으로 처리해야 한다.** 
>
>   ##### :book: Auto commit 하는법  : "set autocommit on;"을 SQL*PLUS에서 실행하면 자동으로 COMMIT된다
>
>   ```mysql
>   commit;
>   ```
>
>    
>
>   ## ROLLBACK
>
>   -   ROLLBACK을 실행하면 데이터에 대한 변경 사용을 모두 취소하고 트랜잭션을 종료한다
>   -   INSERT, UPDATE , DELETE문의 작업을 모두 취소한다 단, 이전에 COMMIT한 곳까지만 복구한다.
>   -   ROLLBACK을 실행하면 LOCK이 해제되고 다른 사용자도 데이터베이스 행을 조작할 수 있다.
>
>   ```mysql
>   rollback;
>   ```
>
>   
>
>   
>
>   ## SAVEPOINT(저장점)
>
>   -   SAVEPOINT는 트랜잭션을 작게 분할하여 관리하는 것으로 SAVEPOINT를 사용하면 지정된 위치 이후의 트랜잭션만 ROLLBACK할 수 있다.
>
>   -   **SAVEPOINT의 지정**
>
>       -    SAVEPOINT <SAVEPOINT명>
>
>   -   ##### 지정된 SAVEPOINT까지만 데이터 변경을 취소하고 싶은 경우
>
>       -   ROLLBACK TO <SAVEPOINT명>
>
>   -   ROLLBACK을 실행하면 SAVEPOINT와 관계없이 데이터의 모든 변경사항을 저장하지 않는다 
>
>   ```mssql
>   update emp et ename='조조' where empno=1001;
>   select ename from emp where empno=1001;
>   rollback;
>   
>   
>   update emp et ename='조조' where empno=1001;
>   savepoint t1;
>   update emp set ename='관우' where empno=1003;
>   savepoint t2;
>   rollback to t2;  --savepoint t2까지 변경된 것을 최소한다 
>   ```
>
>   



