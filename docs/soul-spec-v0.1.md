# ClawSouls 패키지 스펙 v0.1

## soul.json

Soul 패키지의 메타데이터 파일.

```json
{
  "name": "senior-devops-engineer",
  "displayName": "Senior DevOps Engineer",
  "version": "1.0.0",
  "description": "Infrastructure-obsessed DevOps engineer with strong opinions on CI/CD, monitoring, and incident response.",
  "author": {
    "name": "TomLee",
    "github": "TomLeeLive"
  },
  "license": "Apache-2.0",
  "tags": ["devops", "infrastructure", "cicd", "monitoring"],
  "category": "work/devops",
  "compatibility": {
    "openclaw": ">=2026.2.0",
    "models": ["anthropic/*", "openai/*"]
  },
  "files": {
    "soul": "SOUL.md",
    "identity": "IDENTITY.md",
    "agents": "AGENTS.md",
    "heartbeat": "HEARTBEAT.md",
    "userTemplate": "USER_TEMPLATE.md",
    "avatar": "avatar/avatar.png"
  },
  "skills": [
    "github",
    "healthcheck"
  ],
  "repository": "https://github.com/TomLeeLive/clawsoul-devops"
}
```

---

## 필수 필드

| 필드 | 타입 | 설명 |
|------|------|------|
| `name` | string | 고유 식별자 (kebab-case) |
| `displayName` | string | 표시명 |
| `version` | semver | 버전 |
| `description` | string | 한 줄 설명 (160자 이내) |
| `author` | object | 제작자 정보 |
| `license` | string | SPDX 라이선스 식별자 |
| `tags` | string[] | 검색 태그 (최대 10개) |
| `category` | string | 카테고리 경로 |
| `files.soul` | string | SOUL.md 경로 |

## 선택 필드

| 필드 | 타입 | 설명 |
|------|------|------|
| `compatibility.openclaw` | string | 최소 OpenClaw 버전 |
| `compatibility.models` | string[] | 권장 모델 (glob 패턴) |
| `files.identity` | string | IDENTITY.md 경로 |
| `files.agents` | string | AGENTS.md 경로 |
| `files.heartbeat` | string | HEARTBEAT.md 경로 |
| `files.userTemplate` | string | USER 템플릿 경로 |
| `files.avatar` | string | 아바타 이미지 경로 |
| `skills` | string[] | 권장 Skill 목록 |
| `repository` | string | 소스 저장소 URL |

---

## 카테고리 체계

```
work/
  engineering/frontend
  engineering/backend
  engineering/fullstack
  engineering/gamedev
  devops
  data
  pm
  writing
creative/
  design
  storytelling
  music
education/
  programming
  language
  science
lifestyle/
  assistant
  health
  cooking
enterprise/
  support
  onboarding
  review
```

---

## CLI 명령어 (제안)

```bash
# Soul 설치
openclaw soul install senior-devops-engineer

# Soul 검색
openclaw soul search "game dev"

# 설치된 Soul 목록
openclaw soul list

# Soul 적용 (현재 에이전트에)
openclaw soul use senior-devops-engineer

# Soul 제거
openclaw soul remove senior-devops-engineer

# Soul 패키지 생성
openclaw soul init

# Soul 배포
openclaw soul publish
```

---

## 설치 동작

`openclaw soul install <name>` 실행 시:

1. ClawSouls 레지스트리에서 패키지 다운로드
2. `~/.openclaw/souls/<name>/` 에 저장
3. `openclaw soul use <name>` 시:
   - SOUL.md → workspace에 복사
   - IDENTITY.md → workspace에 복사
   - AGENTS.md → workspace에 병합 (사용자 설정 유지)
   - USER_TEMPLATE.md → USER.md 없을 시에만 복사
   - avatar → workspace에 복사
4. 기존 파일 백업: `~/.openclaw/souls/_backup/`

---

## 보안 고려사항

- Soul 패키지에 실행 코드 포함 금지 (마크다운만)
- AGENTS.md의 외부 액션 규칙은 사용자 확인 후 적용
- 퍼블리시 시 자동 스캔 (프롬프트 인젝션 탐지)
- 리포트 & 신고 시스템
