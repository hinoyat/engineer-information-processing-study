## 🔹 230. DDL (Data Definition Language)

#### 📘 정의
**DDL(Data Definition Language)**은 데이터베이스의 **구조와 스키마를 정의하고 관리**하는 SQL 언어로, 테이블, 뷰, 인덱스 등 데이터베이스 객체의 **생성, 수정, 삭제** 작업을 수행한다.

#### 🧩 주요 특징
- 데이터베이스 구조 변경 시 **즉시 반영** (AUTO COMMIT)
- **ROLLBACK 불가능**한 명령어들
- 스키마 정의 및 데이터 저장 공간 할당
- 데이터베이스 객체의 생명주기 관리

#### 🧩 DDL 명령어 종류

| 명령어 | 기능 | 예시 |
|--------|------|------|
| **CREATE** | 데이터베이스 객체 생성 | CREATE TABLE, CREATE VIEW |
| **ALTER** | 기존 객체 구조 수정 | ALTER TABLE ADD COLUMN |
| **DROP** | 객체 완전 삭제 | DROP TABLE, DROP INDEX |
| **TRUNCATE** | 테이블 데이터 전체 삭제 | TRUNCATE TABLE 테이블명 |

#### 📝 기출 포맷 예시
- DDL의 특징으로 옳지 않은 것은?
- 다음 중 DDL에 해당하는 명령어는?
- DDL과 DML의 차이점을 설명하시오.

#### 🧠 용어 설명
- **DDL**: 데이터베이스 구조 정의 언어
- **AUTO COMMIT**: 명령 실행 즉시 데이터베이스에 반영
- **스키마**: 데이터베이스의 논리적 구조 정의

---

## 🔹 231. CREATE TABLE

#### 📘 정의
**CREATE TABLE**은 새로운 테이블을 생성하는 DDL 명령어로, **테이블명, 컬럼명, 데이터타입, 제약조건**을 지정하여 데이터베이스에 테이블 구조를 정의한다.

#### 🧩 기본 구문
```sql
CREATE TABLE 테이블명 (
    컬럼명1 데이터타입 [제약조건],
    컬럼명2 데이터타입 [제약조건],
    ...
    [테이블레벨 제약조건]
);
```

#### 🧩 주요 데이터타입

| 데이터타입 | 설명 | 예시 |
|------------|------|------|
| **CHAR(n)** | 고정길이 문자열 | CHAR(10) |
| **VARCHAR(n)** | 가변길이 문자열 | VARCHAR(50) |
| **INT, INTEGER** | 정수형 | INT |
| **NUMBER(p,s)** | 숫자형 (전체자릿수,소수점) | NUMBER(10,2) |
| **DATE** | 날짜형 | DATE |

#### 🧩 제약조건 종류

| 제약조건 | 설명 | 사용법 |
|----------|------|--------|
| **PRIMARY KEY** | 기본키 (중복X, NULL X) | 컬럼명 PRIMARY KEY |
| **FOREIGN KEY** | 외래키 (다른 테이블 참조) | FOREIGN KEY REFERENCES |
| **NOT NULL** | NULL 값 불허 | 컬럼명 NOT NULL |
| **UNIQUE** | 중복값 불허 | 컬럼명 UNIQUE |
| **CHECK** | 조건 검사 | CHECK (조건식) |
| **DEFAULT** | 기본값 설정 | 컬럼명 DEFAULT 값 |

#### 🧩 외래키 삭제 옵션 (ON DELETE)

| 옵션 | 설명 | 동작 방식 |
|------|------|-----------|
| **NO ACTION** | 삭제 방지 (기본값) | 참조되는 데이터 삭제 시 오류 발생 |
| **CASCADE** | 연쇄 삭제 | 부모 데이터 삭제 시 자식 데이터도 함께 삭제 |
| **SET NULL** | NULL로 설정 | 부모 데이터 삭제 시 외래키를 NULL로 변경 |
| **SET DEFAULT** | 기본값으로 설정 | 부모 데이터 삭제 시 외래키를 DEFAULT 값으로 변경 |

```sql
-- 외래키 삭제 옵션 예시
FOREIGN KEY (학과코드) REFERENCES 학과(학과코드) ON DELETE CASCADE;
FOREIGN KEY (학과코드) REFERENCES 학과(학과코드) ON DELETE SET NULL;
FOREIGN KEY (학과코드) REFERENCES 학과(학과코드) ON DELETE NO ACTION;
```

#### 🧩 실제 예시
```sql
CREATE TABLE 학생 (
    학번 CHAR(10) PRIMARY KEY,
    이름 VARCHAR(20) NOT NULL,
    학과 VARCHAR(30),
    학년 INT CHECK (학년 BETWEEN 1 AND 4),
    입학일 DATE DEFAULT SYSDATE
);
```

#### 📝 기출 포맷 예시
- CREATE TABLE 구문에서 제약조건을 추가하는 방법은?
- 다음 중 데이터타입과 용도가 올바른 것은?
- 기본키와 외래키의 차이점을 설명하시오.

#### 🧠 용어 설명
- **제약조건**: 데이터 무결성을 보장하기 위한 규칙
- **기본키**: 테이블에서 각 행을 고유하게 식별하는 컬럼
- **외래키**: 다른 테이블의 기본키를 참조하는 컬럼

---

## 🔹 232. CREATE VIEW

#### 📘 정의
**CREATE VIEW**는 하나 이상의 테이블에서 원하는 컬럼만을 논리적으로 연결하여 만든 **가상 테이블**을 생성하는 명령어이다. 실제 데이터를 저장하지 않고 **질의문 자체를 저장**한다.

#### 🧩 기본 구문
```sql
CREATE VIEW 뷰명 AS
SELECT 컬럼명1, 컬럼명2, ...
FROM 테이블명
[WHERE 조건];
```

#### 🧩 뷰의 특징
- **가상 테이블**: 실제 데이터 저장하지 않음
- **보안성**: 특정 컬럼만 접근 허용 가능
- **독립성**: 논리적 데이터 독립성 제공
- **편의성**: 복잡한 질의를 단순화

#### 🧩 뷰의 장점과 단점

| 장점 | 단점 |
|------|------|
| 논리적 데이터 독립성 제공 | 독립적인 인덱스 생성 불가 |
| 동일 데이터에 대해 다양한 뷰 제공 | 뷰 정의 변경 불가 |
| 사용자의 데이터 관리 단순화 | 삽입/수정/삭제 연산 제약 |
| 접근 제어를 통한 보안성 향상 | |

#### 🧩 실제 예시
```sql
CREATE VIEW 우수학생 AS
SELECT 학번, 이름, 학과
FROM 학생
WHERE 평점 >= 3.5;
```

#### 📝 기출 포맷 예시
- 뷰(View)의 특징으로 옳지 않은 것은?
- CREATE VIEW 구문의 올바른 사용법은?
- 뷰의 장점을 3가지 이상 설명하시오.

#### 🧠 용어 설명
- **뷰(View)**: 실제 테이블로부터 유도된 가상 테이블
- **논리적 독립성**: 응용프로그램과 데이터베이스를 독립시키는 것
- **가상 테이블**: 물리적 저장공간 없이 논리적으로만 존재하는 테이블

---

## 🔹 233. CREATE INDEX

#### 📘 정의
**CREATE INDEX**는 테이블에서 원하는 컬럼에 대해 **색인(Index)**을 생성하는 명령어로, 데이터 검색 속도를 향상시키기 위해 사용된다.

#### 🧩 기본 구문
```sql
-- 일반 인덱스
CREATE INDEX 인덱스명 ON 테이블명 (컬럼명);

-- 유니크 인덱스
CREATE UNIQUE INDEX 인덱스명 ON 테이블명 (컬럼명);

-- 복합 인덱스
CREATE INDEX 인덱스명 ON 테이블명 (컬럼1, 컬럼2);

-- 정렬 순서 지정
CREATE INDEX 인덱스명 ON 테이블명 (컬럼명 ASC);
CREATE INDEX 인덱스명 ON 테이블명 (컬럼명 DESC);

-- 클러스터 인덱스
CREATE CLUSTERED INDEX 인덱스명 ON 테이블명 (컬럼명);
CREATE NONCLUSTERED INDEX 인덱스명 ON 테이블명 (컬럼명);
```

#### 🧩 인덱스의 특징
- **검색 속도 향상**: WHERE, ORDER BY 절에서 성능 개선
- **자동 정렬**: 지정된 컬럼을 기준으로 자동 정렬 유지
- **저장공간 필요**: 별도의 물리적 저장공간 사용
- **갱신 오버헤드**: INSERT, UPDATE, DELETE 시 인덱스도 함께 갱신

#### 🧩 인덱스 종류

| 종류 | 설명 | 특징 |
|------|------|------|
| **UNIQUE INDEX** | 중복값 허용하지 않는 인덱스 | PRIMARY KEY, UNIQUE 제약조건 시 자동 생성 |
| **NON-UNIQUE INDEX** | 중복값 허용하는 인덱스 | 일반적인 검색 성능 향상용 |
| **COMPOSITE INDEX** | 여러 컬럼으로 구성된 인덱스 | 복합 조건 검색 시 효과적 |
| **CLUSTERED INDEX** | 물리적 데이터 순서와 논리적 순서가 같음 | 테이블당 1개만 생성 가능, 검색 속도 빠름 |
| **NONCLUSTERED INDEX** | 물리적 순서와 논리적 순서가 다름 | 테이블당 여러 개 생성 가능 |

#### 🧩 정렬 순서
- **ASC**: 오름차순 정렬 (기본값)
- **DESC**: 내림차순 정렬
- 복합 인덱스에서는 각 컬럼별로 정렬 순서 개별 지정 가능

#### 🧩 실제 예시
```sql
-- 학번에 유니크 인덱스 생성
CREATE UNIQUE INDEX idx_student_no ON 학생(학번);

-- 이름에 일반 인덱스 생성 (오름차순)
CREATE INDEX idx_student_name ON 학생(이름 ASC);

-- 학과와 학년에 복합 인덱스 생성 (내림차순)
CREATE INDEX idx_dept_grade ON 학생(학과 DESC, 학년 ASC);

-- 클러스터 인덱스 생성
CREATE CLUSTERED INDEX idx_clustered ON 학생(학번);

-- 논클러스터 인덱스 생성
CREATE NONCLUSTERED INDEX idx_nonclustered ON 학생(이름);
```

#### 📝 기출 포맷 예시
- 인덱스의 장점과 단점을 설명하시오.
- UNIQUE INDEX와 일반 INDEX의 차이점은?
- 다음 중 인덱스 생성이 필요한 경우는?

#### 🧠 용어 설명
- **인덱스(Index)**: 데이터 검색 속도 향상을 위한 색인 구조
- **복합 인덱스**: 두 개 이상의 컬럼으로 만든 인덱스
- **클러스터 인덱스**: 물리적 데이터 순서와 인덱스 순서가 같은 인덱스

---

## 🔹 234. ALTER TABLE

#### 📘 정의
**ALTER TABLE**은 기존에 생성된 테이블의 구조를 수정하는 DDL 명령어로, **컬럼 추가/삭제/수정, 제약조건 추가/삭제** 등의 작업을 수행한다.

#### 🧩 기본 구문
```sql
-- 컬럼 추가
ALTER TABLE 테이블명 ADD 컬럼명 데이터타입 [제약조건];

-- 컬럼 수정
ALTER TABLE 테이블명 MODIFY 컬럼명 데이터타입;

-- 컬럼 기본값 설정/삭제
ALTER TABLE 테이블명 ALTER 컬럼명 SET DEFAULT 값;
ALTER TABLE 테이블명 ALTER 컬럼명 DROP DEFAULT;

-- 컬럼 삭제
ALTER TABLE 테이블명 DROP COLUMN 컬럼명;

-- 제약조건 추가
ALTER TABLE 테이블명 ADD CONSTRAINT 제약조건명 제약조건;

-- 제약조건 삭제
ALTER TABLE 테이블명 DROP CONSTRAINT 제약조건명;
```

#### 🧩 주요 ALTER TABLE 연산

| 연산 | 설명 | 예시 |
|------|------|------|
| **ADD** | 새로운 컬럼이나 제약조건 추가 | ADD 전화번호 VARCHAR(15) |
| **MODIFY** | 기존 컬럼의 데이터타입이나 크기 변경 | MODIFY 이름 VARCHAR(30) |
| **ALTER** | 컬럼의 기본값 설정/삭제 | ALTER 컬럼명 SET DEFAULT 값 |
| **DROP** | 컬럼이나 제약조건 삭제 | DROP COLUMN 주소 |
| **RENAME** | 컬럼명 변경 | RENAME COLUMN 구명 TO 신명 |

#### 🧩 실제 예시
```sql
-- 학생 테이블에 전화번호 컬럼 추가
ALTER TABLE 학생 ADD 전화번호 VARCHAR(15);

-- 이름 컬럼 크기 변경
ALTER TABLE 학생 MODIFY 이름 VARCHAR(30);

-- 학년 컬럼에 기본값 설정
ALTER TABLE 학생 ALTER 학년 SET DEFAULT 1;

-- 학년 컬럼 기본값 삭제
ALTER TABLE 학생 ALTER 학년 DROP DEFAULT;

-- 주소 컬럼 삭제
ALTER TABLE 학생 DROP COLUMN 주소;

-- 외래키 제약조건 추가
ALTER TABLE 학생 ADD CONSTRAINT fk_dept 
FOREIGN KEY (학과코드) REFERENCES 학과(학과코드);
```

#### 🧩 주의사항
- **데이터 손실 위험**: DROP 연산 시 데이터 완전 삭제
- **데이터타입 제약**: 기존 데이터와 호환되지 않는 타입으로 변경 불가
- **제약조건 충돌**: 기존 데이터가 새 제약조건에 위배되면 실행 불가

#### 📝 기출 포맷 예시
- ALTER TABLE로 수행할 수 있는 작업은?
- 컬럼 삭제 시 주의해야 할 점은?
- 제약조건 추가 구문을 작성하시오.

#### 🧠 용어 설명
- **스키마 변경**: 테이블 구조의 논리적 변경
- **컬럼 추가**: 기존 테이블에 새로운 속성 추가
- **제약조건**: 데이터 무결성을 보장하는 규칙

---

## 🔹 235. DROP

#### 📘 정의
**DROP**은 데이터베이스에서 **테이블, 뷰, 인덱스 등의 객체를 완전히 삭제**하는 DDL 명령어로, 구조와 데이터를 모두 제거한다.

#### 🧩 기본 구문
```sql
-- 스키마 삭제
DROP SCHEMA 스키마명;

-- 도메인 삭제
DROP DOMAIN 도메인명;

-- 테이블 삭제
DROP TABLE 테이블명;

-- 뷰 삭제
DROP VIEW 뷰명;

-- 인덱스 삭제
DROP INDEX 인덱스명;

-- 제약조건 삭제
ALTER TABLE 테이블명 DROP CONSTRAINT 제약조건명;
```

#### 🧩 DROP vs DELETE vs TRUNCATE

| 명령어 | 삭제 범위 | 복구 가능 | 속도 | AUTO COMMIT |
|--------|-----------|-----------|------|-------------|
| **DROP** | 테이블 구조 + 데이터 | 불가 | 빠름 | 예 |
| **TRUNCATE** | 데이터만 (구조 유지) | 불가 | 빠름 | 예 |
| **DELETE** | 데이터만 (구조 유지) | 가능 | 느림 | 아니오 |

#### 🧩 CASCADE 옵션
```sql
-- 참조 관계가 있어도 강제 삭제
DROP TABLE 테이블명 CASCADE;

-- 참조 관계 확인 후 삭제 (기본값)
DROP TABLE 테이블명 RESTRICT;
```

#### 🧩 실제 예시
```sql
-- 대학교 스키마 삭제
DROP SCHEMA 대학교;

-- 학년타입 도메인 삭제
DROP DOMAIN 학년타입;

-- 학생 테이블 완전 삭제
DROP TABLE 학생;

-- 우수학생 뷰 삭제
DROP VIEW 우수학생;

-- 학번 인덱스 삭제
DROP INDEX idx_student_no;

-- 외래키 제약조건 삭제
ALTER TABLE 학생 DROP CONSTRAINT fk_dept;
```

#### 🧩 주의사항
- **복구 불가능**: 한번 삭제하면 ROLLBACK 불가
- **참조 무결성**: 외래키로 참조되는 테이블은 삭제 제약
- **권한 필요**: 객체 소유자 또는 DROP 권한 필요

#### 📝 기출 포맷 예시
- DROP과 DELETE의 차이점을 설명하시오.
- CASCADE 옵션의 역할은?
- 다음 중 복구 가능한 명령어는?

#### 🧠 용어 설명
- **DROP**: 데이터베이스 객체의 완전 삭제
- **CASCADE**: 종속 객체까지 함께 삭제하는 옵션
- **RESTRICT**: 종속 관계가 있으면 삭제를 거부하는 옵션

---

## 🔹 236. DCL (Data Control Language)

#### 📘 정의
**DCL(Data Control Language)**은 데이터베이스에 접근하거나 객체를 사용하도록 **권한을 부여하고 회수**하는 언어로, 데이터베이스의 **보안과 무결성을 제어**하는 역할을 한다.

#### 🧩 주요 특징
- **사용자 권한 관리**: 데이터베이스 객체에 대한 접근 권한 제어
- **보안 강화**: 무단 접근 방지 및 데이터 보호
- **무결성 보장**: 권한 없는 사용자의 데이터 변경 방지
- **동시성 제어**: 트랜잭션 격리 수준 관리

#### 🧩 DCL 명령어 종류

| 명령어 | 기능 | 설명 |
|--------|------|------|
| **GRANT** | 권한 부여 | 사용자에게 데이터베이스 객체 사용 권한 부여 |
| **REVOKE** | 권한 회수 | 사용자로부터 데이터베이스 객체 사용 권한 회수 |
| **COMMIT** | 트랜잭션 확정 | 변경사항을 데이터베이스에 영구 저장 |
| **ROLLBACK** | 트랜잭션 취소 | 변경사항을 취소하고 이전 상태로 복구 |

#### 🧩 권한의 종류

| 권한 | 설명 |
|------|------|
| **SELECT** | 데이터 조회 권한 |
| **INSERT** | 데이터 삽입 권한 |
| **UPDATE** | 데이터 수정 권한 |
| **DELETE** | 데이터 삭제 권한 |
| **ALL** | 모든 권한 |
| **EXECUTE** | 프로시저/함수 실행 권한 |

#### 📝 기출 포맷 예시
- DCL의 기능으로 옳은 것은?
- 다음 중 DCL에 해당하는 명령어는?
- 권한 부여와 회수 명령어를 각각 쓰시오.

#### 🧠 용어 설명
- **DCL**: 데이터베이스 접근 권한을 제어하는 언어
- **권한**: 데이터베이스 객체에 대한 접근 및 조작 허가
- **트랜잭션**: 데이터베이스 작업의 논리적 단위

---

## 🔹 237. GRANT / REVOKE

#### 📘 정의
**GRANT**는 사용자에게 데이터베이스 객체에 대한 접근 권한을 부여하는 명령어이고,  
**REVOKE**는 사용자로부터 부여된 권한을 회수하는 명령어이다.

#### 🧩 GRANT 기본 구문
```sql
-- 특정 권한 부여
GRANT 권한 ON 객체명 TO 사용자명;

-- 모든 권한 부여
GRANT ALL ON 객체명 TO 사용자명;

-- 권한 부여와 동시에 다른 사용자에게 권한 부여 허용
GRANT 권한 ON 객체명 TO 사용자명 WITH GRANT OPTION;

-- 여러 사용자에게 권한 부여
GRANT 권한 ON 객체명 TO 사용자1, 사용자2;

-- 모든 사용자에게 권한 부여
GRANT 권한 ON 객체명 TO PUBLIC;
```

#### 🧩 REVOKE 기본 구문
```sql
-- 특정 권한 회수
REVOKE 권한 ON 객체명 FROM 사용자명;

-- 모든 권한 회수
REVOKE ALL ON 객체명 FROM 사용자명;

-- 권한 부여 옵션까지 회수
REVOKE GRANT OPTION FOR 권한 ON 객체명 FROM 사용자명;

-- 연쇄 권한 회수
REVOKE 권한 ON 객체명 FROM 사용자명 CASCADE;
```

#### 🧩 권한 부여 옵션

| 옵션 | 설명 |
|------|------|
| **WITH GRANT OPTION** | 부여받은 권한을 다른 사용자에게 부여할 수 있음 |
| **WITH ADMIN OPTION** | 시스템 권한을 다른 사용자에게 부여할 수 있음 |
| **GRANT OPTION FOR** | 특정 권한에 대한 부여 옵션만 회수 |
| **PUBLIC** | 모든 사용자에게 권한 부여 |
| **CASCADE** | 권한 회수 시 연쇄적으로 회수 |

#### 🧩 실제 예시
```sql
-- 김철수에게 학생 테이블 조회 권한 부여
GRANT SELECT ON 학생 TO 김철수;

-- 이영희에게 학생 테이블 모든 권한 부여 (다른 사용자에게 권한 부여 가능)
GRANT ALL ON 학생 TO 이영희 WITH GRANT OPTION;

-- 모든 사용자에게 학과 테이블 조회 권한 부여
GRANT SELECT ON 학과 TO PUBLIC;

-- 박민수에게 학생 테이블 조회, 삽입 권한 부여
GRANT SELECT, INSERT ON 학생 TO 박민수;

-- 김철수로부터 학생 테이블 조회 권한 회수
REVOKE SELECT ON 학생 FROM 김철수;

-- 이영희로부터 권한 부여 옵션만 회수
REVOKE GRANT OPTION FOR SELECT ON 학생 FROM 이영희;

-- 이영희로부터 모든 권한 회수 (연쇄 회수)
REVOKE ALL ON 학생 FROM 이영희 CASCADE;
```

#### 🧩 시스템 권한 예시
```sql
-- 데이터베이스 연결 권한 부여
GRANT CONNECT TO 사용자명;

-- 테이블 생성 권한 부여
GRANT CREATE TABLE TO 사용자명;

-- DBA 권한 부여
GRANT DBA TO 사용자명;
```

#### 📝 기출 포맷 예시
- GRANT와 REVOKE 구문을 각각 작성하시오.
- WITH GRANT OPTION의 의미는?
- 다음 중 권한 회수에 관한 설명으로 옳은 것은?

#### 🧠 용어 설명
- **GRANT**: 사용자에게 권한을 부여하는 명령어
- **REVOKE**: 사용자로부터 권한을 회수하는 명령어
- **WITH GRANT OPTION**: 부여받은 권한을 다른 사용자에게 재부여 가능
- **CASCADE**: 연쇄적으로 권한 회수
- **PUBLIC**: 모든 사용자를 의미하는 키워드

---

## 🔹 238. ROLLBACK

#### 📘 정의
**ROLLBACK**은 트랜잭션 실행 중에 발생한 변경사항을 취소하고, 트랜잭션이 시작되기 전의 상태로 데이터베이스를 복구하는 명령어이다.

#### 🧩 기본 구문
```sql
-- 전체 트랜잭션 롤백
ROLLBACK;

-- 특정 저장점까지 롤백
ROLLBACK TO 저장점명;

-- 저장점 생성
SAVEPOINT 저장점명;
```

#### 🧩 트랜잭션 제어 명령어

| 명령어 | 기능 | 설명 |
|--------|------|------|
| **BEGIN** | 트랜잭션 시작 | 새로운 트랜잭션 시작 |
| **COMMIT** | 트랜잭션 확정 | 변경사항을 영구 저장 |
| **ROLLBACK** | 트랜잭션 취소 | 변경사항을 취소하고 복구 |
| **SAVEPOINT** | 저장점 생성 | 트랜잭션 내 중간 지점 저장 |

#### 🧩 ROLLBACK 특징
- **자동 롤백**: 시스템 오류나 교착상태 발생 시 자동 실행
- **부분 롤백**: SAVEPOINT를 이용한 부분 취소 가능
- **전체 롤백**: 트랜잭션 전체 취소
- **DDL 제약**: DDL 명령어는 롤백 불가 (AUTO COMMIT)

#### 🧩 실제 예시
```sql
-- 트랜잭션 시작
BEGIN;

-- 데이터 삽입
INSERT INTO 학생 VALUES ('2024001', '홍길동', '컴퓨터공학과');

-- 저장점 생성
SAVEPOINT sp1;

-- 데이터 수정
UPDATE 학생 SET 이름 = '홍길순' WHERE 학번 = '2024001';

-- 저장점 생성
SAVEPOINT sp2;

-- 데이터 삭제
DELETE FROM 학생 WHERE 학번 = '2024001';

-- sp2 지점까지 롤백 (DELETE 취소)
ROLLBACK TO sp2;

-- 전체 롤백 (모든 변경사항 취소)
ROLLBACK;
```

#### 🧩 COMMIT vs ROLLBACK

| 구분 | COMMIT | ROLLBACK |
|------|--------|----------|
| **기능** | 변경사항 확정 | 변경사항 취소 |
| **실행 후** | 변경사항 영구 저장 | 트랜잭션 시작 전 상태로 복구 |
| **되돌리기** | 불가능 | 가능 (SAVEPOINT 이용) |
| **자동 실행** | DDL 명령어 후 | 시스템 오류 시 |

#### 🧩 트랜잭션 예시 시나리오
```sql
-- 계좌 이체 트랜잭션 예시
BEGIN;

-- A 계좌에서 출금
UPDATE 계좌 SET 잔액 = 잔액 - 100000 WHERE 계좌번호 = 'A001';

-- B 계좌에 입금
UPDATE 계좌 SET 잔액 = 잔액 + 100000 WHERE 계좌번호 = 'B001';

-- 잔액 확인 후 오류 발생 시
IF (잔액 < 0) THEN
    ROLLBACK;  -- 전체 취소
ELSE
    COMMIT;    -- 확정
END IF;
```

#### 📝 기출 포맷 예시
- ROLLBACK의 기능을 설명하시오.
- SAVEPOINT와 ROLLBACK TO의 관계는?
- 트랜잭션 제어 명령어를 모두 나열하시오.

#### 🧠 용어 설명
- **ROLLBACK**: 트랜잭션 내 변경사항을 취소하는 명령어
- **SAVEPOINT**: 트랜잭션 내 중간 저장점
- **트랜잭션**: 데이터베이스 작업의 논리적 단위
- **부분 롤백**: 저장점까지만 취소하는 롤백
- **전체 롤백**: 트랜잭션 전체를 취소하는 롤백

---

## 🔹 239. DML (Data Manipulation Language)

#### 📘 정의
**DML(Data Manipulation Language)**은 데이터베이스에 저장된 데이터를 **검색, 삽입, 수정, 삭제**하는 언어로, 실제 데이터를 조작하여 사용자가 원하는 결과를 얻는 데 사용한다.

#### 🧩 주요 특징
- **데이터 조작**: 테이블의 실제 데이터를 처리
- **ROLLBACK 가능**: 트랜잭션 내에서 실행 취소 가능
- **WHERE 절**: 조건을 지정하여 특정 데이터만 처리
- **실행 결과**: 영향받은 행의 수를 반환

#### 🧩 DML 명령어 종류

| 명령어 | 기능 | 설명 |
|--------|------|------|
| **SELECT** | 데이터 검색 | 테이블에서 원하는 데이터를 조회 |
| **INSERT** | 데이터 삽입 | 테이블에 새로운 행을 추가 |
| **UPDATE** | 데이터 수정 | 기존 데이터의 값을 변경 |
| **DELETE** | 데이터 삭제 | 테이블에서 특정 행을 제거 |

#### 🧩 DML vs DDL 비교

| 구분 | DML | DDL |
|------|-----|-----|
| **대상** | 테이블의 데이터 | 테이블의 구조 |
| **ROLLBACK** | 가능 | 불가능 (AUTO COMMIT) |
| **예시** | INSERT, UPDATE, DELETE | CREATE, ALTER, DROP |
| **영향** | 데이터 내용 변경 | 스키마 구조 변경 |

#### 🧩 트랜잭션 처리
```sql
-- 트랜잭션 시작
BEGIN;

-- DML 명령어 실행
INSERT INTO 학생 VALUES ('2024001', '홍길동', '컴퓨터공학과');
UPDATE 학생 SET 학과 = '소프트웨어학과' WHERE 학번 = '2024001';

-- 확정 또는 취소
COMMIT;   -- 변경사항 확정
-- 또는
ROLLBACK; -- 변경사항 취소
```

#### 📝 기출 포맷 예시
- DML의 특징으로 옳은 것은?
- 다음 중 DML에 해당하는 명령어는?
- DML과 DDL의 차이점을 설명하시오.

#### 🧠 용어 설명
- **DML**: 데이터베이스의 데이터를 조작하는 언어
- **트랜잭션**: 하나의 논리적 작업 단위
- **WHERE 절**: 조건을 지정하는 구문

---

## 🔹 240. 삽입문 (INSERT INTO~)

#### 📘 정의
**INSERT INTO**는 테이블에 새로운 행(레코드)을 추가하는 DML 명령어로, 지정된 테이블에 하나 이상의 행을 삽입한다.

#### 🧩 기본 구문
```sql
-- 모든 컬럼에 값 삽입
INSERT INTO 테이블명 VALUES (값1, 값2, 값3, ...);

-- 특정 컬럼에만 값 삽입
INSERT INTO 테이블명 (컬럼1, 컬럼2, ...) VALUES (값1, 값2, ...);

-- 여러 행 동시 삽입
INSERT INTO 테이블명 VALUES 
(값1, 값2, 값3),
(값4, 값5, 값6),
(값7, 값8, 값9);

-- 다른 테이블의 데이터 삽입
INSERT INTO 테이블명 SELECT 컬럼1, 컬럼2, ... FROM 다른테이블명;
```

#### 🧩 INSERT 유형별 특징

| 유형 | 설명 | 예시 |
|------|------|------|
| **전체 삽입** | 모든 컬럼에 값 지정 | INSERT INTO 학생 VALUES (...) |
| **부분 삽입** | 특정 컬럼에만 값 지정 | INSERT INTO 학생 (학번, 이름) VALUES (...) |
| **다중 삽입** | 여러 행을 한 번에 삽입 | INSERT INTO 학생 VALUES (...), (...) |
| **서브쿼리 삽입** | 다른 테이블 결과를 삽입 | INSERT INTO ... SELECT ... FROM ... |

#### 🧩 실제 예시
```sql
-- 학생 테이블 구조: 학번, 이름, 학과, 학년, 입학일

-- 1. 모든 컬럼에 값 삽입
INSERT INTO 학생 VALUES ('2024001', '홍길동', '컴퓨터공학과', 1, '2024-03-02');

-- 2. 특정 컬럼에만 값 삽입 (학년, 입학일은 DEFAULT 값 사용)
INSERT INTO 학생 (학번, 이름, 학과) VALUES ('2024002', '김철수', '전자공학과');

-- 3. 여러 행 동시 삽입
INSERT INTO 학생 VALUES 
('2024003', '이영희', '소프트웨어학과', 2, '2023-03-02'),
('2024004', '박민수', '컴퓨터공학과', 1, '2024-03-02');

-- 4. 다른 테이블에서 데이터 복사
INSERT INTO 우수학생 
SELECT 학번, 이름, 학과 FROM 학생 WHERE 평점 >= 4.0;
```

#### 🧩 주의사항
- **제약조건 준수**: PRIMARY KEY, FOREIGN KEY 등 제약조건 위반 시 오류
- **데이터타입 일치**: 컬럼의 데이터타입과 삽입할 값의 타입이 일치해야 함
- **NOT NULL 컬럼**: NULL 값을 허용하지 않는 컬럼에는 반드시 값 지정
- **DEFAULT 값**: 값을 지정하지 않은 컬럼은 DEFAULT 값 또는 NULL 삽입

#### 📝 기출 포맷 예시
- INSERT 구문의 올바른 사용법은?
- 다음 중 INSERT 실행 시 오류가 발생하는 경우는?
- 서브쿼리를 이용한 INSERT 구문을 작성하시오.

#### 🧠 용어 설명
- **INSERT INTO**: 테이블에 새로운 행을 삽입하는 명령어
- **VALUES**: 삽입할 값들을 지정하는 키워드
- **서브쿼리**: 다른 테이블의 SELECT 결과를 삽입하는 방식

---

## 🔹 241. 삭제문 (DELETE FROM~)

#### 📘 정의
**DELETE FROM**은 테이블에서 특정 조건을 만족하는 행(레코드)을 삭제하는 DML 명령어로, WHERE 절을 이용하여 삭제할 행을 지정한다.

#### 🧩 기본 구문
```sql
-- 조건에 맞는 행 삭제
DELETE FROM 테이블명 WHERE 조건;

-- 모든 행 삭제 (테이블 구조는 유지)
DELETE FROM 테이블명;

-- 서브쿼리를 이용한 삭제
DELETE FROM 테이블명 WHERE 컬럼 IN (SELECT 컬럼 FROM 다른테이블명);
```

#### 🧩 DELETE 유형별 특징

| 유형 | 설명 | 위험도 |
|------|------|--------|
| **조건부 삭제** | WHERE 절로 특정 행만 삭제 | 낮음 |
| **전체 삭제** | 테이블의 모든 행 삭제 | 높음 |
| **서브쿼리 삭제** | 다른 테이블 조건으로 삭제 | 중간 |

#### 🧩 실제 예시
```sql
-- 1. 특정 학생 삭제
DELETE FROM 학생 WHERE 학번 = '2024001';

-- 2. 조건에 맞는 여러 학생 삭제
DELETE FROM 학생 WHERE 학과 = '컴퓨터공학과' AND 학년 = 1;

-- 3. 평점이 낮은 학생들 삭제
DELETE FROM 학생 WHERE 평점 < 2.0;

-- 4. 서브쿼리를 이용한 삭제
DELETE FROM 학생 
WHERE 학과코드 IN (SELECT 학과코드 FROM 학과 WHERE 폐지여부 = 'Y');

-- 5. 조인을 이용한 삭제
DELETE FROM 학생 
WHERE 학번 IN (SELECT 학번 FROM 징계 WHERE 징계종류 = '퇴학');
```

#### 🧩 DELETE vs DROP vs TRUNCATE

| 명령어 | 삭제 범위 | 구조 보존 | ROLLBACK | 속도 |
|--------|-----------|-----------|----------|------|
| **DELETE** | 데이터 (조건부 가능) | 보존 | 가능 | 느림 |
| **DROP** | 테이블 전체 | 제거 | 불가능 | 빠름 |
| **TRUNCATE** | 모든 데이터 | 보존 | 불가능 | 빠름 |

#### 🧩 주의사항
- **WHERE 절 필수**: WHERE 절 없으면 모든 행 삭제
- **참조 무결성**: 외래키로 참조되는 행은 삭제 불가 (CASCADE 옵션 제외)
- **ROLLBACK 가능**: 트랜잭션 내에서 실행 취소 가능
- **성능**: 대량 데이터 삭제 시 TRUNCATE 고려

#### 📝 기출 포맷 예시
- DELETE 구문의 올바른 사용법은?
- DELETE와 TRUNCATE의 차이점을 설명하시오.
- 외래키 참조 관계에서 DELETE 실행 시 주의사항은?

#### 🧠 용어 설명
- **DELETE FROM**: 테이블에서 행을 삭제하는 명령어
- **WHERE 절**: 삭제할 행의 조건을 지정
- **참조 무결성**: 외래키 관계에서 데이터 일관성 유지

---

## 🔹 242. 갱신문 (UPDATE~ SET~)

#### 📘 정의
**UPDATE~ SET**은 테이블의 기존 데이터를 수정하는 DML 명령어로, SET 절에서 변경할 값을 지정하고 WHERE 절에서 수정할 행의 조건을 지정한다.

#### 🧩 기본 구문
```sql
-- 기본 UPDATE 구문
UPDATE 테이블명 SET 컬럼1 = 값1, 컬럼2 = 값2, ... WHERE 조건;

-- 계산식을 이용한 UPDATE
UPDATE 테이블명 SET 컬럼 = 컬럼 + 값 WHERE 조건;

-- 서브쿼리를 이용한 UPDATE
UPDATE 테이블명 SET 컬럼 = (SELECT 값 FROM 다른테이블명 WHERE 조건) WHERE 조건;

-- 여러 테이블을 참조한 UPDATE
UPDATE 테이블1 SET 컬럼 = 값 
WHERE 테이블1.키 = (SELECT 키 FROM 테이블2 WHERE 조건);
```

#### 🧩 UPDATE 유형별 특징

| 유형 | 설명 | 예시 |
|------|------|------|
| **단순 갱신** | 지정된 값으로 직접 변경 | SET 이름 = '홍길동' |
| **계산 갱신** | 기존 값을 이용한 계산 | SET 급여 = 급여 * 1.1 |
| **서브쿼리 갱신** | 다른 테이블 값으로 변경 | SET 학과 = (SELECT...) |
| **조건부 갱신** | WHERE 절로 특정 행만 변경 | WHERE 학번 = '2024001' |

#### 🧩 실제 예시
```sql
-- 1. 특정 학생의 학과 변경
UPDATE 학생 SET 학과 = '소프트웨어학과' WHERE 학번 = '2024001';

-- 2. 여러 컬럼 동시 변경
UPDATE 학생 SET 학과 = '컴퓨터공학과', 학년 = 2 WHERE 학번 = '2024002';

-- 3. 계산식을 이용한 갱신
UPDATE 성적 SET 점수 = 점수 + 5 WHERE 점수 >= 90;

-- 4. 조건에 맞는 여러 행 변경
UPDATE 학생 SET 학년 = 학년 + 1 WHERE 입학년도 = 2023;

-- 5. 서브쿼리를 이용한 갱신
UPDATE 학생 SET 학과명 = (
    SELECT 학과명 FROM 학과 WHERE 학과.학과코드 = 학생.학과코드
) WHERE 학과코드 IS NOT NULL;

-- 6. CASE 문을 이용한 조건부 갱신
UPDATE 학생 SET 장학금 = 
    CASE 
        WHEN 평점 >= 4.0 THEN 1000000
        WHEN 평점 >= 3.5 THEN 500000
        ELSE 0
    END;
```

#### 🧩 주의사항
- **WHERE 절 필수**: WHERE 절 없으면 모든 행이 변경됨
- **데이터타입 일치**: 변경할 값이 컬럼의 데이터타입과 일치해야 함
- **제약조건 준수**: PRIMARY KEY, UNIQUE 등 제약조건 위반 시 오류
- **NULL 값 처리**: NULL 값으로 변경 시 NOT NULL 제약조건 확인

#### 🧩 UPDATE vs INSERT vs DELETE

| 명령어 | 기능 | 행 수 변화 | 사용 시점 |
|--------|------|-----------|-----------|
| **UPDATE** | 기존 데이터 수정 | 변화 없음 | 데이터 변경 시 |
| **INSERT** | 새로운 데이터 추가 | 증가 | 데이터 입력 시 |
| **DELETE** | 기존 데이터 삭제 | 감소 | 데이터 제거 시 |

#### 📝 기출 포맷 예시
- UPDATE 구문의 올바른 사용법은?
- 서브쿼리를 이용한 UPDATE 구문을 작성하시오.
- UPDATE 실행 시 주의해야 할 점은?

#### 🧠 용어 설명
- **UPDATE**: 테이블의 기존 데이터를 수정하는 명령어
- **SET**: 변경할 컬럼과 값을 지정하는 절
- **WHERE**: 수정할 행의 조건을 지정하는 절
- **서브쿼리**: 다른 테이블의 값을 참조하여 갱신하는 방식

---

## 🔹 243. SELECT

#### 📘 정의
**SELECT**는 데이터베이스 테이블에서 원하는 데이터를 조회하는 DML 명령어로, 가장 자주 사용되는 SQL 문이며 다양한 절(Clause)과 함께 사용하여 복잡한 질의를 수행할 수 있다.

#### 🧩 기본 구문
```sql
SELECT [DISTINCT] 컬럼명1, 컬럼명2, ...
FROM 테이블명
[WHERE 조건]
[GROUP BY 컬럼명]
[HAVING 조건]
[ORDER BY 컬럼명 [ASC|DESC]]
[LIMIT 개수];
```

#### 🧩 SELECT 절의 실행 순서

| 순서 | 절 | 기능 |
|------|---|------|
| 1 | **FROM** | 조회할 테이블 지정 |
| 2 | **WHERE** | 행 필터링 조건 |
| 3 | **GROUP BY** | 그룹화 |
| 4 | **HAVING** | 그룹 필터링 조건 |
| 5 | **SELECT** | 출력할 컬럼 선택 |
| 6 | **ORDER BY** | 정렬 |
| 7 | **LIMIT** | 출력 행 수 제한 |

#### 🧩 주요 키워드

| 키워드 | 기능 | 예시 |
|--------|------|------|
| **\*** | 모든 컬럼 선택 | SELECT * FROM 학생 |
| **DISTINCT** | 중복 제거 | SELECT DISTINCT 학과 FROM 학생 |
| **AS** | 별칭 지정 | SELECT 이름 AS 학생명 FROM 학생 |
| **COUNT()** | 행 개수 계산 | SELECT COUNT(*) FROM 학생 |

#### 🧩 실제 예시
```sql
-- 1. 모든 컬럼 조회
SELECT * FROM 학생;

-- 2. 특정 컬럼만 조회
SELECT 학번, 이름, 학과 FROM 학생;

-- 3. 별칭 사용
SELECT 학번 AS 번호, 이름 AS 학생명, 학과 AS 전공 FROM 학생;

-- 4. 중복 제거
SELECT DISTINCT 학과 FROM 학생;

-- 5. 계산식 사용
SELECT 이름, 점수, 점수*0.1 AS 가산점 FROM 성적;

-- 6. 함수 사용
SELECT COUNT(*) AS 총학생수 FROM 학생;
SELECT AVG(점수) AS 평균점수 FROM 성적;
```

#### 🧩 컬럼 표현 방식

| 방식 | 설명 | 예시 |
|------|------|------|
| **컬럼명** | 테이블의 실제 컬럼 | SELECT 이름 FROM 학생 |
| **상수** | 고정된 값 | SELECT '2024학년도' AS 학년도 |
| **계산식** | 연산 결과 | SELECT 점수+10 AS 보정점수 |
| **함수** | 내장 함수 사용 | SELECT UPPER(이름) AS 대문자이름 |

#### 📝 기출 포맷 예시
- SELECT 문의 실행 순서를 설명하시오.
- DISTINCT의 기능은?
- 다음 중 올바른 SELECT 구문은?

#### 🧠 용어 설명
- **SELECT**: 데이터를 조회하는 DML 명령어
- **DISTINCT**: 중복된 행을 제거하는 키워드
- **별칭(Alias)**: 컬럼이나 테이블에 임시로 부여하는 이름
- **절(Clause)**: SQL 문을 구성하는 각 부분

---

## 🔹 244. 기본 검색

#### 📘 정의
기본 검색은 SELECT 문을 사용하여 **테이블의 모든 행 또는 특정 컬럼**을 조회하는 가장 기본적인 형태의 데이터 검색이다.

#### 🧩 기본 검색 유형

| 검색 유형 | 구문 | 설명 |
|-----------|------|------|
| **전체 검색** | SELECT * FROM 테이블명 | 모든 컬럼, 모든 행 조회 |
| **컬럼 지정** | SELECT 컬럼1, 컬럼2 FROM 테이블명 | 특정 컬럼만 조회 |
| **중복 제거** | SELECT DISTINCT 컬럼 FROM 테이블명 | 중복 행 제거하여 조회 |
| **별칭 사용** | SELECT 컬럼 AS 별칭 FROM 테이블명 | 컬럼에 별칭 부여 |

#### 🧩 실제 예시
```sql
-- 학생 테이블 구조: 학번, 이름, 학과, 학년, 평점

-- 1. 전체 데이터 조회
SELECT * FROM 학생;

-- 2. 특정 컬럼만 조회
SELECT 학번, 이름 FROM 학생;

-- 3. 중복 제거 조회
SELECT DISTINCT 학과 FROM 학생;

-- 4. 별칭을 사용한 조회
SELECT 학번 AS 번호, 이름 AS 성명, 학과 AS 전공학과 FROM 학생;

-- 5. 계산 컬럼 조회
SELECT 이름, 평점, 평점*25 AS 백분율점수 FROM 학생;

-- 6. 상수 컬럼 추가
SELECT '2024학년도' AS 학년도, 이름, 학과 FROM 학생;
```

#### 🧩 와일드카드(*) 사용

| 사용법 | 설명 | 권장사항 |
|--------|------|----------|
| **SELECT \*** | 모든 컬럼 조회 | 개발/테스트 시에만 사용 |
| **운영환경** | 필요한 컬럼만 지정 | 성능상 유리 |
| **대용량 테이블** | * 사용 지양 | 네트워크 부하 증가 |

#### 🧩 별칭(Alias) 규칙
```sql
-- 별칭 사용 방법들
SELECT 이름 AS 학생명 FROM 학생;        -- AS 키워드 사용
SELECT 이름 학생명 FROM 학생;           -- AS 생략 가능
SELECT 이름 AS "학생 이름" FROM 학생;    -- 공백 포함 시 따옴표 필요
SELECT 이름 AS '학생이름' FROM 학생;     -- 단일 따옴표도 가능
```

#### 🧩 데이터 타입별 조회
```sql
-- 문자형 데이터
SELECT 이름, 학과 FROM 학생;

-- 숫자형 데이터
SELECT 학년, 평점 FROM 학생;

-- 날짜형 데이터
SELECT 입학일, 졸업예정일 FROM 학생;

-- NULL 값 처리
SELECT 이름, ISNULL(전화번호, '미등록') AS 연락처 FROM 학생;
```

#### 📝 기출 포맷 예시
- 전체 컬럼을 조회하는 방법은?
- DISTINCT 키워드의 사용법은?
- 별칭 지정 시 주의사항은?

#### 🧠 용어 설명
- **기본 검색**: 조건 없이 테이블 데이터를 조회하는 방식
- **와일드카드(*)**: 모든 컬럼을 의미하는 특수 기호
- **별칭**: 컬럼이나 테이블에 부여하는 임시 이름

---

## 🔹 245. 조건 지정 검색

#### 📘 정의
조건 지정 검색은 **WHERE 절**을 사용하여 특정 조건을 만족하는 행만을 선택적으로 조회하는 검색 방법이다.

#### 🧩 WHERE 절 기본 구문
```sql
SELECT 컬럼명
FROM 테이블명
WHERE 조건식;
```

#### 🧩 비교 연산자

| 연산자 | 의미 | 예시 |
|--------|------|------|
| **=** | 같음 | WHERE 학년 = 1 |
| **<>** , **!=** | 같지 않음 | WHERE 학과 <> '컴퓨터공학과' |
| **>** | 크다 | WHERE 평점 > 3.0 |
| **>=** | 크거나 같다 | WHERE 평점 >= 3.5 |
| **<** | 작다 | WHERE 학년 < 4 |
| **<=** | 작거나 같다 | WHERE 평점 <= 2.0 |

#### 🧩 논리 연산자

| 연산자 | 의미 | 예시 |
|--------|------|------|
| **AND** | 그리고 (모든 조건 만족) | WHERE 학과='컴공' AND 학년=1 |
| **OR** | 또는 (하나라도 만족) | WHERE 학년=1 OR 학년=2 |
| **NOT** | 아니다 (조건의 반대) | WHERE NOT 학과='컴공' |

#### 🧩 특수 연산자

| 연산자 | 의미 | 구문 | 예시 |
|--------|------|------|------|
| **BETWEEN** | 범위 조건 | BETWEEN A AND B | WHERE 평점 BETWEEN 3.0 AND 4.0 |
| **IN** | 목록 조건 | IN (값1, 값2, ...) | WHERE 학과 IN ('컴공', '전자') |
| **LIKE** | 패턴 매칭 | LIKE '패턴' | WHERE 이름 LIKE '김%' |
| **IS NULL** | NULL 값 확인 | IS NULL / IS NOT NULL | WHERE 전화번호 IS NULL |

#### 🧩 LIKE 패턴 매칭

| 와일드카드 | 의미 | 예시 | 설명 |
|------------|------|------|------|
| **%** | 0개 이상의 임의 문자 | '김%' | 김으로 시작하는 모든 문자열 |
| **_** | 정확히 1개의 임의 문자 | '김_수' | 김○수 형태의 3글자 |
| **[]** | 지정된 범위의 문자 | '[가-나]%' | 가~나로 시작하는 문자열 |
| **[^]** | 지정된 범위가 아닌 문자 | '[^가-나]%' | 가~나가 아닌 문자로 시작 |

#### 🧩 실제 예시
```sql
-- 1. 단순 조건 검색
SELECT * FROM 학생 WHERE 학년 = 1;
SELECT * FROM 학생 WHERE 학과 = '컴퓨터공학과';

-- 2. 논리 연산자 사용
SELECT * FROM 학생 WHERE 학과 = '컴퓨터공학과' AND 학년 = 1;
SELECT * FROM 학생 WHERE 학년 = 1 OR 학년 = 2;
SELECT * FROM 학생 WHERE NOT 학과 = '컴퓨터공학과';

-- 3. 범위 검색
SELECT * FROM 학생 WHERE 평점 BETWEEN 3.0 AND 4.0;
SELECT * FROM 학생 WHERE 입학일 BETWEEN '2020-01-01' AND '2024-12-31';

-- 4. 목록 검색
SELECT * FROM 학생 WHERE 학과 IN ('컴퓨터공학과', '전자공학과', '기계공학과');
SELECT * FROM 학생 WHERE 학년 IN (1, 2);

-- 5. 패턴 검색
SELECT * FROM 학생 WHERE 이름 LIKE '김%';           -- 김으로 시작
SELECT * FROM 학생 WHERE 이름 LIKE '%수';           -- 수로 끝남
SELECT * FROM 학생 WHERE 이름 LIKE '%민%';          -- 민이 포함
SELECT * FROM 학생 WHERE 이름 LIKE '김_수';         -- 김○수 (3글자)
SELECT * FROM 학생 WHERE 학번 LIKE '2024%';        -- 2024로 시작

-- 6. NULL 값 검색
SELECT * FROM 학생 WHERE 전화번호 IS NULL;         -- 전화번호가 없는 학생
SELECT * FROM 학생 WHERE 전화번호 IS NOT NULL;     -- 전화번호가 있는 학생
```

#### 🧩 조건 우선순위
```sql
-- 괄호를 사용한 조건 그룹화
SELECT * FROM 학생 
WHERE (학과 = '컴퓨터공학과' OR 학과 = '전자공학과') 
  AND 평점 >= 3.5;

-- 연산자 우선순위: NOT > AND > OR
SELECT * FROM 학생 
WHERE NOT 학과 = '컴퓨터공학과' AND 학년 = 1 OR 평점 >= 4.0;
```

#### 📝 기출 포맷 예시
- WHERE 절에서 사용하는 연산자 종류는?
- LIKE 연산자의 와일드카드 기능을 설명하시오.
- BETWEEN과 IN 연산자의 사용법은?

#### 🧠 용어 설명
- **WHERE 절**: 조회할 행의 조건을 지정하는 구문
- **와일드카드**: 패턴 매칭에 사용되는 특수 문자
- **NULL**: 값이 없음을 나타내는 특별한 상태

---

## 🔹 246. 정렬 검색

#### 📘 정의
정렬 검색은 **ORDER BY 절**을 사용하여 조회 결과를 특정 컬럼을 기준으로 **오름차순 또는 내림차순**으로 정렬하여 출력하는 검색 방법이다.

#### 🧩 ORDER BY 기본 구문
```sql
SELECT 컬럼명
FROM 테이블명
[WHERE 조건]
ORDER BY 컬럼명 [ASC|DESC];
```

#### 🧩 정렬 옵션

| 옵션 | 의미 | 기본값 | 예시 |
|------|------|--------|------|
| **ASC** | 오름차순 (Ascending) | 기본값 | ORDER BY 이름 ASC |
| **DESC** | 내림차순 (Descending) | 명시 필요 | ORDER BY 평점 DESC |

#### 🧩 정렬 기준별 특징

| 데이터 타입 | 오름차순 (ASC) | 내림차순 (DESC) |
|-------------|----------------|------------------|
| **숫자** | 작은 수 → 큰 수 | 큰 수 → 작은 수 |
| **문자** | A → Z, 가 → 힣 | Z → A, 힣 → 가 |
| **날짜** | 과거 → 미래 | 미래 → 과거 |
| **NULL** | 마지막 (또는 첫번째) | 첫번째 (또는 마지막) |

#### 🧩 다중 정렬
```sql
-- 여러 컬럼으로 정렬 (우선순위 순서)
SELECT * FROM 학생 
ORDER BY 학과 ASC, 학년 DESC, 평점 DESC;

-- 첫 번째: 학과 오름차순
-- 두 번째: 같은 학과 내에서 학년 내림차순  
-- 세 번째: 같은 학과, 같은 학년에서 평점 내림차순
```

#### 🧩 실제 예시
```sql
-- 1. 단일 컬럼 정렬
SELECT * FROM 학생 ORDER BY 이름;                    -- 이름 오름차순 (기본)
SELECT * FROM 학생 ORDER BY 이름 ASC;                -- 이름 오름차순 (명시)
SELECT * FROM 학생 ORDER BY 평점 DESC;               -- 평점 내림차순

-- 2. 다중 컬럼 정렬
SELECT * FROM 학생 ORDER BY 학과, 학년;              -- 학과→학년 순 오름차순
SELECT * FROM 학생 ORDER BY 학과 ASC, 평점 DESC;     -- 학과 오름차순, 평점 내림차순

-- 3. 조건과 정렬 함께 사용
SELECT * FROM 학생 
WHERE 학과 = '컴퓨터공학과' 
ORDER BY 평점 DESC;

-- 4. 계산 컬럼으로 정렬
SELECT 이름, 평점, 평점*25 AS 백분율 
FROM 학생 
ORDER BY 백분율 DESC;

-- 5. 컬럼 순서 번호로 정렬
SELECT 학번, 이름, 학과, 평점 
FROM 학생 
ORDER BY 4 DESC;  -- 4번째 컬럼(평점)으로 내림차순 정렬

-- 6. NULL 값 처리
SELECT * FROM 학생 ORDER BY 전화번호;                -- NULL 값은 마지막에 표시
```

#### 🧩 정렬과 성능

| 상황 | 성능 영향 | 권장사항 |
|------|-----------|----------|
| **인덱스 있음** | 빠른 정렬 | 자주 정렬하는 컬럼에 인덱스 생성 |
| **인덱스 없음** | 느린 정렬 | 대용량 데이터 시 인덱스 고려 |
| **다중 정렬** | 성능 저하 | 필요한 정렬만 사용 |
| **함수 사용** | 성능 저하 | ORDER BY UPPER(이름) 등 지양 |

#### 🧩 특수한 정렬 방법
```sql
-- 1. CASE를 이용한 사용자 정의 정렬
SELECT * FROM 학생 
ORDER BY 
    CASE 학과
        WHEN '컴퓨터공학과' THEN 1
        WHEN '전자공학과' THEN 2
        WHEN '기계공학과' THEN 3
        ELSE 4
    END;

-- 2. 함수를 이용한 정렬
SELECT * FROM 학생 ORDER BY LENGTH(이름), 이름;      -- 이름 길이순, 같으면 가나다순

-- 3. 무작위 정렬
SELECT * FROM 학생 ORDER BY RANDOM();               -- PostgreSQL
SELECT * FROM 학생 ORDER BY RAND();                 -- MySQL
```

#### 🧩 ORDER BY 실행 순서
```sql
-- SQL 실행 순서에서 ORDER BY는 마지막
SELECT 학과, COUNT(*) AS 학생수
FROM 학생
WHERE 평점 >= 3.0
GROUP BY 학과
HAVING COUNT(*) >= 5
ORDER BY 학생수 DESC;

-- 실행 순서: FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY
```

#### 📝 기출 포맷 예시
- ORDER BY 절의 정렬 옵션을 설명하시오.
- 다중 컬럼 정렬 시 우선순위는?
- NULL 값이 있을 때 정렬 결과는?

#### 🧠 용어 설명
- **ORDER BY**: 조회 결과를 정렬하는 구문
- **ASC**: 오름차순 정렬 (기본값)
- **DESC**: 내림차순 정렬
- **다중 정렬**: 여러 컬럼을 기준으로 하는 정렬

---

## 🔹 247. 하위 질의 (서브쿼리)

#### 📘 정의
**하위 질의(서브쿼리)**는 하나의 SQL 문 안에 포함되어 있는 또 다른 SQL 문으로, **메인 쿼리의 조건이나 컬럼 값으로 사용**되어 더 복잡한 검색을 가능하게 한다.

#### 🧩 기본 구문
```sql
-- WHERE 절에서 사용
SELECT 컬럼명 
FROM 테이블명 
WHERE 컬럼명 연산자 (SELECT 컬럼명 FROM 테이블명 WHERE 조건);

-- SELECT 절에서 사용
SELECT 컬럼명, (SELECT 컬럼명 FROM 테이블명 WHERE 조건) AS 별칭
FROM 테이블명;

-- FROM 절에서 사용
SELECT 컬럼명 
FROM (SELECT 컬럼명 FROM 테이블명 WHERE 조건) AS 별칭;
```

#### 🧩 서브쿼리 종류

| 종류 | 위치 | 설명 | 예시 |
|------|------|------|------|
| **스칼라 서브쿼리** | SELECT 절 | 단일 값 반환 | SELECT (SELECT COUNT(*) FROM 학과) |
| **인라인 뷰** | FROM 절 | 가상 테이블 역할 | FROM (SELECT * FROM 학생) |
| **중첩 서브쿼리** | WHERE 절 | 조건으로 사용 | WHERE 학과 = (SELECT...) |

#### 🧩 반환 값에 따른 분류

| 분류 | 반환 값 | 사용 연산자 | 예시 |
|------|---------|-------------|------|
| **단일행 서브쿼리** | 1개 행, 1개 컬럼 | =, <>, >, <, >=, <= | WHERE 평점 = (SELECT MAX(평점)...) |
| **다중행 서브쿼리** | 여러 행, 1개 컬럼 | IN, ANY, ALL, EXISTS | WHERE 학과 IN (SELECT 학과...) |
| **다중컬럼 서브쿼리** | 여러 행, 여러 컬럼 | IN, EXISTS | WHERE (학과, 학년) IN (SELECT...) |

#### 🧩 다중행 서브쿼리 연산자

| 연산자 | 의미 | 예시 |
|--------|------|------|
| **IN** | 목록 중 하나와 일치 | WHERE 학과 IN (SELECT...) |
| **ANY (SOME)** | 목록 중 하나라도 만족 | WHERE 평점 > ANY (SELECT...) |
| **ALL** | 목록의 모든 값과 만족 | WHERE 평점 > ALL (SELECT...) |
| **EXISTS** | 서브쿼리 결과가 존재 | WHERE EXISTS (SELECT...) |

#### 🧩 실제 예시
```sql
-- 1. 단일행 서브쿼리
-- 평점이 가장 높은 학생 조회
SELECT * FROM 학생 
WHERE 평점 = (SELECT MAX(평점) FROM 학생);

-- 평균 평점보다 높은 학생들 조회
SELECT * FROM 학생 
WHERE 평점 > (SELECT AVG(평점) FROM 학생);

-- 2. 다중행 서브쿼리 - IN
-- 컴퓨터공학과나 전자공학과 학생들 조회
SELECT * FROM 학생 
WHERE 학과 IN (SELECT 학과명 FROM 학과 WHERE 단과대학 = '공과대학');

-- 3. 다중행 서브쿼리 - ANY
-- 1학년 학생 중 누구보다 평점이 높은 상급생 조회
SELECT * FROM 학생 
WHERE 학년 > 1 AND 평점 > ANY (SELECT 평점 FROM 학생 WHERE 학년 = 1);

-- 4. 다중행 서브쿼리 - ALL
-- 모든 1학년 학생보다 평점이 높은 상급생 조회
SELECT * FROM 학생 
WHERE 학년 > 1 AND 평점 > ALL (SELECT 평점 FROM 학생 WHERE 학년 = 1);

-- 5. EXISTS 서브쿼리
-- 수강 신청한 학생들만 조회
SELECT * FROM 학생 s
WHERE EXISTS (SELECT 1 FROM 수강신청 WHERE 학번 = s.학번);

-- 6. 스칼라 서브쿼리 (SELECT 절)
-- 학생과 함께 해당 학과의 총 학생 수 조회
SELECT 학번, 이름, 학과, 
       (SELECT COUNT(*) FROM 학생 s2 WHERE s2.학과 = s1.학과) AS 학과별학생수
FROM 학생 s1;

-- 7. 인라인 뷰 (FROM 절)
-- 각 학과별 평균 평점이 3.5 이상인 학과의 학생들 조회
SELECT * FROM 학생 
WHERE 학과 IN (
    SELECT 학과 
    FROM (SELECT 학과, AVG(평점) AS 평균평점 FROM 학생 GROUP BY 학과) AS 학과평균
    WHERE 평균평점 >= 3.5
);
```

#### 🧩 상관 서브쿼리
```sql
-- 상관 서브쿼리: 메인 쿼리의 값을 참조
-- 자신의 학과에서 평점이 가장 높은 학생들 조회
SELECT * FROM 학생 s1
WHERE 평점 = (SELECT MAX(평점) FROM 학생 s2 WHERE s2.학과 = s1.학과);

-- 자신보다 평점이 높은 동기가 3명 이상인 학생 조회
SELECT * FROM 학생 s1
WHERE (SELECT COUNT(*) FROM 학생 s2 
        WHERE s2.입학년도 = s1.입학년도 AND s2.평점 > s1.평점) >= 3;
```

#### 🧩 서브쿼리 주의사항
- **단일행 서브쿼리**: 반드시 1개의 값만 반환해야 함
- **NULL 처리**: 서브쿼리 결과에 NULL이 있으면 예상과 다른 결과 가능
- **성능**: 중첩이 깊을수록 성능 저하, JOIN으로 대체 고려
- **상관 서브쿼리**: 메인 쿼리 각 행마다 실행되어 성능 주의

#### 📝 기출 포맷 예시
- 서브쿼리의 종류와 특징을 설명하시오.
- ANY와 ALL 연산자의 차이점은?
- EXISTS와 IN의 차이점을 설명하시오.

#### 🧠 용어 설명
- **서브쿼리**: SQL문 내부에 포함된 또 다른 SELECT문
- **상관 서브쿼리**: 메인 쿼리의 컬럼을 참조하는 서브쿼리
- **스칼라 서브쿼리**: 단일 값을 반환하는 서브쿼리

---

## 🔹 248. 그룹 함수

#### 📘 정의
**그룹 함수**는 여러 행들의 집합에 대해 연산을 수행하여 **하나의 결과값을 반환**하는 함수로, 집계 함수(Aggregate Function)라고도 한다.

#### 🧩 주요 그룹 함수

| 함수 | 기능 | 예시 | 특징 |
|------|------|------|------|
| **COUNT()** | 행의 개수 | COUNT(*), COUNT(컬럼) | NULL 값 제외 (COUNT(*) 제외) |
| **SUM()** | 합계 | SUM(급여) | 숫자형 데이터만 |
| **AVG()** | 평균 | AVG(점수) | 숫자형 데이터만, NULL 제외 |
| **MAX()** | 최댓값 | MAX(점수) | 모든 데이터 타입 |
| **MIN()** | 최솟값 | MIN(점수) | 모든 데이터 타입 |
| **STDDEV()** | 표준편차 | STDDEV(점수) | 숫자형 데이터만 |
| **VARIANCE()** | 분산 | VARIANCE(점수) | 숫자형 데이터만 |

#### 🧩 COUNT 함수 상세

| 사용법 | 설명 | NULL 처리 |
|--------|------|-----------|
| **COUNT(\*)** | 전체 행 수 | NULL 포함 |
| **COUNT(컬럼명)** | NULL이 아닌 값의 개수 | NULL 제외 |
| **COUNT(DISTINCT 컬럼명)** | 중복 제거한 값의 개수 | NULL 제외 |

#### 🧩 실제 예시
```sql
-- 학생 테이블 기준 예시

-- 1. COUNT 함수
SELECT COUNT(*) AS 총학생수 FROM 학생;                    -- 모든 학생 수
SELECT COUNT(전화번호) AS 연락처등록학생수 FROM 학생;        -- 전화번호가 있는 학생 수
SELECT COUNT(DISTINCT 학과) AS 학과수 FROM 학생;           -- 중복 제거한 학과 수

-- 2. SUM 함수
SELECT SUM(학점) AS 총학점 FROM 수강;                     -- 전체 취득 학점 합계
SELECT SUM(장학금) AS 총장학금 FROM 학생;                  -- 전체 장학금 합계

-- 3. AVG 함수
SELECT AVG(평점) AS 평균평점 FROM 학생;                   -- 전체 학생 평균 평점
SELECT AVG(점수) AS 평균점수 FROM 성적;                   -- 전체 과목 평균 점수

-- 4. MAX, MIN 함수
SELECT MAX(평점) AS 최고평점, MIN(평점) AS 최저평점 FROM 학생;
SELECT MAX(입학일) AS 최근입학일, MIN(입학일) AS 최초입학일 FROM 학생;

-- 5. 여러 함수 조합
SELECT COUNT(*) AS 학생수,
       AVG(평점) AS 평균평점,
       MAX(평점) AS 최고평점,
       MIN(평점) AS 최저평점,
       STDDEV(평점) AS 평점표준편차
FROM 학생;
```

#### 🧩 그룹 함수와 NULL

| 함수 | NULL 처리 방식 |
|------|----------------|
| **COUNT(\*)** | NULL 값도 행으로 계산 |
| **COUNT(컬럼)** | NULL 값 제외하고 계산 |
| **SUM, AVG** | NULL 값 제외하고 계산 |
| **MAX, MIN** | NULL 값 제외하고 계산 |

```sql
-- NULL 처리 예시
-- 전화번호: 10명 중 3명이 NULL인 경우
SELECT COUNT(*) AS 전체학생,           -- 결과: 10
       COUNT(전화번호) AS 연락처보유학생  -- 결과: 7
FROM 학생;
```

#### 🧩 DISTINCT와 그룹 함수
```sql
-- 중복 제거 후 집계
SELECT COUNT(DISTINCT 학과) AS 학과수 FROM 학생;
SELECT AVG(DISTINCT 평점) AS 고유평점평균 FROM 학생;
SELECT SUM(DISTINCT 급여) AS 고유급여합계 FROM 교수;
```

#### 🧩 조건부 집계
```sql
-- CASE문을 이용한 조건부 집계
SELECT COUNT(CASE WHEN 성별 = '남' THEN 1 END) AS 남학생수,
       COUNT(CASE WHEN 성별 = '여' THEN 1 END) AS 여학생수,
       COUNT(*) AS 전체학생수
FROM 학생;

-- WHERE절과 함께 사용
SELECT AVG(평점) AS 컴공과평균평점 
FROM 학생 
WHERE 학과 = '컴퓨터공학과';
```

#### 🧩 그룹 함수 주의사항
- **일반 컬럼과 함께 사용 불가**: GROUP BY 없이는 일반 컬럼과 함께 SELECT 불가
- **중첩 불가**: 그룹 함수 안에 그룹 함수 사용 불가 (예: MAX(COUNT(*)) 불가)
- **WHERE 절 사용 불가**: 그룹 함수는 HAVING 절에서 조건 지정

```sql
-- 잘못된 예시
SELECT 학과, COUNT(*) FROM 학생;  -- 오류: GROUP BY 없이 일반 컬럼과 함께 사용

-- 올바른 예시
SELECT 학과, COUNT(*) FROM 학생 GROUP BY 학과;
```

#### 📝 기출 포맷 예시
- 주요 그룹 함수의 종류와 기능을 설명하시오.
- COUNT(*)와 COUNT(컬럼명)의 차이점은?
- 그룹 함수 사용 시 주의사항은?

#### 🧠 용어 설명
- **그룹 함수**: 여러 행을 그룹화하여 하나의 결과를 반환하는 함수
- **집계 함수**: 그룹 함수와 같은 의미
- **NULL 처리**: 대부분의 그룹 함수는 NULL 값을 제외하고 계산

---

## 🔹 249. 그룹 지정 검색

#### 📘 정의
**그룹 지정 검색**은 **GROUP BY 절**을 사용하여 특정 컬럼의 값이 같은 행들을 하나의 그룹으로 묶고, **HAVING 절**로 그룹에 대한 조건을 지정하는 검색 방법이다.

#### 🧩 기본 구문
```sql
SELECT 컬럼명, 그룹함수
FROM 테이블명
[WHERE 조건]              -- 그룹화 전 행 필터링
GROUP BY 컬럼명           -- 그룹화 기준
[HAVING 그룹조건]         -- 그룹화 후 그룹 필터링
[ORDER BY 컬럼명];        -- 정렬
```

#### 🧩 GROUP BY 규칙
- SELECT 절에 그룹 함수가 아닌 컬럼은 **반드시 GROUP BY 절에 포함**
- GROUP BY 절에 명시된 컬럼만 SELECT 절에서 사용 가능
- **여러 컬럼으로 그룹화** 가능
- **NULL 값들은 하나의 그룹**으로 처리

#### 🧩 WHERE vs HAVING

| 구분 | WHERE | HAVING |
|------|-------|--------|
| **사용 시점** | 그룹화 전 | 그룹화 후 |
| **대상** | 개별 행 | 그룹 |
| **사용 함수** | 일반 함수 | 그룹 함수 가능 |
| **실행 순서** | GROUP BY 전 | GROUP BY 후 |

#### 🧩 실제 예시
```sql
-- 1. 기본 그룹화
-- 학과별 학생 수
SELECT 학과, COUNT(*) AS 학생수
FROM 학생
GROUP BY 학과;

-- 2. 여러 컬럼으로 그룹화
-- 학과별, 학년별 학생 수
SELECT 학과, 학년, COUNT(*) AS 학생수
FROM 학생
GROUP BY 학과, 학년;

-- 3. WHERE와 GROUP BY 함께 사용
-- 3학년 이상 학생들의 학과별 평균 평점
SELECT 학과, AVG(평점) AS 평균평점
FROM 학생
WHERE 학년 >= 3
GROUP BY 학과;

-- 4. HAVING 절 사용
-- 학생 수가 10명 이상인 학과만 조회
SELECT 학과, COUNT(*) AS 학생수
FROM 학생
GROUP BY 학과
HAVING COUNT(*) >= 10;

-- 5. WHERE와 HAVING 동시 사용
-- 3학년 이상 학생 중에서 평균 평점이 3.5 이상인 학과
SELECT 학과, AVG(평점) AS 평균평점
FROM 학생
WHERE 학년 >= 3
GROUP BY 학과
HAVING AVG(평점) >= 3.5;

-- 6. 복잡한 그룹 조건
-- 학과별 최고 평점이 4.0 이상이고 최저 평점이 2.0 이상인 학과
SELECT 학과, 
       COUNT(*) AS 학생수,
       MAX(평점) AS 최고평점,
       MIN(평점) AS 최저평점,
       AVG(평점) AS 평균평점
FROM 학생
GROUP BY 학과
HAVING MAX(평점) >= 4.0 AND MIN(평점) >= 2.0;
```

#### 🧩 다양한 그룹화 예시
```sql
-- 1. 날짜별 그룹화
SELECT DATE(입학일) AS 입학날짜, COUNT(*) AS 입학자수
FROM 학생
GROUP BY DATE(입학일);

-- 2. 연도별 그룹화
SELECT YEAR(입학일) AS 입학년도, COUNT(*) AS 입학자수
FROM 학생
GROUP BY YEAR(입학일);

-- 3. 조건별 그룹화
SELECT 
    CASE 
        WHEN 평점 >= 4.0 THEN 'A등급'
        WHEN 평점 >= 3.0 THEN 'B등급'
        WHEN 평점 >= 2.0 THEN 'C등급'
        ELSE 'D등급'
    END AS 등급,
    COUNT(*) AS 학생수
FROM 학생
GROUP BY 
    CASE 
        WHEN 평점 >= 4.0 THEN 'A등급'
        WHEN 평점 >= 3.0 THEN 'B등급'
        WHEN 평점 >= 2.0 THEN 'C등급'
        ELSE 'D등급'
    END;
```

#### 🧩 실행 순서
```sql
-- SQL 실행 순서
SELECT 학과, AVG(평점) AS 평균평점      -- 5. 결과 선택
FROM 학생                              -- 1. 테이블 선택
WHERE 학년 >= 2                        -- 2. 행 필터링
GROUP BY 학과                          -- 3. 그룹화
HAVING AVG(평점) >= 3.0                -- 4. 그룹 필터링
ORDER BY 평균평점 DESC;                -- 6. 정렬
```

#### 🧩 NULL 값 처리
```sql
-- NULL 값들은 하나의 그룹으로 처리됨
SELECT 전화번호, COUNT(*) AS 학생수
FROM 학생
GROUP BY 전화번호;
-- 전화번호가 NULL인 학생들은 모두 한 그룹으로 계산됨

-- NULL 값 제외하고 그룹화
SELECT 전화번호, COUNT(*) AS 학생수
FROM 학생
WHERE 전화번호 IS NOT NULL
GROUP BY 전화번호;
```

#### 🧩 주의사항
- **SELECT 절 제약**: 그룹 함수가 아닌 컬럼은 GROUP BY에 포함 필요
- **ORDER BY 주의**: GROUP BY 컬럼이나 그룹 함수만 사용 가능
- **성능 고려**: 인덱스가 있는 컬럼으로 그룹화하면 성능 향상

#### 📝 기출 포맷 예시
- GROUP BY와 HAVING의 차이점을 설명하시오.
- WHERE와 HAVING 절의 실행 순서는?
- 그룹화 시 SELECT 절 사용 규칙은?

#### 🧠 용어 설명
- **GROUP BY**: 지정된 컬럼 값이 같은 행들을 그룹화
- **HAVING**: 그룹화된 결과에 조건을 적용
- **그룹화**: 같은 값을 가진 행들을 하나로 묶는 작업

---

## 🔹 250. 집합 연산자를 이용한 통합 질의

#### 📘 정의
**집합 연산자**는 두 개 이상의 SELECT 문의 결과를 하나로 결합하여 **통합된 결과 집합**을 만드는 연산자로, 관계 대수의 집합 연산을 SQL에서 구현한 것이다.

#### 🧩 집합 연산자 종류

| 연산자 | 기능 | 중복 처리 | 예시 |
|--------|------|-----------|------|
| **UNION** | 합집합 (중복 제거) | 제거 | SELECT ... UNION SELECT ... |
| **UNION ALL** | 합집합 (중복 포함) | 포함 | SELECT ... UNION ALL SELECT ... |
| **INTERSECT** | 교집합 | 제거 | SELECT ... INTERSECT SELECT ... |
| **EXCEPT (MINUS)** | 차집합 | 제거 | SELECT ... EXCEPT SELECT ... |

#### 🧩 기본 구문
```sql
SELECT 컬럼1, 컬럼2, ...
FROM 테이블1
[WHERE 조건1]

집합연산자

SELECT 컬럼1, 컬럼2, ...
FROM 테이블2
[WHERE 조건2]
[ORDER BY 컬럼명];
```

#### 🧩 집합 연산자 사용 규칙
- **컬럼 수 일치**: 두 SELECT 문의 컬럼 개수가 같아야 함
- **데이터 타입 호환**: 같은 위치의 컬럼끼리 데이터 타입이 호환되어야 함
- **ORDER BY 위치**: 마지막 SELECT 문 뒤에만 사용 가능
- **컬럼명**: 첫 번째 SELECT 문의 컬럼명 사용

#### 🧩 UNION vs UNION ALL

| 구분 | UNION | UNION ALL |
|------|-------|-----------|
| **중복 처리** | 중복 행 제거 | 중복 행 포함 |
| **성능** | 느림 (중복 검사) | 빠름 |
| **사용 시점** | 중복 제거 필요 시 | 모든 결과 필요 시 |

#### 🧩 실제 예시
```sql
-- 1. UNION (합집합 - 중복 제거)
-- 2020년 또는 2021년 입학생 조회
SELECT 학번, 이름, 입학년도 FROM 학생 WHERE 입학년도 = 2020
UNION
SELECT 학번, 이름, 입학년도 FROM 학생 WHERE 입학년도 = 2021;

-- 2. UNION ALL (합집합 - 중복 포함)
-- 컴퓨터공학과 학생과 우수 학생 모두 조회 (중복 포함)
SELECT 학번, 이름, '컴공과' AS 구분 FROM 학생 WHERE 학과 = '컴퓨터공학과'
UNION ALL
SELECT 학번, 이름, '우수학생' AS 구분 FROM 학생 WHERE 평점 >= 4.0;

-- 3. INTERSECT (교집합)
-- 컴퓨터공학과이면서 평점이 3.5 이상인 학생
SELECT 학번, 이름 FROM 학생 WHERE 학과 = '컴퓨터공학과'
INTERSECT
SELECT 학번, 이름 FROM 학생 WHERE 평점 >= 3.5;

-- 4. EXCEPT/MINUS (차집합)
-- 전체 학생 중 수강신청하지 않은 학생
SELECT 학번, 이름 FROM 학생
EXCEPT
SELECT 학번, 이름 FROM 학생 WHERE 학번 IN (SELECT 학번 FROM 수강신청);
```

#### 🧩 복잡한 집합 연산
```sql
-- 1. 여러 테이블의 통합 조회
-- 학생, 교수, 직원의 연락처 통합 조회
SELECT 이름, 전화번호, '학생' AS 구분 FROM 학생 WHERE 전화번호 IS NOT NULL
UNION
SELECT 이름, 전화번호, '교수' AS 구분 FROM 교수 WHERE 전화번호 IS NOT NULL
UNION
SELECT 이름, 전화번호, '직원' AS 구분 FROM 직원 WHERE 전화번호 IS NOT NULL
ORDER BY 이름;

-- 2. 집합 연산 중첩
-- (A UNION B) INTERSECT C
SELECT 학번 FROM 학생 WHERE 학과 = '컴퓨터공학과'
UNION
SELECT 학번 FROM 학생 WHERE 평점 >= 4.0
INTERSECT
SELECT 학번 FROM 수강신청 WHERE 년도 = 2024;

-- 3. 서브쿼리와 집합 연산
SELECT * FROM 학생 
WHERE 학번 IN (
    SELECT 학번 FROM 성적 WHERE 점수 >= 90
    UNION
    SELECT 학번 FROM 장학생 WHERE 년도 = 2024
);
```

#### 🧩 집합 연산자 우선순위
```sql
-- 괄호를 사용한 우선순위 조정
(SELECT 학번 FROM 학생 WHERE 학과 = '컴공'
 UNION
 SELECT 학번 FROM 학생 WHERE 평점 >= 4.0)
INTERSECT
SELECT 학번 FROM 수강신청;

-- vs.

SELECT 학번 FROM 학생 WHERE 학과 = '컴공'
UNION
(SELECT 학번 FROM 학생 WHERE 평점 >= 4.0
 INTERSECT
 SELECT 학번 FROM 수강신청);
```

#### 🧩 성능 고려사항

| 연산자 | 성능 특성 | 권장사항 |
|--------|-----------|----------|
| **UNION** | 중복 제거로 인한 오버헤드 | 중복이 없다면 UNION ALL 사용 |
| **UNION ALL** | 가장 빠름 | 가능하면 우선 고려 |
| **INTERSECT** | JOIN으로 대체 고려 | EXISTS나 IN 사용 검토 |
| **EXCEPT** | NOT EXISTS로 대체 고려 | 성능 테스트 후 선택 |

#### 🧩 대체 방법
```sql
-- INTERSECT 대신 JOIN 사용
-- 원본: INTERSECT 사용
SELECT 학번 FROM 학생 WHERE 학과 = '컴공'
INTERSECT
SELECT 학번 FROM 우수학생;

-- 대체: JOIN 사용
SELECT DISTINCT s.학번 
FROM 학생 s 
JOIN 우수학생 u ON s.학번 = u.학번 
WHERE s.학과 = '컴공';

-- EXCEPT 대신 NOT EXISTS 사용
-- 원본: EXCEPT 사용
SELECT 학번 FROM 학생
EXCEPT
SELECT 학번 FROM 수강신청;

-- 대체: NOT EXISTS 사용
SELECT 학번 FROM 학생 s
WHERE NOT EXISTS (SELECT 1 FROM 수강신청 WHERE 학번 = s.학번);
```

#### 🧩 집합 연산 결과 처리
```sql
-- 1. 집합 연산 결과를 테이블로 저장
CREATE TABLE 통합명단 AS
SELECT 학번, 이름, '학생' AS 구분 FROM 학생
UNION
SELECT 교수번호, 이름, '교수' AS 구분 FROM 교수;

-- 2. 집합 연산 결과에 추가 조건 적용
SELECT * FROM (
    SELECT 학번, 이름, 평점 FROM 학생 WHERE 학과 = '컴공'
    UNION
    SELECT 학번, 이름, 평점 FROM 학생 WHERE 평점 >= 4.0
) AS 통합결과
WHERE 평점 >= 3.5
ORDER BY 평점 DESC;

-- 3. 집합 연산 결과 개수 계산
SELECT COUNT(*) AS 총개수 FROM (
    SELECT 학번 FROM 학생 WHERE 학과 = '컴공'
    UNION
    SELECT 학번 FROM 학생 WHERE 평점 >= 4.0
) AS 합집합결과;
```

#### 🧩 주의사항
- **NULL 값 처리**: 집합 연산에서 NULL 값들은 동일한 것으로 처리
- **정렬**: ORDER BY는 전체 결과에 대해서만 적용
- **데이터 타입**: 암시적 형변환이 가능한 타입이어야 함
- **성능**: 대용량 데이터에서는 인덱스 활용 고려

#### 📝 기출 포맷 예시
- UNION과 UNION ALL의 차이점을 설명하시오.
- 집합 연산자 사용 시 제약사항은?
- INTERSECT와 JOIN의 차이점은?

#### 🧠 용어 설명
- **집합 연산자**: 두 개 이상의 SELECT 결과를 결합하는 연산자
- **합집합**: 두 집합의 모든 원소를 포함하는 집합
- **교집합**: 두 집합에 공통으로 포함된 원소들의 집합
- **차집합**: 첫 번째 집합에서 두 번째 집합의 원소를 제외한 집합

---

## 🔹 251. JOIN

#### 📘 정의
**JOIN**은 두 개 이상의 테이블을 **관계(외래키)를 통해 연결**하여 여러 테이블의 데이터를 함께 조회하는 방법으로, 관계형 데이터베이스의 핵심 기능이다.

#### 🧩 JOIN의 필요성
- **정규화**: 데이터 중복을 피하기 위해 테이블을 분리
- **관계 활용**: 분리된 테이블들을 연결하여 원하는 정보 조회
- **무결성**: 외래키 관계를 통한 데이터 일관성 보장

#### 🧩 JOIN 종류

| JOIN 종류 | 설명 | 특징 |
|-----------|------|------|
| **INNER JOIN** | 양쪽 테이블에 모두 존재하는 데이터만 | 교집합 |
| **LEFT OUTER JOIN** | 왼쪽 테이블의 모든 데이터 + 매칭되는 오른쪽 데이터 | 왼쪽 기준 |
| **RIGHT OUTER JOIN** | 오른쪽 테이블의 모든 데이터 + 매칭되는 왼쪽 데이터 | 오른쪽 기준 |
| **FULL OUTER JOIN** | 양쪽 테이블의 모든 데이터 | 합집합 |
| **CROSS JOIN** | 두 테이블의 모든 행을 조합 | 곱집합 |
| **SELF JOIN** | 같은 테이블을 자기 자신과 조인 | 별칭 필수 |

#### 🧩 기본 구문
```sql
-- ANSI 표준 (명시적 JOIN)
SELECT 컬럼명
FROM 테이블1 별칭1
JOIN 테이블2 별칭2 ON 조인조건
[WHERE 추가조건];

-- 전통적 방식 (암시적 JOIN)
SELECT 컬럼명
FROM 테이블1 별칭1, 테이블2 별칭2
WHERE 조인조건 [AND 추가조건];
```

#### 🧩 JOIN 조건
- **동등 조인**: 컬럼 값이 같은 경우 (=)
- **비동등 조인**: 범위나 부등호 조건 (>, <, BETWEEN)
- **자연 조인**: 같은 이름의 컬럼으로 자동 조인

#### 🧩 실제 예시
```sql
-- 테이블 구조 예시
-- 학생(학번, 이름, 학과코드)
-- 학과(학과코드, 학과명, 단과대학)

-- 1. INNER JOIN (명시적)
SELECT s.학번, s.이름, d.학과명
FROM 학생 s
JOIN 학과 d ON s.학과코드 = d.학과코드;

-- 2. INNER JOIN (암시적)
SELECT s.학번, s.이름, d.학과명
FROM 학생 s, 학과 d
WHERE s.학과코드 = d.학과코드;

-- 3. 3개 테이블 JOIN
-- 학생 + 학과 + 수강신청
SELECT s.이름, d.학과명, c.과목명
FROM 학생 s
JOIN 학과 d ON s.학과코드 = d.학과코드
JOIN 수강신청 r ON s.학번 = r.학번
JOIN 과목 c ON r.과목코드 = c.과목코드;

-- 4. JOIN과 WHERE 조건 함께
SELECT s.이름, d.학과명
FROM 학생 s
JOIN 학과 d ON s.학과코드 = d.학과코드
WHERE s.학년 >= 3 AND d.단과대학 = '공과대학';
```

#### 🧩 CROSS JOIN
```sql
-- 모든 조합 생성 (카티션 곱)
SELECT s.이름, d.학과명
FROM 학생 s
CROSS JOIN 학과 d;

-- 또는
SELECT s.이름, d.학과명
FROM 학생 s, 학과 d;
-- 주의: WHERE 조건 없으면 CROSS JOIN과 동일
```

#### 🧩 SELF JOIN
```sql
-- 선후배 관계 조회 (같은 학과 내)
SELECT s1.이름 AS 선배, s2.이름 AS 후배
FROM 학생 s1
JOIN 학생 s2 ON s1.학과 = s2.학과 
WHERE s1.학년 > s2.학년;

-- 조직도 조회 (상하급자 관계)
SELECT 상급자.이름 AS 상급자, 하급자.이름 AS 하급자
FROM 직원 상급자
JOIN 직원 하급자 ON 상급자.직원번호 = 하급자.상급자번호;
```

#### 🧩 JOIN 성능 최적화
- **인덱스 활용**: 조인 컬럼에 인덱스 생성
- **조건 최적화**: WHERE 조건을 먼저 처리
- **조인 순서**: 작은 테이블을 먼저 조인
- **적절한 JOIN 타입**: 필요한 데이터만 조회

#### 📝 기출 포맷 예시
- JOIN의 종류와 특징을 설명하시오.
- INNER JOIN과 OUTER JOIN의 차이점은?
- SELF JOIN의 사용법과 예시는?

#### 🧠 용어 설명
- **JOIN**: 두 개 이상의 테이블을 연결하는 연산
- **조인 조건**: 테이블들을 연결하는 기준 조건
- **카티션 곱**: 두 테이블의 모든 행을 조합한 결과

---

## 🔹 252. EQUI JOIN

#### 📘 정의
**EQUI JOIN**은 조인 조건에서 **등호(=) 연산자**를 사용하여 두 테이블의 컬럼 값이 **정확히 일치하는 행**들만을 결합하는 가장 일반적인 조인 방법이다.

#### 🧩 EQUI JOIN 특징
- **등호 조건**: 반드시 = 연산자 사용
- **INNER JOIN**: 기본적으로 INNER JOIN과 동일
- **가장 일반적**: 실무에서 가장 많이 사용되는 조인
- **외래키 관계**: 주로 기본키-외래키 관계에서 사용

#### 🧩 기본 구문
```sql
-- ANSI 표준 방식
SELECT 테이블1.컬럼, 테이블2.컬럼
FROM 테이블1
JOIN 테이블2 ON 테이블1.컬럼 = 테이블2.컬럼;

-- 전통적 방식
SELECT 테이블1.컬럼, 테이블2.컬럼
FROM 테이블1, 테이블2
WHERE 테이블1.컬럼 = 테이블2.컬럼;

-- NATURAL JOIN (자동 EQUI JOIN)
SELECT 컬럼1, 컬럼2
FROM 테이블1
NATURAL JOIN 테이블2;
```

#### 🧩 EQUI JOIN vs NON-EQUI JOIN

| 구분 | EQUI JOIN | NON-EQUI JOIN |
|------|-----------|---------------|
| **조건** | = 연산자 | >, <, >=, <=, BETWEEN |
| **사용 빈도** | 매우 높음 | 낮음 |
| **예시** | 학생.학과코드 = 학과.학과코드 | 급여 BETWEEN 최소급여 AND 최대급여 |

#### 🧩 실제 예시
```sql
-- 1. 기본 EQUI JOIN
-- 학생과 학과 정보 함께 조회
SELECT s.학번, s.이름, s.학과코드, d.학과명
FROM 학생 s
JOIN 학과 d ON s.학과코드 = d.학과코드;

-- 2. 여러 컬럼 EQUI JOIN
-- 학생과 성적 정보 (학번 + 과목코드로 조인)
SELECT s.이름, g.과목코드, g.점수
FROM 학생 s
JOIN 성적 g ON s.학번 = g.학번;

-- 3. 3개 테이블 EQUI JOIN
-- 학생 + 수강신청 + 과목
SELECT s.이름, c.과목명, r.신청일자
FROM 학생 s
JOIN 수강신청 r ON s.학번 = r.학번
JOIN 과목 c ON r.과목코드 = c.과목코드;

-- 4. NATURAL JOIN (자동 EQUI JOIN)
-- 같은 이름의 컬럼으로 자동 조인
SELECT 학번, 이름, 학과명
FROM 학생
NATURAL JOIN 학과;
-- 주의: 학과코드 컬럼이 양쪽 테이블에 있어야 함

-- 5. USING 절 사용
SELECT s.학번, s.이름, d.학과명
FROM 학생 s
JOIN 학과 d USING (학과코드);
```

#### 🧩 별칭과 컬럼 지정
```sql
-- 별칭 사용으로 가독성 향상
SELECT 학생.이름 AS 학생명, 
       학과.학과명 AS 소속학과,
       학과.단과대학 AS 소속대학
FROM 학생
JOIN 학과 ON 학생.학과코드 = 학과.학과코드;

-- 테이블 별칭 사용
SELECT s.이름, d.학과명, d.단과대학
FROM 학생 s
JOIN 학과 d ON s.학과코드 = d.학과코드;

-- 중복 컬럼명 처리
SELECT s.학번, s.이름, s.학과코드 AS 학생_학과코드,
       d.학과코드 AS 학과_학과코드, d.학과명
FROM 학생 s
JOIN 학과 d ON s.학과코드 = d.학과코드;
```

#### 🧩 복잡한 EQUI JOIN 예시
```sql
-- 1. 조건이 있는 EQUI JOIN
-- 공과대학 소속 3학년 이상 학생의 수강 정보
SELECT s.이름, d.학과명, c.과목명, g.점수
FROM 학생 s
JOIN 학과 d ON s.학과코드 = d.학과코드
JOIN 수강신청 r ON s.학번 = r.학번
JOIN 과목 c ON r.과목코드 = c.과목코드
JOIN 성적 g ON s.학번 = g.학번 AND c.과목코드 = g.과목코드
WHERE d.단과대학 = '공과대학' AND s.학년 >= 3;

-- 2. 그룹 함수와 EQUI JOIN
-- 학과별 평균 점수
SELECT d.학과명, AVG(g.점수) AS 평균점수
FROM 학생 s
JOIN 학과 d ON s.학과코드 = d.학과코드
JOIN 성적 g ON s.학번 = g.학번
GROUP BY d.학과명
HAVING AVG(g.점수) >= 80;

-- 3. 서브쿼리와 EQUI JOIN
-- 평균 이상 점수를 받은 학생들의 상세 정보
SELECT s.이름, d.학과명, g.점수
FROM 학생 s
JOIN 학과 d ON s.학과코드 = d.학과코드
JOIN 성적 g ON s.학번 = g.학번
WHERE g.점수 > (SELECT AVG(점수) FROM 성적);
```

#### 🧩 NON-EQUI JOIN 예시 (비교)
```sql
-- 급여 등급 테이블을 이용한 NON-EQUI JOIN
SELECT e.이름, e.급여, s.등급
FROM 직원 e
JOIN 급여등급 s ON e.급여 BETWEEN s.최소급여 AND s.최대급여;

-- EQUI JOIN과 NON-EQUI JOIN 비교
-- EQUI: 정확한 일치
-- NON-EQUI: 범위나 조건 일치
```

#### 🧩 주의사항
- **NULL 값**: NULL과 NULL도 같지 않으므로 조인되지 않음
- **중복 데이터**: 일대다 관계에서 데이터 중복 발생 가능
- **성능**: 조인 컬럼에 인덱스 필요
- **카티션 곱**: 조인 조건 누락 시 모든 조합 생성

#### 📝 기출 포맷 예시
- EQUI JOIN과 NON-EQUI JOIN의 차이점은?
- NATURAL JOIN의 특징과 주의사항은?
- USING 절의 사용법은?

#### 🧠 용어 설명
- **EQUI JOIN**: 등호 조건을 사용하는 조인
- **NATURAL JOIN**: 같은 이름의 컬럼으로 자동 조인
- **NON-EQUI JOIN**: 등호가 아닌 조건을 사용하는 조인

---

## 🔹 253. OUTER JOIN

#### 📘 정의
**OUTER JOIN**은 조인 조건을 만족하지 않는 행도 결과에 포함시키는 조인으로, **한쪽 테이블의 모든 데이터를 보존**하면서 다른 테이블과 조인하는 방법이다.

#### 🧩 OUTER JOIN 종류

| 종류 | 설명 | 키워드 |
|------|------|--------|
| **LEFT OUTER JOIN** | 왼쪽 테이블의 모든 행 보존 | LEFT JOIN |
| **RIGHT OUTER JOIN** | 오른쪽 테이블의 모든 행 보존 | RIGHT JOIN |
| **FULL OUTER JOIN** | 양쪽 테이블의 모든 행 보존 | FULL OUTER JOIN |

#### 🧩 기본 구문
```sql
-- LEFT OUTER JOIN
SELECT 컬럼명
FROM 테이블1
LEFT JOIN 테이블2 ON 조인조건;

-- RIGHT OUTER JOIN  
SELECT 컬럼명
FROM 테이블1
RIGHT JOIN 테이블2 ON 조인조건;

-- FULL OUTER JOIN
SELECT 컬럼명
FROM 테이블1
FULL OUTER JOIN 테이블2 ON 조인조건;
```

#### 🧩 INNER JOIN vs OUTER JOIN

| 구분 | INNER JOIN | OUTER JOIN |
|------|------------|------------|
| **결과** | 양쪽 테이블에 모두 있는 데이터만 | 한쪽 테이블의 모든 데이터 + 매칭되는 데이터 |
| **NULL 처리** | 매칭되지 않는 행 제외 | 매칭되지 않는 부분은 NULL |
| **사용 목적** | 관련 데이터만 조회 | 전체 데이터 현황 파악 |

#### 🧩 실제 예시
```sql
-- 테이블 예시
-- 학생: 학번, 이름, 학과코드
-- 수강신청: 학번, 과목코드, 신청일자

-- 1. LEFT OUTER JOIN
-- 모든 학생 + 수강신청 정보 (수강신청 안 한 학생도 포함)
SELECT s.학번, s.이름, r.과목코드, r.신청일자
FROM 학생 s
LEFT JOIN 수강신청 r ON s.학번 = r.학번;

-- 결과: 수강신청하지 않은 학생은 과목코드, 신청일자가 NULL

-- 2. RIGHT OUTER JOIN
-- 모든 수강신청 + 학생 정보 (학생 정보가 없는 수강신청도 포함)
SELECT s.학번, s.이름, r.과목코드, r.신청일자
FROM 학생 s
RIGHT JOIN 수강신청 r ON s.학번 = r.학번;

-- 결과: 학생 테이블에 없는 학번의 수강신청은 이름이 NULL

-- 3. FULL OUTER JOIN
-- 모든 학생과 모든 수강신청 정보
SELECT s.학번, s.이름, r.과목코드, r.신청일자
FROM 학생 s
FULL OUTER JOIN 수강신청 r ON s.학번 = r.학번;

-- 결과: 양쪽에서 매칭되지 않는 모든 데이터 포함
```

#### 🧩 실무 활용 예시
```sql
-- 1. 수강신청하지 않은 학생 찾기
SELECT s.학번, s.이름
FROM 학생 s
LEFT JOIN 수강신청 r ON s.학번 = r.학번
WHERE r.학번 IS NULL;

-- 2. 모든 학과와 소속 학생 수 (학생이 없는 학과도 포함)
SELECT d.학과명, COUNT(s.학번) AS 학생수
FROM 학과 d
LEFT JOIN 학생 s ON d.학과코드 = s.학과코드
GROUP BY d.학과명;

-- 3. 상품별 판매 현황 (판매되지 않은 상품도 포함)
SELECT p.상품명, COALESCE(SUM(o.수량), 0) AS 총판매량
FROM 상품 p
LEFT JOIN 주문 o ON p.상품코드 = o.상품코드
GROUP BY p.상품명;

-- 4. 직원과 관리자 관계 (관리자가 없는 직원도 포함)
SELECT 직원.이름 AS 직원명, 관리자.이름 AS 관리자명
FROM 직원
LEFT JOIN 직원 관리자 ON 직원.관리자번호 = 관리자.직원번호;
```

#### 🧩 OUTER JOIN과 NULL 처리
```sql
-- 1. COALESCE로 NULL 값 대체
SELECT s.이름, COALESCE(r.과목코드, '수강신청안함') AS 수강상태
FROM 학생 s
LEFT JOIN 수강신청 r ON s.학번 = r.학번;

-- 2. ISNULL/IFNULL로 NULL 값 대체
SELECT s.이름, ISNULL(r.과목코드, '미신청') AS 과목
FROM 학생 s
LEFT JOIN 수강신청 r ON s.학번 = r.학번;

-- 3. CASE문으로 NULL 값 처리
SELECT s.이름,
       CASE 
           WHEN r.과목코드 IS NULL THEN '수강신청 안함'
           ELSE r.과목코드
       END AS 수강과목
FROM 학생 s
LEFT JOIN 수강신청 r ON s.학번 = r.학번;
```

#### 🧩 복잡한 OUTER JOIN
```sql
-- 1. 다중 테이블 OUTER JOIN
-- 모든 학생 + 수강신청 + 성적 (일부 정보가 없어도 학생은 모두 포함)
SELECT s.이름, r.과목코드, g.점수
FROM 학생 s
LEFT JOIN 수강신청 r ON s.학번 = r.학번
LEFT JOIN 성적 g ON s.학번 = g.학번 AND r.과목코드 = g.과목코드;

-- 2. OUTER JOIN + WHERE 조건
-- 2024년 수강신청한 학생 + 신청하지 않은 모든 학생
SELECT s.이름, r.신청일자
FROM 학생 s
LEFT JOIN 수강신청 r ON s.학번 = r.학번 AND r.년도 = 2024;

-- 3. OUTER JOIN + 집계함수
-- 학과별 수강신청 현황 (신청자가 없는 학과도 포함)
SELECT d.학과명, COUNT(r.학번) AS 신청자수
FROM 학과 d
LEFT JOIN 학생 s ON d.학과코드 = s.학과코드
LEFT JOIN 수강신청 r ON s.학번 = r.학번
GROUP BY d.학과명;
```

#### 🧩 성능 고려사항
- **인덱스**: 조인 컬럼에 인덱스 필요
- **데이터 크기**: 큰 테이블을 LEFT에 두면 성능 저하
- **필터링**: WHERE 조건을 ON 절에 포함할지 고려
- **NULL 처리**: 불필요한 NULL 체크 최소화

#### 📝 기출 포맷 예시
- LEFT JOIN과 RIGHT JOIN의 차이점은?
- OUTER JOIN에서 NULL 값이 나오는 경우는?
- INNER JOIN과 OUTER JOIN의 결과 차이를 설명하시오.

#### 🧠 용어 설명
- **OUTER JOIN**: 조인 조건을 만족하지 않는 행도 포함하는 조인
- **LEFT JOIN**: 왼쪽 테이블의 모든 행을 보존하는 조인
- **NULL 보완**: 매칭되지 않는 부분을 NULL로 채우는 방식

---

## 🔹 254. 트리거 (Trigger)

#### 📘 정의
**트리거(Trigger)**는 데이터베이스에서 **특정 이벤트가 발생할 때 자동으로 실행**되는 저장 프로시저로, 데이터의 무결성 유지와 비즈니스 규칙 적용을 위해 사용된다.

#### 🧩 트리거 특징
- **자동 실행**: 사용자가 직접 호출하지 않음
- **이벤트 기반**: INSERT, UPDATE, DELETE 시 실행
- **투명성**: 애플리케이션에서 인식하지 못함
- **무결성 보장**: 데이터 일관성 유지

#### 🧩 트리거 종류

| 분류 기준 | 종류 | 설명 |
|-----------|------|------|
| **실행 시점** | BEFORE | 이벤트 발생 전 실행 |
|              | AFTER | 이벤트 발생 후 실행 |
|              | INSTEAD OF | 이벤트 대신 실행 (뷰에서 사용) |
| **이벤트** | INSERT | 행 삽입 시 |
|           | UPDATE | 행 수정 시 |
|           | DELETE | 행 삭제 시 |
| **단위** | ROW TRIGGER | 각 행마다 실행 |
|         | STATEMENT TRIGGER | 문장당 한 번 실행 |

#### 🧩 기본 구문
```sql
-- 트리거 생성
CREATE TRIGGER 트리거명
{BEFORE | AFTER | INSTEAD OF} {INSERT | UPDATE | DELETE}
ON 테이블명
[FOR EACH ROW]
BEGIN
    트리거 본문
END;

-- 트리거 삭제
DROP TRIGGER 트리거명;

-- 트리거 비활성화/활성화
ALTER TRIGGER 트리거명 DISABLE;
ALTER TRIGGER 트리거명 ENABLE;
```

#### 🧩 트리거 내부 변수

| 변수 | 설명 | 사용 시점 |
|------|------|-----------|
| **NEW** | 새로운 값 (삽입/수정 후) | INSERT, UPDATE |
| **OLD** | 이전 값 (수정/삭제 전) | UPDATE, DELETE |

#### 🧩 실제 예시
```sql
-- 1. AFTER INSERT 트리거 - 로그 기록
CREATE TRIGGER tr_student_insert_log
AFTER INSERT ON 학생
FOR EACH ROW
BEGIN
    INSERT INTO 학생로그 (학번, 이름, 작업구분, 작업일시)
    VALUES (NEW.학번, NEW.이름, 'INSERT', NOW());
END;

-- 2. BEFORE UPDATE 트리거 - 데이터 검증
CREATE TRIGGER tr_student_update_check
BEFORE UPDATE ON 학생
FOR EACH ROW
BEGIN
    IF NEW.평점 < 0 OR NEW.평점 > 4.5 THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = '평점은 0~4.5 사이여야 합니다';
    END IF;
END;

-- 3. AFTER DELETE 트리거 - 관련 데이터 정리
CREATE TRIGGER tr_student_delete_cleanup
AFTER DELETE ON 학생
FOR EACH ROW
BEGIN
    DELETE FROM 수강신청 WHERE 학번 = OLD.학번;
    DELETE FROM 성적 WHERE 학번 = OLD.학번;
    
    INSERT INTO 삭제로그 (학번, 이름, 삭제일시)
    VALUES (OLD.학번, OLD.이름, NOW());
END;

-- 4. 집계 테이블 유지 트리거
CREATE TRIGGER tr_order_summary_update
AFTER INSERT ON 주문
FOR EACH ROW
BEGIN
    UPDATE 월별집계 
    SET 주문건수 = 주문건수 + 1,
        주문금액 = 주문금액 + NEW.금액
    WHERE 년월 = DATE_FORMAT(NEW.주문일자, '%Y-%m');
END;
```

#### 🧩 트리거 활용 예시
```sql
-- 1. 자동 순번 부여
CREATE TRIGGER tr_auto_sequence
BEFORE INSERT ON 게시글
FOR EACH ROW
BEGIN
    IF NEW.글번호 IS NULL THEN
        SET NEW.글번호 = (SELECT COALESCE(MAX(글번호), 0) + 1 FROM 게시글);
    END IF;
END;

-- 2. 상태 변경 이력 관리
CREATE TRIGGER tr_status_history
AFTER UPDATE ON 주문
FOR EACH ROW
BEGIN
    IF OLD.주문상태 <> NEW.주문상태 THEN
        INSERT INTO 상태변경이력 (주문번호, 이전상태, 새상태, 변경일시)
        VALUES (NEW.주문번호, OLD.주문상태, NEW.주문상태, NOW());
    END IF;
END;

-- 3. 재고 관리
CREATE TRIGGER tr_inventory_update
AFTER INSERT ON 주문상세
FOR EACH ROW
BEGIN
    UPDATE 상품 
    SET 재고수량 = 재고수량 - NEW.주문수량
    WHERE 상품코드 = NEW.상품코드;
    
    IF (SELECT 재고수량 FROM 상품 WHERE 상품코드 = NEW.상품코드) < 0 THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = '재고가 부족합니다';
    END IF;
END;

-- 4. 감사(Audit) 트리거
CREATE TRIGGER tr_salary_audit
AFTER UPDATE ON 직원
FOR EACH ROW
BEGIN
    IF OLD.급여 <> NEW.급여 THEN
        INSERT INTO 급여변경감사 (직원번호, 이전급여, 새급여, 변경자, 변경일시)
        VALUES (NEW.직원번호, OLD.급여, NEW.급여, USER(), NOW());
    END IF;
END;
```

#### 🧩 트리거 제어문
```sql
-- 1. 조건문 사용
CREATE TRIGGER tr_grade_validation
BEFORE INSERT ON 성적
FOR EACH ROW
BEGIN
    IF NEW.점수 < 0 OR NEW.점수 > 100 THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = '점수는 0~100 사이여야 합니다';
    ELSEIF NEW.점수 >= 90 THEN
        SET NEW.등급 = 'A';
    ELSEIF NEW.점수 >= 80 THEN
        SET NEW.등급 = 'B';
    ELSEIF NEW.점수 >= 70 THEN
        SET NEW.등급 = 'C';
    ELSE
        SET NEW.등급 = 'F';
    END IF;
END;

-- 2. 변수 사용
CREATE TRIGGER tr_complex_calculation
AFTER INSERT ON 주문
FOR EACH ROW
BEGIN
    DECLARE discount_rate DECIMAL(3,2) DEFAULT 0.00;
    DECLARE final_amount DECIMAL(10,2);
    
    -- 할인율 계산
    IF NEW.주문금액 >= 100000 THEN
        SET discount_rate = 0.10;
    ELSEIF NEW.주문금액 >= 50000 THEN
        SET discount_rate = 0.05;
    END IF;
    
    -- 최종 금액 계산
    SET final_amount = NEW.주문금액 * (1 - discount_rate);
    
    -- 결과 저장
    UPDATE 주문 SET 할인율 = discount_rate, 최종금액 = final_amount 
    WHERE 주문번호 = NEW.주문번호;
END;
```

#### 🧩 트리거 주의사항

| 주의사항 | 설명 | 해결방안 |
|----------|------|----------|
| **성능 저하** | 모든 DML 작업 시 실행 | 최소한의 로직만 포함 |
| **무한 루프** | 트리거 내에서 같은 테이블 수정 | 조건 검사로 방지 |
| **디버깅 어려움** | 자동 실행으로 추적 곤란 | 로그 테이블 활용 |
| **데이터 일관성** | 롤백 시 트리거 작업도 롤백 | 트랜잭션 단위 고려 |

#### 🧩 트리거 vs 제약조건

| 구분 | 트리거 | 제약조건 |
|------|--------|----------|
| **실행 시점** | 이벤트 발생 시 | 데이터 입력 시 |
| **복잡도** | 복잡한 로직 가능 | 단순한 규칙만 |
| **성능** | 상대적으로 느림 | 빠름 |
| **유지보수** | 어려움 | 쉬움 |

#### 🧩 트리거 모니터링
```sql
-- 1. 트리거 정보 조회
SELECT TRIGGER_NAME, EVENT_MANIPULATION, ACTION_TIMING, TABLE_NAME
FROM INFORMATION_SCHEMA.TRIGGERS
WHERE TABLE_SCHEMA = 'your_database';

-- 2. 트리거 실행 로그
CREATE TABLE 트리거실행로그 (
    로그번호 INT AUTO_INCREMENT PRIMARY KEY,
    트리거명 VARCHAR(100),
    테이블명 VARCHAR(100),
    실행시간 TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    실행내용 TEXT
);

-- 트리거 내에서 로그 기록
INSERT INTO 트리거실행로그 (트리거명, 테이블명, 실행내용)
VALUES ('tr_student_insert', '학생', CONCAT('학번: ', NEW.학번, ' 삽입'));
```

#### 🧩 대안 기술

| 대안 | 설명 | 장점 | 단점 |
|------|------|------|------|
| **저장 프로시저** | 명시적 호출 | 제어 가능 | 수동 실행 |
| **애플리케이션 로직** | 코드에서 처리 | 유연성 | 일관성 위험 |
| **이벤트 스케줄러** | 정기적 실행 | 배치 처리 | 실시간 아님 |

#### 🧩 트리거 성능 최적화
```sql
-- 1. 조건 최적화
CREATE TRIGGER tr_optimized_update
AFTER UPDATE ON 학생
FOR EACH ROW
BEGIN
    -- 평점이 실제로 변경된 경우에만 실행
    IF OLD.평점 <> NEW.평점 THEN
        UPDATE 학과통계 
        SET 평균평점 = (SELECT AVG(평점) FROM 학생 WHERE 학과 = NEW.학과)
        WHERE 학과 = NEW.학과;
    END IF;
END;

-- 2. 배치 처리 고려
CREATE TRIGGER tr_batch_friendly
AFTER INSERT ON 주문
FOR EACH ROW
BEGIN
    -- 실시간 집계 대신 플래그 설정
    UPDATE 집계상태 SET 갱신필요 = 1 WHERE 구분 = '일별주문';
END;
```

#### 📝 기출 포맷 예시
- 트리거의 종류와 실행 시점을 설명하시오.
- BEFORE 트리거와 AFTER 트리거의 차이점은?
- 트리거 사용 시 주의사항을 3가지 이상 설명하시오.

#### 🧠 용어 설명
- **트리거**: 특정 이벤트 발생 시 자동 실행되는 프로시저
- **NEW/OLD**: 트리거에서 사용하는 행 참조 변수
- **FOR EACH ROW**: 각 행마다 트리거 실행을 의미
- **SIGNAL**: 트리거에서 오류를 발생시키는 명령

---
