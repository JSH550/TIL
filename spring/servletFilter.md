# Servlet Filter

## 개요
- 로그인 인증같이 공통 관심사(cross-cuttin concern) 처리할때 사용한다.
- HTTP 요청 ->WAS(ex:tomcat) -> servlet filter(request가 적절하지 않으면 sevlet 호출 막음) -> => servlet(Dispatcher Servlet ) -> 컨트롤러
- node.js의 middleware와 비슷한 기능이라 이해하자.