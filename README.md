# 박미르 · Mireu Park

**Software Engineer | Backend & AI**

메시지와 문서를 처리하는 소프트웨어를 만듭니다. Java 라이브러리의 명확한 결과 계약과 Python API의 데이터 저장 흐름을 구현하고, 외부 AI 모델을 연결할 때 호출 범위와 검증 근거를 함께 정리합니다.

[대표 프로젝트](#featured-projects) · [경험과 관심](#backend--ai) · [기술](#core-technologies) · [알고리즘 학습](#algorithm-learning)

---

## Featured Projects

### 01 · [Chat Moderation](https://github.com/NIGHTPURI/Chat-Moderation)

> **대표 프로젝트 · Java library**

명시적인 규칙과 문맥 판단을 함께 다루는 **Java 21 채팅 moderation 라이브러리**입니다.

- Aho-Corasick 다중 패턴 검색, 우회 표현 정규화, 전화번호·이메일 마스킹을 구현했습니다.
- 불확실한 메시지에 외부 모델 API를 선택적으로 호출하고, 실패 시 동작을 정책으로 분리했습니다.
- `ALLOW` / `MASK` / `BLOCK` 결과 계약과 저장 전 처리 순서를 simulation 테스트로 표현했습니다.
- [320건 합성 holdout 평가 기록](https://github.com/NIGHTPURI/Chat-Moderation/blob/main/docs/FINAL_LUNA_EVALUATION.md)이 있습니다. 기존 실험 보고서이며 실제 서비스 트래픽 성능이나 이번 문서 정리에서 재실행한 결과는 아닙니다.

![Java 21](https://img.shields.io/badge/Java-21-B45309?style=flat)
![AI: API integration](https://img.shields.io/badge/AI-API_integration-374151?style=flat)

`Aho-Corasick` · `JUnit` · `OpenAI API`

### 02 · [DocInsight AI](https://github.com/NIGHTPURI/docinsight-ai)

> **보조 프로젝트 · Document API & UI**

PDF 업로드부터 **텍스트 추출·요약·질문 응답·DB 저장·React UI**까지 연결한 보조 프로젝트입니다.

- FastAPI API와 SQLAlchemy·SQLite로 문서·요약·질문 이력을 저장합니다.
- PyMuPDF로 추출한 텍스트의 앞 12,000자를 외부 모델 API에 전달합니다.
- embedding 검색을 사용하는 RAG나 OCR은 구현하지 않았습니다. 자동 테스트와 정량적인 답변 품질 평가는 남은 작업입니다.

![FastAPI](https://img.shields.io/badge/FastAPI-00796B?style=flat&logo=fastapi&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=flat&logo=react&logoColor=61DAFB)

`Python` · `SQLAlchemy` · `SQLite` · `PyMuPDF`

---

## Backend & AI

- **Backend 경험** — 웹 프레임워크와 분리된 Java moderation core, FastAPI의 Router / Service / Repository 구조, SQLAlchemy·SQLite 기반 문서와 질문 이력 저장을 구현했습니다.
- **AI 경험** — 모델 API를 연결해 채팅 문맥 판단과 PDF 요약·질문 응답을 구현했습니다. 채팅 프로젝트에서는 선택적 API 호출, 개인정보 마스킹, provider 장애 정책과 합성 데이터 평가를 다뤘습니다. 직접 모델 학습·파인튜닝 경험으로 소개하지 않습니다.
- **앞으로의 관심** — 외부 AI API의 실패와 지연을 다루는 Backend 설계, 평가 데이터의 대표성, 문서 기반 응답의 근거 검증에 관심이 있습니다.

## Core Technologies

| 분야 | 프로젝트에서 사용한 기술 |
|---|---|
| 언어 | Java, Python, JavaScript |
| Backend / Data | FastAPI, SQLAlchemy, SQLite, Java HttpClient |
| AI 연동 / 문서 처리 | OpenAI API, PyMuPDF |
| 검증 / UI | JUnit, React, Vite |

## Algorithm Learning

서비스 프로젝트와 별도로 문제 풀이와 자료구조 선택을 연습합니다. 아래 저장소의 채점 정보는 기존 제출 기록이며 전체 재채점 결과가 아닙니다.

- [CodeTree](https://github.com/NIGHTPURI/CodeTree) — Python·Java 기초 문법, 함수, 격자 탐색·시뮬레이션 학습
- [Practice](https://github.com/NIGHTPURI/Practice) — Python 백준·SWEA 풀이와 복습 기록
