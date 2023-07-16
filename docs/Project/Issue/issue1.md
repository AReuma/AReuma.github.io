---
layout: default
title: 이슈관리
grand_parent: Project 
---
    
# [JPA] Executing an update/delete query 에러 해결  
    
## Reason 
![error.png](/assets/images/Project/Issue/Issue2/error.png)
    
![before.png](/assets/images/Project/Issue/Issue2/before.png)

update/ delete 쿼리를 사용할때는 Transaction 처리를 해야한다.  
    

## Solution  
![after.png](/assets/images/Project/Issue/Issue2/after.png)