# Pagenation

## 정의
- 대량의 데이터를 일정한 크기로 나누어 여러 페이지로 분할하여 나타내는 것을 페이지네이션 이라고 한다.
- 대량의 데이터는 로딩시간 증가, 서버 성능 저하를 발생시켜 애플리케이션 전체의 성능을 저하시킨다.

## 페이지네이션 관련 class


### findAll - Spring Data JPA
- findAll() 메서드 (정확히는 PagingAndSortingRepository 인터페이스)를 통해 쉽게 페이지네이션을 할 수 있다.
- 파라미터로 Pageable 자료형 객체를 받는다.
- Pageable 클래스를 상속받은 PageRequest 을 사용하면 쉽게 구현할 수 있다.
#### 예시
```
Page<T> findAll(Pageable pageable);
```

### PageRequest (Class)
- `spring framwork`에서 제공되는 페이지네이션을 위한 class이다.
- 첫번째 파라미터는 `pageNumber` 두번째 파라미터는 `pageSize`를 받는다.
- `pageNumber`는 0부터 시작하며 음수일 수 없다.
- `pageSize`는 한페이지에 포함되는 데이터 갯수이며, 0보다 커야한다.


### Page (Interface)
- Spring 에서 메타 데이터와 실제 데이터를 포함하는 데이터를 표현할때 사용하는 인터페이스
- 페이지 정보(MetaData)
  - Total elements
  - Total Pages
  - Page size
  - Page number
  - Has previous
  - Has next
  - Number of elements
- 페이징된 데이터(content)



### 예시
```
 public Page<PostListDto> getPostList(int pageNumber, int pageSize) {
// pageNumber는 0부터 시작하므로 1을 빼 보정합니다..
        pageNumber -= 1;

//PageRequest 객체를 생성합니다. 파라미터로 pageNumber와 pageSize를 받습니다.
PageRequest pageRequest = PageRequest.of(pageNumber,pageSize);


//Spring Data JPA의 JpaRepository findAll 인터페이스를 상속받은 메서드로 엔티티를 조회합니다.
//pageRequest에 저장된 페이지 번호와 크기로 데이터를 반환합니다. 반환값은 Page<T> 객체 형태로 반환됩니다.
Page<Post> allPosts = postRepository.findAll(pageRequest);
 }
```