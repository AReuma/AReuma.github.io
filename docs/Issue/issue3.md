---
layout: default
title: NotBlank 어노테이션 잘못 사용으로 인한 에러 
parent: Issue
---

# 이슈관리

## <span style="background-color:skyblue; color: white">Reason</span>
회원가입을 진행할때 발생하는 에러문구 
![errorCode.png](/assets/images/Issue/Issue3/errorCode.png)
    
User Entity에 @NotBlank 어노테이션 사용으로 인한 오류 발생.    

![before.png](/assets/images/Issue/Issue3/before.png)
## <span style="background-color:pink; color: white"> Solution </span>  
@NotBlank/ @NotEmpty/ @NotNull 이용해서 DB에 저장되는 데이터를 설정할 수 있다.  

| 어노테이션                                       | 거부            | 허용     |
|---------------------------------------------|---------------|--------|
| <span style="color:yellow">@NotNull</span>  | Null          | "", " " |
| <span style="color:yellow">@NotEmpty</span> | Null, ""      | " "    |
| <span style="color:yellow">@NotBlank</span> | Null, "", " " |        |

<span style="color:yellow">@NotBlank</span>는 <span style="color:red">Null, "", " "</span> 값이 허용되지 않는 어노테이션인데 Enum타입에서는 공백과 null 값이 올 수 없기때문에 에러가 발생함.   

<span style="color:yellow">@NotBlank</span> 대신 <span style="color:yellow">@NotNull</span>을 사용하면 에러 해결한다. 
    

![after.png](/assets/images/Issue/Issue3/after.png)
    
<details>
<summary>에러 코드</summary>
<div markdown="1">
V000030: No validator could be found for constraint 'jakarta.validation.constraints.NotBlank' validating type 'com.example.bossi.entity.SocialType'. Check configuration for 'socialType'
</div>
</details>
