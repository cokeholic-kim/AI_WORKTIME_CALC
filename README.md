# AI_WORKTIME_CALC

근무 기록 텍스트를 **Gemini API**로 파싱해 JSON/테이블/차트로 보여주는 단일 HTML 웹앱입니다.

## 주요 기능

- 자유 형식 근무 텍스트 입력
- Gemini 모델 자동 선택(가능한 최신 Flash 모델 탐색)
- 결과를 3가지 뷰로 제공
  - JSON
  - 테이블(일자별 세션/합계)
  - 막대 차트(Chart.js)
- 총 근무시간 자동 계산
- API Key 브라우저 로컬 저장(localStorage)

## 파일 구조

```text
.
├── index.html        # HTML/CSS/JS가 한 파일에 포함된 SPA 형태
└── README.md
```

## 동작 개요

1. 사용자가 근무 로그 텍스트 입력
2. Gemini API Key 입력
3. 모델 목록 API(`/v1beta/models`)를 조회해 사용 가능한 최신 Flash 모델 선택
4. `generateContent` 호출로 텍스트를 정규화된 JSON으로 변환
5. 변환 결과를 JSON/테이블/차트로 렌더링

## JSON 출력 스키마(요약)

```json
[
  {
    "date": "YYYY-MM-DD",
    "dayOfWeek": "월|화|수|목|금|토|일",
    "sessions": [
      {
        "start": "HH:MM",
        "end": "HH:MM",
        "durationMinutes": 70,
        "note": "optional"
      }
    ],
    "totalMinutes": 240
  }
]
```

## 실행 방법

별도 빌드 없이 정적 파일로 실행 가능합니다.

- VSCode Live Server 또는 임의의 정적 서버에서 `index.html` 오픈
- Gemini API Key 입력 후 사용

## 사용 기술

- Vanilla JavaScript
- Chart.js (CDN)
- Gemini REST API (`v1beta/models`, `:generateContent`)

## 보안/운영 주의사항

- API Key는 localStorage에 저장됩니다. 공유 PC에서는 사용 후 삭제하세요.
- 프로덕션 배포 시에는 API Key를 클라이언트에 노출하지 않도록 서버 프록시 구조를 권장합니다.
- 단일 파일 구조 특성상 기능 확장 시 JS/CSS 분리를 권장합니다.

## 개선 아이디어

- 404/네트워크 오류 UX 강화
- 입력 템플릿 예시 프리셋 제공
- 결과 내보내기(JSON/CSV)
- API Key 저장 옵션(세션 저장/비저장) 선택화

---

원본 소스: 서버 `html/index.html`에서 수집한 파일을 기반으로 구성했습니다.
