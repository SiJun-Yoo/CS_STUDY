# DB

1. [Database](#database)
2. [Schema](#schema)
3. [DBMS(Database Management System)](#dbmsdatabase-management-System)
4. [DBMS(Relational Database Management System)](#rdbmsrelational-database-management-system )
   - [키(Key)](###키key)
5. [조인(Join)]()
6. [SQL,NoSQL]()
7. [정규화]()
8. [트랜잭션]()
9. [이상]()
10. [RDBMS & NoSQL]
11. [Isolation Level]()
---



### Database

- 정의

  - 데이터를 저장하는 곳

  - **여러 사람이 공유하고 사용할 목적으로 체계화해 통합,관리되는 정보의 집합**
  - 자료 파일을 통합하여 자료 항목의 **중복을 없애고 자료를 구조화하여 기억**시켜 놓은 자료의 집합체

- 특징
  - `실시간 접근` :  사용자 요구에 즉시 응답
  - `계속적 변화` : 데이터 삽입, 삭제, 수정을 통하여 최신 데이터를 동적으로 유지 가능
  - `내용 기반 참조` : 데이터를 참조할 때 데이터가 저장된 주소나 위치가 아닌 내용으로 참조
  - `동시 공유` : 여러 이용자가 동시에 원하는 데이터를 공유
  - `데이터 독립성` : 응용프로그램과 데이터베이스를 독립시킴으로써 데이터 논리적 구조를 변경시키더라도 응용프로그램은 변경되지 않는다.
- 장단점
  - 장점
    - 데이터 중복 최소화
    - 데이터 공유
    - 일관성, 무결성, 보안성 유지
    - 최신의 데이터 유지
    - 데이터의 표준화 기능
    - 데이터의 논리적, 물리적 독립성
    - 용이한 데이터 접근
    - 데이터 저장 공간 절약
  - 단점
    - 데이터베이스 전문가 필요
    - 많은 비용 부담
    - 데이터 백업과 복구가 어려움
    - 시스템의 복잡함
    - 대용량 디스크로 엑세스가 집중되면 과부하 발생



### Schema

: 데이터베이스의 구조와 제약조건에 관해 전반적인 명세를 기술한 것

- 스키마의 3계층
  - 스키마는 사용자의 관점에 따라 외부 스키마, 개념 스키마, 내부 스키마로 나뉜다
  - DBMS는 외부적 스키마에 따라 명시된 사용자의 요구를 개념적 스키마에 적합한 형태로 변경하고 이를 다시 내부적 스키마에 적합한 형태로 변환한다.
  - `외부 스키마(External Schema)` : 사용자나 프로그래머의 입장에서 데이터베이스의 모습으로 조직의 일부분을 정의한 것
  - `개념 스키마(Conceptual Schema)` :  모든 응용 시스템과 사용자들이 필요로하는 데이터를 통합한 조직 전체의 데이터베이스 구조를 논리적으로 정의한 것
  - `내부 스키마(Internal Schema)` : 물리적 저장장치의 입장에서 본 데이터베이스 구조로, 물리적인 저장장치와 밀접한 계층

![img](https://media.vlpt.us/images/ash3767/post/7a1fd722-8012-47a5-9b3a-f4512e309447/image.png) ![스키마](https://t1.daumcdn.net/cfile/tistory/9936823A5B698C4023)



### DBMS(Database Management System)

: **데이터베이스 내의 데이터를 접근 및 조작 할 수 있도록 해주는 소프트웨어 도구의 집합** , 사용자 또는 다른 프로그램의 요구를 처리하고 적절히 응답하여 데이터를 사용할 수 있도록 해준다.

- MySql, Oracle, MSSql, MongoDB 등



### RDBMS(Relational Database Management System) 

: RDB를 생성하고 수정하고 관리할 수 있는 소프트웨어, **관계형 모델을 기반으로하는 DBMS 유형**

- RDB(Relational Database) : **관계형 데이터 모델**에 기초를 둔 데이터 베이스 , 모든 데이터를 2차원의 테이블 형태로 표현한다

- 관계형 데이터 모델

  - `릴레이션(Relation)`
    - 개체를 표현하기 위한 데이터 구조로서 2차원 테이블로 표현
    - heading(스키마) , body(본체)로 구성
      - heading은 속성(attribute)이 n개가 모인 집합이며, 이름과 데이터형으로 구성
      - body는 속성값의 집합인 튜플(tuple)의 집합
    - SQL의 테이블과 대응
  - `튜플(Tuples)`
    - 하나의 개체를 의미하고 Relation에서 행으로 표현하며, 이를 릴레이션 상태(Relation State)라고도 함
    - 각 튜플은 유일해야 한다는 특징을 가지고 있음
    - SQL의 row와 대응
  - `속성(Attributes)`
    - 개체의 속성들을 의미하며 Relation에서 열로 표현
    - SQL의 column과 대응

  ![img](https://t1.daumcdn.net/cfile/tistory/99F23C505A77D5700B) ![img](https://media.vlpt.us/images/sysop/post/ede750c2-ec03-43d7-bad0-9de78b7cefe9/image.png)

  - #### 키(Key)

    : 데이터베이스에서 조건에 만족하는 튜플 검색 및 정렬시 다른 튜플들과 구별할 수 있는 유일한 기준이 되는 속성(Attribute)

    - 조건

      - **유일성** : 키로 하나의 튜플을 유일하게 식별할 수 있어야 한다. 즉, 키 값이 같은 튜플은 존재하지 않아야함
      - **최소성** : 꼭 필요한 최소한의 속성으로만 구성해야 한다.

    - 종류

      **<학생> 릴레이션** 

      | 학번 | 주민번호       | 성명   | 성별 |
      | ---- | -------------- | ------ | ---- |
      | 1001 | 810429-1231457 | 김형석 | 남   |
      | 1002 | 800504-1546781 | 김현천 | 남   |
      | 1002 | 811216-2547842 | 류기선 | 여   |
      | 1003 | 910322-1233445 | 홍영선 | 여   |

      **<수강> 릴레이션**

      | 학번 | 과목명 |
      | ---- | ------ |
      | 1001 | 영어   |
      | 1001 | 전산   |
      | 1002 | 영어   |
      | 1003 | 수학   |
      | 1004 | 영어   |
      | 1004 | 전산   |

      1. **후보키(Candidate Key)**

         - 릴레이션을 구성하는 속성들 중에서 **튜플을 유일하게 식별할 수 있는 속성들의 부분집합**
         - **모든 릴레이션은 반드시 하나 이상의 후보키를 가져야** 함
         - 릴레이션에 있는 모든 튜플에 대해서 **유일성, 최소성을 만족**시켜야 함

      2. **기본키(Primary Key)**

         - 후보키 중에서 선택한 Main Key
         - 한 릴레이션에서 **특정 튜플을 유일하게 구별할 수 있는 속성**
         - **NULL 값을 가질 수 없음** (개체 무결성의 첫번째 조건)
         - 기본키로 정의된 속성에는 **동일한 값이 중복되어 저장될 수 없음**(개체 무결성의 두번째 조건)

      3. **고유키(Unique Key)**

         - 테이블에 있는 데이터를 유일하게 식별
           - 값이 중복되지 않음
           - 값을 입력하지 않아도 된다. (NULL 허용)
         - 중복된 값을 허용하지 않지만 여러 개의 NULL 값은 허용
           - NULL 값은 비교 불가능함으로 여러 개 있어도 중복된 값이 아니기 때문이다
         - 고유 인덱스가 자동 생성됨

      4. Primary Key 와 Unique Key 차이점

         - Primary Key와 Unique Key는 유일함이라는 조건을 만족하는 것은 공통적
         - 하지만 Primary Key는 테이블당 하나만 생성할 수 있고, Unique Key는 여러 개 생성 가능
         - 또한, Primary Key는 NULL 값을 가질 수 없지만, Unique Key는 가질 수 있음
         - 

      5. **대체키(Alternate Key)**

         - **후보키가 둘 이상일 때 기본키를 제외한 나머지 후보키**

         - 보조키라고도 함

      6. **슈퍼키(Super Key)**

         - **슈퍼키는 한 릴레이션 내에 있는 속성들의 집합으로 구성된 키**로서 릴레이션을 구성하는 모든 튜플 중 슈퍼키로 구성된 속성의 집합과 동일한 값은 나타내지 않음
         - 릴레이션을 구성하는 모든 튜플에 대해 **유일성은 만족하지만, 최소성은 만족시키지 못함**

      7. **외래키(Foreign key)**

         - 관계를 맺고 있는 릴레이션 R1, R2에서 R1이 참조하고 있는 릴레이션의 R2의 기본키와 같은 R1 릴레이션의 속성을 외래키라고 함
         - 즉, **두 테이블을 서로 연결하는 데 사용하는 키**
         - 외래키는 참조되는 릴레이션의 기본키와 대응되어 릴레이션 간에 참조관계를 표현하는데 중요한 도구
         - 외래키로 지정되면 참조 테이블의 기본키에 없는 값을 입력할 수 없다.(참조 무결성)

    - 무결성 제약 조건

      - 


# index

## 왜?

* 책의 색인, 배열의 index 모두 빠르게 데이터를 조회하기 위한 것으로 DB의 index와 그 목적이 같다.
* 데이터에 대한 검색속도를 향상 시키기 위한 자료구조
* 테이블 내의 1개의 컬럼 혹은 여러개의 컬럼을 이용해 생성될 수 있다.

>
'느려'

index를 사용하지 않은 컬럼들을 조회 할 때 테이블 전체를 탐색(Table Full Scan)해야한다. 그렇기 때문에 처리속도가 떨어진다. Table Full Scan을 하지 않으려고 index를 만들어 데이터 관리를 한다.

## 인덱스 장/단점

장점

* 검색 속도 향상
* 시스템의 부하를 줄일 수 있다.

단점

* 추가 저장공간이 필요하다.
* 삽입,삭제,갱신이 빈번한 컬럼에서는 성능이 저하될 수 있음

## 언제?

* 삽입,삭제,갱신이 적은 컬럼 
* 데이터의 중복도가 낮은 컬럼
* 검색,join등이 자주 발생하는 컬럼
* 규모가 큰 테이블

## 삽삭갱과 index
>
index가 적용된 컬럼에 insert,update,delete가 수행된다면 일련의 연산을 추가적으로 진행하고 그에 따른 오버헤드가 발생한다.

* insert : 새로운 데이터에 인덱스를 추가해야함
* delete : 삭제하는 데이터의 인덱스를 사용하지 않는다는 작업을 진행해야함
* update : 기존의 인덱스를 사용하지 않음 처리하고 갱신된 데이터에 대해 인덱스를 추가해야함

## 문제점
>삭제와 갱신이 빈번하게 일어난다면?

인덱스는 정렬된 상태로 저장이 되는데 insert는 기존에 데이터를 뒤로 밀어야하는 경우가 발생할 수 있어서 비효율적이다.
update와 delete는 인덱스를 삭제하는게 아니라 사용하지  않음 처리를 해준다. 그렇기 때문에 인덱스가 계속 누적되어 sql처리시에 오히려 성능저하가 나타날 수 있다. 그래서 사용하지 않는 index는 바로 제거를 해주어야한다.

## 어떻게?
> 해쉬와 B+Tree를 이용해 구현함

* DB 인덱스에서 해시 테이블이 사용되는 경우는 제한적인데, 그러한 이유는 해시가 등호(=) 연산에만 특화되었기 때문이다. 해시 함수는 값이 1이라도 달라지면 완전히 다른 해시 값을 생성하는데, 이러한 특성에 의해 부등호 연산(>, <)이 자주 사용되는 데이터베이스 검색을 위해서는 해시 테이블이 적합하지 않다.

* B+Tree는 자식노드가 2개 이상인 B-Tree를 개선시킨 자료구조로서 리프노드에만 인덱스와 데이터를 가지고 있고 나머지 노드들은 데이터를 위한 인덱스만을 갖는다.
![](https://images.velog.io/images/dbtlwns/post/b0197a7c-d51f-4736-8663-a01552466db8/image.png)

## 인덱스 예시
![](https://images.velog.io/images/dbtlwns/post/8841fe0e-8d30-49fe-8568-aff35ec38bcd/image.png)
## 출처 및 참고사이트
* [망나니개발자님 블로그](https://mangkyu.tistory.com/96)
* [위키백과 인덱스](https://ko.wikipedia.org/wiki/%EC%9D%B8%EB%8D%B1%EC%8A%A4_(%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4))

# 트랜잭션 (Transaction)
- 트랜잭션이란
   - 데이터베이스의 상태를 변화시키는 하나의 논리적인 작업 단위이며, 여러개의 연산이 수행될 수 있다.
   ```
   트랜잭션의 예(A계좌에서 B계좌로 일정 금액을 이체)
      1. A계좌의 잔액을 확인
      2. A계좌의 금액에서 이체할 금액을 빼고 다시 저장
      3. B계좌의 잔액을 확인
      4. B계좌의 금액에서 이체할 금액을 더하고 다시 저장
   이러한 과정을 모두 합쳐 계좌이체라는 하나의 작업단위를 구성
   ```
   - 수행중에 한 작업이라도 실패하면 전부 실패하고, 모두 성공해야 성공이라고 할 수 있다.
   - 하나의 트랜재션은 Commit, Rollback 된다.
      - Commit
         - 한개의 논리적 단위에 대한 작업(트랜잭션)에 대한 작업이 성공적으로 끝나 데이터베이스가 다시 일관된 상태에 있을 때, 이 트랜잭션이 행한 갱신 연산이 완료된 것을 트랜잭션 관리자에게 알려주는 연산
      - Rollback
         - 하나의 트랜잭션 처리가 비정상적으로 종료되어 데이터베이스의 일관성을 깨뜨렸을 때, 이 트랜잭션의 일부가 정상적으로 처리되었어도 트랜잭션이 행한 모든 연산을 취소하는 연산
 - 트랜잭션의 성질(ACID)
    - Atomicity(원자성)
       - 트랜잭션의 모든 연산이 정상적으로 수행 완료되거나, 아니면 전혀 어떠한 연산도 수행되지 않은 상태를 보장
    - Consistency(일관성)
       - 트랜잭션이 성공적으로 완료되면 일관적인 DB상태를 유지
       - 일관성이란 위의 계좌이체 예제에서 금액의 데이터 타입이 정수(integer)에서 문자열(String)으로 되지않는 것
    - Isolation(독립성)
       - 트랜잭션 수행시 다른 트랜잭션의 작업이 끼어들지 못하도록 보장하는 것
       - 트랜잭션은 동시에 실행될 경우 다른 트랜잭션에 의해 영향을 받지 않고 독립적으로 실행되어야 함.
    - Durability(지속성)
       - 성공적으로 수행된 트랜잭션은 영원히 반영
 - 트랜잭션의 필요성
    -  DB서버에 여러 개의 클라이언트가 동시에 액세스 하거나 응용프로그램이 갱신을 처리하는 과정에서 중단될 수 있는 경우 등 데이터 부정합을 방지하고자 할 때 사용
    -  트랜잭션에서 중요한 것은 스케줄 관리, 스케줄을 잘못 짜면 데드락에 빠지게 됨
 - 트랜잭션 격리 수준
    - Isolation Level(격리 수준)이란
       - 각기 다른 트랜잭션들이 서로에게서 어느 정도 격리되어 있는지를 나타냄
    - Lsolation Level의 종류
       - Read Uncommitted (레벨0)
          - 잠금을 일절 실행하지 않아 미처 커밋되지 않고 트랜잭션이 진행 중인 기록조차도 조회할 수 있도록 하는 격리 수준
          - 어떤 사용자가 A라는 데이터를 B라는 데이터로 변경하는 동안 다른 사용자는 아직 완료되지 않은(Uncommitted 혹은 Dirty) 트랜잭션이지만 변경된 데이터인 B를 읽을 수 있다.
       - Read Committed (레벨1)
          - 어떤 트랜잭션의 변경 내용이 Commit 되어야만 다른 트랜잭션에서 조회할 수 있다.
       - Repeatable Read (레벨2)
          - 트랜잭션이 시작되기 전에 커밋된 내용에 대해서만 조회할 수 있는 격리 수준
       - Serializable (레벨3)
          - 읽기 작업에도 공유 잠금을 설정, 동시에 다른 트랜잭션에서 이 레코드를 변경하지 못함
          - 동시처리 능력이 다른격리수준보다 떨어지고, 성능 저하가 발생     
   - 낮은 단계의 Isolation Level에서 발생하는 현상
     ![isolation-level](https://user-images.githubusercontent.com/61149599/124345150-0bc64f80-dc12-11eb-8bb7-8c92d56bdac9.png)
      - Dirty Read
         - 커밋되지 않은 수정 중인 데이터를 다른 트랜잭션에서 읽을 수 있도록 허용할 때 발생하는 현상
      - Non-Repeatable Read
         - 한 트랜잭션에서 같은 쿼리를 두번 수행할 때 그 사이에 다른 트랜잭션이 값을 수정 또는 삭제함으로써 두 쿼리의 결과가 상이하게 나타나는 비 일관성 현상
      - Phantom Read
         - 한 트랜잭션 내에서 같은 쿼리문이 실행되었음에도 불구하고 조회 결과가 다른 경우
         - 트랜잭션 도중 새로운 레코드가 삽입되는 것을 허용하기 때문에 나타난다.
> https://joont92.github.io/db/%ED%8A%B8%EB%9E%9C%EC%9E%AD%EC%85%98-%EA%B2%A9%EB%A6%AC-%EC%88%98%EC%A4%80-isolation-level/

### Database와 DBMS 그리고 SQL
   - Databse란 일반적으로 컴퓨터 시스템에 전자 방식으로 저장된 구조화된 정보 또는 데이터의 체계적인 집합을 의미합니다.
   - DBMS란(DataBase Management System) 사용자와 데이터베이스 사이에서 사용자의 요구에 따라 정보를 생성해 주고 데이터베이스를 관리해 주는 소프트웨어입니다.
   - SQL이란(Strucured Query Language) 관계형 데이터베이스 관리 시스템의 데이터를 관리하기 위해 설계된 특수 목적의 프로그래밍 언어이며 관계형 데이터베이스 관리 시스템에서 자료의 검색과 관리, 데이터베이스 스키마 생성과 수정, 데이터베이스 객체 접근 조정 관리를 위해 고안되었습니다.

### RDBMS 
   - 위에서 DBMS는 사용자와 데이터베이스 사이에서 사용자의 요구에 따라 정보를 생성해주고 데이터베이스를 관리해 주는 소프트웨어라고 설명을 했습니다. 
   - 또한 기존의 RDBMS에서의 저장 방식은 SQL에 의해 저장되고 있으며 정해진 스키마에 따라 데이터를 저장하여야 합니다. RDBMS에는 DBMS앞에 R이 붙어 있습니다. 
      - 이 R은(Relational)의 약자로 RDBMS는 관계형 데이터베이스 관리 시스템을 의미합니다. 
      - 이름과 같이 RDBMS는 RDB를 관리하는 시스템이며 RDB는 관계형 데이터 모델을 기초로 두고 모든 데이터를 2차원 테이블 형태로 표현하는 데이터베이스입니다. 
------------
   - 관계형 데이터베이스(RDMBS)는 아래와와 같이 구성된 테이블이 다른 테이블들과 관계를 맺고 모여있는 집합체로 이해할 수 있습니다.
   - 관계형 데이터베이스(RDMBS)에서는 이러한 관계를 나타내기 위해 `외래 키(foreign key)`라는 것을 사용합니다.
   - 이러한 테이블간의 관계에서 외래 키를 이용한 테이블 간 Join이 가능하다는 게 RDBMS의 가장 큰 특징입니다.

![image](https://user-images.githubusercontent.com/77487962/125055461-2d2bad80-e0e2-11eb-83ea-27ee5dd920e2.png)
------------
### NoSQL
   - NoSQL이란(Not Only SQL)의 약자로 말 그대도 위에서 설명한 RDB 형태의 관계형 데이터베이스가 아닌 다른 형태의 데이터 저장 기술을 의미하고 있습니다. 또한 NoSQL에서는 RDBMS와는 달리 테이블 간 관계를 정의하지 않습니다. 데이터 테이블은 그냥 하나의 테이블이며 테이블 간의 관계를 정의하지 않아 일반적으로 테이블 간 `Join도 불가능`합니다. 

   - NoSQL은 점점 빅데이터의 등장으로 인해 데이터와 트래픽이 기하급수적으로 증가함에 따라 RDBMS에 단점인 성능을 향상시키기 위해서는 장비가 좋아야 하는 Scale-Up의 특징이 비용을 기하급수적으로 증가시키기 때문에 데이터 `일관성은 포기`하되 비용을 고려하여 `여러 대의 데이터에 분산하여 저장하는 Scale-Out을 목표`로 등장하였습니다.

 `NoSQL을 하면 가장 유명한 Document 기반의 MongoDB를 많이 떠올리지만 MongoDB는 NoSQL한 종류로 NoSQL은 하기와 같이 다양한 형태의 저장 기술을 지원하고 있습니다.`

   - 이 다양한 형태의 저장기술은 RDBMS 스키마에 맞추어 데이터를 관리해야 된다는 한계를 극복하고 `수평적 확장성(Scale-out)을 쉽게 할 수 있다는 장점`을 가지고 있습니다.

 

   #### 1. Key-Value Database

   **Key-Value Database**는 데이터가 `Key와 Value의 쌍`으로 저장된다.
   - Key는 Value에 접근하기 위한 용도로 사용되며, 값은 어떠한 형태의 데이터라도 담을 수 있다. 
   - 심지어는 이미지나 비디오도 가능하다. 
   - 또한 간단한 API를 제공하는 만큼 질의의 속도가 굉장히 빠른 편이다. 
   `대표적인 NoSQL Key-Value Model로는 Redis, Riak, Amazon Dynamo DB 등이 있다.`
 

   #### 2. Document Database

   **Documnet Database** 데이터는 `Key와Document의 형태`로 저장된다. Key-Value 모델과 다른 점이라면 Value가 계층적인 형태인 도큐먼트로 저장된다는 것이다. 
   - 객체지향에서의 객체와 유사하며, 이들은 하나의 단위로 취급되어 저장된다. 다시 말해 하나의 객체를 여러 개의 테이블에 나눠 저장할 필요가 없어진다는 뜻이다. 
   - 주요한 특징으로는 객체-관계 매핑이 필요하지 않다. 객체를 Document의 형태로 바로 저장 가능하기 때문이다. 
   - 또한 검색에 최적화되어 있는데, 이는 Ket-Value 모델의 특징과 동일하다. 단점이라면 사용이 번거롭고 쿼리가 SQL과는 다르다는 점이다. 
   - 도큐먼트 모델에서는 질의의 결과가 JSON이나 xml 형태로 출력되기 때문에 그 사용 방법이 RDBMS에서의 질의 결과를 사용하는 방법과 다르다. 
   `대표적인 NoSQL Document Model로는 MongoDB, CouthDB 등이 있다.`
 

   #### 3. Wide Column Database

   **Column-family Model 기반의 Database**이며 이전의 모델들이 Key-Value 값을 이용해 필드를 결정했다면, 특이하게도 이 모델은 `키에서 필드를 결정`한다. 
   - 키는 Row(키 값)와 Column-family, Column-name을 가진다. 연관된 데이터들은 같은 Column-family 안에 속해 있으며, 각자의 Column-name을 가진다. 관계형 모델로 설명하자면 어트리뷰트가 계층적인 구조를 가지고 있는 셈이다. 
   - 이렇게 저장된 데이터는 하나의 커다란 테이블로 표현이 가능하며, 질의는 Row, Column-family, Column-name을 통해 수행된다.
   `대표적인 NoSQL Column-family Model로는 HBase, Hypertable 등이 있다.`
 

   #### 4. Graph Database 

   **Graph Model Model**에서는 데이터를 `Node와 Edge, Property와 함께 그래프 구조를 사용`하여 데이터를 표현하고 저장하는 Database입니다.
   - 개체와 관계를 그래프 형태로 표현한 것이므로 관계형 모델이라고 할 수 있으며, 데이터 간의 관계가 탐색의 키일 경우에 적합하다. 
   - 페이스북이나 트위터 같은 소셜 네트워크에서(내 친구의 친구를 찾는 질의 등) 적합하고, 연관된 데이터를 추천해주는 추천 엔진이나 패턴 인식 등의 데이터베이스로도 적합하다.
   `대표적인 NoSQL Graph Model로는 Neo4J가 있다.`
 

### RDBMS와 NoSQL의 장단점
#### RDBMS
   `장점`
   ```
      - RDBMS는 위에서 설명을 하였듯이 정해진 스키마에 따라 데이터를 저장하여야 하므로 명확한 데이터 구조를 보장하고 있습니다. 
      - 또한 관계는 각 데이터를 중복없이 한 번만 저장할 수 있습니다.
   ```
   `단점`
   ```
      -  테이블간테이블 간 관계를 맺고 있어 시스템이 커질 경우 JOIN문이 많은 복잡한 쿼리가 만들어질 수 있습니다.
      -  성능 향상을 위해서는 서버의 성능을 향상 시켜야하는 Scale-up만을 지원합니다. 이로 인해 비용이 기하급수적으로 늘어날 수 있습니다.
      -  스키마로 인해 데이터가 유연하지 못합니다. 나중에 스키마가 변경 될 경우 번거롭고 어렵습니다.
   ```
#### NoSQL
   `장점`
   ```
      - NoSQL에서는 스키마가 없기 때문에 유연하며 자유로운 데이터 구조를 가질 수 있습니다. 
      - 언제든 저장된 데이터를 조정하고 새로운 필드를 추가할 수 있습니다.
      - 데이터 분산이 용이하며 성능 향상을 위한 Saclue-up 뿐만이 아닌 Scale-out 또한 가능합니다.
   ```
   `단점`
   ```
      - 데이터 중복이 발생할 수 있으며 중복된 데이터가 변경 될 경우 수정을 모든 컬렉션에서 수행을 해야 합니다.
      - 스키마가 존재하지 않기에 명확한 데이터 구조를 보장하지 않으며 데이터 구조 결정가 어려울 수 있습니다.
   ```

### RDBMS, NoSQL 언제 사용해야 될까요?
   **RDBMS**는 데이터 구조가 명확하며 변경 될 여지가 없으며 `명확한 스키마가 중요한 경우` 사용하는 것이 좋습니다.<br />
   또한 중복된 데이터가 없어(데이터 무결성) 변경이 용이하기 때문에 관계를 맺고 있는 데이터가 자주 변경이 이루어지는 시스템에 적합합니다. 

   **NoSQL**은 정확한 데이터 구조를 알 수 없고 `데이터가 변경/확장이 될 수 있는 경우`에 사용하는 것이 좋습니다.<br />
   또한 단점에서도 명확하듯이 데이터 중복이 발생할 수 있으며 `중복된 데이터가 변경될 시`에는 `모든 컬렉션에서 수정`을 해야 합니다.<br />
   이러한 특징들을 기반으로 Update가 많이 이루어지지 않는 시스템이 좋으며,<br />
   또한 Scale-out이 가능하다는 장점을 활용해 막대한 데이터를 저장해야 해서 Database를 Scale-Out를 해야 되는 시스템에 적합합니다.

### JDBC vs SQLMapper vs ORM

> 공통점 

* Persistence(영속성): 프로그램의 실행이 종료되더라도 사라지지 않는 데이터의 특성
#### JDBC (Java Database Connectivity)
![](https://images.velog.io/images/dbtlwns/post/03e2f8c5-963e-47cd-9a63-5d440c515700/image.png)
* 자바에서 데이터베이스에 접속할 수 있도록 하는 자바 API
* 각 DB와의 연결을 드라이버를 통해 하며 DB종류에 종속적이지 않다.
* 중복 코드가 많고 Connection관리를 계속 해야함.

#### SQLMapper
* 객체(Object)와 SQL 문을 매핑하여 데이터를 객체화하는 기술
* 객체와 관계를 매핑하기보다는 SQL문의 질의 결과와 객체를 매핑시켜줌
> Spring JDBC

![](https://images.velog.io/images/dbtlwns/post/66765372-2445-4288-a189-edfba829befc/image.png)
* JDBC API만을 사용할 때보다, Connection에 대한 Configuration을 JdbcTemplate이라는 클래스에 담아 Spring을 통해 주입받음. 또, 메소드에 쿼리를 매핑해두고 RowMapper를 통해 쿼리 메소드의 결과를 통해 DB의 각 row마다 하나의 인스턴스화를 지원해준다.

> MyBatis

* 복잡한 JDBC 코드가 없다.
* 결과값을 매핑하는 객체가 없다.
* 설정이 간단하고 Java 코드에서 SQL을 쓰는 것을 분리했다. 즉 관심사를 분리하였다.
![](https://images.velog.io/images/dbtlwns/post/db1450c3-b510-4712-9d0b-1e394c6fcd85/image.png)
#### 한계점
```java
public class Student{
	private int id;
    	private String name;
}
```
* Student라는 클래스가 있다.
```java
public class Student{
	private int id;
    	private String name;
    	private String nickName;//새로 추가됨
}
```
* nickName이라는 멤버변수가 추가된다면 SQL구문도 다 수정이 필요하다.(강한 의존 관계)
```java
public class Student{
	private int id;
    	private String name;
    	private Team team; // 새로 추가됨
}
```
* team이라는 객체가 또 추가 된다면?
* 멤버변수가 객체인 class는 실제 RDB에서는 Team의 id를 외래키로 관계를 표현해주는 형태로 나타낼 것 이다. 객체지향과 RDB에서의 괴리감이 있다.(패러다임의 불일치)
> **물리적으로 SQL과 JDBC API를 데이터 접근 계층에 숨기는데 성공했을지는 몰라도, 논리적으로는 엔티티와 아주 강한 의존 관계를 가지고 있다.** - 김영한님  
#### ORM
> JPA(Java Persistence API)

![](https://images.velog.io/images/dbtlwns/post/1b252cf5-7849-4c9d-9ab8-328bd49de1bf/image.png)
* JPA는 표준 인터페이스가 있다.
* 이를 구현하는 구현체중 하나가 Hibernate이고, 그 외 다양하게 존재한다.
* 핵심모델은 EntityManager와 영속성 컨텍스트이다.
![](https://images.velog.io/images/dbtlwns/post/74e862aa-b1a1-49a5-8596-94ebdf5e5737/image.png)
* EntityManager가 Entity를 관리함
* Entity는 persist를 통해 PersistenceContext에 올라옴
* 그 상태에서 EntityManager에게 관리를 받음
* flush()가 발생하면 DB에 접근하고 SQL을 생성함.
* 쿼리를 개발자가 관리하지 않고 EntityManager에게 위임
![](https://images.velog.io/images/dbtlwns/post/5315f608-3f71-469c-877b-3abd8945335b/image.png)
* Lazy Loading: 사용 상황에 알맞게 Proxy 객체를 사용해 필요한 정보만 가져오기 위한 Concept
* Dirty Checking: 해당 객체의 변경 사항만 관리하는 Concept
* Caching: DB의 Connection을 최소화해 효율적으로 사용할 수 있도록 가능하면 Cache를 사용하는 Concept

> Spring Data JPA

* SpringData진영에서 만든 JPA
* EntityManager가 복잡하기 때문에 Spring에서 한번 더 추상화를 해 개발자가 보다 편리하게 이를 이용할 수 있도록 제공
*  interface 형태로 Repository를 제공해 개발자는 이를 가져다 사용
![](https://images.velog.io/images/dbtlwns/post/fae810bd-c7eb-4884-9cb2-9c7ef55e0deb/image.png)

> Spring Data JDBC

![](https://images.velog.io/images/dbtlwns/post/e532f89e-f8ab-42fa-b524-63baf2044417/image.png)
* Hibernate와 같은 기술을 사용하지 않고 JDBC API를 그대로 직접 구현해서 사용하는 방식으로 동작된다. 
* Spring Data 이므로 Repository 개념은 그대로 갖고 있다.

### [ 정규화 ]
#### 개념
* 테이블을 무손실 분해 하는 과정
* 테이블 간에 중복된 데이터를 허용하지 않는 목표를 통해 무결성(Integrity)을 유지할 수 있으며, DB의 저장 용량 역시 줄일 수 있다
* 1정규화 ~ 5정규화 로 갈 수록 엄격한 조건을 갖추어 단계적으로 진행된다
* 반드시 높은 정규화가 답은 아닐 수 있으니 인지해야 함
    
 너무 분해하면 JOIN시 큰 비용이 발생
 -> 이렇게 되면 결국 비 정규화를 통해 다시 합치는 과정이 필요

#### 종류
##### 제 1정규화(1NF)
* 모든 속성의 도메인이 원자 값으로만 이루어짐
##### 제 2정규화(2NF)
* 기본키가 아닌 속성들은 기본키에 대해 완전 함수적 종속인 관계
* 기본키의 부분집합이 어떤 속성을 결정하는 결정자가 되어서는 안됨!
![1정규화](https://user-images.githubusercontent.com/77487962/130339306-9f1733aa-8671-493f-8c1c-f16afdddd0c3.PNG)

현재 강좌이름이라는 기본키의 부분집합이 강의실이라는 속성의 결정자라서 제2정규형 만족 X
-> 테이블을 분리해서 따로 유지해야 함

![2정규화](https://user-images.githubusercontent.com/77487962/130339313-59c1100b-a2b5-4562-809c-13be58e06d8b.PNG)

##### 제 3정규화(3NF)
* 기본키가 아닌 속성들은 기본키에 대해 이행적 함수적 종속이 아닌 관계
* 이행적 종속이라는 것은 A->B, B->C 일 때 A->C가 성립되는 것
![3정규화](https://user-images.githubusercontent.com/77487962/130339324-8c85320a-f411-4008-89b2-999f10254553.PNG)

##### BCNF 정규화
* 모든 결정자는 후보키를 만족하는 것
![BCNF](https://user-images.githubusercontent.com/77487962/130339345-c02bcbd1-edfd-41b1-87d6-4bf2b2b83f35.PNG)

현재 교수는 특강이름을 결정하는 결정자이지만, 모든 튜플을 유일하게 식별하는 후보키가 아님 -> 테이블 분리 필요
![BCNF2](https://user-images.githubusercontent.com/77487962/130339356-ca3a5875-866b-42a6-a883-c092d3963819.PNG)

##### 제 4정규화 / 제 5정규화는 아래 참조
4정규화 및 5정규화 참조글
https://zzozzomin08.tistory.com/12

### [ 비 정규화 ]
#### 개념
* 의도적으로 정규화를 위배하여 성능 향상 및 편의성을 이루는 과정
* 시스템의 성능과 효율성은 증가되지만, 데이터의 일관성과 정합성은 저하될 수 있음
#### 장점 & 단점
##### 장점
* 빠른 데이터 조회 -> JOIN 비용이 줄어듬
* 데이터 조회 쿼리가 간단해짐 -> 버그 발생 가능성 하락
##### 단점
* 데이터 갱신이나 삽입 비용이 높음 -> 테이블이 커지기 때문
* 데이터간의 일관성과 정합성이 저하될 수 있음
* 데이터를 중복 저장하여 더 많은 저장공간이 필요
#### 종류
* 테이블 통합
    - 두 테이블의 조인이 많이 사용되는 경우 하나의 테이블로 합치는 것
* 테이블 분할
    - 특정 속성 혹은 레코드가 많이 사용되는 경우 테이블을 수직 / 수평으로 분할
* 중복 테이블 추가
    - 여러 테이블에서 데이터를 자주 추출할 때 차라리 하나의 중복 테이블을 추가하는 방법
* 중복 속성 추가
    - 조인해서 데이터를 처리할 때 데이터를 조회하는 경로를 단축하기 위해 사용
# 레디스 (Redis)

+ #### NOSQL(Not Only SQL)란

  + RDBMS는 `관계형 데이터베이스` 라고 하며, NOSQL은 `비관계형 데이터베이스`이다. 보통 NOSQL은 `Key-Value형(키-벨류형)`, `Wide Column형(열 지향와디이드형)`,`Document형(문서형)`을 이용한다.

> `NOSQL`은 왜 사용하나?
>
> ​	아주 많은 양의 데이터를 효율적으로 처리가 필요할 때, 데이터의 분산처리, 빠른 쓰기 및 데이터의 안정성이 필요할 때 사용
>
> ​	특정서버에 장애가 발생했을 때에도 데이터 유실이나 서비스 중지가 없는 형태의 구조이기 때문이다.	



+ #### 레디스(Redis)란

  + REDIS(REmote Dictionary Server)는 메모리 기반의 `Key-Value형` 구조 데이터 관리 시스템이며, 모든 데이터를 메모리에 저장하고 조회하기에 빠른 Read, Write 속도를 보장하는 비 관계형 데이터베이스
  + Redis는 크게 5가지 `String`,`Set`,`Sorted Set`, `Hash`, `List`의 데이터 형식을 지원
  + Redis는 빠른 오픈 소스인 메모리 키-값 데이터 구조 스토어이며, 다양한 인 메모리 데이터 구조 집합을 제공하므로 사용자 정의 애플리케이션을 손쉽게 생성할 수 있다.



+ #### Redis와 Memcached 비교

 ![](https://images.velog.io/images/qjatn1009/post/b77ddc01-3e70-4499-906f-ae00f32cd0d6/image.png)

  > 추가
  >
  > 1. Memcached는 멀티 스레드를 지원하고 Redis는 싱글스레드 기반 동작
  >
  >    > Redis는 싱글 스레드이기 때문에 처리 시간이 긴 명령어가 들어오면 그 뒤 명령어들은 전부 대기가 필요





> Redis 추가적인 내용
>
> <https://velog.io/@hyeondev/Redis-란-무엇일까>

## Transaction이란

데이터베이스에서 하나의 논리적 작업 단위를 구성하는 일련의 연산들의 집합을 **트랜잭션**이라고 한다.

트랜잭션은 ***A.C.I.D*** 성질이라고 하는 다음의 네 가지 성질로 설명된다.

- **A**tomicity
    - 트랜잭션의 모든 연산들이 정상적으로 수행 완료되거나 아니면 전혀 어떠한 연산도 수행되지 않은 상태를 보장 (0 or 1)
- **C**onsistency
    - 고립된 트랜잭션의 수행이 데이터베이스의 **일관성**을 보존
    - 트랜잭션 수행 전후의 데이터베이스 상태는 각각 일관성이 보장되는 서로 다른 상태
- **I**solation
    - 여러 트랜잭션이 동시에 수행되더라도 각각의 트랜잭션은 다른 트랜잭션의 수행에 영향을 받지 않고 독립적으로 수행되어야 한다.
- **D**urability
    - 트랜잭션이 성공적으로 완료되어 커밋되고 나면, 해당 트랜잭션에 의한 모든 변경은 향후에 어떤 소프트웨어나 하드웨어 장애가 발생되더라도 보존되어야 한다.

## Isolation Level

먼저 **isolation level**이란 트랜잭션에서 일관성이 없는 데이터를 허용하도록 하는 수준을 의미한다.

**ANSI**(미국 국가표준 협회)에서 작성된 SQL-92 표준은 **네 종류**의 Isolation Level을 정의하고 있으며 SQL Server 7.0은 이 표준을 준수합니다. 

**Isolation Level을 조정하는 경우** 동시성이 증가되는데 반해 데이터의 무결성에 문제가 발생할 수 있거나, 데이터의 무결성을 완벽하게 유지하는 데 반하여 동시성이 떨어질 수 있으므로 그 기능을 완벽하게 이해한 후에 사용해야 합니다.

![Untitled](https://user-images.githubusercontent.com/77487962/134809872-7bc34996-b272-415c-831c-1b5125c17478.png)


isolation level에 따른 부작용, isolation level이 낮을 수록 부작용이 커진다.

---

## Isolation Level에 따라 나타나는 현상 3가지

먼저 Isolation Level에 따라 나타나는 현상을 보고 가겠습니다.

### 1. Dirty Read

어떤 트랜잭션에서 아직 실행이 끝난지 않은 다른 트랜잭션에 의한 변경 사항을 보게 되는 되는 경우를 **dirty read** 라고 합니다. 

만약 원래 트랜잭션에서 그 변경 사항을 **롤백(`rollback`)**하면 그 데이터를 읽은 트랜잭션은 **dirty data**를 가지고 있다고 말합니다.

### 2. Repeatable Read

어떤 트랜잭션에서 같은 질의를 사용했을 때 **질의(`select`)**를 아무리 여러번 해도 그리고 다른 트랜잭션에서 아무리 여러 번 그 행을 **변경(`update`)**해도 항상 같은 데이터만 읽어드리는 경우를 **repeatable read** 라고 합니다.

즉 **repeatable read** 가 요구되는 트랜잭션에서는 다른 트랜잭션에 의한 변경 사항을 볼 수가 없습니다. 그러한 변경 사항을 보고 싶으면 어플리케이션에서 트랜잭션을 새로 시작해야 합니다.

### 3. Phantom Read

**phantom read** 는 다른 트랜잭션에 의한 **변경(`update`)** 사항으로 인해 현재 사용 중인 트랜잭션의 `WHERE` 절의 조건에 맞는 새로운 행이 생길 수 있는 경우에 관한 것입니다.

가장 쉬운 표현으로 내가 딱히 새로 만들거나 지운 것도 아닌데, 없던 놈이 보이고, 있던 놈이 사라지는 것이다.

---

## Isolation level 종류 (ANSI/ISO SQL Standard)

### 1. read uncommitted

![Untitled (1)](https://user-images.githubusercontent.com/77487962/134809891-edadda55-1270-4139-9199-513d1d094628.png)

한 **transaction**(T1)이 데이터베이스 **row**를 이미 `update`은 하고 `commit`은 하지 않은 경우 다른 **transaction**(T2)은 해당 **row**를 `update`할 수 없다.

`SELECT` 문장을 수행하는 경우 해당 데이터에 **Shared Lock**이 걸리지 않는 level 이다. 

이렇게 하면 

- `update`가 손실되지 않도록 보호되지만,
- **Dirty Data**의 **질의**(`select`)는 허용한다.

### 2. read committed

![Untitled (2)](https://user-images.githubusercontent.com/77487962/134809907-ad137d0f-4c21-42fc-823d-2d54be030cb2.png)

`SELECT` 문장이 수행되는 동안 해당 데이터에 **Shared Lock**이 걸린다.

**Read Committed Isolation level**은 `commit`되지 않은 **트랜젝션**(T1)이 **쓴**(`update`) row를 **다른 트랜젝션**(T2)가 쓰거(`updtae`)나 읽을(`select`) 수 있도록 허용하지 않는다.

 **쓰고**(`update`) 있는 **트랜잭션**(T1)이 동일한 `row`에 **질의**(`select`)하는 **트랜잭션**(T2)이 액세스하는 것을 `commit` 될 때 까지 차단한다.

이렇게 되면 트랜젝션(T2)는 손실된 업데이트 및 dirty read로 부터 보호를 받을 수 있다.

### 3. repeatable read

![Untitled (3)](https://user-images.githubusercontent.com/77487962/134809916-709f62a8-b63b-4c2b-821d-56d84e06de19.png)

**Repeatable Read Isolation level**은 Row에서 데이터를 **질의**(`select`)하는 **트랜잭션**(T1)이 동일한 row를 **업데이트**(`update`)하려는 **트랜잭션**(T2)을 차단한다.

### 4. serializable

이 격리 모드는 다른 트랜잭션에서 데이터를 삽입하거나 읽지 못하도록 테이블 전체를 잠근다.

**Serializable Isolation**는 사용 가능한 모든 레벨 중에서 가장 엄격하고 비용이 많이 든다. 전체 테이블이 잠기면 다른 트랜잭션이 대기해야 할 확률이 매우 크다.

이 경우 테이블이 잠기기 때문에 `insert`도 불가능하다!

[Ansi Isolation Levels의 범위](https://www.notion.so/1a3cae49afe34fa9b41848dbee4b7be7)

Mysql 의 **InnoDB** 스토리지 엔진의 기본 Isolation Level이 **REPEATABLE-READ**.

### Isolation level은 왜 사용하는 겁니까?

> 당연히 성능이다. 예를 들어, 한 사용자가 어떠한 데이터를 수정하고 있는 경우 다른 사용자들이 그 데이터에 접근하는 것을 차단함으로써 완전한 데이터만을 사용자들에게 제공하게 됩니다. 
또한, 많은 사용자들의 수정 작업으로 인하여 통계 자료를 작성할 수 없는 사용자를 위하여 읽기 작업을 수행할 수 있도록 Isolation Level을 변경할 수 있습니다.

하지만 자세한 사용 **예시**를 들어본 적이 없다 ㅠ

---

### 참고

- 트랜잭션 격리 이야기에서 팬텀 읽기 현상 : [https://postgresql.kr/blog/pg_phantom_read.html](https://postgresql.kr/blog/pg_phantom_read.html)
- Transaction Isolation Levels With Examples : [https://allaroundjava.com/transaction-isolation-levels/](https://allaroundjava.com/transaction-isolation-levels/)
- 데이터베이스 Transaction Isolation Level : [https://effectivesquid.tistory.com/entry/데이터베이스-Isolation-Level](https://effectivesquid.tistory.com/entry/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4-Isolation-Level)

---

### 더 알아보기

- [ ]  [ JPA ] 비관적 락 vs 낙관적 락
