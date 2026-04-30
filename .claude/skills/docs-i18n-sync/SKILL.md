---
name: docs-i18n-sync
description: 한국어 가이드 PR이 alpha에 머지된 변경을 en/ja/zh로 동기화하는 워크플로우. zh는 영문 그대로 사용 정책, ja는 일본어 번역 매핑 적용. 표/문구의 컬럼 폭과 글자 수 매핑까지 일관되게 옮긴다. "다국어 PR 만들어줘", "i18n 동기화", "en ja zh 가이드 반영", "한국어 변경 다국어 적용", "영문/일문/중문 가이드 반영", "다국어 가이드 동기화" 같은 요청이 보이면 즉시 이 스킬을 사용한다.
---

# OCR-docs 다국어 동기화 워크플로우

한국어 가이드 변경이 alpha에 머지된 후 en/ja/zh 디렉터리로 동기화한다.

## 트리거 예시

- "다국어 PR 만들어줘"
- "i18n 동기화 진행"

## 사전 요구

- 한국어 PR이 alpha에 이미 머지된 상태
- OCR-docs fork + upstream(`TOAST-DOCS/OCR`) remote 설정

## 언어별 정책

| 언어 | 본문 | 비고 |
|---|---|---|
| en | 영문 번역 | 한국어 원본 의미를 유지하며 자연스러운 영문 |
| ja | 일본어 번역 | `templates.md` 매핑 사전 참조 |
| zh | 영문 그대로 | en과 완전히 동일한 영어 텍스트 사용 |

## Step

### 1. alpha 최신화

```bash
git checkout alpha
git fetch upstream
git reset --hard upstream/alpha
git checkout -b feature/<topic>-i18n
```

브랜치명 컨벤션: `feature/<kebab-case-topic>-i18n` (한국어 PR 토픽에 `-i18n` 접미사).

### 2. 한국어 머지 결과 diff 추출

```bash
git log --oneline alpha | head -10
git show <merge-sha> -- 'ko/*.md'
```

또는 한국어 PR diff 직접 조회:

```bash
gh pr diff <ko-pr-number>
```

각 변경 라인을 정확히 파악하면 다국어 매핑 시 누락이 줄어든다.

### 3. 변경 위치 매핑

각 한국어 변경 라인에 대해 en/ja/zh 동일 위치를 찾는다. 라인 번호는 다를 수 있으므로 컨텍스트 키워드로 grep.

```bash
grep -n "<korean-keyword-or-context>" ko/<file>.md
grep -n "<en-equivalent>" en/<file>.md
grep -n "<ja-equivalent>" ja/<file>.md
```

번역어 추정이 어려운 경우 `templates.md` 참조 또는 ja 파일을 직접 읽어 기존 표현 차용.

### 4. 편집 적용

- **en, zh**: 동일 영어 변경 적용 (zh는 en과 같은 텍스트). 새로 zh 전용 표현 만들지 않는다.
- **ja**: 일본어 번역 적용 (`templates.md` 참조).
- 표 영역 변경 시 컬럼 폭(공백) 가능한 한 유지. Edit 도구로 다중 행 교체할 때는 trailing space까지 정확히 매치 필요. raw alignment가 깨져도 markdown 렌더링은 동일하지만 diff 가독성을 위해 유지가 좋다.

### 5. 커밋

관심사별로 커밋 분리하거나 한 번에 묶어도 된다. 한국어 PR과 같은 의도이므로 같은 메시지 톤.

```
feat(en/ja/zh): <한국어 변경 요지> 동기화

한국어 PR 머지 결과를 다국어로 반영.
- 변경 1
- 변경 2
```

### 6. PR 생성 (alpha 대상)

```bash
gh pr create --repo TOAST-DOCS/OCR --base alpha \
  --head <fork-owner>:feature/<topic>-i18n \
  --title "docs(en/ja/zh): <action> from OCR guides" \
  --body "$(cat <<'EOF'
## 배경
한국어 PR 머지 결과를 영문/일문/중문 가이드에 동기화합니다.

## 변경 내용
각 언어별 어떤 표현으로 옮겼는지

## 적용 범위 / 제외
- 한국어 PR 리뷰에서 원복된 부분은 다국어에서도 손대지 않음
- 분석 결과(KeyValues) 등 진위확인과 무관한 영역은 그대로 유지

## 별건 알림
작업 중 발견된 cleanup 사안 (PR 범위 외)
EOF
)"
```

### 7. Dooray 안내 댓글 (필요 시)

원 업무에 다국어 PR 진행 사실을 안내한다 (멘션 + PR 링크). 패턴은 `dooray-task-to-docs-update` 스킬 참조.

## 흔한 함정

- **ja 파일이 부분 번역 / 한국어 잔존**: 일부 ja 파일은 일본어가 아닌 한국어/영어가 그대로 남아 있을 수 있다. 실제 ja 파일 내용을 먼저 확인 후 변경.
- **ja 본문 중복 라인**: 과거 작업 흔적으로 같은 의미 라인이 두 줄로 남은 경우가 있다. 본 PR 범위가 아니면 별건 cleanup으로 PR 본문에 메모만 남기고 손대지 않는다.
- **zh 본문 영문 동일**: zh는 en과 동일 영어 사용. zh-only 표현/번역 만들지 않는다.
- **표 polish의 한계**: ja 표에서 한자/가나는 monospace 폭 2칸 차지하므로 ASCII 공백으로 visual width를 정확히 맞추기 어렵다. 글자 수 단위로만 맞추면 충분(렌더링 영향 없음).
- **누락 검증**: 한국어 PR diff의 모든 변경이 다국어에 반영됐는지 다시 한 번 grep 또는 diff stat으로 확인.
