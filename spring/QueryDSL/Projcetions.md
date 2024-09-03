# Projections

# 1. 개요
- QueryDSL에서 쿼리 결과를 Java 객체로 매핑하기 위한 유틸들을 제공하는 클래스
- 쿼리 결과를 DTO로 변환할때 주로 사용된다.

# 2. 주요 메서드

## Projcetions.bean()
- DTO를 생성하고 쿼리 결과를 `DTO` 클래스의 `필드`에 매핑한다.
- 필드명을 정확하게 기재하지 않으면 에러가 발생한다.

### 사용법
```
Projections.bean(
    DTO클래스명.class, // DTO 클래스
    Q타입엔티티객체.엔티티필드명.as("DTO필드명") // 엔티티 필드와 DTO 필드 매핑
)
```
  
### 예시

-`Tag` 엔티티가 있고, `TagDataDto` DTO가 있다고 가정하자.


```
public class Tag {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @NotBlank
    @Column(unique = true, nullable = false)
    private String name;

    @Enumerated(EnumType.STRING)
    @Column(nullable = false)
    private TagStatus status;
}

```

```
public class TagDataDto {
    private Long id;

    private String name;

    private TagStatus status;
}

```

- Tag 엔티티를 찾아 DTO로 반환하는 로직은 다음과 같이 작성할 수 있다.
```
public List<TagDataDto> findTagData() {
    // QTag 타입 엔티티 객체 생성
    QTag tag = QTag.tag;

    // DTO를 생성하여 데이터를 매핑
    List<TagDataDto> fetch = jpaQueryFactory.select(Projections.bean(TagDataDto.class,
            tag.id.as("id"),      // Tag 엔티티의 id와 DTO의 id 필드 매핑
            tag.name.as("name"),  // Tag 엔티티의 name과 DTO의 name 필드 매핑
            tag.status.as("status") // Tag 엔티티의 status와 DTO의 status 필드 매핑
    ))
    .from(tag) // Tag 엔티티를 기준으로 쿼리 수행
    .fetch(); // 결과를 List<TagDataDto>로 가져오기

    return fetch; // 결과 반환
}
```

## 참고문헌
http://querydsl.com/static/querydsl/3.4.2/reference/html/ch03s02.html