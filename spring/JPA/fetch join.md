# join fetch
## 개요
- JPQL에서 사용되는 구문
- JPA는 연관된 entity들을 lazy loading으로 설정하여 필요할때만 가져온다.
- `eager loading`은 항상 mapping된 entity를 즉시 로딩한다.
- `특정 쿼리`에서 연관된 entity를 전부 load하고 싶을때 join fetch를 사용하여 fetch type을  `eager loading` 으로 바꾸지 않고도 `즉시로딩`이 가능해진다.
### 예시

```
public interface RegionRepository extends JpaRepository<Region,Long> {
    @Query("SELECT DISTINCT r FROM Region r " +
            "LEFT JOIN FETCH r.subRegions " +//subRegions을 함께 로딩하기 위한 LEFT JOIN FETCH
            "WHERE r.regionName LIKE %:keyword%")//지정된 키워드를 포함하는 Region 검색
    List<Region> findRegionsWithSubRegionsAndPlacesByNameContaining(String keyword);
}

```


### JPQL DISTINCT
- JPQL 에서 distinct는 엔티티 값이나 어떠한 유형의 결과도 중복되지 않게 한다.
- SQL에 distinct 키워드를 추가해주고, 또한 중복되는 엔티티를 제거해 준다.
- 1대다 관계에서 join으로 데이터가 중복될 경우 (row 증가)유용하다.
- `1대다 관계에서 fetch join 하면 페이징이 안나간다.`
- join으로 인해 row가 증가하였기 때문에 페이징이 불가능해졌기 때문이다.
- 메모리에서 페이징을 해버린다(out of memory 발생할 가능성 높음)
- 1:다 fetch join은 1개만 사용하자, row가 너무 늘어날 수 있다.(To One 관계는 row를 증가시키지 않음, To Many 관계에서는 Many 기준으로 row가 생성됨)

```
"SELECT DISTINCT p FROM Place p"

```
위 쿼리는 중복되는 Place 엔티티를 제거한후 반환한다.


### To Many 관계 풀기
- To One 관계는 fetch join을 건다(To one은 row수 증가 x)
- 컬렉션은 지연 로딩으로 조회한다.
- 지연 로딩 성능 최적화 `@BatchSize`를 적용한다.
- 예를들어 `order`와 `orderItem`이 1:N 관계라면
- 