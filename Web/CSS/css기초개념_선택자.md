### 1. CSS란?

- **CSS (Cascading Style Sheets)**  
  : HTML 요소들의 **스타일(색상, 크기, 배치 등)**을 지정하는 언어
- HTML이 **구조**, CSS는 **디자인** 담당

예:
```html
<p style="color: red;">이건 빨간색 글씨입니다.</p>
```

---

### 2. CSS 적용 방식 3가지

| 방식 | 설명 | 예시 |
|------|------|------|
| 인라인 스타일 | HTML 요소에 직접 `style` 속성 | `<p style="color: blue;">텍스트</p>` |
| 내부 스타일 (Internal) | `<style>` 태그를 `<head>`에 작성 | `<style>p { color: blue; }</style>` |
| 외부 스타일시트 (External) | `.css` 파일로 분리해서 `<link>`로 불러오기 | `style.css` 파일에서 정의 후 `<link rel="stylesheet" href="style.css">` |

**가장 권장**되는 방식은 외부 스타일시트 방식 (유지보수 용이)

---

### 3. 기본 선택자

CSS에서 어떤 HTML 요소에 스타일을 적용할지 지정하는 방법

#### 1) 전체 선택자 (`*`)
- 모든 요소에 스타일 적용

```css
* {
  margin: 0;
  padding: 0;
}
```

#### 2) 태그 선택자 (`태그명`)
- 특정 태그에 일괄 적용

```css
p {
  color: gray;
}
```

#### 3) 클래스 선택자 (`.클래스명`)
- `class` 속성이 같은 요소들에 적용
- **중복 사용 가능**

```html
<p class="highlight">강조 문장</p>
```
```css
.highlight {
  color: red;
  font-weight: bold;
}
```

#### 4) 아이디 선택자 (`#아이디명`)
- `id` 속성이 같은 요소에 적용
- **중복 사용 X (하나만 존재)**

```html
<p id="main-title">제목입니다</p>
```
```css
#main-title {
  font-size: 24px;
}
```

---

### 4. 자주 쓰는 기본 속성들

#### 글자 관련

| 속성 | 설명 | 예시 |
|------|------|------|
| `color` | 글자 색 | `color: blue;` |
| `font-size` | 글자 크기 | `font-size: 16px;` |
| `font-weight` | 굵기 (normal, bold 등) | `font-weight: bold;` |
| `text-align` | 정렬 (left, center, right) | `text-align: center;` |

#### 배경 & 박스

| 속성 | 설명 | 예시 |
|------|------|------|
| `background-color` | 배경색 | `background-color: yellow;` |
| `width`, `height` | 너비와 높이 | `width: 300px;` |
| `padding` | 안쪽 여백 | `padding: 10px;` |
| `margin` | 바깥 여백 | `margin: 20px;` |
| `border` | 테두리 | `border: 1px solid black;` |

---

### 5. 예제 전체 코드

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      background-color: #f5f5f5;
      font-family: Arial;
    }

    h1 {
      color: darkblue;
      text-align: center;
    }

    .highlight {
      color: red;
      font-weight: bold;
    }

    #main-box {
      background-color: white;
      padding: 20px;
      border: 2px solid gray;
      width: 300px;
      margin: 0 auto;
    }
  </style>
</head>
<body>

  <h1>CSS 연습</h1>

  <div id="main-box">
    <p class="highlight">이건 강조된 문장입니다.</p>
    <p>이건 일반 문장입니다.</p>
  </div>

</body>
</html>
```

---

### 요약

| 개념 | 설명 |
|------|------|
| CSS 역할 | HTML 요소에 디자인을 입힘 |
| 적용 방식 | 인라인, 내부, 외부 (외부 권장) |
| 선택자 | 태그, 클래스 `.`, 아이디 `#`, 전체 `*` |
| 속성 | color, font-size, padding, margin, border 등 |
| 클래스 vs 아이디 | 클래스는 여러 개 사용 가능, 아이디는 고유 |
