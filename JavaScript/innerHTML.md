# innerHTML
- JavaScript에서 HTML 요소의 내용을 문자열로 조작할때 사용되는 속성이다.
- 선택한 요소의 내용을 문자열로 바꿀때 유용하다.
## 예시
- div 박스 안에 `<p>` 태그 내용을 바꿔보자
- `"문자열"` 로 바꿔도 되지만, `Template Literals` 을 이용하는게 더 실용적이다.

```
//테스트를 진행할 div 박스
<div id="test">
<p>테스트 내용</p>
</div>

<script>
const test = document.querySelector("#test");//쿼리 셀렉터로 div 박스 객체에 저장
test.innerHTML=`<p>테스트입니다</p>`;//innerHTML 속성으로 test div 박스 안의 HTML을 바꿈


</script>
```
- test div는 다음과 같이 바뀌게 된다.
```
<div id="test">
<p>테스트입니다</p>
</div>
```

## 결론
- innerHTML과 template literals를 이용해서 쉽게 요소의 HTML 내용을 변경할 수 있다.
- 설문지나 비밀번호 변경과 같이 view에서 유저의 행동을 검증할때 오류메시지를 변경해서 보여주기 편하다.