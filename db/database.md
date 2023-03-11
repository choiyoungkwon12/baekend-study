# DB (Database)

```
organized collection of data stored and accessed

구조화된 정보 or 데이터의 조직화된 모음을 데이터 베이스라고 함.
```

### DBMS (Database Management System)

- 말 그대로 데이터 베이스 관리 시스템
- 사실상 개발하면서 DB라고하면 DBMS를 뜻한다.
  - 사용자 or 응용 프로그램은 DB에서 데이터를 쉽게 찾고, 효율적으로 조작(CUD) 할 수 있어야 한다.
  - 또, 보안 문제, 접근 권한 문제를 다룰 수 있어야 함.

### DBMS에서 제공하는 언어
- DDL (Data Definition Language) -> 테이블 스키마와 관련
- DML (Data Manipulation Language) -> 데이터를 쿼리 or Command 하는 것과 관련
- DCL (Data Control Language) -> Grant, Revoke, Commit, Rollback 같은 형태

### Data Model

데이터 모델은 보통 크게 3가지로 분류함.
1. Conceptual Data Model (개념적 데이터 모델)
2. Logical Data Model (논리적 데이터 모델)
3. Physical Data Model (물리적 데이터 모델)

### Relational Model (관계형 모델)

Entity-Relationship Model(ERM)과 Relational Model(RM)
- 엄격하게 따지면 ERM의 Relationship은 Entity 사이의 관계를 의미하고,
- Relational Model(RM)의 Relational은 Tuple의 집합을 의미함.
  맥락이 달라서 사실 아무 상관없는 다른 용어지만 실용적으로 사용할때는 거의 같은 의미로 쓰이는 경우가 많음

### 관계형 모델에서 쓰이는 3가지 개념
- Relation
- Tuple
- Attribute

`속성(Attribute)`

- 속성은 이름과 타입으로 구성되고 이름은 속성 집합 안에서 유일해야 함.
- 보통 column으로 구현됨.
  `ex) 이름/문자열`

`튜플(Tuple)`

- (속성, 값) 쌍의 집합. 으로 하나의 집합에서 속성 이름은 유일하기 때문에 겹치지 않아야함.

  `ex) { (이름/문자열, 견우), (나이/정수, 13), (성별/문자, 남) }`

- 보통 row, record로 구현됨.
- 이론상으로는 유일하지만, 대부분 RDBMS에서는 중복 및 NULL을 허용한다.

`관계 (Relation)`
![img.png](img.png)

- 관계(Relation)는 (속성의 집합, 튜플의 집합) 쌍.
- 속성의 집합을 heading, 튜플의 집합을 body라고 구분한다.
- 그냥 관계는 “튜플의 집합”이라고 할 수도 있다.

관계는 대부분 Table로 구현되고, 속성 집합을 Schema라고 표현한다.

# Relational Algerbra (관계 대수)

### 연산
- 하나 이상의 Relation으로 새로운 Relation을 만들 수 있음.
  - ex) Projection 과 같이 조회할때 원하는 Attribute을 가져오는 것도 하나의 새로운 Relation을 만드는 것이다.

### Projection
- 원하는 Attribute을 포함하는 Pair로 Tuple을 구성하는것.
```sql
SELECT name, age, gender
FROM people;
```
그냥 sql에서는 원하는 속성을 가져오는것으로 표현

### Selection
주어진 술어(조건)을 만족하는 Tuple만 선택
sql에서는 where로 표현
```sql
SELECT name, age, gender
FROM people
WHERE age < 13;
```

### Cartesian Product

Relation의 Cartesian Product는 원래 의미와 다르다. 
원래는 각 요소의 쌍을 요소로 취하지만(x와 y가 있다면 (x, y)를 새로운 요소로 사용), 관계 대수에서는 그냥 Tuple을 합친다.

![img_1.png](img_1.png)

- 대부분은 Cartesian Product를 그대로 사용하지 않고 Selection과 함께 사용하는데, 이를 Join이라고 한다.
- 보통 Cartesian Product은 조인으로 사용함.
```
σpeople.name = items.person_name(people × items)
σ = Selection
× = Cartesian Product
```
```
SELECT items.name AS name, usage, people.gender
FROM items
JOIN people ON items.person_name = people.name;
```




