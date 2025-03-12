## 웹 애플리케이션에서 세션(Session)과 쿠키(Cookie)

### 기본 개념

- **세션(Session)**
  - 서버가 사용자의 상태를 기억하기 위해 생성하는 데이터
  - 로그인 여부, 장바구니 정보와 같은 상태를 서버에서 관리

- **쿠키(Cookie)**
  - 브라우저에 저장되는 작은 크기의 텍스트 파일
  - 서버에 요청할 때마다 브라우저가 자동으로 전송하여 사용자를 구분하는 데 사용

### 역할과 차이점

| 구분       | 세션(Session)                   | 쿠키(Cookie)                   |
|------------|---------------------------------|--------------------------------|
| 저장 위치  | 서버                             | 브라우저 (클라이언트)          |
| 유지 방식  | 서버의 메모리나 DB에 저장       | 브라우저 내 저장               |
| 보안       | 서버에 저장되어 상대적으로 안전  | 브라우저에서 쉽게 수정 가능하여 보안 취약 |

### 세션과 쿠키의 보안 이슈

#### 1. 세션 하이재킹(Session Hijacking)
- **개념**: 공격자가 다른 사용자의 세션 ID를 훔쳐서 로그인된 사용자인 것처럼 위장하는 공격
- **공격 방식**:
  - 네트워크 상에서 전송되는 쿠키 값을 가로채는 방법
  - 악성 스크립트(XSS)를 통해 세션 ID 탈취
- **실제 사례**:
  - 카페나 공공장소의 오픈 와이파이 환경에서 사용자가 로그인된 상태로 접속하면 세션을 가로채어 피해자의 계정으로 접근한 사례
- **해결 방법**:
  - 세션 쿠키에 `HttpOnly`, `Secure`, `SameSite` 옵션을 적용하여 탈취 가능성을 최소화
  ```javascript
  res.cookie('session_id', sessionId, { httpOnly: true, secure: true, sameSite: 'Strict' });
  ```

#### 2. 세션 고정 공격(Session Fixation)
- **개념**: 공격자가 미리 생성한 세션 ID를 사용자에게 제공하여 사용자가 로그인할 때 동일한 세션 ID를 사용하게 유도하여, 해당 세션을 공격자가 탈취하는 공격
- **공격 방식**:
  - 공격자가 만든 링크나 이메일을 사용자에게 보내고, 사용자가 이 링크로 접속하여 로그인하면 공격자가 접근 가능
- **실제 사례**:
  - 이메일 피싱을 통해 미리 설정된 세션을 피해자에게 전달, 이후 피해자가 로그인하면 공격자가 그 계정을 무단으로 사용할 수 있었던 사례
- **해결 방법**:
  - 사용자가 로그인할 때마다 새로운 세션 ID를 발급
  ```javascript
  req.session.regenerate((err) => {
    req.session.user = user;
  });
  ```

#### 3. XSS(Cross-site scripting)와 쿠키 탈취
- **개념**: 웹사이트에 악성 스크립트를 주입하여 사용자가 페이지를 방문했을 때 쿠키와 같은 민감한 데이터를 탈취하는 공격
- **공격 방식**:
  - 게시판 등 사용자 입력이 가능한 웹페이지에서 악성 스크립트 실행
- **해결 방법**:
  - 쿠키의 `HttpOnly`, `Secure` 옵션 설정
  ```javascript
  res.cookie('token', token, { httpOnly: true, secure: true });
  ```

#### 4. CSRF(크로스사이트 요청 위조)
- **개념**: 사용자가 의도하지 않은 요청을 강제로 보내도록 하는 공격
- **공격 방식**:
  - 악성 웹사이트가 사용자가 이미 로그인한 웹사이트에서 자동으로 요청을 보냄
- **해결 방법**:
  - CSRF 토큰을 활용하여 요청의 정당성을 검증
  ```html
  <form method="POST">
    <input type="hidden" name="csrf_token" value="{{csrf_token}}">
    <input type="submit">
  </form>
  ```

### 실무에서 적용할 좋은 예시시

#### 세션과 쿠키 보안을 강화하기 위한 설정
- 쿠키 옵션 `Secure`, `HttpOnly`, `SameSite` 필수 적용
- 세션 유효 시간(타임아웃) 설정
- 주기적인 세션 ID 재생성

#### 보안 정책과 예제 코드

```javascript
app.use(session({
  secret: 'secureKey',
  resave: false,
  saveUninitialized: false,
  cookie: {
    httpOnly: true,
    secure: true,
    sameSite: 'Strict',
    maxAge: 3600000 // 1시간 유지
  }
}));
```

### JWT(JSON Web Token)와 세션 기반 인증 비교
- JWT
  - 클라이언트 측에 저장, 서버는 상태 유지하지 않음
  - 서버 확장성에 유리
  - 정보가 토큰 내에 포함되어 있어 민감한 정보를 담을 경우 위험성 증가

- 세션 기반 인증
  - 서버에서 상태를 관리하므로 민감한 정보 보호에 유리
  - 서버의 자원 소모가 큼

### 추가적으로 고려해야 할 보안 요소

#### HTTPS 데이터 암호화
- HTTPS는 HTTP 프로토콜을 보안 강화한 버전으로, TLS(Transport Layer Security) 또는 SSL(Secure Sockets Layer)을 이용하여 데이터를 암호화함
- 이를 통해 데이터를 안전하게 전송하고 중간에서 데이터를 탈취하거나 변조하는 것을 방지함

#### 브라우저 SameSite 정책
- 브라우저의 기본 정책인 `SameSite` 속성을 활용하여 불필요한 크로스 도메인 요청 방지

```javascript
res.cookie('auth_token', token, { httpOnly: true, secure: true, sameSite: 'Lax' });
```

### 최신 웹 보안 트렌드 및 실무 고려사항
- CSP(Content Security Policy)를 설정하여 XSS 공격을 효과적으로 차단
- 주기적인 보안 점검과 코드 리뷰 실시
- 로그 기록 및 실시간 모니터링을 통해 보안 위협 조기 발견 및 대응
- 정기적인 침투 테스트 및 보안 교육 실시

