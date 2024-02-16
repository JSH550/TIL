# Input 태그

### input tag 란?
HTML `<input>` 태그는 클라이언트로부터 데이터를 입력받을 수 있는 요소다.

주로 `<form>` 태그 같이 클라이언트가 서버로 데이터를 전송할때 데이터를 담을 공간을 마련해준다.

`required` 속성을 추가하면 form에서 해당 `<input>` 태그를 비워둔상태로 `submit` 하게되면 메시지를 표시하여, 필드가 `null` 상태로 전송되는걸 막을 수 있다. 

### input tag의 type
input tag에는 여러가지 type을 지정할 수 있으며, 필드에 입력되는 `type` 을 제한하여 클라이언트 단에서 잘못된 request를 사전에 막을 수 있다.

* text 문자열 데이터
* number 숫자 데이터
* email email형식 데이터(@이 들어가야함)
* password 입력되는 데이터가 가려짐
* submit 제출 버튼이 생성된다.
* file 파일 업로드 버튼이 생성된다.multiple="multiple"을 추가하면 여러개의 파일 전송이 가능하다.

### 예시

```
<input type="email" required name="email">
```