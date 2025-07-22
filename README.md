# koreanair_handson_250724

## Hands On 세션 소개

### 01. Genie 실습

1. **데이터 준비**

   - '/Data' 경로의 Parquet 파일 다운로드
2. **스키마 생성**

   - Unity Catalog 내 개별 스키마 생성
3. **테이블 생성**

   - 데모용 스키마에 데이터 업로드하여 테이블 생성
   - AI Assistant 기반 메타데이터 생성
4. **Genie Space 구성**

   - 생성된 테이블 기반의 Genie Space 구성
   - Instruction 설정
   - Sample SQL Queries 설정

### 02. RAG Agent 구성

[노트북 문서 Link](https://docs.databricks.com/aws/en/notebooks/source/generative-ai/unstructured-data-pipeline.html)

##### 🔍 비정형 데이터 파이프라인 개요 (Databricks 기반)

이 노트북은 **비정형 문서 데이터를 처리하여 Generative AI 검색 및 요약 파이프라인**을 구성하는 전체 흐름을 시연합니다.

주요 목적은 **문서 → 벡터 인덱스 → RAG 검색**으로 이어지는 LLM 기반 응답 시스템을 구축하는 것입니다.

###### 📌 주요 수행 작업

1. **문서 업로드 및 수집**

   - PDF, Word 등 다양한 비정형 문서를 수집하고 Databricks Volumes에 저장
2. **문서 파싱 및 청크 분할**

   - LangChain을 활용하여 문서를 의미 단위(Chunk)로 분할
   - Chunk 단위로 메타데이터와 함께 구조화
3. **임베딩 벡터 생성**

   - Foundation 모델(OpenAI 또는 Databricks Foundation Model)을 활용한 임베딩 생성
   - Unity Catalog에 등록된 모델 또는 외부 API 사용
4. **벡터 인덱스에 저장**

   - Databricks Vector Search를 통해 벡터 인덱스 생성
   - 쿼리 시 유사한 문서 Chunk 검색 가능
5. **질문 응답 (RAG) 데모**

   - 사용자가 입력한 질문에 대해 관련 문서를 검색 후, LLM이 응답 생성

### 03. MCP with Databricks

##### 🧠 Claude Desktop + Genie 연결 테스트 개요

Databricks의 Managed MCP(Model Context Protocol) 기능을 활용하여 **Claude Desktop 애플리케이션에서 Genie 기반 LLM 툴 호출을 테스트**하는 워크플로우입니다.

##### 🎯 목표

- Claude Desktop에서 Databricks Genie MCP 서버에 연결
- Genie에 정의된 툴 및 워크플로우를 통해 자연어 질의 처리
- Databricks 내 엔드포인트 및 툴 호출 성능 검증

---

##### 📌 주요 구성 요소

1. **Managed Datbricks MCP 유형 확인**
   🔗 [주요 MCP 서버 타입 및 엔드포인트](https://docs.databricks.com/aws/en/generative-ai/mcp#managed-mcp-servers) 

| MCP 서버 유형                     | 기능 설명                                                          | 엔드포인트 예시                                                           |
| --------------------------------- | ------------------------------------------------------------------ | ------------------------------------------------------------------------- |
| **Vector Search**           | Unity Catalog 내 Vector Index를 검색하여 유사 문서 쿼리 가능       | `https://<workspace-host>/api/2.0/mcp/vector-search/{catalog}/{schema}` |
| **Unity Catalog Functions** | UC에 등록된 사용자 정의 함수(UDF, Stored Procedure 등)를 실행 가능 | `https://<workspace-host>/api/2.0/mcp/functions/{catalog}/{schema}`     |
| **Genie Space**             | 지정된 Genie Space에 대해 구조화된 데이터에 대한 질의 및 분석 수행 | https://`<your-workspace-hostname>`/api/2.0/mcp/genie/{genie_space_id}  |

2. **Genie MCP URL 및 Token 확보**

- `https://<workspace-host>/2.0/mcp/genie/<server-id>` 형태의 URL 사용
- PAT(Personal Access Token) 발급 `dapi...` 형식의 인증 토큰 필요

3. **Claude Desktop 설정**

- 모델 설정에서 **MCP URL**과 **Bearer Token**을 입력
- 클라이언트 → MCP 서버로 요청 전송되도록 설정

4. **Tool 테스트**

- Claude Desktop에서 자연어로 명령 입력
- Genie에 정의된 Tool (예: SQL 실행, 웹 검색, 파일 요약 등)이 실행되는지 확인

---
