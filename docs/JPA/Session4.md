---
layout: default
title: 양방향 연관관계와 연관관계의 주인
parent: JPA
---

# 양방향 연관관계와 연관관계의 주인
  

## 1. 양방향 연관관계
  
![img.png](/assets/images/JPA/Section4/img_1.png)  
  

* 회원은 하나의 팀에만 소속될 수 있음.
    
 
회원 한명은 여러 팀에 소속 될 수 없음.   
팀은 여러명의 회원을 가질 수 있음.  
  
n명의 회원은 같은 팀에 들어갈 수 있음.  
  
> member : team = N : 1
  
테이블 연관관계에서는 N인 쪽에서 FK를 가짐.  
그럼 테이블 연관관계와 같이 객체연관관게에서도 N인쪽에서 연관관계를 매핑해야함.  
      
```java
@Entity
public class Member{
    @ManyToOne
    @JoinColumn(name = "TEAM_ID")
    private Team team;
}
```    
```java
@Entity
public class Team{
    @OneToMany(mappedBy="team")
    private List<Mebmer> members = new ArrayList<>();
}
```
      
객체 연관관계는 단방향 2개가 존재, 참조 값 2개.  
회원 -> 팀  
팀 -> 회원  
  
테이블 연관관계는 참조 값 1개.  
회원 <-> 팀 (외래키로 조회)  
    
테이블은 외래키 하나로 두 테이블의 연관관계를 관리함.  
  
Member 객체와 Team 객체 둘 중 한곳에서 외래 키를 관리해야함.  
    
  
## 2. 연관관계의 주인  
* 객체 두 관계중 하나를 연관관계의 주인으로 지정해야함.    
* 연관관계의 주인만이 외래 키를 관리함(등록, 수정)
* 주인이 아니쪽은 읽기만 가능해야함. 
    

### 누구를 주인으로 
외래 키가 있는 곳을 주인으로 정해야함.  
    
> 변경을 할때 다른 테이블로 쿼리가 날라감.
> 방지하기 위해서 외래 키가 있는 곳으로 정함.  

  
### 주의사항 
* 연관관계의 주인이 아닌 객체에서 연관관계의 주인의 값을 입력하면 DB에 반영이 안됨.
* 양방향 매핑시 양쪽 다 값을 입력해야함.  
> 양쪽 다 값을 설정하지 않을 경우에 em.flush()가 없을때 값을 찾을 수 없게됨. 
> 1차 캐시에 값이 없기 때문에 List<Member> members를 조회할 수 없음.  
* 양방향 매핑시 무한 루프 조심해야함. 
> 양쪽에서 객체를 부르기 때문에 무한 루프에 빠짐. 
  
  
  
<span style="color: blue">설계할때 단방향 매핑만으로 하고 필요할때 추가하는 쪽이 좋음.</span>
