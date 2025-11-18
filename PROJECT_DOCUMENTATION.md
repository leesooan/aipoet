# 🎨 인공지능 시인 프로젝트 문서

## 📋 프로젝트 개요

이 프로젝트는 LangChain과 OpenAI API를 활용하여 사용자가 입력한 주제로 한국어 시를 자동으로 생성하는 Streamlit 기반 웹 애플리케이션입니다.

---

## 📁 파일 구조

```
project/
├── app.py              # 메인 애플리케이션 파일
└── requirements.txt    # Python 의존성 패키지 목록
```

---

## 🔍 파일 상세 설명

### 1. app.py

**파일 유형**: Python 애플리케이션 파일  
**목적**: AI 기반 시 생성 웹 인터페이스

#### 주요 기능

1. **API 키 관리**
   - 사이드바를 통한 OpenAI API 키 입력
   - 비밀번호 타입으로 안전하게 입력 처리
   - API 키 유효성 상태 표시

2. **시 생성 인터페이스**
   - 사용자로부터 시의 주제 입력받기
   - "시 작성 요청하기" 버튼으로 생성 시작
   - 생성 중 로딩 스피너 표시

3. **AI 모델 통합**
   - GPT-4o-mini 모델 사용
   - LangChain 프레임워크로 구조화된 처리
   - 한국어 시 생성에 최적화된 프롬프트

#### 코드 구조

```python
# 주요 컴포넌트
├── Streamlit UI 설정
├── 사이드바 (API 키 입력)
├── 메인 화면 (주제 입력)
└── 시 생성 로직
    ├── LLM 초기화
    ├── 프롬프트 템플릿
    ├── 체인 생성
    └── 결과 출력
```

#### 사용된 주요 라이브러리

- `langchain.chat_models`: LLM 모델 초기화
- `langchain_core.prompts`: 프롬프트 템플릿 관리
- `langchain_core.output_parsers`: 출력 파싱
- `streamlit`: 웹 UI 프레임워크
- `os`: 환경 변수 관리

#### 처리 흐름

```
사용자 입력 (주제)
    ↓
API 키 검증
    ↓
LLM 모델 초기화 (GPT-4o-mini)
    ↓
프롬프트 생성 ("아름다운 시를 써 줘")
    ↓
LangChain 체인 실행
    ↓
시 생성 및 화면 출력
```

#### 에러 핸들링

- API 키 미입력 시 에러 메시지
- 주제 미입력 시 에러 메시지
- API 호출 실패 시 상세 에러 정보 제공
- API 키 오류 특별 처리

#### 개선 필요 사항

⚠️ **주의**: 코드 주석에 "Google API Key"로 표기되어 있으나, 실제로는 OpenAI API 키를 사용합니다. 주석 수정이 필요합니다.

---

### 2. requirements.txt

**파일 유형**: Python 의존성 명세 파일  
**목적**: 프로젝트 실행에 필요한 모든 패키지와 버전 정보

#### 주요 패키지 카테고리

##### 🤖 AI/LLM 관련
| 패키지 | 버전 | 용도 |
|--------|------|------|
| `langchain` | 1.0.5 | LLM 애플리케이션 개발 프레임워크 |
| `langchain-core` | 1.0.4 | LangChain 핵심 기능 |
| `langchain-openai` | 1.0.2 | OpenAI 통합 |
| `openai` | 2.7.2 | OpenAI API 클라이언트 |
| `langsmith` | 0.4.42 | LangChain 모니터링 |

##### 🔄 LangGraph 관련
| 패키지 | 버전 | 용도 |
|--------|------|------|
| `langgraph` | 1.0.3 | 상태 기반 워크플로우 |
| `langgraph-checkpoint` | 3.0.1 | 체크포인트 관리 |
| `langgraph-prebuilt` | 1.0.2 | 사전 구축 컴포넌트 |
| `langgraph-sdk` | 0.2.9 | SDK 도구 |

##### 🌐 HTTP/네트워크
| 패키지 | 버전 | 용도 |
|--------|------|------|
| `httpx` | 0.28.1 | 비동기 HTTP 클라이언트 |
| `httpcore` | 1.0.9 | HTTP 핵심 기능 |
| `requests` | 2.32.5 | HTTP 라이브러리 |
| `urllib3` | 2.5.0 | HTTP 클라이언트 |

##### ✅ 데이터 검증
| 패키지 | 버전 | 용도 |
|--------|------|------|
| `pydantic` | 2.12.4 | 데이터 검증 및 설정 |
| `pydantic_core` | 2.41.5 | Pydantic 핵심 |

##### 🛠️ 유틸리티
| 패키지 | 버전 | 용도 |
|--------|------|------|
| `python-dotenv` | 1.2.1 | 환경 변수 관리 |
| `tiktoken` | 0.12.0 | 토큰 계산 |
| `tenacity` | 9.1.2 | 재시도 로직 |
| `tqdm` | 4.67.1 | 진행 표시줄 |

##### 📦 데이터 처리
| 패키지 | 버전 | 용도 |
|--------|------|------|
| `orjson` | 3.11.4 | 빠른 JSON 처리 |
| `ormsgpack` | 1.12.0 | MessagePack 직렬화 |
| `PyYAML` | 6.0.3 | YAML 파싱 |

#### ⚠️ 누락된 패키지

**Streamlit**이 requirements.txt에 명시되어 있지 않습니다. 다음을 추가해야 합니다:

```txt
streamlit>=1.28.0
```

---

## 🚀 설치 및 실행 가이드

### 1. 환경 준비

#### Python 버전 요구사항
- Python 3.8 이상 권장

#### 가상환경 생성 (권장)

```bash
# Windows
python -m venv venv
venv\Scripts\activate

# macOS/Linux
python3 -m venv venv
source venv/bin/activate
```

### 2. 의존성 설치

```bash
pip install -r requirements.txt
pip install streamlit  # requirements.txt에 누락됨
```

### 3. API 키 준비

OpenAI API 키가 필요합니다:
1. [OpenAI Platform](https://platform.openai.com/)에 가입
2. API Keys 섹션에서 새 키 생성
3. 키를 안전하게 보관

### 4. 애플리케이션 실행

```bash
streamlit run app.py
```

실행 후 브라우저가 자동으로 열리며 기본 주소는:
- **로컬**: http://localhost:8501

### 5. 사용 방법

1. **사이드바에서 API 키 입력**
   - "Google API Key를 입력하세요" 필드에 OpenAI API 키 입력
   - 키가 유효하면 성공 메시지 표시

2. **시의 주제 입력**
   - 메인 화면의 입력창에 원하는 시의 주제 입력
   - 예: "가을", "사랑", "그리움" 등

3. **시 생성**
   - "시 작성 요청하기" 버튼 클릭
   - 잠시 대기하면 AI가 생성한 시가 표시됨

---

## 🔧 기술 스택

### 프레임워크 & 라이브러리
- **Frontend**: Streamlit
- **LLM Framework**: LangChain 1.0.5
- **AI Model**: OpenAI GPT-4o-mini
- **Language**: Python 3.x

### 아키텍처 패턴
- **체인 패턴**: `prompt | llm | output_parser`
- **프롬프트 엔지니어링**: 시스템 프롬프트로 역할 정의
- **스트림 기반 UI**: Streamlit의 반응형 인터페이스

---

## 💡 주요 특징

### ✅ 장점
1. **간단한 인터페이스**: 초보자도 쉽게 사용 가능
2. **안전한 API 키 관리**: 비밀번호 타입 입력
3. **실시간 피드백**: 로딩 스피너와 에러 메시지
4. **한국어 최적화**: 한국어 시 생성에 특화
5. **확장 가능성**: LangChain 기반으로 기능 추가 용이

### ⚠️ 제한사항
1. API 키가 세션에만 저장 (영구 저장 없음)
2. 생성 히스토리 미저장
3. 시의 스타일이나 길이 조절 불가
4. 단일 사용자 환경

---

## 🔄 개선 제안

### 우선순위 높음
1. **requirements.txt 수정**: `streamlit` 패키지 추가
2. **주석 수정**: "Google API Key" → "OpenAI API Key"
3. **환경변수 처리 개선**: `.env` 파일 사용 고려

### 추가 기능 제안
1. **시 스타일 선택**: 자유시, 정형시, 하이쿠 등
2. **생성 히스토리**: 이전에 생성한 시 저장 및 조회
3. **다운로드 기능**: 생성된 시를 텍스트 파일로 저장
4. **다양한 모델 지원**: Claude, Gemini 등 선택 가능
5. **길이 조절**: 짧은 시, 긴 시 선택
6. **감정 선택**: 슬픔, 기쁨, 그리움 등 감정 선택

---

## 📝 코드 예시

### 기본 사용 예시

```python
# 프롬프트 생성
prompt = ChatPromptTemplate.from_messages([
    ("system", "You are a helpful assistant that writes beautiful Korean poetry."),
    ("user", "{input}")
])

# 체인 생성 및 실행
chain = prompt | llm | output_parser
result = chain.invoke({"input": "가을에 대한 아름다운 시를 써 줘"})
```

### 커스텀 프롬프트 예시

```python
# 더 구체적인 프롬프트
prompt = ChatPromptTemplate.from_messages([
    ("system", "당신은 한국의 전통 시인입니다. 정서적이고 서정적인 시를 쓰세요."),
    ("user", "{style} 스타일로 {topic}에 대한 {length} 시를 써주세요.")
])
```

---

## 🐛 트러블슈팅

### 문제: API 키 오류
```
해결: OpenAI API 키가 올바른지 확인하고, 계정에 크레딧이 있는지 확인
```

### 문제: ModuleNotFoundError
```bash
# 해결: 모든 의존성 재설치
pip install -r requirements.txt --force-reinstall
```

### 문제: Streamlit 실행 안됨
```bash
# 해결: Streamlit 설치 확인
pip install streamlit
streamlit --version
```

---

## 📚 참고 자료

### 공식 문서
- [LangChain 문서](https://python.langchain.com/)
- [OpenAI API 문서](https://platform.openai.com/docs)
- [Streamlit 문서](https://docs.streamlit.io/)

### 관련 튜토리얼
- [LangChain Quickstart](https://python.langchain.com/docs/get_started/quickstart)
- [Streamlit 튜토리얼](https://docs.streamlit.io/library/get-started)

---

## 📄 라이선스

이 프로젝트는 사용된 라이브러리들의 라이선스를 따릅니다:
- LangChain: MIT License
- OpenAI: OpenAI Terms of Use
- Streamlit: Apache License 2.0

---

## 👥 기여 방법

1. 이슈 등록
2. 기능 개선 제안
3. 버그 리포트
4. Pull Request

---

## 📞 문의

프로젝트 관련 문의사항이 있으시면 이슈를 등록해 주세요.

---

**마지막 업데이트**: 2025년 11월 18일  
**버전**: 1.0.0
