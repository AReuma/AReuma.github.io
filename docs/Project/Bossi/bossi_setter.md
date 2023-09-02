---
layout: default
title: Setter 사용 지양/ Builder 패턴  
parent: Bossi
grand_parent: Project
---

# Setter 사용 지양과 Builder 패턴
    


# 1. Setter 문제점 
    
> 1. 일관성 문제 
> 2. 의도를 파악하기 힘든 문제 

## 1) 일관성 문제
``` java
@Override
public void snsRegister(Member member) {
     Member memberEntity = memberRepository.findByMemberId(member.getId());

     memberEntity.setName(member.getName());
     memberEntity.setRegion(member.getRegion());
     memberEntity.setLat(member.getLat());
     memberEntity.setLng(member.getLng());
     memberEntity.setRegisterStatus(Boolean.TRUE);

     memberRepository.save(memberEntity);
}
``` 
    
예전에 진행한 프로젝트에서 코드를 가져와서 보면,  
SNS로 가입한 사람들도 현재 위치가 필요했기때문에 따로 받아서 저장하는 코드이다.  
    
여기서 setLat가 없어도 컴파일 시점에서는 오류가 없다.  
하지만 고객 입장에서 검색을 할 시점에 현재위치를 찾을 수 없어서 검색하는데 오류가 생긴다.  
    
<mark style="background-color: pink">즉, 일관성이 무너진 상태에서도 사용이 가능하게 된다.</mark>

    


## 2) 의도 파악의 문제

![useSwagger_Operation.png](/assets/images/Project/Bossi/setter/bossi_reviewImgDelete_Setter.png)
     

![useSwagger_parameters.png](/assets/images/Project/Bossi/setter/bossi_reviewImgSave_Setter.png)         

리뷰를 작성하기 위해서 setter를 사용하는건지, 값을 변경하기 위해서 사용하는건지 알 수가 없다.    


```java 
public void changeReviewCount(int count){
    this.reviewCount = count; 
}
```  

변경을 할 때 사용하는 메서드를 만들어서 사용하게 되면 메서드의 의미를 바로 파악하고 사용이 가능하다.  
    

   
# 2. Setter 대신 다른것     
    
## 1) 생성자 오버로딩 
    

```java
public class User{
    private String id;
    private String pw; 
    private String nickName;
    private String phoneNum;
    
    public Member(String id){
        this.id = id;
    }
    
    public Member(String id, String pw){
        this.id = id;
        this.pw = pw;
    }
    
    public Member(String id, String pw, String nickName){
        this.id = id;
        this.pw = pw;
        this.nickName = nickName;
    }
    
    public Member(String id, String pw, String phoneNum){
        this.id = id;
        this.pw = pw;
        this.phoneNum = phoneNum;
    }
}

```    
    
생성자 메서드가 많아지면서 코드량이 증가할 수 있다.  
또, 3번째와 4번째의 메서드는 오버로딩 기본원칙이 어긋나서 사용할 수 없다.  
같은 매개변수의 값을 가지면 생성할 수 없는 문제점이 발생한다.  



## 2) Builder 클래스    
    
```java
public class User {
    static public class Builder {
        private String id; 
        private String pw;
        private String nickName;
        
        public Builder setId(String id){
            this.id = id;
            return this;
        }

        public Builder setPw(String pw){
            this.pw = pw;
            return this;
        }

        public Builder setNickName(String nickName){
            this.nickName = nickName;
            return this;
        }
        
        public User build(){
            return new User(id, pw, nickName);
        }
    }
}
```
    
    
```java
User user = new User.Builder()
                    .setId("id")
                    .setPw("pw")
                    .setNickName("nickName")
                    .build();
```    
    
Builder 클래스를 이용하면 어떤 값을 세팅하는지 확실하게 알 수 있다.  
마지막 build() 메서드를 호출해야만 객체로서 활용할 수 있기때문에 일관성을 지킬 수 있다.  
    
   
    
### Spring boot의 lombok을 이용해서 Builder 클랙스를 쉽게 사용가능함.  
    

```java
@Builder
@RequiredArgsConstructor
public class User {
    static public class Builder {
        private String id;
        private String pw;
        private String nickName;
    }
}
````    
@Builder 어노테이션을 사용하면 해당 클래스의 모든 필드를 빌더 메서드로 사용가능함.    
      
        

<hr/>

> 이번 개인프로젝트에서 Builder 클래스를 사용하는 중 특정 값을 변경하고 싶은데  
> 수정이 아니라 객체가 덮어지는 문제가 발생함.  
    
      
    
### 비밀번호 변경하는 코드
```java
public ResponseEntity<String> changePw(UserLoginRequest dto) {
     User findUser = userRepository.findUserByEmail(dto.getEmail());

     User encryptedUser = findUser.toBuilder()
             .password(passwordEncoder.encode(dto.getPassword()))
             .build();

     serRepository.save(encryptedUser);

     return ResponseEntity.ok().body("비밀번호 변경 성공");
    }
```    
    
```java
@Entity
@Builder(toBuilder = true)
@RequiredArgsConstructor
@Getter
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "USER_ID")
    private Long id;

    @NotBlank
    @Email(message = "이메일 형식이 아닙니다.")
    private String email;

}
```    
    
@Builder(toBuilder = true) 를 이용하면 수정을 할 수 있다.  
    
    
### 그럼 여기서 변경할때 사용할 메서드를 만들어서 이용을 했다면?    
    
```java
public class User {

    public void changePassword(User user, String password){
        this.password = password;
    }
}

```
    
```java
public ResponseEntity<String> changePw(UserLoginRequest dto) {
     User findUser = userRepository.findUserByEmail(dto.getEmail());

     findUser.changePassword(passwordEncoder.encode(dto.getPassword()));
     userRepository.saveAndFlush(findUser);

     return ResponseEntity.ok().body("비밀번호 변경 성공");
}
```   
    
toBuilder는 찾은 객체를 가지고 똑같은 객체를 만들어서 저장되는것이다.  
새로 생긴 객체는 저장이 되고 이전 객체는 삭제가 된다.  
    
    
비밀번호를 변경할 메서드를 만들면 찾은 객체를 변경하는것이다.  
  
  
어떤 상황에서 어떤걸 선택해야할지 모르겠지만, 이번 상황에서는 toBuilder보다는 메서드를 만들어서 사용하는게 더 효율이 좋아보인다.  
    
    
<hr>
    
> 저번 프로젝트에서는 setter를 무분별하게 사용했지만 이번 프로젝트에서는 
> setter를 사용하는건 지양해야한다는걸 지키기 위해 Builder와 메서드를 생성해서 사용하고 있다!!!

