# setTimeout
- JavaScript에서 일정한 시간을 설정하여, 해당 시간이 지난 뒤에 함수가 실행되도록 예약하는 함수
- 첫번째 파라미터로 `콜백함수` 를 받으며 두번째 파라미터로 `ms 단위 시간`을 받는다.
- 시간이 지난 후에 콜백함수가 실행된다.

### 예시
```

setTimeout(function() {
  console.log("Hello, world!");
}, 3000); // 3초 후에 실행됩니다.



```