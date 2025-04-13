## Day 2: Form과 Input 태그, 시맨틱 태그

---

### 1. 폼 기본 구조

#### `<form>`

- 사용자 입력을 서버로 전송하기 위한 영역을 묶는 태그
- `action`: 데이터를 보낼 서버 주소  
- `method`: 전송 방식 (`GET` 또는 `POST`)

```html
<form action="/submit" method="post">
  <!-- 입력 요소들 -->
</form>
```

#### `<input>`

- 사용자 입력을 받는 기본 태그
- `type` 속성으로 입력 형식을 설정함 (text, number, email, password 등)

```html
<input type="text" name="username" placeholder="아이디 입력">
<input type="password" name="password" placeholder="비밀번호 입력">
```

#### `<button>`

- 클릭 가능한 버튼 생성
- `type="submit"`은 폼 제출, `type="button"`은 단순 버튼

```html
<button type="submit">제출</button>
<button type="button">일반 버튼</button>
```

---

### 2. 폼 입력 요소

#### `<select>` + `<option>`

- 드롭다운 리스트를 생성

```html
<select name="region">
  <option value="seoul">서울</option>
  <option value="busan">부산</option>
</select>
```

#### `<textarea>`

- 여러 줄 입력이 가능한 텍스트 박스

```html
<textarea name="message" rows="4" cols="50">기본 내용</textarea>
```

#### 라디오 버튼 (`type="radio"`)

- 여러 개 중 하나만 선택할 수 있는 선택지

```html
<label><input type="radio" name="gender" value="male"> 남자</label>
<label><input type="radio" name="gender" value="female"> 여자</label>
```

※ `name` 속성을 같게 해야 그룹으로 묶여 한 가지만 선택 가능

#### 체크박스 (`type="checkbox"`)

- 여러 개를 중복 선택할 수 있는 선택지

```html
<label><input type="checkbox" name="interest" value="sports"> 스포츠</label>
<label><input type="checkbox" name="interest" value="music"> 음악</label>
```

---

### 3. 시맨틱 태그

HTML5에서 새로 도입된 시맨틱(Semantic) 태그는 코드만 봐도 어떤 역할인지 알 수 있도록 의미를 부여하는 태그들이야. 구조적이고 접근성 높은 웹사이트 제작에 도움이 됨.

<div align="center">
    <img src="https://github.com/user-attachments/assets/e61627c7-ec08-44fa-8263-6f959ab1658a" alt="Image" />
</div>

| 태그 | 역할 |
|------|------|
| `<header>` | 페이지 또는 섹션의 머리말 (로고, 네비게이션 등) |
| `<nav>` | 주된 네비게이션 메뉴 영역 |
| `<main>` | 본문 주요 콘텐츠 |
| `<section>` | 주제별 콘텐츠 영역, 구분 가능한 묶음 |
| `<article>` | 독립적인 콘텐츠 (뉴스, 블로그 포스트 등) |
| `<aside>` | 보조 콘텐츠 (광고, 사이드바 등) |
| `<footer>` | 페이지 하단 (저작권, 연락처 등) |

예시 구조:

```html
<header>
  <h1>사이트 로고</h1>
  <nav>
    <a href="#">홈</a>
    <a href="#">소개</a>
  </nav>
</header>

<main>
  <section>
    <h2>공지사항</h2>
    <p>여기에 공지 내용을 작성</p>
  </section>

  <article>
    <h2>블로그 포스트 제목</h2>
    <p>글 본문</p>
  </article>
</main>

<aside>
  <h3>광고 배너</h3>
</aside>

<footer>
  <p>© 2025 회사 이름. All rights reserved.</p>
</footer>
```

---

## 요약

| 태그 | 용도 | 특징 |
|------|------|------|
| `<form>` | 사용자 입력 묶음 | 서버로 전송할 때 사용 |
| `<input>` | 다양한 입력 필드 | type 속성 다양 (text, password, radio 등) |
| `<select>`, `<option>` | 드롭다운 메뉴 | select 안에 여러 option |
| `<textarea>` | 여러 줄 입력 | 줄 수 조정 가능 |
| `<button>` | 버튼 | submit 또는 일반 용도 |
| `<header>`, `<footer>` | 머리말/꼬리말 | 반복되는 사이트 구조 |
| `<nav>` | 네비게이션 | 메뉴 링크에 적합 |
| `<main>`, `<section>`, `<article>` | 본문 구조화 | 명확한 콘텐츠 구분 |
| `<aside>` | 부가 정보 영역 | 광고나 사이드 콘텐츠 |

---
