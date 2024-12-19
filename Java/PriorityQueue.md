# PriorityQueue(우선순위 큐)

## 개요
- 우선순위큐는 요소의 **우선순위**가 높은 요소가 큐의 맨앞에 위치하는 자료구조
- 기본적으로 **오름차순** 정렬
- 내부적으론 **Heap** 자료구조
- `Comparator` 로 우선순위를 지정할 수 있음음

## 주요 메서드

### add(E e)
- 요소를 추가하는 메서드
```
pq.add(10);
pq.add("abc");
```
### offer(E e)
- 요소를 추가하는 메서드, 실패시 `false` 반환

### peek()
- 우선순위가 가장 높은 요소 조회
- 요소가 **제거되지 않음**

```
int a = pq.peek();//요소 제거되지 않음
```

### poll()
- 우선순위가 가장 높은 요소 조회
- 요소가 **제거됨**
```
int a = pq.poll();//요소제거됨
```

### isEmpty()
- 큐가 비어있는지 여부를 확인후 결과반환

### size()
- 큐의 크기를 반환
```
int a = pq.size();
```







## 사용예시

### 오름차순 큐 생성 및 활용

```
import java.util.PriorityQueue;

public class Main {
    public static void main(String[] args) {
        // 우선순위 큐 생성
        PriorityQueue<Integer> pq = new PriorityQueue<>();

        // 요소 추가
        pq.add(10);
        pq.add(5);
        pq.add(20);

        // 출력 (정렬된 순서는 아님)
        System.out.println("Peek: " + pq.peek()); // 5 (최소값)

        // 요소 제거
        while (!pq.isEmpty()) {
            System.out.println(pq.poll()); // 5, 10, 20 순서로 출력
        }
    }
}



```

### 내림차순 큐 생성

```
PriorityQueue<Integer> pq = new PriorityQueue<>(Collections.reverseOrder());

```

### Comparator 로 정렬

```
PriorityQueue<Task> taskQueue = new PriorityQueue<>(Comparator.comparingInt(t -> t.priority));

```