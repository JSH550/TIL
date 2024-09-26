# Functionl Interface

## 개요
- Java에서 사용되는 하나의 추상 메서드만을 갖고있는 인터페이스
- 람다식, 메서드 참조와 함께 사용하여 코드를 간결하게 만들 수 있다.

## `1. Consumer<T>`
- 파라미터를 하나만 받아서 처리하지만 반환값이 없는 함수형 인터페이스
- 파라미터를 받은 객체를 유연하게 처리할 수 있다.
- `accept(T t)` 추상 메서드를 가지며, 전달받은 값을 처리할때 호출하여 사용

### 예시
- updateIfPresent 메서드는 두 개의 파라미터를 받는다
  - `Consumer<T> updateFunction`: 업데이트할 작업(메서드)을 전달하는 파라미터.
  - `T value`: 실제로 업데이트될 값, null 체크에 사용됨
  
- updateIfPresent 메서드는 value가 null이 아닌 경우에만 updateFunction.accept(value)를 호출하여 값을 업데이트

- 이렇게 하면 null 체크를 간단하게 처리하고, null이 아닌 함수를 호출해 유연하게 작업을 진행할 수 있다.

```

public Boolean updateNovel(NovelUpdateDto novelUpdateDto){

...나머지 코드생략

//updateIfPresent 호출, DTO의 getTitle 값이 null 이 아닐경우, updateTitle 메서드가 실행됨
updateIfPresent(novel::updateTitle, novelUpdateDto.getTitle());
    
    }

//업데이트 메서드 정의
 private <T> void updateIfPresent(Consumer<T> updateFunction, T value){

//value가 null 이 아니면 Cunsumer로 전달된 메서드를 실행시킴
    if (!(value ==null)) {
            updateFunction.accept(value);
     }

 }
```


## `2. Supplier<T>`
- 파라미터는 받지 않고 값을 반환하는 함수형 인터페이스