# BeanValidation

### 개요

유효성 검사를 하기 위한 JAVA 표준 기술이다. 편의상 spring에 작성했다.

annotation으로 보다 편하게 유효성 검사를 진행 할수 있다.

entity 보단 DTO 계층에 사용해서 사전에 유효성 검사를 진행하는것이 좋다.
(동일 entity라도 DTO가 여러개이니.. 알맞게 사용하도록 하자.. 남발x)

Spring boot에서 사용시 build.gradle에 아래 implemetation을 추가하자

```
implementation 'org.springframework boot:spring-boot-starter-validation'
```


대표적인 annotation은 다음과 같다.

`@NotNull` Null을 체크한다. empty(""), 공백("    ") 은 검출하지 못한다.

`@NotEmpty` Null과 empty("") 을 체크한다.

`@NotBlank` Null과 empty(""), 공백("    ") 을 체크한다

`@Max(number), @Min(number)` 숫자필드의 max min 값을 설정한다.

`@Range(min=number, max=number)` 숫자필드의 range를 설정한다.

`@Size(min=number, max=number)` 문자필드의 크기를 제한한다.

`@Email` string 형식이 email 형식인지 체크한다.

`@AssertTrue, @AssertFalse` boolean 필드가 true 혹은 false인지 체크한다.


### Controller에서 사용법

Controller의 parameter 유효성 검사를 위해선 spring framework에서 제공하는 annotation `@Validated`를 사용하면 된다.

이때 `BindingResult` class 객체를 이용하면 손쉽게 error메시지를 객체에 담을 수 있다.

#### 예시

예시에는 클라이언트에서 Post요청이 왔을때 DTO 유효성 검사를 진행하고, error발생시 다시 form으로 돌아가도록 설계했다.

```
@PostMapping("/new")
public String addNewProduct(@Validated @ModelAttribute("productSaveDto") ProductSaveDto productSaveDto,BindingResult bindingResult){
    //유효성 검사에서 error 발생시 bindingResult에 error가 담긴다.
 if(bindingResult.hasErrors()){
  log.info("errors={}", bindingResult);
            return "/product/product-addform";
        }
    ...codes
}
```


```
@RequiredArgsConstructor
@Getter
@Setter
//저장용 DTO
public class ProductSaveDto {

    @NotBlank(message = "제조사를 입력해주세요.")
    private String productManufacturer;
    @NotBlank(message = "제품명을 입력해주세요.")
    private String productName;
    @Range(min=0, max=100000,message = "가격은 1에서 100,000 사이여야 합니다.")
    private int productPrice;
    }
```

error 발생시 서버에 error log가 남게 된다.
productPrice가 2000000이라 유효성 검사에서 Field 에러가 발생했을경우 log를 살펴보자.
어떤 유효성 검사에서 error가 났는지와 default message가 출력된다. 이를 model에담아 view로 전송하면 클라이언트가 어떤부분이 잘못되었는지 더 정확히 파악할 수 있다.

```
Field error in object 'productSaveDto' on field 'productPrice': rejected value [2000000]; codes [Range.productSaveDto.productPrice,Range.productPrice,Range.int,Range]; arguments [org.springframework.context.support.DefaultMessageSourceResolvable: codes [productSaveDto.productPrice,productPrice]; arguments []; default message [productPrice],100000,0]; default message [가격은 1에서 100,000 사이여야 합니다.]
```

또한 thymeleaf 기능을 이용해서, error 정보가 있을때 특별한 동작을 수행할 수 있다.

예를들어 `th:errorclass=""` 는 error 정보가 있으면 특정 class를 추가해준다. 

아래 예시에서 에러가 있을시 class에 form-field-error가 추가되어 border가 붉은색으로 변하게 된다. 이렇게 하면 클라이언트가 시각적으로 오류를 캐치할 수 있다.



```
.form-field-error{
border-color: red  !important;
}
```

```
<input type="number" class="form-control" required th:field="*{productPrice}"placeholder="상품가격을 입력하세요" th:value="${productPrice}" th:errorclass="form-field-error">
```

![Alt text](../img/redbox.png)