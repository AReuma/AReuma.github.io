---
layout: default
title: Open API Swagger 3.0 사용법  
parent: Bossi
grand_parent: Project
---

# Open API Swagger 3.0 사용법


![useSwagger_title.png](/assets/images/Project/Bossi/useSwagger/useSwagger_title.png)    
    

# 1. @Controller 설정
    
## 1) @Tag
``` java
@Slf4j
@RestController
@RequiredArgsConstructor
@Tag(name = "UserController", description = "인증 관련 api 입니다.")
@RequestMapping("/api/v1/users")
public class UserController {

}
```
![useSwagger_tag.png](/assets/images/Project/Bossi/useSwagger/useSwagger_tag.png)     
    
@Tag를 이용해서 각 API를 그룹화 할 수 있는 어노테이션이다. 
    

| 속성          | 설명               |
|-------------|------------------|
| name        | API 태그 이름 설정     |
| description | API 태그에 대한 설명 설정 |
    

![useSwagger_method.png](/assets/images/Project/Bossi/useSwagger/useSwagger_method.png)    

![useSwagger_method_checkPhone.png](/assets/images/Project/Bossi/useSwagger/useSwagger_method_checkPhone.png)

## 2) @Operation
```java 
@Operation(summary = "회원가입 전화번호 중복 체크 메서드", description = "회원가입 전화번호 중복 체크 메서드입니다.",
            parameters = {
                    @Parameter(
                            name = "phoneNum",
                            description = "조회할 전화번호",
                            in = ParameterIn.PATH
                    )
})
@ApiResponses(value = {
     @ApiResponse(responseCode = "200", description = "전화번호 인증코드 발급"),
      @ApiResponse(responseCode = "400", description = "전화번호 형식이 다름"),
})
@GetMapping("/checkPhone/{phoneNum}")
public ResponseEntity<?> checkPhoneNum(@PathVariable String phoneNum){
     log.info("checkPhoneNum(): " + phoneNum);

    return messageService.checkPhoneNum(phoneNum);
}
```
![useSwagger_Operation.png](/assets/images/Project/Bossi/useSwagger/useSwagger_Operation.png)
     

![useSwagger_parameters.png](/assets/images/Project/Bossi/useSwagger/useSwagger_parameters.png)         

@Operation은 API 작업을 정의하는데 사용되는 어노테이션이다.  

| 속성          | 설명                  |
|-------------|---------------------|
| summary        | API 작업의 간략한 설명 설정   |
| description | API 작업에 대한 자세한 설명 설정 |
| parameters | API 작업에 전달되는 매개변수 정의 |
| responses | api 작업이 반환하는 응답 형식 및 상태 코드를 정의     |


## 3) @ApiResponse    
![useSwagger_responseCode.png](/assets/images/Project/Bossi/useSwagger/useSwagger_responseCode.png)
       
@ApiResponse는 API 작업의 응답을 설명하는데 사용하는 어노테이션이다. 

| 속성          | 설명                  |
|-------------|---------------------|
| responseCode        | 응답의 HTTP 상태 코드를 정의   |
| description | 응답에 대한 간단한 설명 |
| content | 응답 본문의 미디어 타입과 스키마를 정의     |


## 3) @ApiImplicitParam    
~~~ java
@ApiImplicitParam(name = "phoneNum", value = "전화번호")
@GetMapping("/checkPhone/{phoneNum}")
public ResponseEntity<?> checkPhoneNum(@PathVariable String phoneNum){
     log.info("checkPhoneNum(): " + phoneNum);

    return messageService.checkPhoneNum(phoneNum);
}
~~~    
@ApiImplicitParam은 API 작업의 매개변수를 설명하고 문서화하는데 사용하는 어노테이션이다.         

| 속성          | 설명                  |
|-------------|---------------------|
| name        | 매개변수의 이름을 정의   |
| value | 매개변수에 대한 설명을 설정 |
| defaultValue | 매개변수의 기본값을 지정     |
| required | 매개변수가 필수인지 여부 설정     |
| dataType | 매개변수의 데이터 타입을 지정  |
| paramType | 매개변수의 위치 정의 ex) query, path, body, header   |    
      
    
# 2. Response, Request 설정    
    
## 1) @Schema
![useSwagger_schema.png](/assets/images/Project/Bossi/useSwagger/useSwagger_schema.png)
```java
@RequiredArgsConstructor
@Schema(description = "아이디 비밀번호 찾기 전화번호 인증 응답 DTO")
@Getter
public class FindIdPwResponseDto {

    @Schema(description = "인증코드")
    private final String num;

    @Schema(description = "아이디")
    private final String email;

    @Schema(description = "회원가입한 소셜타입")
    private final String socialType;
}

```    
    
@Schema는 API 모델의 속성을 설명하고 문서화하는 사용되는 어노테이션이다.     


| 속성          | 설명                |
|-------------|-------------------|
| name        | 속성의 이름을 정의        |
| description | 속성에 대한 설명을 설정     |
| type | 속성의 데이터 타입을 지정    |
| format | 데이터의 형식을 지정       |
| example | 속성의 예제 값을 설정      |
| required | 속성이 필수인지 여부 설정    |    
| allowableValues | 허용 가능한 값의 범위를 지정  |    
| hidden | 속성을 문서에 숨길지 여부 설정 |    
