# DateTimeFormatter 
## 개요
- Java에서 날짜와 시간을 문자열로 변경하는 방법을 알아보자
## 사용법


```
LocalDateTime localDateTime = LocalDateTime.now();


DateTimeFormatter dateTimeFormatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm");

//변수에 저장된 시간을 미리 지정한 문자열로 포맷팅 합니다.
String formattedDateTime = localDateTime.format(formatter);

//저장된값을 출력합니다.
System.out.println(formattedDateTime);
//출력 결과 :2024-03-26 15:12

```

## 패턴 문자
- 포맷 패턴을 지정할때 사용하는 패턴 문자들은 다음과 같다.
```
yyyy 연도
MM 월
dd 일
HH 시간(0~24시)
hh 시간(1~12시)
mm 분
ss 초

```