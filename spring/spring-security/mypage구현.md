# mypage 구현
## 개요
- spring secutiry 기능으로 mypage를 구현한다.

## Thymeleaf 문법
- `sec:authorize = "isAuthenticated()"`  Spring Security의 Thymeleaf 지시어로, session이 있을때 해당 DOM을 표기한다.
- `sec:authorize = "anonymous`
  - session에 로그인 정보가 없을때 해당 DOM을 표시한다.
 - `sec:authentication="principal.username"`
   - 현재 로그인 세션에서 유저이름을 가져와 태그안에 넣는다.


```
    <!-- spring security thmleaf 문법입니다. 로그인한 상태에서 출력됩니다. -->
    <div sec:authorize = "isAuthenticated()">
        <span>환영합니다!</span>
        <div sec:authentication="principal.username"></div>
    </div>
    <!-- spring security thmleaf 문법입니다. 로그인 하지 않은 상태에서 출력됩니다. -->
    <div sec:authorize = "anonymous">
        <span>로그인 해주세요!</span>
    </div>

```