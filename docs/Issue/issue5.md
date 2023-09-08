---
layout: default
title: Scheduled 사용 시 @Transactional 메소드 사용으로 인한 에러 
parent: Issue
---

# @Scheduled 사용 시 @Transactional 메소드 사용으로 인한 에러

## <span style="background-color:skyblue; color: white">Reason</span>
![before.png](/assets/images/Issue/Issue5/before.png)
    
```shell
Unexpected error occurred in scheduled task
```  
  
에러 발생



## <span style="background-color:pink; color: white"> Solution </span> 
![after.png](/assets/images/Issue/Issue5/after.png)     

![after_1.png](/assets/images/Issue/Issue5/after_1.png)
[참고자료1](https://www.inflearn.com/questions/297130/scheduled-%EC%82%AC%EC%9A%A9-%EC%8B%9C-transactional-%EB%A9%94%EC%86%8C%EB%93%9C-%EC%82%AC%EC%9A%A9-%EC%8B%A4%ED%8C%A8-%EA%B4%80%EB%A0%A8)
  
[참고자료2](https://jo5ham.tistory.com/45)  

@Scheduled 와 @Transactional 어노테이션을 분리해야한다.  

해결방법이 2가지가 있다.  
### 1) @Scheduled을 가진 클래스가 참조하는 메서드의 @Transactional을 지우는 방법이 있다.  
하지만 JPA에서 값 변경은 트랜잭션 내에서 이루어져야하기 때문에 삭제하는건 좋은 방법이 아니라고 생각해 다른 방법을 찾았다.  

### 2) @Scheduled 클래스에서 @Transactional을 가진 repository와 분리  

