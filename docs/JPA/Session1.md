---
layout: default
title: JPA 구동 방식/ JPQL과 SQL의 차이
parent: JPA
---

# JPA 구동 방식/ JPQL과 SQL의 차이점  
  

## 1. JPA 구동 방식 

JPA는 Persistence라는 클래스가 존재 
  
1. persistence.xml 설정 정보를 조회 
2. 설정 정보에 맞춰서 EntityManagerFactory 클래스를 만듬
3. 고객 요청이 발생할때 EntityManger 생성 
  
> 앤티티 매니저 팩토리는 하나만 생성해서 애플리케이션 전체에서 공유한다.  
> 앤티티 매니저는 사용 후 버려야 한다.  
> JPA의 단순 조회는 괜찮으나, 모든 데이터 변경은 트랜잭션 안에서 실행되야한다.
  
  
## 2. JPQL과 SQL의 차이점 
JPQL은 엔티티 객체를 대상으로 쿼리  
SQL은 데이터베이스 테이블을 대상으로 쿼리  
  
> JPQL은 **객체를** 대상으로 검색하는 객체 지향 쿼리.

``` java
List<Member> result = em.createQuery("select m from Member as m", Member.class).getResultList();  
// JPQL 방식
```
  
