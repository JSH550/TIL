# access modifiers
- 접근제어자(access modifiers)는 클래스의 멤버에 대한 접근 권한을 제어하는데 사용되는 제어자이다.
- 클래스 멤버에는 변수, 메서드, 필드, 생성자 등이 있다.
## public
- 다른 class에서도 접근할 수 있게 하는 접근 제어자.
## default(package-private)
- 접근 제어자를 지정하지 않으면 package-private 상태가 된다.
- `같은 package 내`의 class에서만 참조가 가능하다.

## private
- 동일한 class 내에서만 접근이 가능하다.
- 접근하려면 `getter` `setter ` `메서드`를 통해 접근한다.

## protected
- `같은 package 내`의 class에서만 참조가 가능하다.
- 상속 관계의 하위 클래스에서도 참조가 가능하다.