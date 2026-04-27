---
name: dooray-task-to-docs-update
description: 사내 이슈 트래커(Dooray) 업무 번호로부터 가이드 수정 요청을 분석해 OCR-docs alpha PR로 가는 워크플로우. dooray-cli로 본문/댓글을 조회하고 docs URL을 ko/<file>.md 경로로 매핑한 뒤 alpha 기반 PR을 생성한다.
---

# Dooray 업무 → OCR-docs PR 워크플로우

OCR 가이드 수정 요청 한 건을 Dooray 업무 조회부터 alpha PR 생성, 댓글 회신까지 일관된 흐름으로 처리한다.

## 트리거 예시

- "Dooray <project-code> <post-number> 처리해줘"
- "<project-code> 업무 N번 가이드 수정안 검토"

## 사전 요구

- `dooray-cli` 설치 및 인증 — https://github.com/jon890/dooray-cli
- OCR-docs fork + upstream(`TOAST-DOCS/OCR`) remote 설정
- (선택) OCR API 코드 저장소 클론 — 필드/검증 로직 검증용
- (선택) `gh` CLI 인증 — PR 생성/리뷰 코멘트 조회

## Step

### 1. 업무 본문/댓글 조회

```bash
dooray post get <project-code> <post-number>
dooray --json post comment list <project-code> <post-number>
```

`--json`은 댓글 마크다운 본문을 그대로 받아오기 위함. 본문/댓글에서 `https://docs.alpha-nhncloud.com/...` 또는 `https://docs.nhncloud.com/...` URL을 추출해 가이드 파일로 매핑한다.

### 2. URL → 파일 매핑

| URL 경로 (예: `/ko/AI%20Service/OCR/ko/<segment>/`) | OCR-docs 파일 |
|---|---|
| `overview` | `ko/overview.md` |
| `document-ocr-console-guide` | `ko/document-ocr-console-guide.md` |
| `document-ocr-api-guide-v2.0` | `ko/document-ocr-api-guide-v2.0.md` |
| `document-ocr-api-guide-v2.1` | `ko/document-ocr-api-guide-v2.1.md` |
| `general-ocr-*` / `document-ai-*` | 같은 패턴으로 추론 |

URL 끝의 `#_NN` 같은 fragment는 페이지 내 섹션 앵커이므로 파일 매핑에는 영향 없음(어느 섹션을 손댈지 본문/댓글 텍스트로 판단).

자세한 파일 명명/버전 규칙은 `api-guide` 스킬 참조.

### 3. (필요 시) 코드 검증

API 필드 표나 검증 규칙이 변경 대상이면 OCR API 저장소에서 관련 클래스를 확인해 가이드와 코드의 정합성을 맞춘다.

```bash
grep -rln "<keyword>" <ocr-api-repo>/src --include="*.java"
```

특히 요청 모델 `validate()` 메서드와 `to...Bean()` 빌더에서 idType/타입별 필수 필드를 확인하면 가이드 표가 정확한지 검증할 수 있다. 예: 어떤 필드가 정말 특정 idType 전용인지.

### 4. 변경안 옵션 도출 + 사용자 컨펌

같은 요청도 보수적/적극적 안이 갈릴 때가 많다.

- A안: 댓글에 명시된 변경만 (보수적)
- B안: 전체 의도에 맞춘 정리 (예: 사용 안 하는 idType 행 함께 제거)
- C안: 문장 자체 삭제 (의미 변화 큰 경우 비추천)

각 안의 영향과 트레이드오프를 정리해 사용자에게 어느 안으로 갈지 컨펌받는다. 사용자가 명시 동의하기 전에는 큰 의미 변경을 임의로 적용하지 않는다.

### 5. 작업 브랜치 생성 (alpha 기반)

OCR-docs는 alpha → beta → real 환경 흐름이므로 모든 변경은 alpha에 먼저 들어간다.

```bash
git checkout alpha
git fetch upstream
git reset --hard upstream/alpha
git checkout -b feature/<topic>
```

브랜치명: `feature/<kebab-case-topic>` (예: `feature/remove-foo-from-bar`).

### 6. 편집 + 커밋

- 한국어부터 적용. 다국어는 머지 후 별도 PR(`docs-i18n-sync` 스킬).
- 커밋 메시지: 한국어, `type(scope): <한국어 설명>` 형식
- 커밋 메시지·PR 본문에 **외부에 공개되면 안 되는 정보**(사내 시스템 링크, 사내 식별자, 멤버 이름) 절대 포함 금지 — OCR-docs는 외부 공개 저장소

```
feat(ko): <한국어 변경 요지>

- 변경 1
- 변경 2
- 변경 3
```

표 영역 변경 시 컬럼 폭(공백) 가능한 한 유지. Edit 도구로 다중 행 교체할 때는 trailing space까지 정확히 매치해야 한다.

### 7. push + PR 생성

```bash
git push -u origin feature/<topic>
gh pr create --repo TOAST-DOCS/OCR --base alpha \
  --head <fork-owner>:feature/<topic> \
  --title "docs(ko): <영문 한 줄 요약>" \
  --body "$(cat <<'EOF'
## 배경
<한국어로 변경 배경 — 외부 노출 가능 형태>

## 변경 내용
파일별 변경 요약

## 검토 노트
- 영향 범위 / 정합성 검증 결과
- 코드 검증 사실(있다면)

## 적용 범위
- 본 PR 한국어만 / 다국어 후속 PR 예정
EOF
)"
```

PR 본문 양식: 배경 / 변경 내용 / 검토 노트 / 적용 범위 + (선택) 별건 알림.

### 8. Dooray 안내 댓글

```bash
cat <<'EOF' | dooray post comment add <project-code> <post-number> --body-file -
[@<요청자>](dooray://...) 님, 안녕하세요.

요청 사항을 반영한 alpha PR을 생성했습니다. 검토 부탁드립니다.

cc. [@<관련자>](dooray://...)

#### 처리 내역
- PR: <PR URL>
- 적용 범위: ...
- 변경 요약: ...

#### 검토 요청 사항
- alpha 환경 노출 확인 부탁드립니다.
- ...
EOF
```

멘션 우선순위: **요청자(댓글/업무 작성자)** 메인, 관련자 cc. 멤버 ID는 사용자별 메모리 또는 기존 댓글 본문의 `[@이름](dooray://.../members/ID)` 패턴에서 추출. (관련 dooray-cli 기능 요청: `https://github.com/jon890/dooray-cli/issues/17`)

### 9. 리뷰 피드백 처리

```bash
gh api repos/TOAST-DOCS/OCR/pulls/<num>/comments
gh api -X POST repos/TOAST-DOCS/OCR/pulls/<num>/comments/<comment-id>/replies \
  -f body="<응답>"
```

수정 커밋을 푸시한 뒤 답글에 커밋 SHA를 명시해 반영 사실을 알린다.

### 10. 머지 후 후속

머지되면 사용자 명시 요청 시 `docs-i18n-sync` 스킬로 다국어 동기화 PR 진행. 사용자 요청 없이 임의로 beta/real로 승격하거나 다국어를 진행하지 않는다.

## 흔한 함정

- **분석 vs 진위확인 같은 인접 기능 혼동**: 한 가이드 파일 안에 인접 기능이 같이 있어 함께 손대기 쉽다. 댓글 명시 범위 + 코드 검증으로 정확히 구분.
- **폐기 enum과 분석 결과(KeyValues)의 관계**: 보조 기능(예: 진위확인)을 끄더라도 분석(추출) 자체가 살아있으면 결과 키 목록은 유지. 무리하게 함께 지우지 말 것.
- **표 컬럼 폭 정렬**: markdown 렌더는 raw 정렬 무시하지만 diff 가독성을 위해 가능한 한 유지.
- **"외국인 ~의 경우" 같은 한정자 삭제는 의미 변화 큼**: 자체적으로 판단 말고 사용자/책임자에게 한 번 더 컨펌.
- **alpha만 적용**: beta/real 승격은 사용자 명시 지시가 있을 때만.
