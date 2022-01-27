# JWT

## 구성
1. Header
    - Signature를 해싱하기 위한 알고리즘 정보들이 담김
2. Payload
    - 서버와 클라이언트가 주고받는 시스템에서 실제로 사용될 정보에 대한 내용들을 담고 있음
3. Signature
    - 토큰의 유효성 검증을 위한 문자열

## 장점
- 중앙의 인증서버, 데이터 스토어에 대한 의존성 없음, 시스템 수평 확장 유리
- Base64 URL Safe Encoding > URL, Cookie, Header 모두 사용 가능

## 단점
- Payload의 정보가 많아지면 네트워크 사용량 증가, 데이터 설계 고려 필요
- 토큰이 클라이언트에 저장, 서버에서 클라이언트의 토큰을 조작할 수 없음

## Spring SecurityConfig
- API 인증 필요 유무 설정
```java
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    @Override
    protected void configure(HttpSecurity http) throws Exception {
    http
            .httpBasic().disable()
            .csrf().disable()
            .sessionManagement().sessionCreationPolicy(SessionCreationPolicy.STATELESS) // 토큰 기반 인증이므로 세션 사용 하지않음
            .and()
            .addFilter(new JwtAuthenticationFilter(authenticationManager(), userService)) //HTTP 요청에 JWT 토큰 인증 필터를 거치도록 필터를 추가
            .authorizeRequests()
            .antMatchers("/api/hello").authenticated()       //인증이 필요한 URL과 필요하지 않은 URL에 대하여 설정
                    .anyRequest().permitAll()
            .and().cors();
    }
}
```

`.antMatchers()` 부분이 api 인증 유무를 판단하는 코드이다.

뒤에 `.permitAll()`이 붙으면 해당 api는 인증없이 통신하겠다는 뜻이고

`.authenticated()`이 붙으면 인증을 통해서 통신하겠다는 뜻이다.