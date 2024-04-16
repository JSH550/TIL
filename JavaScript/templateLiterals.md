# Template Literals
## 개요
- ES6에서 추가된 문법으로 좀더 진보된? 방법으로 문자열을 형성하는 방법이다.

## 특징
- backtick (`) 로 둘러쌓인 문자열을 형성하면 된다. 
- ${...} 구문을 이용하면 문자열 안에 변수를 직접 사용할 수 있다.(기존에는 +로 연결했어야한다.. 매우불편했음)
- 여러줄로 이루어진 문자열도 출력할 수 있다. 이를 이용해서 HTML 탬플릿 변수도 만들 수 있다.

### 예시


```
...JS

const name = "John";
const age = "20";

const message1 = `안녕하세요, 저는 ${name}이고 ${age}살 입니다.`

console.log(message1);//출력결과: 안녕하세요, 저는 John이고 20살 입니다.


//여러줄로 이루어진 문자열도 출력가능하다.
const message2 = `안녕하세요
${name}입니다.
${age}살 입니다.`;

console.log(message2);//출력결과 :안녕하세요
John입니다.
20살 입니다.

//HTML 템플릿 작성도 가능하다.

var message3 = `
<div>
  <div>
    ${변수명}
  </div>
</div>`;

```


## Tagged literals
- `Template Literals`와 함께 추가된 기능으로 `Template Literals`의 문자열과 변수들을 파싱하는 함수다.
- 문자열과 변수를 분리하여 문자열은 array 타입으로 저장한다.
- 함수를 실행할때 ()가 아니라 template literals를 넣으면 `Tagged literals`로 동작한다.
- `Tagged literals`의 첫번째 parameter는 문자열들을 array 타입으로 저장하는 parameter이며 두번째 parameter부턴 `Template Literals`안의 변수${}를 저장하는 parameter다



### 예시
```
//첫번째 parameter는 문자열들을 쪼개서 array로 저장하는 parameter
//두번째 세번째 parameter는 변수 ${}를 저장하는 parameter
function tagTest1(strings,var1, var2){
    console.log(strings)
    console.log(var1)
    console.log(var2)
}

tagTest1 `안녕하세요, 저는 ${name}이고 ${age}살 입니다.`//출력결과
['안녕하세요, 저는 ', '이고 ', '살 입니다.']
John
20
```