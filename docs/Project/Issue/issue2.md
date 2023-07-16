---
layout: default
title: 이슈관리
grand_parent: Project
---

# [JAVA] Map안에 map 찾기 (OAuth2 Naver Login 오류 발생)


## Reason 
![error.png](/assets/images/Project/Issue/Issue2/error.png)
    
네이버는 다른 로그인 api와는 다르게 담겨서 넘어온다.  
카카오, 구글, 깃허브는 Map 하나에 담겨온다면, 네이버는 Map안에 map이 있는 형태로 넘어온다.  
      
![img.png](/assets/images/Project/Issue/Issue2/img.png)
         

## Solution 
### 변경 전 
![before.png](/assets/images/Project/Issue/Issue2/before.png)
      
### 변경 후 
![after.png](/assets/images/Project/Issue/Issue2/after.png)
      
      
  

~~~ java
Map response = new HashMap();
Map userInfo = new HashMap();

userInfo.put("id", "areum.com");
userInfo.put("name", "areum");
response.put("userInfo", userInfo);
// response는 {userInfo={id=areuma.com, name=areum}}
~~~

## 해결
~~~ java

String userId = ((HashMap<?,?>) response.get("userInfo").get(id).toString();)

~~~