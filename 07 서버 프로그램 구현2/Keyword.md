## 158. 모듈 (Module)

- [ ] **프로그램을 구성하는 독립적인 단위**, 특정 기능을 수행하는 **하위 프로그램 또는 부품**
- [ ] **모듈화 목적**: 변경 용이성, 재사용성, 분업 개발, **정보 은닉**, **응집도 증가/결합도 감소**
- [ ] **특징**: 각 모듈을 독립적으로 개발 가능, 모듈 단위로 다른 프로그램에서 활용
- [ ] **핵심 지표**: **응집도는 높게, 결합도는 낮게** = 좋은 모듈 구조
- [ ] **전체 시스템을 기능별로 분리**하여 설계하는 방식

---

## 159. 결합도 (Coupling)

- [ ] **모듈 간 상호 의존성의 정도**를 나타내는 지표
- [ ] **낮은 결합도 = 좋은 설계** (유지보수 용이, 변경 영향 최소화, 재사용성 증가)
- [ ] **높은 결합도 = 나쁜 설계** (하나의 변경이 전체 시스템에 연쇄 영향)
- [ ] **모듈화 설계의 핵심 원칙**: **결합도는 낮게, 응집도는 높게**
- [ ] 모듈 간 연결이 **약할수록** 더 좋은 모듈화 구조

---

## 160. 결합도의 종류 (Types of Coupling)

**낮은 결합도(👍) → 높은 결합도(❌) 순서:**

- [ ] **자료 결합** (Data): **단순한 데이터 값만 전달** (함수(a, b)) - **가장 낮음** 👍
- [ ] **스탬프 결합** (Stamp): **전체 자료 구조 전달** (함수(객체 obj)) - 낮음
- [ ] **제어 결합** (Control): **제어 변수(플래그)**로 흐름 제어 (함수(flag)) - 중간
- [ ] **외부 결합** (External): **외부 환경, 장치, 포맷**에 의존 (파일 포맷 직접 참조) - 높음
- [ ] **공통 결합** (Common): **전역 데이터 공유** (전역 변수 사용) - 매우 높음
- [ ] **내용 결합** (Content): 한 모듈이 **다른 모듈 내부 직접 접근** (GOTO, 함수 내부 변수 접근) - **가장 높음** ❌

---

## 161. 응집도 (Cohesion)

- [ ] **하나의 모듈 내부 구성 요소들이 얼마나 밀접하게 관련되어 있는지** 정도
- [ ] **모듈이 단일 기능에 얼마나 집중되어 있는가** 측정, **응집도는 높을수록 좋은 설계**
- [ ] **높은 응집도 = 좋은 설계** (명확한 책임, 유지보수 용이, 재사용성 우수)
- [ ] **낮은 응집도 = 나쁜 설계** (여러 책임 뒤섞여 모듈 목적 불분명)
- [ ] **모듈화 핵심 원칙**: **응집도는 높게, 결합도는 낮게**

---

## 162. 응집도의 종류 (Types of Cohesion)

**높은 응집도(👍) → 낮은 응집도(❌) 순서:**

- [ ] **기능적 응집** (Functional): **하나의 기능 수행**을 위해 구성 요소들이 긴밀히 협력 (정렬 기능) - **가장 높음** 👍
- [ ] **순차적 응집** (Sequential): **출력이 다음 작업의 입력**이 되어 처리 (데이터 읽기→가공→저장) - 높음
- [ ] **통신적 응집** (Communicational): **동일한 데이터 사용** 또는 동일한 입출력 수행 (하나의 고객 정보로 조회·수정) - 보통 이상
- [ ] **절차적 응집** (Procedural): **순서대로 수행**되지만 기능 간 연관 낮음 (로그인→로그기록) - 보통
- [ ] **시간적 응집** (Temporal): **특정 시점에 함께 수행**되지만 기능 무관 (시스템 시작 시 초기화) - 낮음
- [ ] **논리적 응집** (Logical): **유사한 기능을 하나로 묶고** 제어문으로 구분 (여러 출력 함수) - 낮음
- [ ] **우연적 응집** (Coincidental): **아무 관련 없는 기능**이 하나로 묶임 (잡다한 기능 모음) - **가장 낮음** ❌

---

## 163. 팬인 / 팬아웃 (Fan-in / Fan-out)

- [ ] **팬인(Fan-in)**: 특정 모듈을 **호출하는 다른 모듈의 수**
- [ ] **팬아웃(Fan-out)**: 특정 모듈이 **호출하는 다른 모듈의 수**
- [ ] **모듈 간 의존성 관계 수**를 측정하는 지표, **구조적 복잡도와 결합도 수준** 판단 기준
- [ ] **팬인 높음**: 재사용성 높음, 중심 모듈로 기능 집중
- [ ] **팬아웃 높음**: 결합도 증가, 설계 품질 저하 가능
- [ ] **이상적 구조**: **팬인은 높게, 팬아웃은 낮게** 유지

---

## 164. N-S 차트 (Nassi-Shneiderman Chart)

- [ ] **구조적 프로그래밍 표현**을 위한 **도형 기반의 순서도**, **제어 논리를 박스 형태로 표현**
- [ ] **구성**: 순차(위→아래 순서), 선택(조건 분기), 반복(루프 처리)
- [ ] **특징**: **GOTO 문 사용 불가** (구조적 프로그램 설계 적합), 순차도 대비 명확한 논리 흐름
- [ ] **코드 흐름을 구조화**하여 시각적으로 명확하게 표현
- [ ] 조건 분기와 루프 처리가 **직관적으로** 보임

---

## 165. 단위 모듈 (Unit Module)

- [ ] **하나의 명확한 기능을 수행**하도록 설계된 **가장 작은 독립 모듈 단위**
- [ ] **단위 테스트(Unit Test)의 대상**이 되는 최소 코드 블록, **함수 또는 서브루틴 단위**
- [ ] **특징**: 독립적 기능 수행, **하나의 입·출력과 명확한 목적**, 높은 응집도/낮은 결합도
- [ ] **과정**: 단위 기능 명세서 작성 → 입출력 기능 구현 → 알고리즘 구현
- [ ] 재사용성과 유지보수성 향상에 기여

---

## 166. IPC (Inter-Process Communication)

- [ ] **프로세스 간 통신**, 독립된 프로세스들이 **데이터를 주고받기 위한 메커니즘**
- [ ] **주요 방식**: 메시지 큐(큐 형태 저장) + **공유 메모리**(하나의 메모리 영역 공유) + **세마포어**(동기화 제어용 카운터)
- [ ] **소켓**(네트워크 기반 통신, 다른 시스템 간 통신) + **파이프/네임드 파이프**(단방향/양방향 연결)
- [ ] **용도**: 프로세스 간 동기화, 데이터 공유, 메시지 전달
- [ ] 운영체제에서 독립된 프로세스들의 협력 작업 지원

---

## 167. 테스트 케이스 (Test Case)

- [ ] **소프트웨어 요구사항이 올바르게 구현되었는지 검증**하기 위해 설계된 **테스트 단위**
- [ ] **구성요소**: **식별자**(고유 번호) + **입력값**(테스트 데이터) + **실행 조건**(사전 환경/상태) + **기대 결과**(정확한 결과) + **판정 기준**(Pass/Fail)
- [ ] **입력값, 실행 조건, 기대 결과, 판정 기준** 등을 포함한 문서
- [ ] 정확한 테스트 수행과 **결과 판단을 위해 필수적**
- [ ] 소프트웨어 검증을 위한 **명확한 조건과 결과** 명시

---

## 168. 공통 모듈 명세 기법의 종류

- [ ] **모듈의 기능, 인터페이스, 동작**을 명확히 기술하여 **효율적이고 일관된 모듈 관리** 가능한 문서화 방법
- [ ] **명세 기법**: 사양 명세서 + 의사 코드(Pseudocode) + 순서도(Flowchart) + 상태도 + 유스케이스 다이어그램 + 인터페이스 명세서
- [ ] **품질 속성 5가지**: **정확성**(실제 요구사항과 일치) + **명확성**(이해 쉽고 분명) + **완전성**(모든 요구사항 포함)
- [ ] **일관성**(모순 없이 체계적) + **추적성**(요구사항과 명세 간 연관 관계 추적 가능)
- [ ] **정확성, 명확성, 완전성, 일관성, 추적성** 품질 속성 준수 필요

---

## 169. 재사용 (Reuse)

- [ ] **이미 개발된 소프트웨어 구성 요소**를 **새로운 시스템이나 다른 프로젝트에서 다시 사용**
- [ ] **종류**: 코드 재사용(소스 코드 활용) + 모듈 재사용 + 컴포넌트 재사용 + 설계 재사용
- [ ] **규모별 분류**: **함수**(작은 기능 단위) + **객체**(클래스/객체) + **컴포넌트**(독립 기능 단위) + **애플리케이션**(큰 단위)
- [ ] **장점**: 개발 시간 단축, 비용 절감, 품질 향상(검증된 코드), 유지보수 용이
- [ ] 효율적인 개발과 유지보수, **비용 절감** 목적

---

## 170. 코드의 주요 기능

- [ ] **식별**: 처리 대상 **데이터나 객체를 구분**하는 기능
- [ ] **분류**: 데이터를 **유형이나 특성에 따라 구분**하는 기능
- [ ] **배열**: **의미부여 또는 일정한 순서나 구조로 정렬**하는 기능
- [ ] **표준화**: 데이터나 처리 과정을 **일관된 형식으로 통일**
- [ ] **간소화**: 복잡한 처리 과정을 **단순하고 효율적으로** 만드는 기능

---

## 171. 코드의 종류 (Types of Code)

- [ ] **순차 코드**: **일련번호 순**으로 코드 부여 (학번 001, 002)
- [ ] **블록 코드**: **공통 성질별로 블록**을 나누어 구분 (1000번대 전자과)
- [ ] **10진 코드**: **숫자 0~9만 사용**하는 코드
- [ ] **그룹분류 코드**: **계층적으로 분류** (대분류-중분류-소분류)
- [ ] **연상 코드**: **기억하기 쉬운 의미 있는 문자나 약어** 사용 (MON, TUE)
- [ ] **표의 숫자 코드**: **코드 자체가 의미를 가지는** 숫자 코드 (생년월일 930315)
- [ ] **합성 코드**: **두 가지 이상의 코드 방식을 결합**한 형태

---

## 172. 디자인 패턴 (Design Patterns)

- [ ] 소프트웨어 설계 시 **자주 발생하는 문제를 해결하기 위한 재사용 가능한 설계 템플릿**
- [ ] **모듈 간의 관계 및 인터페이스 설계** 시 참조할 수 있는 **전형적인 해결 방식**
- [ ] **특징**: 재사용 가능, 일관성, 효율성 향상, **커뮤니케이션 도구**(개발자 간 의사소통)
- [ ] **3대 분류**: **생성 패턴**(객체 생성) + **구조 패턴**(클래스/객체 구성) + **행위 패턴**(객체 간 상호작용/책임 분배)
- [ ] 효율적이고 **유지보수성이 높은 소프트웨어** 제작 도움

---

## 173. 생성 패턴 (Creational Patterns)

- [ ] **객체 생성과 관련된 문제 해결** 디자인 패턴, **객체 생성 과정을 캡슐화**
- [ ] **싱글톤(Singleton)**: 클래스의 **인스턴스를 하나만 생성**, 전역으로 접근 가능
- [ ] **팩토리 메서드(Factory Method)**: **객체 생성 인터페이스 정의**, 하위 클래스에서 구체적 생성 결정
- [ ] **추상 팩토리(Abstract Factory)**: **관련된 객체들의 집합을 생성**하는 인터페이스
- [ ] **빌더(Builder)**: **복합 객체의 생성 과정을 분리**하여 단계별 생성
- [ ] **프로토타입(Prototype)**: **기존 객체를 복제**하여 새로운 객체 생성

---

## 174. 구조 패턴 (Structural Patterns)

- [ ] **클래스나 객체를 조합하여 더 큰 구조** 만드는 패턴, **객체 간 관계를 쉽게 만들고 유연성** 향상
- [ ] **어댑터(Adapter)**: **인터페이스가 맞지 않는 클래스들을 연결**
- [ ] **데코레이터(Decorator)**: 객체에 **동적으로 기능을 추가**
- [ ] **프록시(Proxy)**: 실제 객체에 접근할 때 **대리인 역할**
- [ ] **브리지(Bridge)**: **구현과 추상을 분리**하여 독립적 변형 가능
- [ ] **컴포지트(Composite)**: 객체들을 **트리 구조로 구성**하여 부분-전체 계층 표현
- [ ] **퍼사드(Facade)**: 복잡한 서브시스템에 **단순한 인터페이스 제공**
- [ ] **플라이웨이트(Flyweight)**: **공유 가능한 객체 사용**해 메모리 절약

---

## 175. 행위 패턴 (Behavioral Patterns)

- [ ] **클래스나 객체들이 서로 상호작용하는 방법**이나 **책임 분배 방법** 정의하는 패턴
- [ ] **책임 연쇄(Chain of Responsibility)**: 요청 처리할 객체가 여러 개일 때 **순서대로 처리 책임** 넘김
- [ ] **커맨드(Command)**: **요청을 객체로 캡슐화**해 재사용, 취소 등 가능
- [ ] **인터프리터(Interpreter)**: **언어의 문법을 클래스 형태로** 표현해 해석
- [ ] **반복자(Iterator)**: 자료 구조에 **내부 구조 노출하지 않고 순차적으로 접근**
- [ ] **중재자(Mediator)**: 객체들 간의 **복잡한 상호작용을 중재**해 결합도 감소
- [ ] **메멘토(Memento)**: 객체의 **내부 상태를 저장하고 복원**
- [ ] **옵서버(Observer)**: 객체 상태 변화 시 **관련 객체에게 자동으로 통보**
- [ ] **상태(State)**: **객체 상태에 따라** 동일한 동작을 다르게 처리
- [ ] **전략(Strategy)**: **알고리즘 군을 캡슐화**하여 필요에 따라 교체 가능
- [ ] **템플릿 메서드(Template Method)**: 상위 클래스에서 **알고리즘 골격 정의**, 하위 클래스가 구체화
- [ ] **방문자(Visitor)**: 각 클래스별로 **처리 기능을 분리**하여 별도 클래스로 구성

---

## 176. crontab 명령어 작성 방법

- [ ] 리눅스/유닉스 시스템에서 **주기적으로 작업을 자동 실행**하기 위한 명령어
- [ ] **5개 필드**: **분**(0~59) + **시**(0~23) + **일**(1~31) + **월**(1~12) + **요일**(0~6, 0=일요일)
- [ ] **특수문자**: **`*`**(모든 값) + **`,`**(값 목록 구분) + **`-`**(범위 지정) + **`/`**(증가 단위)
- [ ] **예시**: `30 3 * * *` (매일 오전 3시 30분), `0 6 * * 1` (매주 월요일 오전 6시)
- [ ] 특정 시간, 날짜, 주기로 **명령이나 스크립트를 예약 실행**