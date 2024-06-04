# Allocation of Physical Memory(메모리할당)
- 메모리는 두 영역으로 나뉘어 사용
  - OS 상주 영역 : interrput vecotr와 함께 낮은 주소 영역 사용
  - 사용자 프로세스 영역 : 높은 주소 영역 사용
# Contiguous allocation(연속 할당)
- 각각의 프로세스가 메모리의 연속적인 공간에 적재되도록 하는 것
- 고정 분할 방식과 가변 분할 방식이 있다.
## 고정 분할 방식 (Fixed partition)
- 물리적 메모리를 몇개의 분할(partition)으로 나눔
- 분할당 하나의 프로세스 적재
- 동시에 메모리에 load되는 프로세스 수가 고정된다.
- internal fargmentation, external fragmentation 발생

## 가변 분할 방식(Variable partition)
- 프로세스 크기를 고려해서 메모리 영역을 할당한다
- 분할의 크기, 개수가 동적으로 변화한다
- 기술적 관리 필요
- external fragmentation 발생

### 외부 단편화(External fragmentation)
![alt text](이미지/ExternalFragmentation.png)

- 기존 프로스세스가 메모리에서 제거되면서 생긴 `빈공간`이, 다른 프로세스가 들어가기엔 작을때 외부 단편화 라고 부른다.
### 내부 단편화(Internal fragmentation)
![alt text](이미지/InternalFragmentation.md.png)

- 프로세스에 할당된 메모리 블록이, 요청된 메모리보다 크게 할당되어 프로세스 내부에 남아있는 조각
- 즉 프로세스 내부의 사용되지 않는 공간을 의미한다


## Dynamic Storage-Allocation(동적 메모리 배치 기법)
- 가변 분할 방식에서 size n 인 요청을 만족하는 가장 적절한 hole(가용 메모리 공간)을 찾는 문제
#### 1. First fit(최초 적합)
- size가 n 이상인 것중 최초로 찾아지는 hole에 할당
#### 2. Best fit(최적 적합)
- size가 n 이상인 가장 작은 hole을 찾아 할당
- hole 리스트를 탐색해야 한다.
- 아주 수많은 hole 들이 생성됨
#### 3. Worst fit(최악 적합)
- 가장 큰 hole에 할당
- 비효율적인 방법

# Noncontiguous allocation
- 하나의 프로세스가 메모리의 여러 영역에 분산되어 올라갈 수 있다.
- 가상 메모리 사용
- 최근에 사용되는 방법
- address binding이 복잡하다.
## Paging 기법
![alt text](이미지/paging.png)
- 논리적 메모리(logical memory)를 `일정한 크기의 page`로 잘라서 물리적 메모리(physical memory)에 적재하는 방식
- 논리적 메모리가 어느 위치의 물리적 메모리에 적재되어 있는지 `page table`에 기록해야 한다.

![alt text](이미지/paging2.png)
- `page table` 에는 페이지 만큼 엔트리가 존재한다.(index 형식)
- 페이지별로 주소변환(address binding)이 필요하다

### Implementation of Page Table

![](이미지/paging3.png)
- page table은 `main memory`에 상주하며 `프로세스마다 각각` 존재한다.
- 모든 메모리 접근 연산에는 최소 두번의 memory access 필요(page table 접근 1회, 메모리의 물리적 주소로 data 접근 1회)
- 속도 향상을 위해 associative register 또는 transiation look-aside-buffer(TLB)라 부르는 고속 lookup hardware cache  사용
- TLB는 논리적 페이지 번호와 물리적 페이지 번호를 갖고 있다.
### Page-Table Base Register(PTBR)
- 메모리 관리에 사용되는 레지스터
- 페이지 테이블의 시작 주소를 갖고 있다.
### Page-table lenth Register (PTLR)
- 메모리 관리에 사용되는 레지스터
- 페이지 테이블의 크기를 저장하고 있다.

### Associative Register(TLB)
- 웹사이트의 북마크와 유사한 기능, 자주 사용하는 페이지의 주소값을 레지스터에 저장한다.
- Associative registers (TLB) : parallel search가 가능하다.
- `page table 일부`가 TLB에 보관되어 있다.(주로 빈번히 사용되는 엔트리)
- 논리적 페이지 번호와 주소 변환된 물리적 페이지 번호(page frame) 정보를 갖고 있다.
- 페이지 테이블의 임시 캐시 역할을 하는것이다.
#### TLB가 있을경우의 Address translation
- 특정 page가 TLB에 있는 경우 곧바로 page frame(메모리에서의 물리적 페이지 번호)을 얻어 접근한다.(TLB 전체를 search)
- 그렇지 않은 경우(TLB에 찾는 page가 없는 경우) main memory의 page table로부터 frame을 얻는다.(index 형식으로 검색)
- TLB는 context switch때 flush하여 다른 프로세스의 정보를 담는다.(엔트리를 전부 지운 후 다시 채움.)


##  Two-Level Page Table (Hierarchical Page table)
- 두단계에 거쳐 물리적 주소에 접근
- 32bit 체계에서 2^32byte(4gb) 주소 공간이 존재
  - page size가 4kb라면 10^6 개의 page table entry 필요
  - page entry가 4byte라면 프로세스당 4mb의 page table 필요
  - 대부분의 프로세스는 일부분의 주소공간만 사용하므로 page table 공간이 낭비된다.
### 페이지 분리
- 기존의 하나의 페이지를 여러개의 페이지로 나누는 작업
- 예를들어 기존에 하나의 페이지를 20bit로 표현했다면, 10bit의 두개로 페이지를 나누면 기존 2^20개의 엔트리에서, 2^10 + 2^10 개의 엔트리로 줄일 수 있다.

### 장점
- page table을 page로 구성하여 `사용되지 않는 주소공간에 대한 outer page table`의 `엔트리값은 NULL상태`로 놔둬 `메모리 공간을 확보`할 수 있다.(대응하는 inner page table이 없는 상태)
- 페이지 엔트리의 개수를 줄일 수 있다.

### 단점
- 계층을 나눌수록 테이블 크기는 줄어들지만, 테이블 개수가 늘어나 메모리를 자주 참조해야 한다(outer table 1회 inner table 1회 물리주소 참조 1회, 계층이 늘어나면 증가)

![alt text](이미지/innertable.png)

### outer page table
- inner page table메모리에 저장하는 프레임 주소를 포함한다.
- outer page table은 논리적 주소공간의 수와 동일하다.

### Inner page table
- 실제 메모리의 물리적 프레임에 매핑하는 정보를 포함한다.
## Multilevel Paging
- address space가 커지면 다단계 페이지 테이블 필요
- 각 단계 페이지 테이블이 메모리에 존재하므로 logical address의 physical address 변환에 더 많은 메모리 접근 필요
- TLB를 통해 메모리 접근 시간을 줄일 수 있음
```
4단계 페이지 테이블을 사용하는 경우
메모리 접근 시간이 100ns TLB 접근 시간이 20ns
TLB hit ration가 98%인경우
effective memory access time = TLB 에 있는 페이지에 접근할때의 시간 + 페이지테이블에 있는 페이지에 접근할때의 시간 =
 0.98*120+0.02*520
=128ns
결과적으로 주소변환을 위해 28ns만 소요

```
  
```
10 bit - outer page table index (p1)
10 bit - page of page table index (p2) 
12 bit - page offset d

```
## Inverted Page Table Architecture
![alt text](이미지/invertedpage.png)
- 단 하나의 페이지 테이블만 존재한다.
- 기존의 page table 방식은 `페이지의 수`로 페이지 엔트리 개수를 결정했다면, Inverted Page Table 에서는  `물리적 메모리 프레임의 수`에 따라 결정된다.
- 주소변환시 기존에는 페이지 번호로 페이지 엔트리를 찾았지만, inverted page table 에서는 물리적 메모리 프레임 기준으로 엔트리를 찾는다.
- 각 엔트리에는 해당 프레임에 들어가는 페이지의 논리적 주소가 저장된다.

### 검색방법
- 기존 페이지 테이블은 index 방식이여서 순차적으로 검색했다.
- inverted page table 에서는 논리적 주소를 통해 물리적 주소를 찾기 위해선 전체 페이지 테이블을 검색해야 한다.
- PID와 해당 프로세스의 몇번째 페이지인지에 대한 정보를 저장한다.(process-id and process logical address)
- 검색시간을 줄이기 위해 Asscociative Register(TLB)를 사용해서 검색시간을 줄인다.

### 장점
- 페이지 테이블 크기가 고정되어 있어 메모리 공간을 절약할 수 있다.

### 단점
- 검색을 위해 페이지 전체를 검색해야 하기 때문에 asscociative Register를 필수적으로 사용해야 한다.


## Shared Page
![alt text](이미지/sharedpages.png)
### shared code(Re-entrant code)
- `read-only`로 하여 프로세스 간에 하나의 code만 메모리에 적재한다.(text editors, compilers, window systems)
- shared code는 모든 프로세스의 `logical address space에서` `동일한 위치`에 있어야 한다.
### Private cod and data
- 각 프로세스는 독자적으로 페이지를 메모리에 적재한다
- logical address sapce 아무 페이지에 와도 무방하다

## Segmentation Architecture
![alt text](이미지/segmentation.png)
- 프로세스를 의미 있는 단위인 segment로 구성(논리적단위)
- 작게는 함수 하나나, 크게는 프로그램 전체를 하나의 세그먼트로 정의한다.
- 일반적으로 code,data,stack이 하나하나의 세그먼트로 구성된다.
- external fragmentation이 발생한다.
- paging 기법에 비해 테이블로 인한 메모리 낭비가 적다.(page 기법은 테이블 수가 많음)
- logical address는 다음 두 가지로 구성
  - <segment-number,offset>
### segment table
- 주소변환을 위한 테이블
- base : 물리적 주소에서 segment의 시작 위치
- limit: segment의 길이(length)
### segment-table base register(STBR)
- 물리적 메모리에서의 segment table의 위치
### Segment-Table Length Register(STLR)
- 프로그램이 사용하는 segment의 수
  - 요청된 segment 번호가 segment의 최대 번호보다 큰지 검증
### Segmentation Translation
![alt text](이미지/segment-translation.png)
- logical memory에는 segment(s) 번호와 offset(d)이 기록되어 있다.
- segment table의 limit와 base 정보로 메모리에서의 위치를 찾는다
- offset 값(d)를 통해 정확한 위치를 탐색한다.
- offset 값이 limit 값(length) 이상일 경우 에러를 발생시킨다.

### Segmentation Protection
- 각 segment 별로 protection bit가 존재
  - 각 엔트리에는, valid bit, 권한 bit(read/write/execution) 존재
- 페이징 기법과 달리, 의미단위로 나누었기 때문에 보안에 유리함

## Paged segmentation
![alt text](이미지/translation-pagedsegmentation.png)
- segment와 page의 결합
- segment의 길이가 커서 주기억장치에 한번에 적재할 수 없는 문제를 해결
- segment-table entry가 segment의 base address를 가지고 있는것이 아니라, segment를 구성하는 `page table`의 `base address`를 가지고 있다.
- `segment별로 page table`이 존재한다.
### Translation
- logical address에는 segment 번호, page 번호, offset이 기록되어 있다.
1. logical address의 segment 번호로 segment table에서 segment를 찾는다
2. logical address의 page 번호로 해당 sement의 page table에서 page 번호로 page를 찾는다.
3. offest 정보로 page frame 번호와 offset byte 수로 실제 메모리 위치를 찾는다.


## Memory Protection
- page table 각 entry 마다 아래의 bit를 둔다.
### protection bit
- page에 연산에 대한 접근권한 제어(read/write/read-only)
### valid-invalid bit
- valid : 해당 주소의 frame에 그 포르세스를 구성하는 유효한 내용이 있음(접근 허용)
- invalid : 해당 주소의 frame에 유효한 내용이 없음
  - 프로세스가 해당 주소 부분을 사용하지 않는 경우
  - 해당 페이지가 메모리에 올라와있지 않고 swap area에 있는 경우(swap out 당함)