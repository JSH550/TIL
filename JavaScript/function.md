# function()
## 개요
함수는 다음과 같은 기능을 한다.

```
1.어떠한 기능을 수행하는 코드의 묶음 기능 구현(재사용 용이)
2.입출력 기계의 기능 구현
```

javascript에서 함수는 function 키워드로 정의된다.

### 예시

```
//정의 방법 1
function 함수명(parameter){
    ...code
}

//정의방법 1 예시
function test2(a,b){
return a+b;
}

//정의 방법 2 함수명을 먼저 선언
var test3 = function(a,b){
return a*b;

}


```

parameter는 여러개를 받을 수 있다.

반환값이 있을경우 return을 통해 반환할 수 있다.

## 호출
함수명을 이용해서 호출할 수 있다.

위에 test2함수를 호출해보자

### 예시

```
test2(3,4)//출력 7

var result = test2(3,4)//result객체에 7이 저장됨
```

## Arrow Function
ES6에 도입된 arrowfunction은 함수를 간단한 방법으로 표현할 수 있다.

### 예시
```
//정의 방법
(parameters) => {codes}

(x,y) =>{
return x+y
};

//function과 마찬가지로 함수명을 먼저 선언할 수 있다.

//제곱을 계산해주는 함수 정의
var squre = (x) =>{
    return x*x
};

//parameter가 하나면 괄호 생략 가능
var squre = x =>{return x*x};

```

### 주의사항

- funcntion에서의 this와 arrow function에서의 this는 다르다.

- function에서 this는 해당 함수를 가진 오브젝트를 뜻하며

- arrow function에서 this는 함수가 정의된 시점의 외부에있는 this를 사용한다.


### 예시

```

var testObject1 = {
 fun1: = function(){ console.log(this) }
}

testObject1.fun1()//출력값 testObject1


var testObject2 = {
  fun2 : () => { console.log(this) }
}

testObject2.fun2()//출력값 window

```