# DataBase

* 데이터베이스
  * 데이터베이스를 사용하는 이유
  * 데이터베이스 시스템 등장
  * 데이터베이스의 장점
  * 데이터베이스의 단점
  * 데이터베이스의 특징
* Schema
  * 스키마란?
  * 스키마 특징
  * 스키마 3계층
* Index
  * 인덱스란?
  * Index의 자료구조
  * Primary index vs Secondary index
  * Composite index
  * Index 의 성능과 고려해야할 사항
* 정규화
  * 정규화 탄생배경
  * 정규화란
  * 정규화종류
  * 정규화 장단점
  * 역정규화
* Transaction
  * 트랜잭션이란
  * 트랜잭션과 lock
  * 트랜잭션 특성
  * 트랜잭션 사용시 주의할점
* 교착상태
  * 교착상태란
  * 교착상태의 예
  * 교착 상태의 빈도를 낮추는 방법
* Statement vs PreparedStatement
* NoSQL
  * 정의
  * CAP 이론
    * 일관성
    * 가용성
    * 네트워크 분할 허용성
  * 저장방식에 따른 분류
    * Key-Value Model
    * Document Model
    * Column Model
    * Graph Model



## 데이터베이스

어느 한 조직에서 업무 처리를 위해 다수의 응용시스템 혹은 다수의 사용자들이 공용으로 사용하기 위해 저장된 운영 데이터의 집합



**데이터베이스를 사용하는 이유**

1. 파일처리에서 데이터베이스로의 시스템 전환

![image-20200805205506745](https://t1.daumcdn.net/cfile/tistory/233E9340543E16CE30)

> 파일처리 시스템

![image-20200805205559854](https://t1.daumcdn.net/cfile/tistory/2136103E543E16DC1E)

* 파일처리 시스템의 문제점
  * 중복: 파일처리시스템은 각 파일마다 필요한 데이터를 각각 가지고 있어야 함으로 전체적인 시간과 노력, 경제비용에 있어서 효율이 없다.
  * 비일관성: 데이터에 변경사항이 조금만 있어도 각 파일에서 해당되는 데이터를 모두 변경해야 함으로 수정에 문제가 있고, 한꺼번에 수정이 되지 않으면 데이터 값이 서로 틀리게 되는 문제점이 있다.
  * 응용 프로그램 개발 문제 : 기존의 파일 시스템은 파일 용도에만 맞춰서 제작되기 때문에 다른 프로그램을 만들때는 다시 데이터베이스 작업을 해야 한다는 문제가 있다.
  * 데이터 추가 및 검색의 문제: 데이터가 여러 파일에 산재하고 또 그 파일마다 데이터베이스 양식이 다르기 때문에 일률적인 검색이나 단순 추가 작업이 어렵다.



**데이터베이스 시스템 등장**

* 등장목적 : 파일처리 시스템의 문제점을 해결하기 위함
* 데이터 베이스 시스템 : 어떤 업무에 필요한 다양한 형태의 데이터를 모아 놓은 데이터의 집합체
* 데이터베이스 관리 시스템: 모든 응용프로그램들이 데이터베이스를 공유할수 있도록 관리해 주는 소프트웨어(ex: 오라클, SQL, DB2, Mysql, MongoDB,MariaDB ..etc)
* 데이터베이스의 구성요소(데이터베이스, DBMS, 데이터 언어, 데이터베이스 관리자, 일반 사용자)



**데이터베이스의 장점**

* 데이터의 중복을 피할수 있다.

* 저장된 자료를 공동으로 이용할수 있다.
* 데이터의 일관성과 무결성을 유지할수 있다.
* 데이터의 논리적, 물리적 독립성이 보장된다.
* 보안을 유지할수 있다.
* 데이터를 표준화 할수 있다.
* 데이터를 통합하여 관리할 수 있다.
* 항상 최신의 데이터 유지가 가능하다.

* 데이터의 실시간 처리가 가능하다.



**데이터베이스 단점**

* 데이터베이스 전문가가 부족하다
* 전산화 비용이 증가한다
* 대용량 디스크로의 집중적인 Access로 Overhead 가 발생한다.
* 파일의 백업과 회복이 어렵다



**데이터 베이스의 특성**

* 실시간 접근성 : 수시적이고 비정형적인 질의(조회)에 대해 실시간 처리 응답이 가능해야 한다.
* 계속적인 변화 : 새로운 데이터의 삽입, 삭제, 갱신으로 항상 최신의 데이터를 유지해야 한다.
* 동시공용 : 여러 사용자가 동시에 자기가 원하는 데이터를 이용할수 있어야한다.
* 내용에 의한 참조 : 데이터 베이스에 있는 데이터를 참조할때 데이터 레코드의 주소나 위치에 의해서가 아니라, 사용자가 요구하는 데이터 내용으로 데이터를 찾는다.



## Schema

**스키마란?**

* 데이터베이스의 구조와 제약 조건에 관한 전반적인 명세를 기술한 메타데이터의 집합
* 스키마는 데이터베이스를 구성하는 데이터 개체(Entity), 속성(Attribute), 관계(Relationship) 및 데이터 조작시 데이터 값들이 갖는 제약 조건등에 관해 전반적으로 정의한다.
* 스키마는 사용자의 관점에 따라 외부스키마, 개념스키마, 내부스키마로 나뉜다.

![image-20200805212716043](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile5.uf.tistory.com%2Fimage%2F9936823A5B698C4023F849)

**스키마 특징**

* 스키마는 데이터 사전(Data Dictionary)에 저장되며, 다른 이름으로 메타데이터라고도 한다.
* 스키마는 현실세계의 특정한 부분의 표현으로서 특정 데이터 모델을 이용해서 만들어진다.
* 스키마는 시간에 따라 불변인 특성을 갖는다.
* 스키마는 데이터의 구조적 특성을 의미하며, 인스턴스에 의해 규정된다.



**스키마의 3계층**

데이터베이스 관리 시스템은 외부적 스키마에 따라 명시된 사용자의 요구를 개념적 스키마에 적합한 형태로 변경하고 이를 다시 내부적 스키마에 적합한 형태로 변환한다.



1. 외부스키마 = 사용자 뷰
   * 외부스키마는 사용자나 응용프로그래머가 각 개인의 입장에서 필요로 하는 데이터베이스의 논리적 구조를 정의한 것이다.
   * 외부스키마는 전체 데이터베이스의 한 논리적인 부분으로 볼 수 있으므로 서브 스키마(Sub Schema) 라고도 한다.
   * 하나의 데이터베이스 시스템에는 여러개의 외부 스키마가 존재할 수 있으며 하나의 외부 스키마를 여러개의 응용 프로그램이나 사용자가 공용할 수도 있다.
   * 같은 데이터베이스에 대해서도 서로 다른 관점을 정의할수 있도록 허용한다.
   * 일반 사용자의 질의어(SQL)을 이용하여 DB를 쉽게 사용할수 있다.
   * 응용 프로그래머는 C, JAVA 등의 언어를 사용하여 DB 에 접근한다.
2. 개념스키마 = 전체적인 뷰
   * 개념 스키마는 데이터베이스의 전체적인 논리적 구조로서, 모든 응용프로그램이나 사용자들이 필요로 하는 데이터를 종합한 조직 전체의 데이터베이스로 하나만 존재한다.
   * 개념스키마는 개체간의 관계와 제약조건을 나타내고 데이터베이스의 접근 권한, 보안 및 무결성 규칙에 관한 명세를 정의한다.
   * 데이터베이스 파일에 저장되는 데이터의 형태를 나타내는 것으로, 단순히 스키마(Schema)라고 하면 개념 스키마를 의미한다.
   * 기관이나 조직체의 관점에서 데이터베이스를 정의한것이다.
   * 데이터베이스 관리자(DBA)에 의해서 구성된다.
3. 내부 스키마 = 저장스키마
   * 내부 스키마는 물리적 저장장치의 입장에서 본 데이터베이스 구조로, 물리적인 저장장치와 밀접한 계층이다.
   * 내부스키마는 실제로 데이터베이스에 저장될 레코드의 물리적인 구조를 정의하고, 저장데이터 항목의 표현방법, 내부 레코드의 물리적 순서등을 나타낸다.
   * 시스템 프로그래머나 시스템 설계자가 보는 관점의 스키마이다.



## Index

**인덱스란?**

인덱스는 말 그대로 책의 맨 처음 또는 맨 마지막에 있는 색인이라고 할수 있다.

이 비유를 그대로 가져와서 인덱스를 살펴본다면 데이터는 책의 내용이고 데이터가 저장된 레코드의 주소는 인덱스 목록에 있는 페이지 번호가 된다.

DBMS도 데이터베이스 테이블의 모든 데이터를 검색해서 원하는 결과를 가져오려면 시간이 오래 걸린다. 그래서 컬럼의 값과 해당 레코드가 저장된 주소를 키와 값의 쌍으로 인덱스를 만들어 준다.

DBMS 의 인덱스는 항상 정렬된 상태를 유지하기 때문에 원하는 값을 탐색하는데는 빠르지만 새로운 값을 추가하거나 삭제, 수정 하는 경우에는 쿼리문 실행 속도가 느려진다. 결론적으로 DBMS에서 인덱스는 데이터의 저장 성능을 희생하고 그 대신 데이터의 읽기 속도를 높이는 기능이다. SELECT 쿼리 문장의 WHERE 조건절에 사용되는 컬럼이라고 전부 인덱스로 생성하면 데이터 저장 성능이 떨어지고 인덱스의 크기가 비대해져서 오히려 역효과만 불러올수 있다.

> 인덱스를 많이 생성하면 인덱스 테이블이라는 테이블이 많이 생성됨으로 메모리를 많이 소비하게 된다.
>
> 따라서 PK 같은 컬럼들을 인덱싱 하도록 하고, 많은 컬럼에 남용하지 않는것이 좋다.



**Index 자료구조**

1. B-Tree 인덱스 알고리즘

* 일반적으로 사용되는 인덱스 알고리즘은 B-Tree알고리즘이다. B-Tree 인덱스는 컬럼의 값을 변형하지 않고(값의 앞부분만 잘라서 관리함) 원래의 값을 이용해 인덱싱하는 알고리즘

2. Hash 인덱스 알고리즘

* 컬럼의 값으로 해시 값을 계산해서 인덱싱하는 알고리즘으로 매운 빠른 검색을 지원한다. 하지만 값을 변형해서 인덱싱하므로, 특정 문자로 시작하는 값으로 검색을 하는 등 전방 일치와 같이 값의 일부만으로 검색하고자 할때는 해시 인덱스를 사용할수 없다. 주로 메모리 기반의 데이터베이스에서 많이 사용한다.

3. 풀 텍스트 인덱스 알고리즘

* 문서의 내용 전체를 인덱스화 해서 특정 키워드가 포함된 문서를 검색하는 풀텍스트 인덱스는 InnoDB 나 MyISAM 스토리지 엔진에서 제공하는 일반적인 용도 B-Tree 인덱스를 사용할수 없어서 대안된 방식

4. R-Tree 인덱스

* 기본적인 내부 메커니즘은 B-Tree 와 흡사하며 , B-Tree의 인덱스를 구성하는 컬럼의 값이 1차원 스칼라 값이라면  R-Tree 의 인덱스는 2차원 공간 개념의 값이다
* GPS 나 지도 서비스 같은 위치 기반의 서비스 구현시 필요한 MySQL 공간확장을 이용할때 사용한다.

**Hash table 보다 b-tree를 자주 사용하는 이유**

SELECT 질의 조건에는 부등호(<>)연산도 포함되는데 Hash table을 사용하게 된다면 등호(=) 연산이 아닌 부등호 연산의 경우에 문제가 발생한다. 

hashtable 은 동등 연산(=)에 특화되어있기 때문에 데이터베이스의 자료구조로 적합하지 않다고 한다.



**Primary Index VS Secondary Index**

클러스터란 여러개를 하나로 묶는다는 의미로 주로 사용되는데, 클러스터드 인덱스도 크게 다르지 않다. 인덱스에서 클러스터드는 비슷한 것들을 묶어서 저장하는 형태로 구현되는데, 이는 주로 비슷한 값들을 동시에 조회하는 경우가 많다는 점에서 착안된 것이다. 여기서 비슷한 값들은 물리적으로 인접한 장소에 저장되어 있는 데이터들을 말한다.



클러스터드 인덱스는 테이블의 PK 에 대해서만 적용되는 내용이다. 즉 PK 값이 비슷한 레코드끼리 묶어서 저장하는 것을 클러스터드 인덱스라고 표현한다.

클러스터드 인덱스에서 PK 값에 의해 레코드의 저장위치가 결정되며 PK 값이 변경되면 그 레코드의 물리적인 저장 위치 또한 변경되어야 한다. 그렇기 때문에 PK 를 신중하게 결정하고 클러스터드 인덱스를 사용해야 한다.



클러스터드 인덱스는 테이블당 한개만 생성할수 있다. PK 값에서만 적용되기 때문이다. 하지만 Non 클러스터드 인덱스는 테이블당 여러개를 생성할수 있다.



**Composite Index**

인덱스로 설정하는 필드의 속성이 중요하다. title, author 이 순서로 인덱스를 설정한다면 title을 검색하는 경우, index 를 생성한 효과를 볼수 있지만, author 만으로 검색하는 경우 index를 생성한 것이 소용이 없어진다. 

따라서 SELECT 질의를 어떻게 할것인가, 인덱스를 어떻게 생성할 것인가에 대해 많은 영향을 끼치게 된다.



**Index의 성능과 고려해야할 사항**

INDEX는 많은면 많을수록 좋지 않다.

* Index를 생성하게 되면 INSERT, DELETE, UPDATE 쿼리문을 실행할때 별도의 과정이 추가적으로 발생한다. 

* INSERT의 경우 INDEX에 대한 데이터도 추가해야 하므로 그만큼 성능에 손실이 따른다. 

* DELETE의 경우 INDEX 에 존재하는 값은 삭제하지 않고 사용 안한다는 표시로 남게된다. 이경우 row의 수는 그대로 남게되는거고 이게 반복되면 100개 행에서 실제데이터는 10개가 있을수도 있다.

* UPDATE의 경우 INSERT와 DELETE의 문제점을 동시에 가진다.

  이전 데이터가 삭제되고 그 자리에 새 데이터가 들어오는 개념이기 때문이고 변경전 데이터는 삭제되지 않고 INSERT로 인한 split 도 발생하게 된다.

* 하지만 더 중요한 것은 컬럼을 이루고 있는 데이터의 형식에 따라서 인덱스의 성능이 악영향을 미칠수도 있다는 것이다. 즉, 데이터의 형식에 따라 인덱스를 만들면 효율적이고 만들면 비효율적인 데이터의 형식이 존재한다는 것이다.

* `이름`,`나이`,`성별` 세가지의 필드를 갖고 있는 테이블의 경우 이름은 온갖 경우의 수가 존재하고 나이는 INT 타입을 갖고, 성별은 남,여 두가지 경우에 대해서만 데이터가 존재할것이다. 이 경우 어떤 컬럼에 대해서 인덱스를 생성하는 것이 효율적인가 라고 한다면 이름에 대해서만 인덱스를 생성하는 것이 효율적이다.

* 성별이나 나이에 인덱스를 생성했을 경우, 10000레코드에 해당하는 테이블에 대해서 2000단위로 성별에 인덱스를 생성했다고 가정한다면 값의 range가 적은 성별은 인덱스를 읽고 다시한번 디스크 I/O가 발생하기 때문에 비효율 적이게 된다.



## 정규화

**정규화 배경**

한 릴레이션에 여러 엔티티의 애트리뷰트들은 혼합하게 되면 정보가 중복되며, 저장 공간을 낭비하게 된다. 또 중복된 정보로 인해 `갱신 이상`이 발생하게 된다. 동일한 정보를 한 릴레이션에는 변경하고, 나머지 릴레이션에서는 변경하지 않은 경우 어느 것이 정확한지 알수 없게 되기 때문에 이런 문제를 해결하기 위해 정규화 과정을 거친다.

1. 갱신이상 종류
   * 삽입이상 : 원하지 않는 자료가 삽입된다던지, 삽입하는데 자료가 부족해 삽입이 되지 않아 발생하는 문제점
   * 삭제이상 : 하나의 자료만 삭제하고 싶지만, 그 자료가 포함된 튜플 전체가 삭제됨으로 원하지 않는 정보 손실이 발생하는 문제점
   * 수정(갱신)이상 : 정확하지 않거나 일부의 튜플만 갱신되어 정보가 모호해지거나 일관성이 없어져 정확한 정보 파악이 되지 않는 문제점

**정규화란**

관계형 데이터베이스에서 중복을 최소화하기 위해 데이터를 구조화하는 작업이다. 좀더 구체적으로는 불만족스러운 **나쁜** 릴레이션의 애트리뷰트들을 나누어서 **좋은** 작은 릴레이션으로 분해하는 작업을 말한다. 정규화 과정을 거치게 되면 정규형을 만족하게 된다. 정규형이란 특징 조건을 만족하는 릴레이션의 스키마의 형태를 말하며 제1정규형, 제2정규형,제3정규형 등이 존재한다.

1. **나쁜** 릴레이션은 어떻게 파악하는가?

   엔티티를 구성하고 있는 애트리뷰트 간에 함수적 종속성을 판단한다. 판단된 함수적 종속성은 좋은 릴레이션 설계의 정형적 기준으로 사용된다. 즉, 각각의 정규형마다 어떤 함수적 종속성을 만족하는지에 따라 정규형이 정의되고, 그 정규형을 만족하지 못하는 정규형을 나쁜 릴레이션으로 파악한다.

2. **함수적 종속성** 이란?

   함수적 종속성이란 애트리뷰트 데이터들의 의미와 애트리뷰트들 간의 상호 관계로 부터 유도되는 제약조건의 일종이다. X와 Y를 임의의 애트리뷰트 집합이라 할때, X의 값이 Y의 값을 유일하게 결정한다면 "X는 Y를 함수적으로 결정한다" 라고 한다. 함수적 중속성은 실세계에서 존재하는 애트리뷰트들 사이의 제약조건으로부터 유도된다. 또한 각종 추론 규칙에 따라서 애트리뷰트들간의 함수적 종속성을 판단할수 있다.

   > 애트리뷰트들의 관계로부터 추론된 함수적 종속성들을 기반으로 추론 가능한 모든 함수적 종속성들의 집합을 폐포라고 한다.
   >
   > * A의 값에 따라 B가 결정
   > * 완전함수 종속 : A1,..An에서 하나도 빠짐없이 전부를 이용해야만 B를 표현할수 있는 경우
   > * 부분 함수 종속 : A1..An중 전부가 아닌 일부만 가지고 B를 표현할수 있는 경우
   > * 이행적 함수 종속: A1..An,B1..Bn,C..Z 이 있을때 B=F(A)이고 C=F(B)이면 C=F(A) 가 성립
   > * 다치 종속: A1..An,B1..Bn,C..Z 이 있을때 C ∈ ***F***(B)이거나 임의의 Ak ∈ ***F***(B)
   > * 조인종속: 원래의 릴레이션을 분해한뒤 자연 조인한 결과가 원래의 릴레이션과 같은 결과가 나오는 종속성

3.  각각의 정규형은 어떠한 조건을 만족해야 하는가?

   * 분해의 대상인 분해 집합 D는 무손실 조인을 보장해야 한다.
   * 분해 집합 D는 함수적 종속성을 보존해야 한다.



**제 1정규형**

애트리뷰트의 도메인이 오직 `원자값`만을 포함하고, 튜플의 모든 애트리뷰트가 도메인에 속하는 하나의 값을 가져야 한다. 즉, 복합 애트리뷰트, 다중값 애트리뷰트, 중첩 릴레이션 등 비 원자적인 애트리뷰트들을 허용하지 않는 릴레이션 형태를 말한다.

**제 2정규형**

모든 비주요 애트리뷰트들이 주요 애트리뷰트에 대해서 **완전 함수적 종속이면** 제2정규형을 만족한다고 볼수 있다. 완전 함수적 종속이란 `X->Y` 라고 가정했을때 , X의 어떤 애트리뷰트라도 제거하면 더 이상 함수적 종속성이 설립하지 않는 경우를 말한다. 즉, 키가 아닌 열들이 각각 후보키에 대해 결정되는 릴레이션 형태를 말한다.

**제 3 정규형**

어떠한 비 주요 애트리뷰트도 기본키에 대해서 **이행적으로 종속되지 않으면** 제 3정규형을 만족한다고 볼 수 있다. 이행 함수적 종속이란 `X->Y`,`Y->Z`의 경우에 의해서 추론될수 있는 `X ->Z` 의 종속관계를 말한다. 즉, 비주요 애트리뷰트가 비주요 애트리뷰트에 의해 종속되는 경우가 없는 릴레이션 형태를 말한다.

**BCNF 정규형**

여러 후보키가 존재하는 릴레이션에 해당하는 정규화 내용이다. 복잡한 식별자 관계에 의해 발생하는 문제를 해결하기 위해 제 3정규형을 보완하는데 의미가 있다. 비 주요 애트리뷰트가 후보키의 일부를 결정하는 분해하는 과정을 말한다.

**제 4정규형**

한 릴레이션에서 다치종속을 제거한 정규형

**제 5 정규형**

한 릴레이션에서 조인 종속이 후보키를 통해서만 성립이 되도록한 정규형

> 각 정규형은 그 선행 정규형보다 더 엄격한 조건을 갖기 때문에 정규형이 높다고 좋은것은 아니다.
>
> 대표적인 데이터베이스 설계 단계는 3NF 또는 BCNF를 갖게 한다.
>
> * 모든 제 2정규형 릴레이션은 제 1정규형을 갖는다.
> * 모든 제 3정규형 릴레이션은 제 2정규형을 갖는다
> * 모든 BCNF 정규형 릴레이션은 제 3정규형을 갖는다.
> * 모든 제 4정규형 릴레이션은 BCNF 를 갖는다.
> * 모든 제 5정규형 릴레이션은 제 5정규형을 갖는다.



**역정규화**

정규화된 릴레이션을 물리적 데이터 모델링 과정에서 다시 통합하거나 분할하여 구조를 재조정하는 것, **정규화된 릴레이션은 실제로 자료를 검색하는 과정에서 성능저하가 발생한다.**

1. 릴레이션 역정규화
   * 릴레이션 병합 : 두 릴레이션을 하나로 합하는 방법
   * 릴레이션 분할 : 자주 사용되는 속성이나 튜플과 자주 사용되지 않는 속성이나 튜플을 분해하는 방법
     * 수직분할 : 속성에 대한 릴레이션 분할
     * 수평분할 : 튜플에 대한 릴레이션 분할
2. 속성 정규화
   * 속성추가 : 두 릴레이션 A,B 에서 A가 B를 자주 참고할때, B의 속성을 A에 추가하는 방법
   * 파생속성 추가 : 릴레이션에 파생속성을 추가하여 성능을 향상시키는 방법
   * 파생속성 : 작업의 효율을 위해 기존 속성으로부터 파생되는 속성

**정규화 장점**

* 데이터베이스 변경시 발생하는 이상현상 제거
* 데이터베이스의 구조 확장시 재 디자인 최소화 정규화된 데이터베이스 구조에서는 새로운 데이터 형의 추가로 인한 확장시, 그 구조를 변경하지 않아도 되거나 일부만 변경해도 된다. 이는 데이터베이스와 연동된 응용 프로그램에 최소한의 영향만을 미치게 됨으로 응용프로그램의 생명을 연장시킨다.
* 사용자에게 데이터 모델을 더욱 의미있게 제공 정규화된 테이블들과 정규화된 테이블들간의 관계들은 현실 세계에서의 개념과 그들간의 관계들을 반영한다.

**정규화 단점**

릴레이션의 분해로 인해 릴레이션 간의 연산(JOIN연산)이 많아진다. 이로 인해 질의에 대한 응답 시간이 느려질수 있다. 정규화를 수행한다는 것은 데이터를 결정하는 결정자에 의해 함수적 종속을 가지고 있는 일반 속성을 의존자로 하여 입력/수정/삭제 이상을 제거하는 것이다. 데이터의 중복 속성을 제거하고 결정자에 의해 동일한 의미의 일반 속성이 하나의 테이블로 집약되므로 한 테이블의 데이터 용량이 최소화되는 효과가 있다. 따라서 정규화된 테이블은 데이터를 처리할 때 속도가 빨라질수도 있고 느려질수도 있는 특성이 있다.



**단점에서 미뤄보았을때 어떤 상황에서 정규화를 진행해야 하는가?**

조회를 하는 SQL 문장에서 조인이 많이 발생하여 이로 인한 성능저하가 나타나는 경우에 역정규화를 적용하는 전략이 필요하다.

디스크I/O량이 많아서 조회시 성능이 저하되거나, 테이블끼리의 경로가 너무 멀어 조인으로 인한 성능 저하가 예상되거나, 칼럼을 계싼하여 조회할때 성능이 저하될 것이 예상되는 경우 역정규화를 수행하게 된다. 

* 역정규화 대상은?
  * 자주 사용되는 테이블에 액세스하는 프로세스의 수가 가장많고, 항상 일정한 범위만을 조회하는 경우
  * 테이블에 대량 데이터가 있고 대량의 범위를 자주 처리하는 경우, 성능 상 이슈가 있을 경우
  * 테이블에 지나치게 조인을 많이 사용하게 되어 데이터를 조회하는 것이 기술적으로 어려울 경우
* 역정규화시 주의할점
  * 역정규화를 과도하게 적용하다보면 데이터의 무결성이 깨질수 있다. 또한 입력, 수정,삭제의 질의문에 대한 응답 시간이 늦어질수 있다.



## Transaction

**트랜잭션이란?**

트랜잭션은 작업의 **완전성**을 보장해주는 것이다. 즉, 논리적인 작업 셋을 모두 완벽하게 처리하거나 또는 처리하지 못할 경우에는 원 상태로 복구해서 작업의 일부만 적용되는 현상이 발생하지 않게 만들어주는 기능이다. 사용자의 입장에서는 작업의 논리적 단위로 이해를 할수 있고 시스템의 입장에서는 데이터들을 접근 또는 변경하는 프로그램의 단위가 된다.



**트랜잭션과 Lock**

잠금(Lock)과 트랜잭션은 서로 비슷한 개념 같지만 사실 잠금은 동시성을 제어하기 위한 기능이고 트랜잭션은 데이터의 정합성을 보장하기 위한 기능이다. 잠금은 여러 커넥션에서 동시에 동일한 자원을 요청할 경우 순서대로 한 시점에는 하나의 커넥션만 변경할 수 있게 해주는 역할을 한다. 여기서 자원은 레코드나 테이블을 말한다. 

이와는 조금 다르게 트랜잭션은 꼭 여러 개의 변경 작업을 수행하는 쿼리가 조합되었을때만 의미있는 개념은 아니다. 트랜잭션은 하난의 논리적인 작업 셋중 하나의 쿼리가 있든 두개 이상의 쿼리가 있든 관계없이 논리적인 작업 셋 자체가 100% 적용되거나 아무것도 적용되지 않아야 함을 보장하는 것이다. 예를 들어 HW에러 또는 SW 에러와 같은 문제로 인해 작업에 실패가 있을 경우, 특별한 대책이 필요하게 되는데 이러한 문제를 해결하는 것이다.



**트랜잭션의 특성**

트랜잭션은 ACID 라는 4가지의 특성을 만족해야 한다.

**원자성(Atomicity)**

만약 트랜잭션 중간에 어떠한 문제가 발생한다면 트랜잭션에 해당하는 어떠한 작업 내용도 수행되어서는 안되며 아무런 문제가 발생되지 않았을 경우에만 모든 작업이 수행되어야 한다.

**일관성(Consistency)**

트랜잭션이 완료된 다음의 상태에서도 트랜잭션이 일어나기 전의 상황과 동일하게 데이터의 일관성을 보장해야 한다.

**고립성(Isolation)**

각각의 트랜잭션은 서로 간섭없이 독립적으로 수행되어야 한다.

**지속성(Durability)**

트랜잭션이 정상적으로 종료된 다음에는 영구적으로 데이터베이스에 작업의 결과가 저장되어야 한다.



**트랜잭션의 상태**

![image-20200806155541699](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/blob/master/Database/images/transaction-status.png?raw=true)

**Active**

트랜잭션의 활동상태. 트랜잭션이 실행중이며 동작중인 상태를 말한다.

**Failed**

트랜잭션 실패 상태. 트랜잭션이 더이상 정상적으로 진행 할수 없는 상태를 말한다.

**Partially Committed**

트랜잭션의 `commit` 명령이 도착한 상태. 트랜잭션의 `commit`이전 `sql` 문이 수행되고 `commit`만 남은 상태를 말한다.

**Committed**

트랜잭션 완료 상태. 트랜잭션이 정상적으로 완료된 상태를 말한다.

**Aborted**

트랜잭션이 취소 상태. 트랜잭션이 취소되고 트랜잭션 실행 이전 데이터로 돌아간 상태를 말한다.

**Partially Committed 와 Committed 의 차이점**

`commit` 요청이 들어오면 상태는 `Partial Commited` 상태가 된다. 이후 `Commit`을 문제없이 수행할수 있으면 `Committed` 상태로 전이되고, 만약 오류가 발생하면 `Failed`상태가 된다. 즉, `Partial Commited`는 `Commit` 요청이 들어왔을때를 말하며, `Commited`는 `Commit`을 정상적으로 완료한 상태를 말한다.

**트랜잭션을 사용할때 주의할점**

트랜잭션은 꼭 필요한 최소의 코드에만 적용하는 것이 좋다. 즉 트랜잭션의 범위를 최소화라는 의미다. 일반적으로 데이터베이스 커넥션은 개수가 제한적이다. 그런데 각 단위 프로그램이 커넥션을 소유하는 시간이 길어진다면 사용가능한 여유 커넥션의 개수는 줄어들게 된다. 그러다 어느 순간에는 각 단위 프로그램에서 커넥션을 가져가기 위해 기다려야 하는 상황이 발생할수도 있다.



**교착상태**

복수의 트랜잭션을 사용하다 보면 교착상태가 일어날수 있다. 교착상태란 두개 이상의 트랜잭션이 특정 자원(테이블 또는 행)의 잠금을 획득한채 다른 트랜잭션이 소유하고 있는 잠금을 요구하면 아무리 기다려도 상황이 바뀌지 않는 상태가 되는데 이것을 `교착상태`라고 한다.

![image-20200806155512490](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/blob/master/Database/images/deadlock.png?raw=true)

트랜잭션 1이 테이블 B의 첫번째 행의 잠금을 얻고 트랜잭션 2도 테이블 A의 첫번째 행의 잠금을 얻었다고 한다면

```sql
Transaction 1> create table B (i1 int not null primary key) engine = innodb;
Transaction 2> create table A (i1 int not null primary key) engine = innodb;

Transaction 1> start transaction; insert into B values(1);
Transaction 2> start transaction; insert into A values(1);
```

트랜잭션을 commit 하지 않은채 서로의 첫번째 행에 대한 잠금을 요청하면

```sql
Transaction 1> insert into A values(1);
Transaction 2> insert into B values(1);
ERROR 1213 (40001): Deadlock found when trying to get lock; try restarting transaction
```

DeadLock 이 발생한다. 일반적인 DBMS는 교착상태를 독자적으로 검출해 보고한다.



**교착 상태의 빈도를 낮추는 방법**

* 트랜잭션을 자주 커밋한다.
* 정해진 순서로 테이블에 접근한다. 위에서 트랜잭션 1이 테이블 B ->A 의 순으로 접근했고, 트랜잭션 2는 테이블 A->B 순으로 접근했다. 트랜잭션들이 동일한 테이블 순으로 접근하게 한다.
* 읽기 잠금 획득(SELECT ~ FOR UPDATE)의 사용을 피한다.
* 한 테이블의 복수 행을 복수의 연결에서 순서없이 갱신하면 교착상태가 발생하기 쉽다. 이 경우에는 테이블 단위의 잠금을 획득해 갱신을 직렬화 하면 동시성이 떨어지지만 교착상태는 회피할수 있다.



## NoSQL

**정의**

관계형 데이터 모델을 지양하며 대량의 분산된 데이터를 저장하고 조회하는데 특화되었으며 스키마 없이 사용 가능하거나 느슨한 스키마를 제공하는 저장소를 말한다.

종류마다 쓰기/읽기 성능 특화, 2차 인덱스 지원, 오토 샤딩 지원 같은 고유한 특징을 가진다. 대량의 데이터를 빠르게 처리하기 위해 메모리에 임시 저장하고 응답하는 등의 방법을 사용한다. 동적인 스케일 아웃을 지원하기도 하며, 가용성을 위하여 데이터 복제등의 방법으로 관계형 데이터베이스가 제공하지 못하는 성능과 특징을 제공한다.



**CAP 이론**

**1. 일관성(Consistency)**

일관성은 동시성 또는 동일성이라고도 하며 다중 클라이언트에서 같은 시간에 조회하는 데이터는 항상 동일한 데이터임을 보증하는 것을 의미한다. 이것은 관계형 데이터베이스가 지원하는 가장 기본적인 기능이지만 일관성을 지원하지 않는 NoSQL을 사용한다면 데이터의 일관성이 느슨하게 처리되어 동일한 데이터가 나타나지 않을수 있다. 느슨하게 처리된다는 것은 데이터의 변경을 시간의 흐름에 따라 여러 노드에 전파하는 것을 말한다. 이러한 방법을 최종적으로 일관성이 유지된다고 하여 최종 일관성 또는 궁극적 일관성을 지원한다고 한다.

각 NoSQL 들은 분산 노드 간의 데이터 동기화를 위해서 두 가지 방법을 사용한다. 첫번째로 데이터의 저장 결과를 클라이언트로 응당하기 전에 모든 노드에 데이터를 저장하는 동기식 방법이 있다. 그만큼 느린 응답시간을 보이지만 데이터의 정합성을 보장한다. 두번째로 메모리나 임시 파일에 기록하고 클라이언트에 먼저 응답한 다음, 특정 이벤트 또는 프로세스를 사용하여 노드로 데이터를 동기화하는 비동기식 방법이 있다. 빠른 응답시간을 보인다는 장점이 있지만, 쓰기 노드에 장애가 발생하였을 경우 데이터가 손실될수 있다.



**2. 가용성(Availability)**

가용성이란 모든 클라이언트의 읽기와 쓰기 요청에 대하여 항상 응답이 가능해야함을 보증하는 것이며 내고장성이라고도 한다. 내고장성을 가진 NoSQL은 클러스터 내에서 몇개의 노드가 망가지더라도 정상적인 서비스가 가능하다.

몇몇 NoSQL은 가용성을 보장하기 위해 데이터 복제(Replication)을 사용한다. 동일한 데이터를 다중 노드에 중복 저장하여 그 중 몇대의 노드가 고장나도 데이터가 유실되지 않도록 하는 방법이다. 데이터 중복 저장 방법에는 동일한 데이터를 가진 저장소를 하나 더 생성하는 Master-Slave 복제 방법과 데이터 단위로 중복 저장하는 Peer-to-Peer 복제 방법이 있다.



**3. 네트워크 분할 허용성(Partition tolerance)**

분할 허용성이란 지역적으로 분할된 네트워크 환경에서 동작하는 시스템에서 두 지역간의 네트워크가 단절되거나 네트워크 데이터의 유실이 일어나더라도 각 지역 내의 시스템은 정상적으로 동작해야 함을 의미한다.



**저장 방식에 따른 NoSQL 분류**

`Key-Value Model`,`Document Model`, `Column Model`, `Graph Model` 로 분류할수 있다.

**1. Key-Value Model**

![image-20200806162209109](https://drive.google.com/a/insilicogen.com/uc?id=13fonXpLANEdRfo7bSip3zG2E09JBhkTq&export=download)

가장 기본적인 형태의 NoSQL이며 키 하나로 데이터 하나를 저장하고 조회할수 있는 단일 키-값 구조를 갖는다. 단순한 저장구조로 인해 복잡한 조회 연산을 지원하지 않는다. 또한 고속 읽기와 쓰기에 최적화된 경우가 많다. 사용자의 프로필 정보, 웹서버 클러스터를 위한 세션 정보, 장바구니 정보, URL 단축 정보 저장등에 사용한다.

하나의 서비스 요청에 다수의 데이터 조회 및 수정 연산이 발생하면 트랜잭션 처리가 불가능하여 데이터 정합성을 보장할수 없으며 대표적으로 **Redis** 가 있다.

**2. Document Model**

![image-20200806162227530](https://drive.google.com/a/insilicogen.com/uc?id=1AeQo0fYs9wQhD6A2vmjSunOH9lTG72Nc&export=download)

키-값 모델을 개념적으로 확장한 구조로 하나의 키에 하나의 구조화된 문서를 저장하고 조회한다. 논리적인 데이터 저장과 조회 방법이 관계형 데이터베이스와 유사하다. 키는 문서에 대한 ID로 표현된다. 또한 저장된 문서를 컬렉션으로 관리하며 문서 저장과 동시에 문서 ID 에 대한 인덱스를 생성한다. 문서 ID 에 대한 인덱스를 사용하여 O(1) 시간 안에 문서를 조회할수 있다.

대부분의 문서 모델 NoSQL은 B트리 인덱스를 사용하여 2차 인덱스를 생성한다. B트리 는 크기가 커지면 커질수록 새로운 데이터를 입력하거나 삭제할때 성능이 떨어지게 된다. 그렇기 때문에 읽기와 쓰기의 비율이 7:3 정도 일때 가장 좋은 성능을 보인다. 중앙 집중식 로그 저장, 타임라인 저장, 통계정보 저장등에 사용되고 대표적으로 **MongoDB** 가 있다.



**3. Column Model**

![image-20200806162248423](https://drive.google.com/a/insilicogen.com/uc?id=1BIvbZU4XQS9pWjiB5BKCNoAYzs9_kTUL&export=download)

하나의 키에 여러 개의 컬럼 이름과 컬럼 값의 쌍으로 이루어진 데이터를 저장하고 조회한다. 모든 컬럼은 항상 타임 스탬프 값과 함께 저장된다.

구글의 빅테이블이 대표적인 예로 차후 컬럼형 NoSQL은 빅테이블의 영향을 받았다. 이러한 이유로 Row key, Column Key, Column Family 같은 빅테이블 개념이 공통적으로 사용된다. 저장의 기본단위는 컬럼으로 컬럼은 컬럼 이름과 컬럼 값, 타임 스탬프로 구성된다. 이러한 컬럼들의 집합이 로우(ROW)이며, 로우키(ROW key)는 각 로우를 유일하게 식별하는 값이다. 이러한 로우들의 집합은 키 스페이스(Key Space)가 된다.

대부분의 컬럼 모델 NoSQL은 쓰기와 읽기 중에 쓰기에 더 특화되어 있다. 데이터를 먼저 커밋로그와 메모리에 저장한 후 응답하기 때문에 빠른 응답속도를 제공한다. 그렇기 때문에 읽기 연산 대비 쓰기 연산이 많은 서비스나 빠른 시간안에 대량의 데이터를 입력하고 조회하는 서비스를 구현할때 가장 좋은 성능을 보인다. 채팅 내용저장, 실시간 분석을 위한 데이터 저장소 등의 서비스 구현에 적합하다.

대표적으로**Cassandra, HBase** 가 있다.



**4. Graph Model**

![image-20200806162321959](https://drive.google.com/a/insilicogen.com/uc?id=1PTyYvAwdRBK90OyF0WGJaB9pJrCTMMVw&export=download)

관계를 저장하고 탐색하도록 특별히 구축되어있는 모델, 그래프 데이터베이스는 노드를 사용하여 데이터 엔티티를 저장하고 엣지로는 엔티티간의 관계를 저장한다. 엣지는 항상 시작 노드, 끝노드, 유형과 방향을 가지며, 상-하 위 관계, 동작, 소유자 등을 문서화 한다. 이때 하나의 노드가 가질수 있는 관계의 수와 종류에는 제한이 없다.



그래프 모델의 그래프는 특정 엣지의 유형 또는 전체 그래프를 전반으로 통하여 트래버스될수 있다. 그래프 모델에서 노드간의 관계는 쿼리 시간에는 포함되지 않지만 데이터베이스에서 유지되기 때문에 조인 또는 관계를 트래버스 하는 속도가 매우 빠르다. 그래프 모델은 데이터 간의 관계를 만들고 이러한 관계를 신속하게 쿼리해야 할때 사용되므로 소셜 네트워크, 추천 엔진, 이상탐지등에서 많이 사용된다. 대표적으로 **Neo4j, OrientDB** 가 있다.