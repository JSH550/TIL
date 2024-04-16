# spilt() 로 문자열 나누기
- JavaScript에서 지정된 기준으로 문자열을 나누는 함수 spilt()에 대해 알아본다.
- spilt("") 으로 문자열을 배열로 분리한다.
- slice() 를 이용하여 분리된 배열의 특정 인덱스값만 반환할 수 있다.
## 예시
```
    let test = "Hello world!";
    let spiltTest = test.split(" ");
    console.log(spiltTest);// 출력결과 ['Hello', 'world!']

    let test2 =  "apple,banana,mango,pineapple,blueberry,cherry";
    let spiltTest2 = test2.split(",");
    console.log(spiltTest2);//출력결과 ['apple', 'banana', 'mango']


    let spiltTest3 = test2.split(",").slice(3);//인덱스 3번부터 배열을 재정의

    console.log(spiltTest3);//출력결과 ['pineapple', 'blueberry', 'cherry'] 인덱스 4 5 6번 출력

    let spiltTest4 = test2.split(",").slice(0,3); //인덱스 0번부터 배열 시작, 인덱스 3번을 만나면 저장하지 않고 멈춤

    console.log(spiltTest4); ['apple', 'banana', 'mango']//출력결과 ['apple', 'banana', 'mango'] 인덱스 0 1 2번 출력

```