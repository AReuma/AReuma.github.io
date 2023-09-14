---
layout: default
title: 23.09.14 TIL
parent: TIL
---

# 23.09.14 TIL  
    
>🗓️ 날짜 : 2023.09.14  
> 📚 할 일 : 개인 프로젝트 진행, 블로그 작성, 강의 듣기  
> 📝오늘의 목표:  [SELLMS], [SELLP]진행  
> ⌛ 공부시간 : 9:00 ~
  

<hr>

## 1. Seller 회원가입 진행  
  
![img_1.png](/assets/images/TIL/project/0914/img_1.png)     
   
![img_2.png](/assets/images/TIL/project/0914/img_2.png)  
  
```java
public enum WaitingListStatus {
    REFUSAL,    // 거절
    ALLOW,      // 승인
    WAIT,       // 신청 후 결과 기다리는 중
    JOIN,       // 가입완료
}
```

입점 심사를 통과하면 allow 그 후 이 페이지에 들어와서 회원 가입으로 하면 JOIN으로 변경됨.  
그 후 WaitingListStatus에 있는 값을 삭제하도록 구현.  
  
vue에서 이미지 파일을 보낼때 formData를 이용해서 보낸다.  
  
```vue
FormData formData = new FormData();

formData.append('image', this.file);
formData.append('name', this.name);
```
  
```java
@PostMapping("/join")
public ResponseEntity<String> sellerRegister(@ModelAttribute JoinSellerRequest joinSellerRequest){
    return sellerService.registerSeller(joinSellerRequest);
}
```  
@ModelAttribute 을 이용해서 dto로 값을 받아오는 방법  

  
```java
@Getter
@AllArgsConstructor
public class JoinSellerRequest implements Serializable {

    private String approvedEmail;
    private String email;
    private String password;
    private String storeName;
    private String storeBio;
    private String storeIntroduction;
    @NotBlank
    private MultipartFile profileImg;
}
```  
Multipartfile과 JsonData를 함께 받으려면 dto를 byte 형식으로 바꾸는 직렬화를 해줘야한다.  
그래서 implements Serializable을 상속받는다.  
  
이 부분을 구현할때 프론트 콘솔에서 formData를 찍었는데 값이 안나와서 뭐가 문제인지 고민하다가 시간을 많이 잡아먹었다.  
  
formData는 브라우저 정책으로 formData만 찍으면 나오지않는다.  
key로 value값을 찾으면 콘솔창에서 볼 수 있다.   
  
  
  
## 2. 판매자 센터 대시보드 구현
![img_4.png](/assets/images/TIL/project/0914/img_4.png)     

## 3. Seller 로그인 진행중
![img_3.png](/assets/images/TIL/project/0914/img_3.png)  
   
Spring boot Security를 사용해서 로그인을 진행하고 있다.  
일반 회원 로그인과 판매자 로그인을 나눠서 로그인을 진행하려하고 있는데 springSecurity 부분에서 막혀있다.  
    
일반 회원의 로그인 폼과 판매자의 로그인 폼을 나눠서 로그인을 할 경우에 SecurityFilterChain을 두개를 구현을 한 후 @Order()로 순서를 정하면 된다고 한다.  
  
하지만 일반 회원 filter에서 넘어가지 않는 문제가 보이고 있다.  

  
<hr>
  
[참고블로그]
  
[Multipartfile 전송하는 방법](https://leeggmin.tistory.com/7)  
  
[SpringSecurity 두개의 폼에서 로그인 구현 참고]  
[https://www.codejava.net/frameworks/spring-boot/multiple-login-pages-examples](https://www.codejava.net/frameworks/spring-boot/multiple-login-pages-examples)
[https://recordsoflife.tistory.com/947](https://recordsoflife.tistory.com/947)

