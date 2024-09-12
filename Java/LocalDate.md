# LocalDate

## 개요
- Java 8에 추가된 클래스
- 날짜 정보를 포함하며 시간정보는 포함하지 않는다.

# 주요 기능

## 1. 날짜 생성
- `now()` 메서드로 현재 로컬 연/월/일 을 객체로 생성할 수 있다.
- `of()` 메서드로 특정 날짜를 생성 할 수 있다(연/월/일 순)

```
//오늘 날짜 생성
LocalDate today = LocalDate.now();

//생일 날짜 생성
LocalDate birthDay = LocalDate.of(1900, 5, 15);

```

## 2. 날짜 조절
- `plus` 또는`minus` 로 시작하는 메서드로 날짜를 조절할 수 있다.

```
//하루전 날짜
LocalDate yesterDay= today.minusDays(1);
//1년전 오늘날짜
LocalDate lastYear = today.minusYears(1);
//하루뒤 날짜
LocalDate tomorrow =today.plusDays(1);
```



## 3. 연/월/주차 정보 파싱
- `get` 으로시작하는 메서드로 `LocalDate` 객체의 연/월/주차정보 등을 파싱할 수 있다.
```
//오늘 날짜
LocalDate today = LocalDate.now();

//연도 
int year = today.getYear();

//월
int monthValue = today.getMonthValue();

//주차 정보(1~52)
int weekOfYear = today.get(IsoFields.WEEK_OF_WEEK_BASED_YEAR); // 주차 계산
```