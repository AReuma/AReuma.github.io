---
layout: default
title: SpringSecurity 다중 로그인 구현  
parent: Bossi
grand_parent: Project
---

# 23.09.15 이번주 진행상황  

![img.png](/assets/images/Project/Bossi/bossi_spring_order/img.png)  
9.17일까지 SELLMS 마무리 예정  
  
&nbsp;
  
# SpringSecurity 다중 로그인 구현  
  &nbsp;

"User"과 "Seller"을 연관 관계를 맺지 않고 각각 따로 가입할 수 있도록 설계했습니다.  
또한, 판매자로 가입한 경우, 관리자가 정보를 확인한 후 입점 승인 또는 보류를 메일로 통지하고, 승인된 사용자는 메일을 통해 인증 후 가입할 수 있도록 구현했습니다.

설계에 맞춰 개발 중에, 일반 회원은 UserDetails와 UserDetailService를 이용하여 로그인하게 되는데, 판매 회원은 어떻게 인증을 해야할지 막막했습니다.  
여러개의 블로그를 찾아보았으나 WebSecurityConfigurerAdapter을 이용해 구현을해막히는 부분이 꽤 있었지만 해결을 해 정리해서 블로그 작성했습니다.  
  
&nbsp;
![loginPage.png](/assets/images/Project/Bossi/bossi_spring_order/loginPage.png) 
&nbsp;
&nbsp;
![sellerLogin.png](/assets/images/Project/Bossi/bossi_spring_order/sellerLogin.png)
&nbsp; 

# 1. SellerUserDetails 구현  
    
``` java
public class CustomSellerDetails implements UserDetails {

    private final Seller seller;

    public CustomSellerDetails(Seller seller) {
        this.seller = seller;
    }

    // 나머지 UserDetails 메서드를 구현
}
```
  
    
  
# 2. CustomSellerAuthenticationProvider 구현
```java 
@Slf4j
@Configuration
public class CustomSellerAuthenticationProvider implements AuthenticationProvider {
    private final SellerDetailsService sellerDetailsService;
    private final PasswordEncoder passwordEncoder;

    public CustomSellerAuthenticationProvider(SellerDetailsService sellerDetailsService, PasswordEncoder passwordEncoder) {
        this.sellerDetailsService = sellerDetailsService;
        this.passwordEncoder = passwordEncoder;
    }

    @Override
    public Authentication authenticate(Authentication authentication) throws AuthenticationException {
        String username = authentication.getName();
        String password = authentication.getCredentials().toString();

        UserDetails userDetails = sellerDetailsService.loadUserByUsername(username);    // 사용자 정보 가지고 오기  

        if (passwordEncoder.matches(password, userDetails.getPassword())) {
            return new UsernamePasswordAuthenticationToken(userDetails, password, userDetails.getAuthorities());
        } else {
            throw new UsernameNotFoundException("Invalid credentials");
        }
    }

    @Override
    public boolean supports(Class<?> authentication) {
        return authentication.equals(UsernamePasswordAuthenticationToken.class);
    }
}

```  
  

# 3. SellerSecurityConfig
  

~~~java
@Configuration
@EnableWebSecurity // 스프링 시큐리티 필터가 스프링 필터체인에 등록이 됨
@RequiredArgsConstructor
@Order(1) // 우선순위 지정  
@Slf4j
public class SellerSecurityConfig {

    private final JwtSellerTokenService jwtSellerTokenService;
    private final SellerRepository sellerRepository;
    private final SellerDetailsService sellerDetailsService;
    private final PasswordEncoder passwordEncoder;

    @Bean
    public CustomSellerAuthenticationProvider customSellerAuthenticationProvider() {   
        return new CustomSellerAuthenticationProvider(sellerDetailsService, passwordEncoder);
    }

    @Bean
    public AuthenticationManager sellerAuthenticationManager(HttpSecurity http) throws Exception {  

        AuthenticationManagerBuilder authenticationManagerBuilder =
                http.getSharedObject(AuthenticationManagerBuilder.class);

        authenticationManagerBuilder.authenticationProvider(new CustomSellerAuthenticationProvider(sellerDetailsService, passwordEncoder));
        return authenticationManagerBuilder.build();
    }


    @Bean
    SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
                .httpBasic().disable()
                .csrf().disable()
                .cors();

        http
                .securityMatcher("/api/v1/seller/login")  
                .formLogin().disable()
                .sessionManagement().sessionCreationPolicy(SessionCreationPolicy.STATELESS)
                .and()
                .addFilter(new CustomSellerAuthenticationFilter(sellerAuthenticationManager(null)))
                .addFilterBefore(new CustomSellerAuthorizationFilter(jwtSellerTokenService, sellerRepository), UsernamePasswordAuthenticationFilter.class);

        return http.build();
    }
    
}
~~~    
  
> .securityMatcher("/api/v1/seller/login")으로 설정을해서 /api/v1/seller/login으로 요청을 받았을때 해당 보안규칙을 따라야한다.  
