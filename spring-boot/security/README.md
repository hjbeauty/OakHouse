# Security

## **Spring Security란?**

{% page-ref page="./" %}

> ### Spring기반  Application의  보안\(인증과권한\)을 담당하는 Framework
>
> 필터기반의 스프링 시큐리티는 보안과 관련해서 체계적으로 많은 옵션들을 지원해주고 Spring MVC프레임과 분리되어 관리 및 동작한다.

### 보안관련 용어

> * **접근주체 \(Principal\)** :  보호된 대상에 접근하는 사용자
> * **인증\(**[Authentication](https://m.blog.naver.com/PostView.nhn?blogId=eternity9us&logNo=221397323452&proxyReferer=https:%2F%2Fwww.google.com%2F)**\)** : 자신이 누구라고 주장하는 **사람을 확인**하는 절차  - 보통 로그인 같이 아이디와 암호를 이용해서  사용자인증하는 절차.
> * **인가\(**Authorize**\)**  : **특정 자원에 대한 접근 권한이 있는지 확인**하는 절차 -  어떤 서비스에 접근할 수 있는 권한이 있는지 검사 
> * 권한 \(Authorization ****\): 인증된 주체가 application의 동작을 수행할 수 있도록  허락되어 있는지를 결정 , 일반 유저 계정과 admin 계정으로 접근할 수 있는 메뉴가 달라지는 것 으로 인증과정을 거쳐 주체가 증명되어야 한다.

### 인증 ==&gt; 인가 ::  인증 절차를 거친 후 미리 부여된 권한에 의해 인가 절차를 진행한다

> 인증 방식
>
> * Credential 기반인증 :  아이디\(principal\)와 비밀번호\(credential\)를 이용하는 방식 ==&gt; Spring Security 가 인증하는 방식 
> * Twofactor 인증\(이중인증\) :  사용자가 입력한 개인 정보를 인증 후 , 다른 인증체계를 이용하여 두가지의 인증방법을 조합하여 인증하는 방식 ==&gt; 은행업무을 위해 공인인증서로 로그인 후 이체를 시키거나 할 때 이체비밀번호 , OTP 를 이용한 번호발생 등이 있다

### \*\*\*\*[**스프링 시큐리티 인증관련 아키텍쳐**](https://spring.io/guides/topicals/spring-security-architecture#_web_security)\*\*\*\*

![](../../.gitbook/assets/spring-security.png)

### Spring Security  기본 인증방식 : 세션-쿠키방식

> * 1번 http request  : 보호된 대상에 접근시도\(로그인\) 하는 사용자   
> * 2번~ 5번. AuthenticationFilter를 통해 사용자정보 토큰을 받음
> * 6번 사용자가 DB에 존재한다면 UserDetails에 의해서  사용자 User의 session 생성
> * 7번~10번 spring security의 세션들은 인메모리 세션저장소인 SecurityContextHolder 에 user의 정보를 저장
> * 사용자에게 session ID를 담아서 response 한다
> * 이후 사용자가 요청하면 쿠키에서 JSESSIONID를 찾아서 검증 후 유효하면 Authenticatione에 담는다.

* WebSecurityConfigurerAdapter 에 의해 ApplicationContext가 생성시DefaultPasswordEncoder AuthenticationManagerBuilder, ProviderManager, DaoAuthenticationProvider, 그리고 서블렛 필터 UsernamePasswordAuthenticationFilter가 만들어진다. 
*  사용자가 POST로 로그인을 시도하면.. 위의 서블릿 필터를 통해 ProviderManager.authenticate\(\)가 호출되고, 이어DaoAuthenticationProvider의 retrieveUser\(\)와 additionalAuthenticationChecks\(\)를 통해 UserDetailsService.loadUserByUsername\(\)과 PasswordEncoder.matches\(\)가 호출되어 로그인 정보를 확인합니다. 확인하여 이상이 없다면, 필터에서는 UsernamePasswordAuthenticationToken을 리턴받아 세션에 저장하고, 다시 successfulAuthentication\(\)을 통해 SecurityContext에 저장하고, 사용자를 로그인 완료 페이지로 리다이렉트 시켜줍니다

> ###   **Authentication/ SecurityContext/ SecurityContextHolder 각 컴포넌트간의 관계**

> > **principal+credential ---- 인증처리--&gt;  Authentication이 사용자정보 저장 --&gt; Authentication을 SecurityContext에 저장 --&gt;**  S**ecurityContext 을  S**ecurityContextHolder 에 저장

### Authentication 인증 모듈

> ####  **AuthenticationManager : 사용자 비밀번호 인증 담당**

```java
public interface AuthenticationManager {
    Authentication authentication(Authentication authentication) 
        throws AuthenticationException;
}
```

> * 인증 성공시 : 인증 정보를 담은 Authentication 객체 리턴한다.  인증 요청은 AuthenticationManager내에서 검색된 AuthenticationProvider에 의해 처리되고, 스프링 시큐리티는 return한 Authentication 객체를 SecurityContext에 인증 및 보관 상태를 유지하기 위해 세션에 보관\)
> * 인증 실패시: AuthenticationException을 발생시킴

### 



