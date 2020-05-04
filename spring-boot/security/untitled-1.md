# Untitled

## 환경설정 추가 Login 화면 실행

* 신규 프로젝트 생성- SpringBooSecurity

void configure\(HttpSecurity http\) 

```java
@Override
public void configure(HttpSecurity http) throws Exception {
  http
    .antMatchers("/admin/*")
      .authenticated()
    .and()
      .formLogin()
          .loginPage("/login")
          .defaultSuccessUrl("/admin/main", true);
}
```

  `.antMatchers()`를 통해  /admin/로 접근하는 url은 로그인이 필요하다고 정의해준다,   
`.formLogin()`을 통해 로그인 페이지와 로그인 성공시 보내줄 url을 정의해다.

```text
login.jsp

<form method="post">
 <input type="text" name="username" />
 <input type="password" name="password" />
</form>
```

 `<form />` 이  [Postback](https://en.wikipedia.org/wiki/Postback#In_web_development)으로 구현되어 있다. 즉, `action` attiribute가 없다 ????????  그럼 입력받은 값과 DB의 값을 어디서 어떻게 처리하라는 것인가 ...... 

`POST`로 들어온 아이디와 비밀번호는   
_**`UserDetailsService`와 `PasswordEncoder`가 처리한**_다!  
1. DB에서 아이디로 사용자 정보를 조회한다 \(=비밀번호 포함\)  
2. 입력받은 비밀번호를 인코딩한다  
3. 인코딩한 비밀번호와 사용자 정보의 비밀번호를 비교한다

