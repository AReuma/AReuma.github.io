---
layout: default
title: 23.09.03 TIL
parent: TIL
---

# 23.09.03 TIL
  
    
> 🗓 날짜 : 2023.09.03  
>📚 할 일 : 개인 프로젝트 진행, 블로그 작성하기  
>📝 오늘의 목표:  [MP], [SELLMS], [SEELP] 진행  
>⌛ 공부시간 : 9:30 ~
    
  
![agile_0903.png](/assets/images/TIL/project/0903/agile_0903.png)    
    

## 1. 메인 페이지 [MP] 
  
    
![categoryMouseover.png](/assets/images/TIL/project/0903/categoryMouseover.png)    
    
![nameMouseover.png](/assets/images/TIL/project/0903/nameMouseover.png)    
    
```vue
<div class="after_login_button" @mouseover="mouseover" @mouseleave="hideList">
    <div>{{ nickName }} 님</div>
    
    <div v-if="mouseoverCheck" style="position: absolute; z-index: 1; height: 170px; right: 320px; width: 150px; margin-top: 2px; padding: 10px; background-color: white; border: 0.5px solid rgba(67,79,88,0.25); border-radius: 4px">
      <div v-for="(item, i) in mouseoverList" :key="i" style="padding: 5px;" @mouseover="changeTextColor(i)" @mouseleave="resetTextColor(i)">
        <router-link class="custom-link" :to="{name: item.routerName}" :style="{color: item.textColor}"> {{item.name}} </router-link>
      </div>
      
      <hr style="margin: 8px 0; border: 0.5px solid rgba(67,79,88,0.2);"/>
      
      <div style="padding: 2px" @click="logout" @mouseover="changeTextColorLogout" @mouseleave="resetTextColorLogout" :style="{color: changeTextColorLogoutColor}">
        로그아웃
      </div>
    </div>
</div>
```
    
    
```vue
data(){
  return {
    mouseoverList: [
        { name: '주문배송', routerName: 'MyOrderDeliveryPage', textColor: 'black'},
        { name: '관심리스트', routerName: 'FavoriteProductPage', textColor: 'black'},
        { name: '쿠폰함', routerName: 'MyCouponListPage', textColor: 'black'},
        { name: '회원 정보관리', routerName: 'PersonalInfoPage', textColor: 'black'},
    ],
  }
},
methods: {
    mouseover(){
        this.mouseoverCheck = true;
    },
    hideList(){
        this.mouseoverCheck = false
    },
    changeTextColor(index) {
        this.mouseoverList[index].textColor = this.hoverColor;
    },
    resetTextColor(index) {
        this.mouseoverList[index].textColor = 'black';
    },
}
```
      
> mouseover 구현    
> div 배치 설정 구현  
    
    
## 문제가 발생했던 부분 🔍  
    
이름 위에 마우스를 올리면 카테고리 박스가 나오도록 구현을 하고 싶어서 mouseover를 사용해서 div 박스가 나오도록 구현을 했으나  
내 정보와 장바구니 버튼이 있는 div가 앞으로 나오는 상황이 발생했다.  
    
검색을 해보니 z-index를 이용해서 배치를 할 수 있다고해서 이용했다.  
    
### z-index   
    
* position 속성이 static인 경우 z-index 속성 값을 변경해도 바뀌지않는다. 
  * position 속성을 relative, absolute, fixed, sticky로 변경해야한다. 
  
* z-index의 속성값의 숫자가 높을수록 앞으로 온다. (음수도 사용가능)
    
    
## 문제가 발생했던 부분 🔍
  
    
### 변경 전 
```vue
 <div v-for="(item, i) in mouseoverList" :key="i" style="padding: 5px;" @mouseover="changeTextColor()" @mouseleave="resetTextColor()">
   <router-link class="custom-link" :to="{name: item.routerName}" :style="{color: textColor}"> {{item.name}} </router-link>
</div>
```
마우스를 올리면 뜰 이름들을 리스트로 만든 후 v-for을 이용해서 출력하도록 구현했다.  
그 후 마우스를 올리면 글씨색이 변경되도록 구현을 원해서 리스트안에 색상을 넣지 않고 메서드에서 바로 this.textColor = 'this.hoverColor'; 변경을 시도했으나 이렇게 구현을하면 
마우스를 올릴때 모든 글씨의 색상이 변경이 되는 문제가 발생했다.  
  
쉽게 생각을해보면 v-for로 반복되는 router-link에서 한번에 똑같은 색상으로 변경되는건 당연한 일이었다.  
그래서 리스트안에 원래 글씨 생상을 넣어두고 마우스 올리는 이벤트가 발생하면 그때 인덱스를 넘겨서 해당의 리스트의 색상을 변경하도록 구현했다.  
  
### 변경 후
```vue
<div v-for="(item, i) in mouseoverList" :key="i" style="padding: 5px;" @mouseover="changeTextColor(i)" @mouseleave="resetTextColor(i)">
   <router-link class="custom-link" :to="{name: item.routerName}" :style="{color: item.textColor}"> {{item.name}} </router-link>
</div>
```

## 2. 입점 페이지 [EP]
  
![enteringStore.png](/assets/images/TIL/project/0903/enteringStore.png)
     
![enteringStoreForms.png](/assets/images/TIL/project/0903/enteringStoreForms.png)    
    

아래 화살표를 클릭하면 스크롤이 내려 고객의 정보를 작성해서 요청하는 폼이 나오도록 구현.  
    
```vue 
<div style="position: absolute; z-index: 4; left: 48%; top: 760px;" @click="scrollClick()">
    <v-icon x-large color="white">mdi-chevron-down</v-icon>
</div>
```

```vue
methods: {
    scrollClick() {
      window.scrollTo(0, 830);
    }
}
```
    
    
### window.scrollBy(x, y)
    
* 상대적인 위치 지정 
* 현재 위치를 기준으로 파라미터 값만큼 이동
  
### windw.scrollTo(x, y)  
    
* 절대적인 위치 지정
* 창의 시작을 기준으로 파라미터 값만큼 이동


## 2. 관리자 페이지 [MAP],[SELLMS]
    
![managerPageMemo.png](/assets/images/TIL/project/0903/managerPageMemo.png)
   
관리자 페이지에서 어떤걸 구현할지 화면설계.  
  
관리자가 입점을 허용하게 되면 사용자의 계정을 어떻게해야할지에 대한 고민이 필요하다. 
새로운 계정을 만들도록 해야할지, 아니면 같은 계정을 사용하도록 해야할지 선택을 해야겠다.  
    
새로운 계정을 만든다면 DB의 연관관계가 조금 간단해질것 같다.  
일반 계정과 판매자 계정이 연결이 되어야하는 이유가 있을까..?
  
새로운 계정을 만들지 않으면 사용자가 판매자인지에 대한 판단을 하기위한 컬럼을 추가해야하고, User 와 연관관계를 맺어야한다.  
새로운 계정을 만들면 그 계정은 어떻게 관리를 해야할까 User DB에 넣어야하는걸까? 추가해야할 내용이 많기 때문에 따로 만들어서 연관관계를 맺어야한다.
그럼 새로운 계저을 만들지 않는거랑 똑같다.  
   
  
그럼 완전히 DB를 분리하게 된다면,, 
왜 분리해야하지?  
이 부분은 조금 더 고민을 해봐야겠다.  
   

## ✅ 마무리  
ERD를 설계할때 고민을 해보고 설계를 했는데, 프로젝트를 진행하면서 설계가 제대로 안된 부분이 생겼다.  
개인 프로젝트라서 상의해서 결정을 하지않고 혼자 해야하니... 조금 더 어려운것 같다.  
  
어떤 이유로 선택했는지 정리는 해둬야겠다.  
  
