---
layout: default
title: 엔티티 매핑
parent: JPA
---

# 엔티티 매핑
  
  
  
## 1. 객체와 테이블 매핑 
    
### 1) @Entity  
  
* @Entity가 붙은 클래스는 JPA가 관리함.
* JPA를 사용해서 테이블과 매핑할 클래스에 @Entity를 붙임. 
* 기본 생성자 필수
    
#### @Entity 속성 
  
```java
@Entity(name = "MEM")
public class Member {
    
}
```  
  
* JPA에서 사용할 엔티티 이름을 지정함. 
* 기본값은 클래스 이름으로 사용함.  


### 2) @Table

* @Table은 엔티티와 매핑할 테이블 지정 

#### @Entity 속성

| 속성                     | 기능                     | 기본값        |
|:-----------------------|:-----------------------|:-----------|
| name                   | 매핑할 테이블 이름             | 엔티티 이름을 사용 |
| catalog                | 데이터베이스 catalog 매핑      |            |
| schema                 | 데이터베이스 schema 매핑       |            |
| uniqueConstraints(DDL) | DDL 생성 시에 유니크 제약 조건 생성 |            |
  
  
## 2. 데이터베이스 스키마 자동 생성 
  
  
### 1) 데이터 베이스 스키마 자동 생성  
    

* DDL을 애플리케이션 실행 시점에 자동 생성함.
* 테이블 중심 -> 객체 중심
* 생성된 DDL은 개발 장비에서만 사용해야함. 
   
  

![img1.png](/assets/images/JPA/Section3/img1.png)  
xml 설정
  
![img2.png](/assets/images/JPA/Section3/img2.png)  
yaml 설정    

| 옵셥          | 설명                              | 
|:------------|:--------------------------------|
| create      | 기존테이블 삭제 후 다시 생성(DROP + CREATE) |
| create-drop | create와 같으나 종료시점에 테이블 DROP      |
| update      | 변경분만 반영(운영DB에는 사용하면 안됨)         |
| validate    | 엔티티와 테이블이 정상 매핑되었는지만 확인         |
| none        | 사용하지않음                          |
    

<span style="color: red"> 운영 장비에서는 절대 create, create-drop, update 사용하면 안됨.</span>  
최대한 none을 사용하자.   
  
  
### 2) DDL 생성 기능 
    
```java
@Column(nullabel = false, length = 10)
```
  
제약조건을 추가 가능함. 
JPA 실행 로직에는 영향을 주지 않고, DDL을 자동 생성할때만 사용함.  
제약조건을 주면 따로 찾아보지않고 확인 할 수 있기때문에 제약조건을 작성하는게 좋음.  

## 3. 필드와 컬럼 매핑

### 1) 매핑 어노테이션    

| 어노테이션       | 설명                                              |
|:------------|:------------------------------------------------|
| @Column     | 컬럼 매핑                                           |
| @Temporal   | 날짜 타입 매핑                                        |
| @Enumerated | enum 타입 매핑                                      |
| @Lob        | BLOB, CLOB 매핑                                   |
| @Transient  | 특정 필드를 컬럼에 매핑하지 않음 (DB와 관계 없이 사용할때, 메모리에서만 사용함) |
    
  

#### @Column


| 속성                    | 설명                                                              | 기본값                   |
|:----------------------|:----------------------------------------------------------------|:----------------------|
| name                  | 필드와 매핑할 테이블의 컬럼 이름                                              | 객체의 필드 이름             |
| insertable, updatable | 등록, 변경 가능 여부                                                    | TRUE                  |
| nullable(DDL)         | null 값의 허용 여부 설정함                                               |                       |
| unique(DDL)           | 한 컬럼에 간단히 유니크 제약조건 걸 때 사용함                                      |                       |
| columnDefinition(DDL) | 데이터베이스 컬럼 정보를 직접 설정함                                            | 필드의 자바 타입과 방언 정보를 사용함 |
| length(DDL)           | 문자 길이 제약조건                                                      | 255                   |
| precision, scale(DDL) | BigDecimal 타입에서 사용함. precision은 소수잠을 초함한 전체 자리수, scale은 소수의 자릿수 | precision=5, scale=2  |
    
  

#### @Enumerate


자바 enum 타입을 매핑할때 사용  
  
```java
@Enumerate(EnumType.ORDINAL)
private RoleType roleType;
``` 
  
* EnumType.ORDINAL: enum 순서를 DB에 저장
* EnumType.STRING: enum 이름을 DB에 저장 
  
기본값은 EnumType.ORDINAL  
EnumType.ORDINAL은 enum의 값을 추가할때 중복이 발생할 수 있기때문에 사용하지 않는게 좋음.  
    
  

#### @Temporal


날짜 타입을 매핑할때 사용.  
java 8 이상은 어노테이션을 사용하지 않고 LocalDate, LocalDateTime 사용함.  

```java
@Temporal(TemporalType.TIMESTAMP)
private Date createdDate; 

private LocalDate testLocalDate;
private LocalDateTime testLocalDateTime;
``` 
    
  

#### @Lob


데이터베이스 BLOB, CLOB 타입과 매핑

```java
@Lob
private String description;
``` 
    
  

#### @Transient


필드 매핑 안함.  
주로 메모리상에서만 임시로 어떤 값을 보관하고 싶을때 사용함. 

```java
@Transient
private Integer temp;
``` 


## 4. 기본 키 매핑
  
  
* @Id
* @GeneratedValue 
  
```java
@Id @GeneratedValue(strategy = GenerationType.AUTO)
private Long id; 
```
    

### 1) @Id

* 직접 할당 
    

### 2) @GeneratedValue
  
* 자동 생성
    
#### IDENTIY  
데이터베이스에 위임, MYSQL  
나는 모르겠고 DB야 알아서 값을 정해줘  
  
DB에 들어가야 pk를 알 수 있다.  
commit하기 전 ID 값을 알 수 없음. 
<span style="color: red">em.persist()시점에 즉시 INSERT SQL 실행하고 DB에서 식별자 조회 </span>

#### SEQUENCE
데이터베이스 시퀀스 오브젝트 사용, ORACLE  
  
* 버퍼링 가능  
* 시퀀스를 미리 확보해서 계속 호출하지 않음.

멤버를 생성 후 ID 값을 알 수 없음.  
DB에서 시퀀스를 알아야함.  
em.perisit(member)할때 DB에서 시퀀스 값 n ~ n+50을 메모리에 저장.  
그 후 DB에 INSERT SQL을 날리지 않아도 ID값을 검색할 수 있음.  

#### TABLE
키 생성용 테이블 사용, 모든 DB  
성능 저하가 일어남.  

#### AUTO
방언에 따라 자동 지정, 기본값



### 권장하는 식별자 전략 

* 긴본 키 제약 조건: null 아님, 유일, 변하면 안됨.  
* 권장: Long형 + 대체키 + 키 생성전략 사용  

