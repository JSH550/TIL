# extends
## 개요
- Java에서 클래스 상속 관계를 정의할때 사용하는 키워드다

## 사용법
- 자식 class에 `extends 부모class` 로 상속관계를 정의한다.
- 자식 class는 부모 class의 모든 필드와 메서드를 상속받는다.
- 자식 class의 생성자에서 `super` 키워드를 사용해 부모 class의 생성자를 호출할 수 있다.

```
/**
 * spring security 의 User class를 상속받는 class입니다.
 * 기존 User class에서 파라미터로 받는 username(로그인 아이디), password, 권한에 닉네임(memberName)을 추가했습니다.
 */
    class CustomUser extends User{
        public String memberName;
        public CustomUser(String username,
                          String password,
                          Collection<? extends GrantedAuthority> authorities){
            super(username, password, authorities);//부모 class의 consturctor
        }
    }

```