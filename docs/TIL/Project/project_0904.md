---
layout: default
title: 23.09.04 TIL
parent: TIL
---

# 23.09.04 TIL


>🗓 날짜 : 2023.09.04  
>📚 할 일 : 개인 프로젝트 진행, 블로그 작성하기, 강의듣기  
>📝 오늘의 목표:   [SELLMS], [SEELP] 30% 이상 진행, [MAF] additional Work로 넘기기  
>⌛ 공부시간 : 9:30 ~



![agile_0904.png](/assets/images/TIL/project/0904/agile_0904.png)

## 1. 관리자 페이지 [MAF]



![managerFront.png](/assets/images/TIL/project/0904/managerFront.png)    
![MAFCategory.png](/assets/images/TIL/project/0904/MAFCategory.png)   
![MAFWaitingUser.png](/assets/images/TIL/project/0904/MAFWaitingUser.png)



> 관리자 페이지에서 카테고리는 v-list-item으로 구현했다.  
> 판매 페이지를 먼저 구현하고 싶었으나, 판매 상품을 작성할 수 있는 사용자를 생성하기 위해서 관리자 페이지를 구현했다.   
> 여부를 선택 후 일정 시간이 지나면 waitingList DB에서 삭제가 되도록 구현중이다.  
> 관리자 계정은 이미 만들어 둔 상태고 관리자 가입을 어떻게 진행해야 할지 고민해야 한다.



## 2. 회원 관리 시스템 [MMS]


오늘 진행을 하면서 연관관계를 맺어야 할지 고민했다.  
![User_WaitingListDB.png](/assets/images/TIL/project/0904/User_WaitingListDB.png)


먼저 그려둔 ERD를 보면 User와 WaitingList를 1:1 연관관계를 맺었다.

아마 기획 시점에서부터 잘못된 것 같다.
무슨 생각으로 기획을 한 건지 모르겠다.

### 1. 누구나 쉽게 판매할 수 있다.
누구나 쉽게 판매할 수 있다고 생각했으면 WaitingList라는 DB를 설계할 필요 없이 Seller db에 insert를 하면 된다.
때문에 허가를 받는 걸 기획했던 것 같다.

### 2. 허가받고 새로운 계정을 만들 동안 사용자 정보를 저장해 두는 DB로 설계한 것이다.
허가받으면 WaitingList에 insert가 되고 따로 판매자로 회원가입을 할 때 User와 연관관계를 맺으려고 만들어 둔 db였다.

### 3. 허가 요청을 기다리는 DB로 설계한 것이다.
사용자가 허가 요청을 하면 WaitingList에 저장이 되고 관리자가 허용하면 Seller에 insert하고 User와 연관관계를 맺는다.



다음 DB 설계할 때는 좀.. 설명도 추가해서 작성해야겠다.
<hr/>

어쨌든 2번과 3번 둘 다 허가를 받고 난 후 Seller와 연관관계를 맺을 때를 위해서 User와 WaitingList를 1:1 연관관계를 맺은 것 같은데,
지금 생각해 보니 연관관계가 딱히 필요 없을 것 같다.

WaitingList에 사용자의 아이디가 있으니깐 허가받은 후 email로 찾아서 Seller와 연관관계를 맺으면 되겠다. (아이디는 중복 불가, 유니크 제약조건)


WaitingList에 있는 사용자는 허가받고 일정 시간이 지나면 사라지도록 구현할 예정이었다.

<hr style="border: dashed 1px black"/>

### Optional
한 명의 회원이 여러 개의 상점을 가질 수 없다고 기획을 잡았다.

그래서 WaitingList 안에 아이디가 있는지 중복 체크를 했다.
중복을 체크하기 위해서 Optional을 사용했는데 보통은 null일 때 예외 처리를 했다.

```java
userRepository.findByEmail(email)
        .orElseThrow(() -> new AppException(ErrorCode.USER_NOT_FOUND, "아이디가 없음"));
```

null이 아닐때 예외처리는 if문을 가지고 했다.
```java
Optional<User> findUser = userRepository.findByEmail(emil);

if(findUser.isPresent()){
    
}
```


한 줄로 멋지게 코드를 작성할 방법이 있지 않을까 하고 검색했더니 Optional 속성을 통해서 작성할 수 있다고 했다.

```java
userRepository.findByEmail(emil)
  .isPresent(e -> new AppException(ErrorCode.USER_DUPLICATED, "아이디가 이미 존재함"));
```  

Optional 속성은 다음에 정리해봐야겠다.


## ✅ 마무리
개인 프로젝트다 보니 기획이 변경되어도 크게 문제 될 건 없다고 생각했다.
다른 사람이랑 코드를 공유하는 게 아니다 보니 그냥 고치면 되겠다고 생각했지만, 구현 도중 다시 설계해야 하고 구현했던 부분을 지워야 하는 문제들이 발생했다.
기획하고 설계할 때 생각보다 더 자세히 작성해야겠다는 생각이 들었다.

이번 프로젝트는 어영부영 굴러가는 것 같다... 💧


