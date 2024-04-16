# @Entity
- JPA에서 `entity` class 정의할때 사용되는 annotation
- JPA가 DB의 talbe과 mapping시켜 관리하게 된다. 

## @Id
- JPA에서 primary key를 지정할때 사용하는 annotation 이다.

##   @GeneratedValue
- JPA에서 primary key값을 자동으로 생성하는 방법을 정하는 속성이다.
### AUTO
- JPA 구현체가 자동으로 키 생성 전략을 선택한다.보통 `auto-increment` 을 선택한다
### IDENTITY
- 데이터베이스의 기본 키 생성 전략을 선택한다
- MySQL 에서는 ` AUTO_INCREMENT` 방식으로 1씩 증가한다.

### SEQUENCE
- 데이터베이스 스퀸스를 사용한다.

### NONE
- primary key를 직접 지정하여 생성한다.


## @Column
- 엔티티 클래스의 필드를 데이터베이스의 컬럼에 매핑시킨다.
- 제약 조건을 추가할 수 있다.
```
 @Column(name = "product_name", nullable = false)
    private String name;
```

##  @CreationTimestamp
- Hibernate(JPA 구현체)에서 제공하는 annotation
- 엔티티 클래스 필드에 사용되며, 데이터베이스에 필드값이 삽입될 때 자동으로 Timestamp 값을 저장한다.

```
@CreationTimestamp
    private Date createdDate;
```

## @ManyToOne
- JPA에서 다대일 관계를 정의할때 사용하는 annotation

## @OneToMany
- JPA에서 일대다 관계를 정의할때 사용하는 annotation
- mappedBy 연관관계에서 필드가 참조되고 있음을 나타낸다.(관계의 주인이 아니라는 의미다.)
- fetch 속성은 연관된 엔티티를 어떻게 가져올지 지정한다
  - FetchType.LAZY는 지연 로딩으로 참조될 경우에만 연관된 엔티티를 가져온다.
  - FetchType.EAGER 즉시 로딩으로 부모 엔티티가 로딩되면 연관된 엔티티들도 가져온다.

```
@Entity
public class Region {
 @Id
private Long id;
@OneToMany(mappedBy = "region", cascade = CascadeType.ALL,fetch = LAZY)
private List<City> cities;//
}

```
## @JoinColumn
- 엔티티 간의 관계를 정의할때 foreign key 컬럼명을 지정하는데 사용된다.
- Many to One 관계에서 다 쪽에 사용한다.
- One to One 관계에서 Owner entity에서 사용한다.

```
@ManyToOne(fetch = FetchType.LAZY)
@JoinColumn(name = "member_id", nullable = false)
    private Member member;
```

# Entity 상속

###`@Inheritance(strategy)`
- JPA에서 상속 mapping을 정의하는데 사용하는 annotation
- 상속예시: 제품의 공통 정보(제품이름,가격..etc)를`product`  `entity`로 정의하고, Book `entity`를 자식 으로 만들어 ISBN을 추가 
- strategy
    - `SINGLE_TABLE`:모든 엔티티를 단일 테이블에 매핑한다.
   - `JOINED`:엔티티를 각각의 table로 분리하고 `join column`으로 mapping 한다. **데이터 정규화** 에 용이하다.

## `@PrimaryKeyJoinColumn(name="")`
- 부모자식 entity 간 table을 분리할때 사용(InheritanceType.JOINED일때)
- 자식 entity가 부모의 primary key를 자신의 primary key로 사용한다.
- `name`은 자식 entity의 name+id를 사용한다.(예시: book_id)


### 예시

```
@Entity
//JOINED로 상속받는 entity table 분리
@Inheritance(strategy = InheritanceType.JOINED)
public abstract class Product {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
}

@Entity
@PrimaryKeyJoinColumn(name = "book_id")//부모의 primary key를 자식(book)의 primary key로 사용
public class Book extends Product {
    private String isbn;
    private String author;
}
```


# `@JsonIgnoreProperties`

# cascade = CascadeType.ALL