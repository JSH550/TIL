# overflow

## 개요
- css에서 넘치는 요소를 처리하는 속성
- 가로 정렬시 부모 요소에 display:flex;로 자식 요소 가로정렬이 가능하다.
- 자식 요소에 `flex-shrink: 0;` 추가하여 부모요소의 display:flex로 자식요소 크기가 바뀌는것을 방지할 수 있다.

## 값
### visible
![alt text](이미지/overflowVisible.png)
- 자식 DOM이 크기를 넘어가더라도 그대로 보여준다

### hidden
![alt text](이미지/overflowHidden.png)
- 자식 DOM이 크기를 넘어가더면 숨긴다.

### scroll
- 자식 DOM이 크기를 넘어가지 않더라도 스크롤바를 표시한다.

### auto
![alt text](이미지/overflowAuto.png)
- 콘텐츠가 DOM을 넘어가는 경우에만 스크롤바를 표시한다.


## 예시코드
```
  <div style="display: flex; width: 500px; height: 300px; overflow-x: hidden; outline: auto;">
    <div style="flex-shrink: 0; margin-right: 3px; width: 100px; height: 100px; outline: auto; background-color: antiquewhite;"></div>
    <div style="flex-shrink: 0; margin-right: 3px; width: 100px; height: 100px; outline: auto; background-color: antiquewhite;"></div>
    <div style="flex-shrink: 0; margin-right: 3px; width: 100px; height: 100px; outline: auto; background-color: antiquewhite;"></div>
    <div style="flex-shrink: 0; margin-right: 3px; width: 100px; height: 100px; outline: auto; background-color: antiquewhite;"></div>
    <div style="flex-shrink: 0; margin-right: 3px; width: 100px; height: 100px; outline: auto; background-color: antiquewhite;"></div>
    <div style="flex-shrink: 0; margin-right: 3px; width: 100px; height: 100px; outline: auto; background-color: antiquewhite;"></div>
    <div style="flex-shrink: 0; margin-right: 3px; width: 100px; height: 100px; outline: auto; background-color: antiquewhite;"></div>
  </div>

```