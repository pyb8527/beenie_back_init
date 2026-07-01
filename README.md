# backend-init

Spring Boot 기반 멀티모듈 백엔드 프로젝트입니다.

## 프로젝트 구조

```
backend-init
│
├── core                  # 실행 가능한 Spring Boot 애플리케이션 모듈
│   ├── BackendApplication.java
│   ├── web               # Controller, Request/Response, 예외 핸들러
│   ├── application       # UseCase, Service, DTO
│   ├── domain            # Entity, VO, Domain Service, Port(인터페이스)
│   └── infrastructure    # Adapter (GitHub OAuth, S3, Security 등)
│
├── storage
│   ├── jpa               # JPA Repository 구현체
│   ├── mybatis           # MyBatis Mapper
│   ├── redis             # Redis Adapter
│   └── rabbitmq          # MQ Producer/Consumer
│
├── support
│   ├── common
│   ├── exception
│   ├── logging
│   └── util
│
├── docs                  # 아키텍처/가이드 문서
├── docker                # 로컬/배포용 docker 설정
│
├── build.gradle
└── settings.gradle
```

모듈 구조와 의존 방향에 대한 자세한 설명은 [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)와
[docs/MULTI_MODULE_GUIDE.md](docs/MULTI_MODULE_GUIDE.md)를 참고하세요.

## 기술 스택

| 영역 | 기술 |
|---|---|
| Language | Java 21 |
| Framework | Spring Boot 3.x |
| Build | Gradle (Multi-Module) |
| Persistence | JPA(Hibernate), MyBatis |
| Cache/Session | Redis |
| Messaging | RabbitMQ |
| Container | Docker / Docker Compose |

> 실제 도입 여부에 맞게 표를 업데이트하세요.

## 시작하기

### 요구 사항

- JDK 21+
- Docker / Docker Compose (로컬 인프라: MySQL, Redis, RabbitMQ 등)

### 로컬 인프라 실행

```bash
docker compose -f docker/docker-compose.yml up -d
```

### 빌드

```bash
./gradlew clean build
```

### 실행

```bash
./gradlew :core:bootRun
```

## 모듈 개요

| 모듈 | 역할 |
|---|---|
| `core` | 실행 모듈. web/application/domain/infrastructure 계층을 패키지로 포함 |
| `storage:jpa` | JPA 기반 영속성 어댑터 구현 |
| `storage:mybatis` | MyBatis 기반 영속성 어댑터 구현 |
| `storage:redis` | Redis 어댑터 구현 |
| `storage:rabbitmq` | RabbitMQ Producer/Consumer 구현 |
| `support:common` | 공통 상수, 응답 포맷 등 |
| `support:exception` | 공통 예외 및 예외 코드 |
| `support:logging` | 로깅 설정/유틸 |
| `support:util` | 범용 유틸리티 |

## 코딩/커밋 컨벤션

- 브랜치: `feature/{issue-no}-{설명}`, `fix/{issue-no}-{설명}`
- 커밋 메시지: `[FEAT] ...`, `[FIX] ...`, `[REFACTOR] ...`, `[DOCS] ...`, `[CHORE] ...`
- 패키지/모듈 추가 규칙은 [docs/MULTI_MODULE_GUIDE.md](docs/MULTI_MODULE_GUIDE.md) 참고

## 문서

- [아키텍처 구성도](docs/ARCHITECTURE.md)
- [멀티모듈 가이드](docs/MULTI_MODULE_GUIDE.md)
