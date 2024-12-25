# TypeCasting

## 서론
- Java에서 타입 캐스팅은 데이터 타입을 변환하는 과정으로, 데이터의 크기와 형식에 따라 명시적 또는 암시적 방식으로 이루어집니다.
- 이 문서에서는 Java에서 사용되는 주요 타입 캐스팅 방법을 정리합니다.




## 1. Explicit Casting(명시적 타입캐스팅)
- 주로 Downcasting 에서 사용되는방법
- `(type)` 형태로 명시적으로 타입캐스팅
```
long longValue = 1000L;
int intValue = (int) longValue;//int 로 타입캐스팅
```

## 2. String -> 숫자
- 문자열에서 숫자타입으로 타입캐스팅할때는 `Wrapper Class` 의 `parse` 메서드 사용

```
String num = "123";

int intNum = Integer.parseInt(num);      // String → int
double doubleNum = Double.parseDouble(num); // String → double
long longNum = Long.parseLong(num);      // String → long
float floatNum = Float.parseFloat(num);  // String → float
```

## 3. 숫자 -> String
- `String.valueof()` 또는 Wrapper class의 `toString()` 사용
```
int intNum = 123;

String strNum1 = String.valueOf(intNum);  // int → String
String strNum2 = Integer.toString(intNum); // int → String

```

