# variables
## 개요
- 변수(variable)은 데이터를 저장하고 참조하기 위한 메모리 공간의 이름이다.
- 프로그래밍 언어에서는 값을 저장하는 공간이라고 이해하자.
- 변수에는 선언 할당 범위 3가지 특징이 있다.
- javascript에서는 ES6에 추가된 변수까지 var let const 3개의 변수 type이 있다.

## var
- ES6 이전에 유일하게 javascript에서 사용되던 변수 type이다

- 재선언, 재할당이 가능하다.
- 범위는 function 안에서만 존재 할 수 있다.


```
var name = 'John'
var name = 'Min' //재선언 가능

name = 'Tom' // 재할당 가능

```



## let
- ES6에서 추가된 변수 타입이다.
- 재선언이 불가능하며 재할당은 가능하다.
- 범위는 {} 안이다.

```
var name = 'John'
var name = 'Min' //재선언 불가능 에러 발생

name = 'Tom' // 재할당 가능


```

## const
- ES6에서 추가된 변수 타입이다.
- 재선언 재할당이 모두 불가능하다.
- 범위는 {} 안이다.

```
var name = 'John'
var name = 'Min' //재선언 불가능 에러 발생

name = 'Tom' // 재할당 불가능 에러 발생

```

- 단 **Object** 안의 값은 재할당이 가능하다. object의 값의 재할당을 막으려면 `Object.freeze(object)` 을 사용하자


```
const object1 = { name : 'John' }
object1.name = 'Park'; //const로 선언되었어도 안의 값은 재할당 가능

Object.freeze(object1)

```



## 전역변수
전역변수를 선언할때 `<script>`태그 안에 변수를 선언하면 된다.

크게 두가지 방법이 있는데


```

<script>
//var로 전역변수 만들기
 var name = "Kim"

//window로 전역변수 만들기(권장되는 방법)
  window.age = 20;  //전역변수만들기
  console.log(window.age);  //전역변수사용하기
  window.age = 30;  //전역변수변경하기
</script>

```