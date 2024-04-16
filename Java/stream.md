# Stream


## 메서드 참조(Method Reference)
- 람다 표현식을 대신해서 메서드의 참조를 전달하는 방법
- `::`로 참조를 전달한다.
- 메서드 참조를 사용할때는, 해당 메서드가 어떤 파라미터를 갖는지 알고 있어야 한다.
- 참조로 전달되는 메서드는 `()`를 입력하지 않는다.
  
1. 메서드 참조
- `class명` `::` `메서드명` 으로 호출한다.
- 정적메서드, 인스턴스메서드 모두 호출 가능하다. 
```
public void test(){
    List<PlaceDto> foundPlaceList = placeService.findPlaceByCategory("요양");

        foundPlaceList.stream()
            .map(PlaceDto::getPlaceName)//PlaceDto class의 getPlaceName 메서드를 참조한다.
            .forEach(System.out::println);

    }
```


1. 생성자 참조
- `className` `::` `new` 형태로 기본 생성자를 참조할 수 있다.
```
ClassName::new;
```


