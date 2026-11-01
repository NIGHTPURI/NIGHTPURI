# 검증 가능한 프로젝트 개선 · 2026-11-01

백엔드·AI 서비스 연동 프로젝트에서 기능 설명과 함께 **어떤 실패를 재현했고, 어느 범위까지 검증했는지**를 확인할 수 있도록 정리했다. 모델 학습, 운영 트래픽, 매출 또는 실사용자 수를 증명하는 자료는 아니다.

아래 네 CI 실행은 2026-11-01에 연결된 각 커밋에서 모두 성공한 것을 확인했다. 이후의 변경이나 기본 브랜치 상태에 대한 보증과는 구분한다.

## IncidentLens: 장애 상태의 소유권을 명시하기

- 변경 전: Redis 장애 상태의 `sessionId`가 null이면 모든 요청에 적용될 수 있었고, JSON `null`은 소비자에서 NPE를 유발할 수 있었다.
- 변경 후: 유효한 소유 세션과 요청 세션이 정확히 일치할 때만 적용한다. JSON null은 기존 읽기 실패 metric을 남기고 비활성 상태로 처리한다.
- 검증: 로컬 common/demo-api/demo-worker 25개 테스트. GitHub Actions는 backend 인프라 통합 테스트, web 테스트·빌드·브라우저, Docker Compose degraded/recovered 실험을 실행한다.
- 한계: 장애 주입 실험의 격리 경계를 보완한 것으로 운영 서비스의 가용성 수치나 장애 감소율을 측정한 것은 아니다.
- [구현 커밋](https://github.com/NIGHTPURI/incident-lens/commit/b8df3bb4ca540b4c858ca3974dd109e9de3f0292) · [CI 실행](https://github.com/NIGHTPURI/incident-lens/actions/runs/41294110343)

## Chat Moderation: 긴 입력과 패키징을 실제로 검증하기

- 변경 전: 10,000개 라벨의 이메일·URL에서 정규식 엔진의 반복 그룹 역추적으로 StackOverflow가 발생했다. 먼저 추가한 회귀 테스트 5개 중 4개가 기존 코드에서 실패했다.
- 변경 후: possessive 반복과 suffix lookahead로 재귀적 역추적을 줄이되 기존 탐지 범위와 마스킹 위치를 유지한다.
- 검증: Java 21 전체 458개 테스트, 고정 주소 25개와 seed 5,000개 × 3변형의 차등 비교. 테스트 classpath 없이 빌드된 production JAR만으로 별도 소비자를 컴파일·실행하고 기본 사전·공개 API·가짜 provider를 확인한다.
- 한계: 모든 가능한 문자열에 대한 정규식 동치나 선형 시간 증명은 아니다. 이번 검증에서 실제 모델 호출·품질 재평가는 하지 않았다.
- [구현 커밋](https://github.com/NIGHTPURI/Chat-Moderation/commit/9ed14f5895b30769e016e6d4524de1e32f334281) · [CI 실행](https://github.com/NIGHTPURI/Chat-Moderation/actions/runs/41295197046)

## DocInsight AI: 모델이 볼 수 있는 문맥을 보여주기

- 변경 전: Q&A와 요약 모두 첫 12,000자만 입력으로 사용했다. API 키가 없으면 기본 문서 기능을 실행하기도 어려웠고 업로드 예산·회귀 테스트가 없었다.
- 변경 후: 전체 텍스트를 어휘 검색해 최대 4개의 원문 구간을 제공한다. 키 없이 업로드·검색 가능, 일치 없으면 모델을 호출하지 않는다. 실제 파일·본문·PDF 페이지·추출 문자 한도와 외부 오류 처리를 추가했다.
- 검증: Python 34개 테스트, 실제 SDK + httpx MockTransport로 요청·응답 계약 검증, React 린트·빌드. 브라우저에서 35,877자 합성 PDF의 마지막 해지 조건을 검색하고 정확한 문자 위치, 390px 화면, 키 누락 안내를 확인했다.
- 한계: 원문 구간은 모델에 제공한 문맥이며 출력의 사실성을 보장하지 않는다. 요약은 여전히 앞 12,000자다. OCR·인증·벡터 검색·실제 모델 품질 평가는 없다. npm 개발 도구 체인에는 upstream 패치가 필요한 moderate advisory 6개가 남아 있다.
- [구현 커밋](https://github.com/NIGHTPURI/docinsight-ai/commit/6313801cf6742ac663fb8b3fe130d20d74aebb77) · [CI 실행](https://github.com/NIGHTPURI/docinsight-ai/actions/runs/41295261487)

## Job Skill Radar: 외부 데이터의 크기를 신뢰하지 않기

- 변경 전: Work24 응답을 `.read()`로 제한 없이 읽었다. 약 5 MiB의 합성 응답도 처리 경로로 들어갔다.
- 변경 후: 4 MiB + 1바이트까지만 읽고 초과하면 decode/XML 처리 전에 `response_too_large`로 거부한다. 오류에는 인증 키나 응답 본문을 포함하지 않는다.
- 검증: 정확한 경계·1바이트 초과·UTF-8 실제 바이트·상세 endpoint·오류 비밀정보·읽기 크기를 검증하는 6개 회귀를 추가했다. v2 전체 462개 테스트와 키 없는 CI.
- 한계: Work24 개인 계정의 API 이용 자격 문제로 중단한 상태를 유지한다. 서비스 재개, 현재 채용 데이터 확보, 전체 프로세스 메모리·시간 상한을 주장하지 않는다.
- 기준 브랜치: `refactor/v2`. 기존 대규모 v2 변경을 main에 합치는 작업과 구분한다.
- [구현 커밋](https://github.com/NIGHTPURI/job-skill-radar/commit/633d1fd06862f5ad78cca27df225acf806662fff) · [CI 실행](https://github.com/NIGHTPURI/job-skill-radar/actions/runs/41293883200)

## 검토 방식

Kiro CLI에서 실제 `claude-opus-5.5`와 세 차례 토론했다. 1차는 커리어 관점의 우선순위와 중단된 프로젝트의 범위, 2차는 재현한 버그와 정규식 호환성·JAR 검증, 3차는 최종 코드와 업로드 취소·SDK 계약을 검토했다. 모델 의견을 실행 결과로 취급하지 않고 회귀 테스트와 브라우저·CI로 확인했다.

회귀 테스트는 누적 전체 개수다. 기존 통과 테스트를 이번에 새로 구현한 것으로 세지 않는다. 실제 AI API 요금·모델 정확도·서비스 운영 실적은 이번 검증 대상이 아니다. 모든 변경은 개별 작업 브랜치로 제공하며 기본 브랜치에 병합했다는 뜻은 아니다.
