# Interceptor
## 개요
- `Springframework`에서 request 요청을 가로채고 controller로 넘어가기 전후의 처리를 진행하는 기능을 `Interceptor`라 한다.
- `Servelt Filter`와 유사한 기능을 한다.

## 주요기능
- `controller`에 도달하기 전/후/View 랜더링후 작업을 수행한다. 
- 로그를 남겨 requestURL, requestID, 요청시간, 요청한 유저 등의 정보를 기록 할 수 있다.
- `controller`를 호출하기 전 로그인 유무, 권한 유무등을 확인하고 조건에 맞지않는 유저일 경우 request를 막을 수 있다.
- `modelandview` 를 로그에 남길경우 클라이언트가 어떤정보를 확인했는지 추적할 수 있다.



## HandlerInterceptor
- `Spring Framework`에서 MVC request를 가로채서 처리하는데 중점을 준 `Interceptor` interface, 3가지 주요 메서드로 이뤄어져 있다.
- 모든 메서드를 사용할 필요는 없다.(메서드에 default로 정의되어 있음)

1. `preHandle`
- `request`가 `controller`에 도달하기 전에 호출되는 메서드(전처리)
- 로그인 여부, 사용자 권한, 로깅 등의 역할을 수행한다.
2. `postHandle` 
- `controller` 에서 `request`를 처리한 후에 호출되는 메서드(후처리)
- `model`에 데이터를 추가하거나 로깅 또는 `view`를 선택하는 등의 역할을 수행한다.
3. `afterCompletion`
- `view` 에서 랜더링이 끝난 후 호출되는 메서드
- 주로 로깅 작업에 사용된다.

### 예시
- 모든 request에 대해서 로깅 하는 `interceptor`를 구현했다(preHandle만 구현).
- 클라이언트가 요청한 URL, request의 고유 ID(UUID로 할당), handler정보를 로깅한다.
- `X-Request-ID` 는 사용자정의 `Header`에 사용하는 name중 하나다.
- preHandle return값이 true일경우 request를 계속 진행하며 `controller`를 호출한다. false일경우 request를 중단한다.

```
@Slf4j
public class LogInterceptor implements HandlerInterceptor {

    //X-Request-ID 사용자 정의 HTTP 헤더
    private static final String REQUEST_ID_HEADER = "X-Request-ID";

    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        //requestURL 객체에 저장
        String requestURL = request.getRequestURL().toString();
        //request에 사용할 고유식별자 생성 및 객체에 추가
        //싱글톤이기 때문에 메서드밖에서 set하면 안됨
        String requestId = UUID.randomUUID().toString();
        request.setAttribute(REQUEST_ID_HEADER, requestId);
        if (handler instanceof HandlerMethod) {
            HandlerMethod handlerMethod = (HandlerMethod) handler;//호출할 컨트롤러 메서드의 모든 정보가 포함되어있음
            log.info("PreHandle - Request URL: {}, Request ID: {}, Handler: {}", requestURL, requestId, handler);
        }else{
            log.info("PreHandle - Request URL :{}, Request ID:{},Handler:{}", requestURL, requestId, handler);
        }
        log.info("Start Time: {}", LocalDateTime.now());
        return true;
    }
}
```