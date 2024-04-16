# JavaScript Redirect

## 개요
- JavaScript에서 page redirect 하는 방법들을 알아보자
  

## 이전 페이지로 리다이렉트
- window.history.back() 현재 URL 방문 전 URL로 리다이렉트 한다.


## 특정 URL로 리다이렉트
- window.location.href ="URL" : ""안의 URL로 리다이렉트 한다.

## window.location
- 현재 페이지의 URL에 관련된 정보를 조회하는 객체
- 제품클릭, 검색어 입력등 이벤트를 통해 리다이렉트 하는경우에 유용하다. 

### 사용법
#### - 현재 URL `https://www.example.com/item?query=string`


1. `window.loaction.href` : 현재 URL 전체를 반환한다.
    - 반환 값 : `"https://www.example.com/item?query=string"`
2. `window.location.origin` : 현재 URL의 프로토콜, 호스트이름 및 포트번호를 반환한다.
    - 반환값 : `"https://www.example.com"`
3. `window.location.pathname` : URL 호스트이름 뒤의 경로를 반환한다.
    - 반환값 : `"/item"`
4. `window.location.search` : URL의 쿼리파라미터 부분을 반환한다.
    - 반환값 : `"?query=string"`


## URL 특정값 저장하기
- URL에 특정 데이터가 포함되어있을경우 따로 저장해야 하는 경우가 생긴다.

### 1. 쿼리 파라미터 추출

- `URL` 객체의 `searchParams` 객체속성 으로 이를 해결할 수 있다.

```

let nowUrl = new URL(window.location.href);//현재 URL을 URL 객체로 저정합니다.

let urlParams = nowUrl.searchParams //URL 객체에서 쿼리파라미터 부분을  key, value로 저장합니다.

let name = urlParams.get('name') //key값이 'name'인 파라미터의 value 값을 저장합니다.

```


### 2. 정규식으로 데이터 추출
- URL에 데이터가 포함되어있을경우 정규식으로 추출할 수있다.

```
// 접속한 URL : 
https://www.example.com/places/1234

let nowUrl = new URL(window.location.href);//현재 URL을 URL 객체로 저정합니다.

// URL에서 숫자 부분 추출

const placeId = currentURL.match(/\/places\/(\d+)/)[1];// "places/" 다음에 오는 숫자 부분을 추출합니다.


```



