# Git Commit Convention

## 🎮 DirectX 12 Git Convention

### ✅ 커밋 메시지 형식

```
[TAG] 한 줄 요약 (영어, 50자 이내)

- 상세 설명 1
- 상세 설명 2 (선택)
```

### 📌 예시

```bash
[Add] Implement command queue and swap chain

[Fix] Prevent crash on window resize
- Caused by uninitialized RTV
- Recreate descriptor heap during resizing

[Refactor] Separate frame resource logic into class

[Docs] Add build instructions to README.md
```

### 📌 작성 규칙

- **무조건 영어**로 작성
- 커밋 제목은 **현재 시제**로 작성 (예: Add, Fix, Refactor)
- 본문은 - 로 시작하는 리스트 형식으로 작성 (선택 사항)
- 제목은 **짧고 명확하게** 작성

---

## 🏷️ 커밋 태그 종류

| 태그 | 설명 |
| --- | --- |
| `[Init]` | 초기 프로젝트 설정, 구조 생성 |
| `[Add]` | 새로운 기능, 클래스, 파일 추가 |
| `[Update]` | 기존 기능 수정 또는 개선 |
| `[Fix]` | 버그 수정 |
| `[Remove]` | 코드, 리소스, 기능 삭제 |
| `[Refactor]` | 리팩토링 (동작 변경 없이 구조 개선) |
| `[Optimize]` | 성능 최적화 |
| `[Docs]` | 문서 추가 및 수정 |
| `[Chore]` | 설정, 의존성, 기타 유지보수 작업 |
| `[Test]` | 테스트 코드 추가 및 수정 |

---

## 🔀 브랜치 네이밍 규칙

```
<타입>/<짧은-설명>
```

- 모든 브랜치 이름은 **소문자**, **kebab-case** 사용
- 작업 목적에 따라 명확한 prefix(type)를 붙임

| 타입 | 설명 | 예시 |
| --- | --- | --- |
| `feature/` | 새로운 기능 개발 | `feature/weapon-system` |
| `bugfix/` | 일반적인 버그 수정 | `bugfix/camera-clip-issue` |
| `refactor/` | 코드 구조 개선 | `refactor/player-input` |
| `hotfix/` | 배포 전 긴급 수정 | `hotfix/loading-screen-bug` |
| `release/` | 릴리즈 준비 | `release/v1.0.0` |
| `test/` | 실험, 테스트 목적 작업 | `test/lighting-tweak` |
| `docs/` | 문서 작성 및 수정 작업 | `docs/update-readme` |
| `chore/` | 설정 파일, 빌드 등 기타 작업 | `chore/update-gitignore` |

> ❗ hotfix/와 release/는 보통 main 또는 release 브랜치 기반으로 작업
>

*이 컨벤션은 DX12 게임 엔진 프로젝트의 커밋 히스토리 추적 등을 향상시키기 위한 가이드라인입니다.*