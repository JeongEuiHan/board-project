# Spring Boot 게시판 프로젝트

Spring Boot 기반의 게시판 웹 애플리케이션으로  
회원 인증, 게시글/댓글 CRUD, 좋아요 기능, 이미지 업로드(S3)를 구현한 개인 프로젝트입니다.

Spring MVC 레이어드 아키텍처를 적용하여  
Controller / Service / Repository 역할을 분리하고 유지보수성과 확장성을 고려해 설계했습니다.

---

## 기술 스택

### Backend
- Java 17
- Spring Boot
- Spring MVC
- Spring Security
- Spring Data JPA
- Hibernate

### Frontend
- Thymeleaf
- HTML / CSS / JavaScript
- Bootstrap

### Database
- MySQL

### Infra / Storage
- AWS S3 (이미지 업로드)

### Build / Tool
- Gradle
- Git / GitHub

---

## 아키텍처

![architecture](docs/architecture.png)

- Spring MVC 기반 레이어드 아키텍처
- Controller → Service → Repository 구조
- 비즈니스 로직은 Service 계층에서 처리
- JPA 기반 ORM 구조

---

## 주요 기능

### 회원 기능
- Spring Security 기반 로그인 / 로그아웃
- 인증 여부에 따른 접근 제어
- 관리자 권한 분리

### 게시판 기능
- 게시글 작성 / 조회 / 수정 / 삭제 (CRUD)
- 게시판 카테고리 분리
- 작성자 및 관리자 권한 검증

### 댓글 기능
- 댓글 작성 / 수정 / 삭제
- 본인 또는 관리자만 수정/삭제 가능

### 좋아요 기능
- 게시글 좋아요 / 좋아요 취소
- 사용자별 중복 좋아요 방지
- 좋아요 수 실시간 반영

### 이미지 업로드
- AWS S3 연동 이미지 업로드
- 이미지 확장자 및 용량 검증
- 게시글 수정 시 기존 이미지 삭제 처리

---

## 좋아요 중복 처리 (문제 해결 경험)

### 문제
- 동일 사용자가 하나의 게시글에 여러 번 좋아요를 누를 수 있는 문제 발생

### 해결
- Service 계층에서 좋아요 존재 여부를 사전 조회하여 중복 저장 방지

```java
public Boolean checkLike(String loginId, Long boardId) {
    return likeRepository.existsByUser_LoginIdAndBoardId(loginId, boardId);
}
```
### 결과
- 중복 데이터 저장 방지
- 비즈니스 로직 책임을 Service 계층에 명확히 분리

---

## 보안 처리
- Spring Security 기반 인증 / 인가 처리
- 로그인 사용자 / 비로그인 사용자 접근 제한
- 작성자 또는 관리자만 수정/삭제 가능
- 서버 단 권한 검증 처리

---

## 실행 방법

1. 프로젝트 클론
```bash
git clone https://github.com/your-id/your-repo.git
```
2. 환경 설정
- MySQL DB 설정
- AWS S3 Access Key / Secret Key 설정
- application.yml 또는 application.properties 환경 변수 설정
3. 실행
```bash
./gradlew bootRun
```
---

## 프로젝트 구조
```arduino
├─ controller
├─ service
├─ repository
├─ domain (entity)
├─ dto
├─ config
└─ templates
```
---

## 성과 및 배운 점
- Spring MVC 레이어드 아키텍처에 대한 이해
- Spring Security 인증/인가 흐름 이해
- JPA 연관관계 매핑 및 ORM 설계 경험
- AWS S3 연동 파일 업로드 처리 경험
- 유지보수성과 확장성을 고려한 서버 설계 경험

---

## 기타
- 개인 학습 및 포트폴리오 용도로 제작한 프로젝트입니다.
- 지속적으로 리팩토링 및 기능 개선 예정입니다
