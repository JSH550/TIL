# spring security 로그인 기능 구현(session 방식)

## 개요
- spring security로 로그인 기능을 구현해본다.(session 방식)
- 사전준비
  - login form, password hash 방법 정의, loing URL 정의
- 프레임워크 추가
```
...build.gradle 추가
implementation 'org.springframework.boot:spring-boot-starter-security'
implementation 'org.thymeleaf.extras:thymeleaf-extras-springsecurity6:3.1.1.RELEASE'

```
## 기능구현
### 1. login URL 정의(어떤 URL을 login URL로 설정할 것인가?)
- `SecurityConfig` class의 `SecurityFilterChain` 메서드에서 login시 사용할 URL 정의하는 과정이다.
- `PasswordEncoder` class를 `Bean`에 등록 어떤 hash 방법을 쓸지 미리 정의해놓는다.
- `http.formLogin()` 메서드를 사용하여 폼 기반 로그인을 설정한다.
- `formLogin.loginPage("/login")` 메서드로 로그인 URL을 지정한다.
- `spring security`에서는 기본적으로 로그인 실패시, 지정해둔 로그인 `URL + ?error`로 이동시킨다. 이를 이용하여 로그인 에러 발생시 view에 에러메시지를 출력시킬 수 있다.
```
로그인 실패시URL 예시
/login?error
```

```
@Configuration
@EnableWebSecurity
public class SecurityConfig {
    @Bean
    PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }
    @Bean
    //어떤 페이지를 검사할지 설정하는 메서드 입니다.(필터)
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        //JWT에서는 fetch header에 토큰을 담아서 보내면 꺼도된다.
        http.csrf((csrf) -> csrf.disable());//CSRF 공격 방지 기능 끄기, 웹브라우저에서 랜덤 문자 전송, 서버에서 검증하는 방법
        http.authorizeHttpRequests((authorize) ->
                authorize.requestMatchers("/**").permitAll()//특정 페이지 로그인 검사 여부 확인 permitAll()는 특정 URL 검사 없이 허용
        );
        http.formLogin((formLogin) ->//폼으로 로그인함을 정의
                        formLogin.loginPage("/login")//로그인 URL
                            .defaultSuccessUrl("/")//로그인 성공시 이동할 URL
//                        .failureUrl("/login")//로그인 실패시 이동할 URL, defautl는 loginURL 뒤에 ?error 추가
        );
        http.logout(logout -> logout.logoutUrl("/logout"));//로그아웃시 사용할 URL 정의
        return http.build();
    }
}
```
### 2. login form에서 서버로 데이터 전달 
- login용 form에서 서버로 유저가 입력한 username과 password를 전달한다
-  `<input>`태그 name은 `spring security` 규칙에 맞춰야 한다. (아래 예시 참고)
   -  로그인 id는 `username` 비밀번호는 `password`로 지정
- thymleaf 문법으로 로그인 실패시 실패 문구를 출력할 수 있다.
```
 <div th:if="${param.error}">//쿼리파라미터에 error가 있으면 해당태그 출력
    <span>아이디 혹은 비밀번호를 확인하세요.</span>
</div>

 <form action="/login" method="POST">
        <input type="text" name="username" id=""> //로그인 id는 필드명 username
        <input type="password" name="password">//비밀번호는 필드명 password
        <button type="submit" class="btn btn-outline-primary"> 전송</button>
     </form>
```
- 
### 3. 미리 정의된 방법대로 유저 정보 검사(UserDetailsService)
- `UserDetailsServiceImpl`는 spring secutiry에서 제공하는 유저 정보 구현용 인터페이스다.
- `UserDetailsServiceImpl` 의 메서드`loadUserByUsername`에 정의된 방법대로 DB에서 유저 정보를 조회(예외처리도 해야한다.)

- `loadUserByUsername` 단일 메서드를 정의하고 있으며, 반환은 `UserDetails` 객체로반환하며 유저의 이름, 비밀번호, 권한 을 담는다.
- 로그인 성공시 `session 쿠키`에 담아 클라이언트에게 전달된다.
```
@Service
public class UserDetailsServiceImpl implements UserDetailsService {
    private final MemberRepository memberRepository;//DTO class DI
    public UserDetailsServiceImpl(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }
    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
        Optional<Member> byMemberEmail = memberRepository.findByMemberEmail(username);//DB에서 찾은값 객체에 저장
        if (byMemberEmail.isEmpty()){
            throw new UsernameNotFoundException("유저 정보가 없습니다.");
        }
        Member loginMember = byMemberEmail.get();//반환된 객체가 Optional이므로 값을 꺼낸다.
        List<GrantedAuthority> authorities = new ArrayList<>();//권한 저장용 객체
        //메모용, 컨트롤러에서 조회했을때 확인용도로 사용 조건문으로 변경해서 쓴다.
        authorities.add(new SimpleGrantedAuthority("일반유저"));
        //User 객체는 username,password,권한 순으로 파라미터 전달한다.
        return new User(loginMember.getMemberEmail(), loginMember.getMemberPassword(), authorities);

    }
}  
```