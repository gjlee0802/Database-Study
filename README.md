# Database-Study

# SQL(Structured Query Language)
데이터베이스에 저장된 데이터를 조회, 입력, 수정 삭제하는 등의 조작이나, 테이블을 비롯한 다양한 객체(시퀀스. 인덱스 등)를 생성 및 제어하는 역할을 합니다. 

## 유용한 자료
SQL Cheat Sheet: https://www.sqltutorial.org/sql-cheat-sheet/   
실제 데이터로 쿼리를 사용하는 실습: https://www.w3schools.com/sql/trysql.asp?filename=trysql_select_all   

## SQL 문법 해석 우선순위
- SELECT column_name(s) : 5   
- FROM table_name : 1   
- WHERE condition : 2   
- GROUP BY column_name(s) : 3   
- HAVING condition : 4   
- ORDER BY column_name(s) : 6   

## SQL의 종류
- 데이터 정의어(DDL)   
데이터베이스 관리자나 응용 프로그래머가 데이터베이스의 논리적 구조를 정의하기 위한 언어로서 데이터 사전(Data Dictionary)에 저장 됩니다.   
- 데이터 조작어(DML)   
데이터베이스에 저장된 데이터를 조작하기 위해 사용하는 언어로서 데이터 검색(Retrieval), 추가(Insert), 삭제(Delete), 갱신(Update) 작업 수행 합니다.   
- 데이터 제어어(DCL)   
데이터에 대한 접근 권한 부여 등의 데이터베이스 시스템의 트랜잭션을 관리하기 위한 목적으로 사용되는 언어입니다.   

DQL: SELECT   
DML: INSERT, UPDATE, DELETE   
DDL: CREATE, ALTER, DROP, RENAME, TRUNCATE   
TCL: COMMIT, ROLLBACK, SAVEPOINT   
DCL: GRANT, REVOKE   

## 제약조건(CONSTRAINT)
=> 데이터 무결성 제약 조건(Data Integrity Constraint Rule)이란 테이블에 부적절한 자료가 입력되는 것을 방지하기 위해서 테이블을 생성할 때 각 컬럼에 대해서 정의하는 여러 가지 규칙

### 제약조건 종류
NOT NULL:  NULL을 허용하지 않는다.   
UNIQUE: 중복된 값을 허용하지 않는다. 항상 유일한 값   
PRIMARY KEY: NULL을 허용하지 않고 중복된 값을 허용하지 않는다.   
NOT NULL: 조건과 UNIQUE 조건을 결합한 형태   
FOREIGN KEY: 부모 테이블의 참조되는 칼럼 값이 존재하면 허용   
CHECK: 저장 가능한 데이터 값의 범위나 조건을 지정하여 설정한 값만을 허용   

### 외래키 제약조건 설정 시 사용하는 ON DELETE CASCADE 옵션
부모테이블의 행이 삭제되면 자식 테이블의 행도 삭제된다. 

## 트랜잭션 (Transaction)
데이터 처리의 한 단위입니다.   
오라클에서 발생하는 여러 개의 SQL 명령문들을 하나의 논리적인 작업 단위로 처리하는데 이를 트랜잭션이라고 합니다.  하나의 트랜잭션은 All-OR-Nothing 방식으로 처리   
여러 개의 명령어의 집합이 정상적으로 처리되면 정상 종료하도록 하고 여러 개의 명령어 중에서 하나의 명령어라도 잘못되었다면 전체를 취소해버립니다.   
데이터의 일관성을 유지하면서 안정적으로 데이터를 복구시키기 위해서 사용.   
### TCL (Transaction Control Language)  
트랜잭션 제어를 위한 명령어(Transaction Control Language)   

## 데이터 딕셔너리 (Data Dictionary)
관계형 데이터베이스에서 객체를 정의하게 되면 그 객체가 가진 메타데이터(객체에 대한 정보들-예를들면 테이블 객체일 경우 컬럼, 도메인 및 제약조건에 대한 내용) 의 정보가 저장되는 시스템 테이블
데이터 딕셔너리는 사용자가 테이블을 생성하거나 사용자를 변경하는 등의 작업을 할 때 데이터베이스 서버에 의해 자동으로 갱신되는 테이블로 사용자는 데이터 딕셔너리의 내용을 직접 수정하거나 삭제할 수 없습니다.   
오라클은 사용자가 이해할 수 있는 데이터를 산출해 줄 수 있도록 하기 위해서 데이터 딕셔너리에서 파생한 데이터딕셔너리 뷰를 제공   

## VIEW  
논리적인 가상 테이블   
실제 테이블에 저장된 데이터를 뷰를 통해서 볼 수 있도록 합니다.   
사용자에게 주어진 뷰를 통해서 기본 테이블을 제한적으로 사용하게 됩니다.   
뷰는 이미 존재하고 있는 테이블에 제한적으로 접근하도록 합니다.   
뷰를 생성하기 위해서는 실질적으로 데이터를 저장하고 있는 물리적인 테이블이 존재해야 하는데 이 테이블을 기본 테이블이라고 합니다.  데이터를 물리적으로 저장하고 있지 않습니다.   
> View 테이블을 쓰는 이유: 복잡하고 긴 쿼리문을 뷰로 정의하면 접근을 단순화시킬 수 있다. 보안에 유리하다.   

## Set Operator  
두 개 이상의 쿼리 결과를 하나로 결합하는 연산자   
여러 개의 select 문을 하나로 연결한다.   
집합 연산자로 결합되는 결과의 컬럼은 데이터 타입이 동일해야한다.   
- union: 합집합, 결합시키는 두 테이블의 중복 데이터는 제거   
- union all: 결합시키는 두 테이블의 중복 데이터까지 반환   
- intersect: 여러개의 sql문의 결과에 대한 교집합을 나타내고 중복 행은 하나의 결과로 보여준다.   
- minus 여러개의 sql문의 결과에 대한 차집합을 나타내고 중복행은 하나의 결과로 보여준다.   

## 조인문 (JOIN)
 > https://kosaf04pyh.tistory.com/287   

한 개 이상의 테이블에서 데이터를 조회하기 위해 사용되는 것을 조인이라고 한다.   
Equi Join 동일 칼럼을 기준으로 조인합니다.   
Non-Equi Join 동일 칼럼이 없이 다른 조건을 사용하여 조인합니다.   
Outer Join 조인 조건에 만족하지 않는 행도 나타낸다.   
Self Join 한 테이블 내에서 조인합니다.   


## Graph DB
https://couplewith.tistory.com/entry/Graph-DB-%EC%99%80-RDBMS-%ED%8A%B8%EB%9E%9C%EB%93%9C-3%EB%B6%80-%EA%B7%B8%EB%9E%98%ED%94%84-%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%EC%9D%98-%EC%A2%85%EB%A5%98
