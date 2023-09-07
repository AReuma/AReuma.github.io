---
layout: default
title: hasRole/ hasAuthority 차이점으로 인한 에러 
parent: Issue
---

# hasRole/ hasAuthority 차이점으로 인한 에러

## <span style="background-color:skyblue; color: white">Reason</span>
![before.png](/assets/images/Issue/Issue4/before.png)
    
ADMIN 권한을 가진 회원이 페이지를 요청해도 권한이 없다고 에러가 프론트로 전해진다.  



## <span style="background-color:pink; color: white"> Solution </span> 
![before.png](/assets/images/Issue/Issue4/after.png)   

hasRole() 대신해서 hasAuthority()을 사용하면 된다.  
  
&nbsp;

![hasRole.png](/assets/images/Issue/Issue4/hasRole.png)  
&nbsp;
![hasRole_1.png](/assets/images/Issue/Issue4/hasRole_1.png)  
&nbsp;
![hasRole_2.png](/assets/images/Issue/Issue4/hasRole_2.png)  
&nbsp;
&nbsp;
  
hasRole을 불러올떄 ROLE_PREFIX 가 붙어서 자동적으로 "ROLE_"을 붙여준다.  
즉, hasRole("ADMIN")인 경우는 ROLE_ADMIN 권한을 가진 사람인 것이다.  

&nbsp;
![roleDB.png](/assets/images/Issue/Issue4/roleDB.png)  
나는 DB에 "USER"와 "ADMIN"으로 저장하기 때문에 hasRole()이 아니라 hasAuthority()를 사용하면 된다.  

  
<hr>
[참고 블로그]   

[https://whitepro.tistory.com/494](https://whitepro.tistory.com/494)