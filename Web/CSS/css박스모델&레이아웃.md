### 1. 박스 모델(Box Model)

모든 HTML 요소는 기본적으로 **박스 형태**로 구성되어 있고, 이 박스는 다음과 같은 구조를 갖고 있어:

```
┌───────────────────────┐  ← margin (바깥 여백)
│      border           │
│  ┌───────────────┐    │  ← padding (안쪽 여백)
│  │  content 영역 │    │  ← 실제 내용
│  └───────────────┘    │
└───────────────────────┘
```

| 영역 | 설명 | 예시 |
|------|------|------|
| `content` | 내용이 들어가는 실제 박스 | 텍스트, 이미지 등 |
| `padding` | 내용과 테두리 사이의 여백 | `padding: 20px` |
| `border` | 요소의 테두리 | `border: 1px solid black` |
| `margin` | 요소 바깥쪽 여백 | `margin: 20px` |

#### 예제

```css
.box {
  width: 200px;
  height: 100px;
  padding: 20px;
  margin: 30px;
  border: 2px solid blue;
  background-color: lightgray;
}
```

---

### 2. display 속성

`display`는 요소가 **어떻게 배치되는지**를 결정함

| 속성값 | 설명 |
|--------|------|
| `block` | 블록 요소 (div, p, h1 등). 줄바꿈 발생 |
| `inline` | 인라인 요소 (span, a 등). 줄바꿈 없음 |
| `inline-block` | 인라인처럼 배치되지만 block처럼 크기 지정 가능 |
| `none` | 요소를 화면에서 숨김 (완전 제거됨) |
| `flex` | Flexbox 레이아웃을 설정 (자식 요소 정렬에 사용) |

#### 예제

```css
span {
  display: block;
}
```

---

### 3. position 속성

요소의 **위치 지정 방식**을 설정함

| 속성값 | 설명 |
|--------|------|
| `static` | 기본값 (문서 흐름에 따라 배치) |
| `relative` | 자기 원래 위치 기준으로 이동 |
| `absolute` | 부모 요소 기준으로 고정 위치 설정 (부모가 `position: relative`일 때 기준이 됨) |
| `fixed` | 화면 기준으로 고정 (스크롤에도 안 움직임) |
| `sticky` | 스크롤에 따라 고정되는 하이브리드 위치 |

#### 예제

```css
.box {
  position: absolute;
  top: 50px;
  left: 100px;
}
```

---

### 4. Flexbox 기초

부모 요소에 `display: flex`를 주면, 자식 요소들의 **정렬과 배치**를 손쉽게 제어할 수 있음

#### 기본 문법

```css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

| 속성 | 설명 |
|------|------|
| `justify-content` | 주 축(가로)의 정렬 방식 (start, center, space-between 등) |
| `align-items` | 교차 축(세로)의 정렬 방식 |
| `flex-direction` | 축의 방향 (row, column) |
| `gap` | 요소 간 간격 |

#### 예제

```html
<div class="container">
  <div class="item">A</div>
  <div class="item">B</div>
  <div class="item">C</div>
</div>
```

```css
.container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 100px;
}

.item {
  width: 50px;
  height: 50px;
  background-color: coral;
}
```

---

### 요약 정리

| 개념 | 설명 |
|------|------|
| 박스 모델 | content + padding + border + margin 구조로 구성 |
| display | 요소의 기본 레이아웃 형태 설정 (block, inline, flex 등) |
| position | 요소의 위치를 제어 (relative, absolute, fixed 등) |
| flexbox | 요소들을 유연하게 정렬하고 배치하는 방법 |
