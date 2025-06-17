# 🌾 HDMS API 문서

하베스팅 데이터 모니터링 시스템(HDMS)의 REST API 문서입니다.

## 📋 개요

이 문서는 HDMS 백엔드 API의 전체 스펙을 제공합니다. 인증, 사용자 관리, 센서 데이터 모니터링 등의 기능을 포함합니다.

## 🚀 빠른 시작

### 로컬에서 Swagger UI 실행

1. **파일 다운로드**
   ```bash
   git clone <repository-url>
   cd swagger
   ```

2. **웹 서버 실행**
   
   **Python 사용:**
   ```bash
   # Python 3
   python -m http.server 8000
   
   # Python 2
   python -m SimpleHTTPServer 8000
   ```
   
   **Node.js 사용:**
   ```bash
   npx http-server
   ```
   
   **Live Server (VS Code 확장) 사용:**
   - VS Code에서 `index.html` 파일 우클릭
   - "Open with Live Server" 선택

3. **브라우저에서 확인**
   ```
   http://localhost:8000
   ```

### 온라인에서 확인

다음 도구들을 사용하여 온라인에서 바로 확인할 수 있습니다:

1. **Swagger Editor**: https://editor.swagger.io/
   - `api-docs.yaml` 파일 내용을 복사해서 붙여넣기

2. **GitHub Pages**: 
   - 이 레포지토리를 GitHub에 올리고 Pages 기능 활성화

## 📁 파일 구조

```
swagger/
├── index.html          # Swagger UI 메인 페이지
├── api-docs.yaml       # OpenAPI 3.0 스펙 파일
└── README.md           # 이 파일
```

## 🔧 파일 설명

### `index.html`
- 한국어로 커스터마이징된 Swagger UI
- 반응형 디자인
- 하베스팅 테마 적용
- CDN을 통한 최신 Swagger UI 사용

### `api-docs.yaml`
- OpenAPI 3.0 스펙
- 전체 API 엔드포인트 정의
- 스키마 및 예시 포함
- 한국어 문서화

## 🔐 API 인증

### JWT Bearer Token 인증

1. **로그인 API 호출**
   ```bash
   curl -X POST http://localhost:8080/api/auth/login \
     -H "Content-Type: application/json" \
     -d '{
       "userIdOrEmail": "admin",
       "password": "admin123!"
     }'
   ```

2. **응답에서 토큰 추출**
   ```json
   {
     "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
     "tokenType": "Bearer",
     "expiresIn": 86400,
     "user": { ... }
   }
   ```

3. **다른 API 호출 시 토큰 사용**
   ```bash
   curl -X GET http://localhost:8080/api/auth/me \
     -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
   ```

## 🎯 주요 API 엔드포인트

### 인증 관리
- `POST /auth/login` - 로그인
- `POST /auth/logout` - 로그아웃  
- `GET /auth/me` - 현재 사용자 정보

### 사용자 관리 (관리자 전용)
- `GET /admin/users` - 사용자 목록 조회
- `POST /admin/users` - 사용자 생성
- `GET /admin/users/{userId}` - 사용자 상세 조회
- `DELETE /admin/users/{userId}` - 사용자 삭제
- `PUT /admin/users/{userId}/toggle-status` - 사용자 상태 변경
- `PUT /admin/users/{userId}/menu-permissions` - 메뉴 권한 수정

## 🛠 개발 도구

### Postman Collection 생성
1. Swagger UI에서 "Download" 버튼 클릭
2. OpenAPI 파일을 Postman으로 import

### 코드 생성
OpenAPI Generator를 사용하여 클라이언트 코드 생성:

```bash
# TypeScript/JavaScript 클라이언트
openapi-generator-cli generate \
  -i api-docs.yaml \
  -g typescript-fetch \
  -o ./generated/typescript

# Java 클라이언트  
openapi-generator-cli generate \
  -i api-docs.yaml \
  -g java \
  -o ./generated/java
```

## 🔄 업데이트 가이드

### API 스펙 수정 시

1. `api-docs.yaml` 파일 수정
2. 로컬에서 Swagger UI로 확인
3. 새로운 API 추가 시 예시와 설명 포함
4. 변경사항을 git으로 관리

### 새로운 엔드포인트 추가 예시

```yaml
/new/endpoint:
  post:
    tags:
      - 새로운 기능
    summary: 새로운 기능 설명
    description: 상세한 설명
    requestBody:
      required: true
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/NewRequest'
    responses:
      '200':
        description: 성공
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/NewResponse'
```

## 🌐 서버 환경

### 개발 서버
- URL: `http://localhost:8080/api`
- 개발 및 테스트용

### 운영 서버  
- URL: `https://api.hdms.com/api`
- 프로덕션 환경

## 📞 지원

문제가 있거나 질문이 있으시면 연락주세요:

- **팀**: HDMS Team
- **이메일**: admin@hdms.com

## 📄 라이선스

MIT License

---

🌾 **HDMS Team** | 하베스팅 데이터 모니터링 시스템 