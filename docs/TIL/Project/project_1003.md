---
layout: default
title: 23.10.03 TIL
parent: TIL
---

# 23.10.03 TIL  
    
> 🗓️ 날짜 : 2023.10.03  
> 📚 할 일 : 개인 프로젝트 진행  
> 📝 오늘의 목표:  [PAYMS] 진행   
> ⌛ 공부시간 : 10:00 ~
  

<hr>

## 1. 장바구니   
     
![장바구니.png](/assets/images/TIL/project/1003/img_1.png)    
  
&nbsp;  

![구매.png](/assets/images/TIL/project/1003/img.png)
  
  
장바구니에 들어있는 상품을 구매하던지, 상품 페이지에서 바로 구매를 하던지 상관없이 바로 장바구니 페이지로 이동하도록 구현했다.  
  
장바구니에 들어있는 상품은 redis를 통해서 구현 예정 중이다.  
바로 구매를 할 경우에는 현재 상품의 특정값과, 옵션, 주문 개수를 쿠키 값(만료시간 지정함)으로 저장하고 그 값을 백엔드로 보내서 원하는 값을 가지고 오도록 구현했다.  
  
처음에는 값을 eventBus로 페이지에서 페이지로 값을 이동하려고 했으나, vue 라이프 사이클 때문에 새로고침을 하면 값이 없어지는 문제가 발생했다.  
해결을 하기 위해서 값을 쿠키에 저장하고 백엔드로 보내서 값을 가지고 옴.  
  
  
이런식으로 구현을 하면 새로고침을 할때마다 쿼리가 발생한다.  
좋은 방법이 없는지 고민을 해봐야겠다.  
  
지금 확인 했는데 배송비 부분에서 일정 값 이상일때 무료인 부분이 구현이 안되어 있다.  
이 부분은 다시 고쳐야겠다.  


## 2. 주문하기   
  
주문을 하기 위해서는 배송 정보, 주문 고객의 정보, 주문 상품의 정보 등등이 필요하다.  
  
그래서 그에 맞는 엔티티 구현을 하고 있다.  

![img_2.png](/assets/images/TIL/project/1003/img_2.png)  
  
