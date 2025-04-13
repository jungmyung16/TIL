### 1. Flexbox 심화

#### Flex 컨테이너 속성 (부모에 적용)

| 속성 | 설명 |
|------|------|
| `flex-direction` | 주 축의 방향 설정: `row`(기본), `row-reverse`, `column`, `column-reverse` |
| `justify-content` | 주 축 정렬: `flex-start`, `center`, `flex-end`, `space-between`, `space-around`, `space-evenly` |
| `align-items` | 교차 축 정렬: `stretch`, `center`, `flex-start`, `flex-end`, `baseline` |
| `flex-wrap` | 자식 요소 줄바꿈 허용: `nowrap`(기본), `wrap`, `wrap-reverse` |
| `gap` | 요소 간 간격 설정 (최신 브라우저 지원) |

#### Flex 아이템 속성 (자식에 적용)

| 속성 | 설명 |
|------|------|
| `flex` | 비율 기반 크기 조절. `flex: 1`은 남은 공간을 균등 분배 |
| `align-self` | 개별 아이템 교차 축 정렬 (부모의 `align-items` 무시) |
| `order` | 아이템의 순서 변경 가능 (`order: 0` 기본값) |

#### 예시

```css
.container {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  gap: 20px;
  flex-wrap: wrap;
}
```

---

### 2. Grid 레이아웃

Flex가 **1차원(가로 또는 세로 한 방향)** 정렬이라면, Grid는 **2차원(행과 열)** 레이아웃을 다룰 수 있어.

#### Grid 컨테이너 속성

```css
.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;  /* 3열 */
  grid-template-rows: auto auto;       /* 2행 */
  gap: 10px;
}
```

- `grid-template-columns`: 열 너비 지정
- `grid-template-rows`: 행 높이 지정
- `fr`: fraction 단위로 나눔 (비율)
- `repeat(3, 1fr)`: `1fr 1fr 1fr`과 같음
- `gap`: 셀 간격

#### Grid 아이템 속성

```css
.item1 {
  grid-column: 1 / 3;  /* 1번부터 3번 전까지 열 차지 (즉, 2칸) */
  grid-row: 1 / 2;     /* 첫 번째 행만 */
}
```

#### 예시

```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: 100px 100px;
  gap: 10px;
}
```

```html
<div class="container">
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">3</div>
</div>
```

---

### 3. 반응형 웹 디자인 (Media Query)

#### 개념

다양한 화면 크기(모바일, 태블릿, PC)에 맞춰 스타일을 다르게 적용하는 기술

#### 기본 문법

```css
@media screen and (max-width: 768px) {
  body {
    background-color: lightblue;
  }

  .container {
    flex-direction: column;
  }
}
```

- `max-width`: 해당 값 이하의 화면에서만 적용
- `min-width`: 해당 값 이상의 화면에서만 적용

#### 반응형 단위

| 단위 | 설명 |
|------|------|
| `px` | 고정 크기 (비권장) |
| `%` | 부모 기준 비율 |
| `vw`, `vh` | 뷰포트 너비, 높이 기준 비율 |
| `em`, `rem` | 폰트 크기 기준 (반응형 글자 설정에 사용) |

#### 반응형 레이아웃 예시

```css
.container {
  display: flex;
  flex-direction: row;
}

@media (max-width: 600px) {
  .container {
    flex-direction: column;
  }
}
```

이렇게 하면 화면이 작아졌을 때 레이아웃이 수직으로 바뀜 (모바일 UI처럼)

---

### 전체 흐름 정리

| 개념 | 요약 설명 |
|------|-----------|
| Flexbox | 1차원 정렬 도구. 정렬과 공간 분배에 탁월 |
| Grid | 2차원 레이아웃 도구. 페이지 전체 구성에 유용 |
| Media Query | 반응형 웹 구현용. 화면 크기에 따라 다른 스타일 적용 |
| 반응형 단위 | %, vw/vh, em/rem을 활용하면 유연한 UI 구현 가능 |

---