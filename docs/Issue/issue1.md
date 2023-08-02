---
layout: default
title: JPA Executing an update/delete query 에러 해결
parent: Issue
---
    
# [JPA] Executing an update/delete query 에러 해결  

## <span style="background-color:skyblue; color: white">Reason</span>
![error.png](/assets/images/Issue/Issue1/error.png)
    
![before.png](/assets/images/Issue/Issue1/before.png)

update/ delete 쿼리를 사용할때는 Transaction 처리를 해야한다.  


## <span style="background-color:pink; color: white"> Solution </span>
![after.png](/assets/images/Issue/Issue1/after.png)