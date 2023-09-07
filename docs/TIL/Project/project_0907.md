---
layout: default
title: 23.09.07 TIL
parent: TIL
---

# 23.09.07 TIL


>🗓 날짜 : 2023.09.07   
> 📚 할 일 : 개인 프로젝트 진행, 블로그 작성  
> 📝 오늘의 목표:  [SELLMS], [SEELP] 진행, [MAS] 진행 
> ⌛ 공부시간 : 9:00 ~  




## 1. 관리자 권한 시스템  [MAS]  

![denied-image.png](/assets/images/TIL/project/0907/denied-image.png)  

> Additional work로 넘겼던 관리자 권한 시스템 [MAS]  
> 페이지에 따른 권한 관리를 하지 않고 넘겼다.  
>   
> 그래서 오늘 페이지에 따른 권한 관리를 진행했다.  

&nbsp;
  

```vue
// actions.js
const config = {
    headers: {
        'Authorization': 'Bearer '+ useCookies().cookies.get('access_token'),
        'Accept' : 'application/json',
        'Content-Type': 'application/json'
    }
};


export default {
    fetchWaitingListUsers({commit}) {
        return axios.get(API_BASE_URL+"/api/v1/manager/waitingList", config)
            .then((res) => {
                commit(FETCH_WAITING_LIST_USERS, res.data)
        })
            .catch((error) => {
                throw error;
        })
    }
}
```
  
페이지가 생성이 되면 fetchWaitingListUsers()이 시작이 되기때문에 권한이 없으면 에러를 던진다.  


```java  
@Configuration
@EnableWebSecurity
@RequiredArgsConstructor
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {

    @Bean
    public SecurityFilterChain filterChain (HttpSecurity http) throws Exception {
        
        // 추가 설정
        
        http.
                formLogin().disable()
                .requestmatchers("/api/v1/manager/**").hasAnyAuthority("ADMIN")
                // 추가 설정
                .anyRequest().permitAll();

        http
                .exceptionHandling()
                .accessDeniedHandler(new CustomAccessDeniedHandler());
        
        return http.build();
    }
}
```  
  
```java
public class CustomAccessDeniedHandler implements AccessDeniedHandler {
    @Override
    public void handle(HttpServletRequest request, HttpServletResponse response, AccessDeniedException accessDeniedException) throws IOException, ServletException {
        response.sendError(HttpServletResponse.SC_FORBIDDEN);
    }

}
```  

```vue
// ManagerWaitingListView

methods: {
    async fetchData(){
        try{
          await this.$store.dispatch('fetchWaitingListUsers')
        }catch (error) {
          await this.$router.push({name: 'ManagerAccessDeniedPage'})
          console.error(error);
      }
    }
},
```  


CustomAccessDeniedHandler를 생성해서 권한이 없을 경우 에러 메세지를 전달하도록 구했다.  

> jwt에 관한 부분은 따로 정리해서 올려야겠다.  
  

## 2. 관리자 권한 시스템 [MAS]: 권한 설정으로 인한 이슈 정리  
  
[hasRole()/ hasAuthority() 차이점으로 인한 에러](https://areuma.github.io/docs/Issue/issue4/)
