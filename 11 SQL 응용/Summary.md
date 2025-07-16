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

# 🎯 SQL 응용 - SELECT 기본 완전정리

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