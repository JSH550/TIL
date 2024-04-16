# fetch
## 개요
- 클라이언트측에서 서버에서 데이터를 받아오기 위해 fetch 함수를 사용할 수 있다.
- fetch함수는 Promise를 반환하며 HTTP 요청을 비동기 방식으로 서버 API와 통신한다.
- 
```
fetch의 기본적인 구조
options 미입력시 GET 메서드로 통신

fetch(url, options)
  .then(response => response.json())//서버에서 보낸 응답에 대한 처리
  .then(result => /* 결과 처리 */)//응답과 함께 보내진 데이터의 처리
  .catch(error =>{})//에러 발생시 처리 방법

```

#### 예시
```
fetch(url),{ 
  method: "PATCH", /HTTP method 설정
  headers: {
  'Content-Type': 'application/json'
   }
   ,
  body: JSON.stringify(postData)//JSON 형태로 data 전송
}
.then(response => {
  if (!response.ok) {//서버 응답에 대한 처리
    return  response.text().then(errorMessage => { // response.text()를 호출하여 Promise를 반환하고, 그 결과를 다시 처리합니다.
    console.log("서버에러: " + errorMessage);
    throw new Error(errorMessage); // 에러를 던져서 catch 블록으로 이동시킵니다.
   });}
  else {
  //해당 요청 대해 서버에선 문자열 형태로 파싱, 다음 then으로 넘깁니다.
  return response.text()
  }
   })
//요청 성공시 데이터 처리
.then(data => {
  console.log("서버 응답 데이터 = " + data);
  if (data == "ok") {
             alert("비밀번호 변경 완료")
    redirectPage("mypage")//비밀번호 변경 성공시 mypage로 되돌아갑니다.
       }
    else {
           throw new Error(data)
       }
       })
//에러 발생시 핸들링
.catch(error => {
 console.log("에러발생")
  alert("에러발생:" +error.message)
   })

```

```
//POST 요청이 필요할시 option을 추가하여 통신한다.
fetch(url,{
    method: 'POST',
    body: JSON.stringify({
key1: 'value1',
key2: 'value2'

    })
})
...codes


```