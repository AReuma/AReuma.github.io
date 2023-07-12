---
layout: default
title: 영속성 관리
parent: JPA
---

# 영속성 관리/ 엔티티 생명주기/ 영속성 컨텍스트의 이점
  

## 1. 영속성 컨텍스트 

### "엔티티를 영구 저장하는 환경"

``` java
EntityManager.persist(entity);
```
  
persist를 할 경우 **DB에 저장되는 것이 아님.**  
영속성 컨텍스트에 저장됨.  
  
> 엔티티 매니저를 통해서 영속성 컨텍스트에 접근함.  

> 엔티티 매니저를 생성하면 일대일로 영속성 컨텍스트가 생긴다고 생각하면 됨.  
  
  
## 2. 엔티티의 생명주기 
  
### 1) 비영속 (new/ transient)  
* jpa와 상관없는 상태
* 객체만 생성된 상태 
  
``` java
Member member = new Member(); // 객체를 생성한 상태
member.setId(1L);
member.setUsername("areum");
```  

### 2) 영속 (managed)
* 비용속이었던 객체가 영속성 컨텍스트에 들어간 상태.
* DB에 들어간 상태는 아님. query가 쌓여 있는 상태  

``` java
Member member = new Member(); // 객체를 생성한 상태
member.setId(1L);
member.setUsername("areum");

EntityManager em = emf.createEntityManager();
em.getTransaction().begin();

em.persist(member); // 객체를  영속성 컨텍스트에 저장한 상태.
```  

### 1) 준영속 (detached)
* 엔티티를 영속성 컨텍스트에서 분리한 상태

``` java
em.detach(member); // 특정 엔티티만 준영속 상태로 전환

em.clear(); // 영속성 컨텍스를 완전히 초기화 

em.close(); // 영속성 컨텍스트를 종료 
```  

### 1) 삭제 (removed)
* 객체가 삭제된 상태

``` java
em.remove(member);
```  


## 3. 영속성 컨텍스트의 이점  
  
### 1) 엔티티 조회, 1차 캐시

``` java
em.persist(member);  
// 1차 캐시에 저장됨. -> commit이 된 상태가 아니라서 DB에 저장이 안된 상태.  
// 1차 캐시에 key로 pk값이 들어가있고, value값으로 member 객체가 들어가 있음.

Membmer findMember = em.find(Member.class, "areum"); 
// DB에서 조회하는게 아니라 우선적으로 1차 캐시에서 조회 
// 1차 캐시에 areum을 가진 key가 있기때문에 DB에서 값을 가져오지 않음.

Membmer findMember2 = em.find(Member.class, "membmer1");
// 1차 캐시에 member1의 key 값이 없기 때문에 DB에서 조회
// 조회 된 값을 1차 캐시에 저장 후 값을 반환  
```  
  
DB에서 조회하지 않고 1차 캐시에서 찾을 수 있다는 이점.  
  
  
### 2) 동일성 보장  

``` java
Membmer a = em.find(Member.class, "member1");
Membmer b = em.find(Member.class, "member1");

System.out.println(a == b) // true 
```  
같은 트랜잭션 안에서비교하면 같다.  


### 3) 트랜잭션을 지원하는 쓰기 보장 

``` java
EntityManager em = emf.createEntityManager();
EntityTransaction transaction = em.getTransaction();

transaction.begin(); // 앤티티 매니저는 데이터 변경시 트랜잭션을 시작해야함. 

em.persist(memberA);
em.persist(memberB);
// 영속성 컨텍스트에 저장만 된 상태
// DB에 JPA가 생성한 INSERT SQL이 전달 된 상태가 아님. 
// 1차 캐시와 쓰기 지연 SQL 저장소에 쿼리가 쌓임. 

transaction.commit(); // 커밋하는 순간 쌓여 있던 INSERT SQL을 DB에 보냄 
```   
  
![JPA_entityManager.jpeg](/assets/images/JPA/Section2/JPA_entityManager.jpeg)
  
### 4) 변경 감지 

``` java
EntityManager em = emf.createEntityManager();
EntityTransaction transaction = em.getTransaction();

transaction.begin();

Member memberA = em.find(Member.class, "memberA");

// 영속 엔티티 데이터 수정
memberA.setUsername("areum");
memberA.setAge(20);

// em.update(memberA) 처럼 따로 업데이트랄 하지 않아도 됨. 
// 자바 컬렉션이랑 같다고 생각하면 됨.

transaction.commit();
```  
commit()을 하면 1차 캐시에 있는 스냅샷과 비교하게됨.  
1차 캐시에 저장될때 최초의 시점을 저장해둠.  
그 후 commit이 발생해 1차 캐시에 있는 스냅샷과 엔티티를 비교해서 다르면 UPDATE SQL 생성이 됨.  
  
> commit 시점에 알아서 반영이 되는구나로 알면 됨.  
  
  
## 4. 플러시 

* 수정된 엔티티를 쓰기 지연 SQL 저장소에 등록함.
* 쓰기 지연 SQL 저장소의 쿼리를 DB에 반영함. 
* 영속성 컨텍스를 비우는 건 아님. 
* **트랜잭션이라는 작업 단위**가 중요함!
  