<p>
<img src="./assets/mireu-cool-skylight.png" width="100%" alt="Mireu Park · Software Engineer">
</p>

## 만들고, 흐름을 살펴보고, 근거를 남깁니다.

박미르 · 백엔드와 AI 서비스 연동을 공부하며 프로젝트로 구현합니다.

<p>
  <img src="./assets/stack-backend.svg" width="310" alt="Backend: Java, FastAPI, SQLite">
  <img src="./assets/stack-ai.svg" width="330" alt="AI and Web: Python, React, LLM API integration">
</p>

### Backend · 데이터가 흐르는 시스템

**Java / Spring Boot · MySQL · Redis · Kafka**

주문 요청이 여러 구성 요소를 지나는 과정을 살펴봅니다. 로컬 환경에 장애를 주입하고 근거를 수집해, 원인과 복구 전후를 비교합니다.

→ [IncidentLens에서 시스템 흐름과 장애 실험 보기](https://github.com/NIGHTPURI/incident-lens)

### AI Integration · 규칙과 모델의 역할 나누기

**Java 규칙 · 선택적 모델 API 호출 · 개인정보 마스킹**

명확한 신호는 규칙으로 처리하고, 문맥 판단이 필요한 후보에만 모델 API를 호출합니다. 전화번호·이메일 마스킹과 외부 API 장애 정책을 함께 다룹니다.

→ [Chat Moderation에서 판정 흐름과 평가 범위 보기](https://github.com/NIGHTPURI/Chat-Moderation)

### Service · 문서에서 서비스 기능까지

**FastAPI · React · SQLite**

PDF 텍스트 추출, 요약, 문서 기반 질문 응답을 연결합니다. 처리 결과를 저장하고 이미 저장한 요약을 재사용합니다.

→ [DocInsight AI에서 문서 처리 구조와 구현 한계 보기](https://github.com/NIGHTPURI/docinsight-ai)

### Practice · 알고리즘과 구현 연습

알고리즘 풀이와 구현 연습 · [CodeTree ↗](https://github.com/NIGHTPURI/CodeTree) · [Practice ↗](https://github.com/NIGHTPURI/Practice)

### Engineering evidence · 실패를 재현하고 검증하기

2026-11-01 개선 커밋에서는 입력 경계, 요청 격리, 배포 산출물, AI에 전달하는 문맥을 보완했습니다. 아래 링크는 검증한 작업 브랜치의 기록이며 기본 브랜치 병합 여부와 구분합니다.

| 프로젝트 | 개선한 문제 | 재현 가능한 근거 |
|---|---|---|
| IncidentLens | 소유 세션이 없는 장애 상태가 다른 요청에 적용되는 문제 | [격리 회귀·인프라 통합·Compose 실험](https://github.com/NIGHTPURI/incident-lens/blob/b8df3bb4ca540b4c858ca3974dd109e9de3f0292/docs/FAULT_ISOLATION_20261101.md) |
| Chat Moderation | 긴 이메일·URL에서 발생하는 StackOverflow | [458개 테스트·기존 판정 비교·배포 JAR 소비자](https://github.com/NIGHTPURI/Chat-Moderation/blob/9ed14f5895b30769e016e6d4524de1e32f334281/docs/REGEX_RESILIENCE_20261101.md) |
| DocInsight AI | 앞 12,000자 이후 내용을 질문할 수 없던 처리 흐름 | [전체 문서 검색·34개 테스트·브라우저 확인](https://github.com/NIGHTPURI/docinsight-ai/blob/6313801cf6742ac663fb8b3fe130d20d74aebb77/docs/DOCUMENT_EVIDENCE_20261101.md) |
| Job Skill Radar | 외부 API 응답 본문을 제한 없이 읽던 처리 | [바이트 한도·462개 테스트·서비스 중단 범위](https://github.com/NIGHTPURI/job-skill-radar/blob/633d1fd06862f5ad78cca27df225acf806662fff/docs/RESPONSE_BUDGET_20261101.md) |

[변경 전후, CI 실행, 검증 한계를 한 문서에서 보기](PORTFOLIO_EVIDENCE.md). 테스트 개수는 해당 저장소의 전체 회귀 테스트 수이며, 모두 이번에 새로 작성했다는 의미는 아닙니다. 실제 모델의 정확도나 운영 성능을 뜻하지도 않습니다.

---

<sub>IncidentLens는 AI 코딩 도구를 활용해 개발하며 설계와 검증 과정을 기록합니다. Chat Moderation과 DocInsight AI의 AI 기능은 외부 모델 API 연동입니다.</sub>
