# Exception 처리

## 개요

예외처리는 정말 중요하다. 코드를 짜더라도 예상치못한 상황이 종종 벌어지기 때문이다.

spring framework에서는 예외처리와 관련된 다양한 기능들을 제공한다. 이러한 기능들을 통해 예외처리를 쉽게 할 수 있다.



## `@ResponseStatus(HTTP code)`
- spring framework에서 특정 메서드의 예외발생시 HTTP 상태코드를 지정하는데 사용되는 annotation

- 단독으로 쓰이기도 하지만 아래 `@ExceptionHandler()` 와 같이쓰는 방법도 있다.

### 예시

아래 메서드에서 RuntimeException 발생시 HTTP 상태코드는 NOT_FOUND(404)로 지정된다.

```

@ResponseStatus(HttpStatus.NOT_FOUND)
public class ResourceNotFoundException extends RuntimeException {
    // 예외 내용 생략
}
```


## `@ExceptionHandler(특정exception.class)`
- spring framework에서 controller의 특정 예외 발생시 예외처리하는 방법을 정의할때 사용하는 annotation
- API 예외처리에 주로 사용되며 HTML 화면오류는 BasicErrorController를 사용하자
- 작동방식
- 컨트롤러에서 예외 발생시 ExceptionResolver를 통해 예외처리 해결을 하려 한다.
- 이때 컨트롤러에 해당 예외에 해당하는 `@ExceptionHandler()` 가 있으면 정의된 방법으로 예외를 처리한다. (기존 예외처리처럼 서블릿컨테이너, 인터셉터..등 복잡한 경로를 거치지않음)
- `@ExceptionHandler()` 호출되면 정상 흐름으로 처리가 되어 status가 200이 되어버리므로 `@ResponseStatus()` 으로 status code를 바꿔주자
- 예외처리시 부모클래스 예외처리 방법을 정의하면 자식클래스도 동일한 방법으로 처리된다.
- 예를들면 `RuntimeException`은 `IllegalArgumentException`을 자식class로 두기 때문에 `RuntimeException`에 대한 예외처리를 정의하면 `IllegalArgumentException` 도 동일한 방법으로 예외처리된다. 단 `IllegalArgumentException` 가 따로 예외처리 되어있으면 해당 방법으로 처리된다. 


#### 예시


```
@Controller
public class SimpleController {

	// ...

	@ExceptionHandler(RemoteException.class)
	public ResponseEntity<String> handle(RemoteException ex) {
		// ...예외처리 코드
	}

    //여러 exception을 동일한 방법으로 처리할 수 있다.
    @ExceptionHandler({FileSystemException.class, RemoteException.class})
    public ResponseEntity<String> handle(Exception ex) {
	    // ...예외처리 코드
}

}

```
ref. spring 공식 문서
https://docs.spring.io/spring-framework/reference/web/webmvc/mvc-controller/ann-exceptionhandler.html#mvc-ann-exceptionhandler-args










## `@ControllerAdvice` 
- `@ExceptionHandler()` 을 이용한 예외처리는 선언된 controller 내에서만 작동한다.
- 전역에서 예외처리를 수행하기 위해선 `@ControllerAdvice`를 추가한 class를 따로만들어야 한다.
- 여러 컨트롤러에서 발생하는 예외처리에 대한 응답 및 수정, 객체에 데이터 삽입, 뷰의 선택 등을 지정한다.
-  `@ControllerAdvice`가 선언된 class 내의 `@ExceptionHandler()` 을통해 전역 예외처리를 실행한다.
- 적용 Target을 지정할 수도 있다.

```
// Target all Controllers annotated with @RestController
@ControllerAdvice(annotations = RestController.class)
public class ExampleAdvice1 {}
// Target all Controllers within specific packages
@ControllerAdvice("org.example.controllers")
public class ExampleAdvice2 {}
// Target all Controllers assignable to specific classes
@ControllerAdvice(assignableTypes = {ControllerInterface.class,AbstractController.class})
public class ExampleAdvice3 {}
```

ref. spring 공식문서

https://docs.spring.io/spring-framework/reference/web/webmvc/mvc-controller/ann-advice.html