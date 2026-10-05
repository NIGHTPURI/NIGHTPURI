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

---

<sub>IncidentLens는 AI 코딩 도구를 활용해 개발하며 설계와 검증 과정을 기록합니다. Chat Moderation과 DocInsight AI의 AI 기능은 외부 모델 API 연동입니다.</sub>
