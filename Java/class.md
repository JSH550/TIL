# class
## 개요
- Java의 class에 대해 알아본다.
## 특징
- 관련있는 변수, 함수들을 class안에 정리할 수 있다.
- 중요한 변수, 함수의 원본들을 지킬 수 있다.
- class 안의 `변수는 field 또는 attribute`, `함수는 method` 라고 부른다.


## new 키워드
- 미리 정의된 class를 호출하여 컴퓨터 메모리의 특정한 공간에 할당할 때 사용하는 키워드다.
- 메모리에 할당하는 과정을 `instance`화 라고 하며, `instance화 된 class` 를 `object` 라고 부른다.
- 즉, 코드로만 존재하는 class는 class라 부르고, 메모리에 할당된 class는 object다.
- 
## 생성자(constructor)
- class로부터 instance화 할때 호출되는 메서드를 생성자(constructor)라 부른다.
- 생성자는 class 내에 class와 동일한 이름으로 메서드를 정의하여 만든다.
- 메서드 형태, 즉 함수이지만 `return값은 없다`.
- 생성자는 여러개를 만들 수 있다.(`overloading` 가능)
- 즉, 생성자는 메모리에 class를 올릴때 class를 초기화 하는 역할을 한다.

## this
- Java에서 사용되는 키워드로 현재의 객체를 가르킨다.
- 클래서 내의 메서드 내에서 해당 객체를 참조할 때 사용한다.
- 생성자가 class를 초기할때, class 안의 변수들을 초기화 할때 사용한다.

## 예시
```
public class Main {
    public static void main(String[] args) {
        /*
        * new Member로 class를 instance 화 합니다.(메모리에 할당)
        * instance 화 된 class(objecct) Member 형태의 member 객체에 저장합니다.
        * parameter "홍길동",20 을 넘깁니다.
        */
        Member member = new Member("홍길동",20);

        // 객체의 메서드 호출
        member.display(); //
    }
}


class Member(){
    String name;
    int age;

    //constructor(생성자) 정의, 파라미터로 name과 age를 받는다. 
    public Member(String name, int age){
        this.name = name;//this.name은 객체의 num  변수, name은 파라미터로 받은 값
        this.age = age;
    }
}

```