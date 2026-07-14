# LangChain 학습 기록

LangChain 기초부터 RAG, Agent/Tool 활용까지 단계별로 학습하며 정리한 개인 학습용 레포입니다.
각 노트북은 코드와 실행 결과, 학습하며 정리한 개념 설명을 함께 담고 있습니다.

## 학습 순서

### 1. [`001_langchain_basic.ipynb`](./src/001_langchain_basic.ipynb) — LangChain 기초
- LCEL(LangChain Expression Language) 기반 Chain 구성 (Prompt + LLM)
- Multiple Chains: 파이프(`|`)와 `RunnableParallel`을 이용한 체인 연결/병렬 실행
- `PromptTemplate`, `ChatPromptTemplate`, `MessagePromptTemplate` 비교
- Message 유형(System/Human/AI) 및 `.format()` vs `.invoke()` 차이 정리

### 2. [`002_langchain_RAG.ipynb`](./src/002_langchain_RAG.ipynb) — RAG 파이프라인
- RAG 5단계 구현: Load → Split → Indexing → Retrieval → Generation
- `WebBaseLoader`로 문서 로드, `RecursiveCharacterTextSplitter`로 청크 분할
- Chroma 벡터 DB에 임베딩 저장 및 `similarity_search()` 활용
- 고정된 RAG 체인과 `create_agent` 기반 ReAct 패턴(자율적 검색 판단) 비교

### 3. [`003_RAG_Agent.ipynb`](./src/003_RAG_Agent.ipynb) — Agent & Tools
- Tavily API를 이용한 실시간 웹 검색 도구 연동 (벡터 DB 없이 최신 정보 조회)
- 도구 사용 유무에 따른 답변 품질 비교 (일반론적 답변 vs 근거 기반 답변)
- Custom `@tool` 정의 및 코드 인터프리터 유무에 따른 LLM 환각(hallucination) 검증
- Middleware(Node-style / Wrap-style 훅)를 활용한 재시도(retry) 로직 구현
- `recursion_limit`을 이용한 무한 루프 방지 및 에이전트 재호출 비용 이슈 정리

## 주요 학습 포인트
- **Chain vs Agent**: 고정된 흐름(Chain)과 LLM이 스스로 도구 사용 여부를 판단하는 흐름(Agent, ReAct 패턴)의 차이를 코드로 직접 비교
- **환각 검증**: 코드 인터프리터 도구 없이 코드 실행을 요청하면 LLM이 실제 실행 없이도 그럴듯한 결과를 생성한다는 점을 실험으로 확인
- **Middleware 비용 구조**: 미들웨어 재시도는 추가 비용이 거의 없지만, 에이전트 재호출은 토큰을 추가로 소모한다는 차이를 실험으로 검증

## 참고
- 사용 모델: Groq (Llama 계열)
- 벡터 DB: Chroma
- 검색 도구: Tavily Search API

---
개인 학습 목적으로 진행한 프로젝트
참고자료 :
- 위키독스 : https://wikidocs.net/231150
- 유튜브 : https://www.youtube.com/watch?v=VwHXDARgsdE&list=PL5bzmUGXvZNQdYaTGYQiGxSllaQ0d1rjW&index=1
- 개인기록(Velog) : https://velog.io/@rldnjs0906/LangChain-%EA%B3%B5%EB%B6%80-%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-%EC%A0%84-3%EB%B2%88-%EC%82%BD%EC%A7%88%ED%95%9C-%EC%9D%B4%EC%95%BC%EA%B8%B0
