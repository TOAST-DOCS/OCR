---
name: sync-upstream
description: fork된 OCR-docs 저장소를 원본(TOAST-DOCS/OCR) 최신 상태와 안전하게 동기화한다. 트래킹 브랜치(alpha/beta/master/release)는 reset, 작업 브랜치(feature/*, chore/*, fix/*)는 rebase 패턴을 분기 적용한다. "fork 동기화", "upstream 가져오기", "원본 저장소 최신화", "alpha/beta/master 동기화", "내 브랜치 최신화" 같은 요청이 보이면 즉시 이 스킬을 사용한다.
---

# Sync Upstream

fork된 OCR-docs 저장소를 원본(`TOAST-DOCS/OCR`)의 최신 상태와 동기화한다. 안전성을 위해 사전 체크 → 분기 판단(트래킹/작업 브랜치) → 적절한 패턴 적용 흐름을 따른다.

## 왜 두 가지 패턴인가?

- **트래킹 브랜치(alpha/beta/master/release)**: fork 측에서는 직접 커밋하지 않고 단지 upstream을 따라가는 용도. `reset --hard upstream/<branch>`가 의도와 정확히 일치(직선 history). rebase보다 결과가 단순하고 충돌 가능성 0.
- **작업 브랜치(`feature/*`, `chore/*`, `fix/*` 등)**: 내가 만든 커밋이 있으므로 reset하면 작업이 사라진다. 베이스 브랜치(보통 alpha) 위에서 `rebase`로 내 커밋을 새 베이스 위에 옮겨야 함. fork에 이미 push된 상태라면 force-push가 필요하므로 `--force-with-lease`로 안전하게 처리.

## 사전 요구

- 원본 저장소 remote 등록 (보통 `upstream`이라는 이름). 미등록 시 SSH/HTTPS 중 origin과 같은 프로토콜로 추가:
  - SSH: `git remote add upstream git@github.com:TOAST-DOCS/OCR.git`
  - HTTPS: `git remote add upstream https://github.com/TOAST-DOCS/OCR.git`

## Step

### 1. 사전 체크

```bash
git status
git branch --show-current
```

다음 조건 중 하나라도 해당하면 **중단하고 사용자에게 알린다**:
- 미커밋 변경(unstaged/staged) 또는 untracked 중요 파일이 있다 → stash 또는 커밋 먼저
- 현재 브랜치가 비어 있다(detached HEAD) → 작업할 브랜치를 먼저 정한다

### 2. upstream 최신 가져오기

```bash
git fetch upstream
```

remote 이름이 `upstream`이 아닐 수 있다(`base`, `origin-upstream` 등). `git remote -v`로 확인.

### 3. 분기 판단

| 현재 브랜치 패턴 | 적용 패턴 | 이유 |
|---|---|---|
| `master`, `main`, `alpha`, `beta`, `release` | reset --hard | 트래킹 브랜치, 직선 동기화 |
| `feature/*`, `chore/*`, `fix/*`, `docs/*` | rebase | 내 커밋 보존하며 베이스만 갱신 |
| 기타 (사용자가 만든 임의 이름) | 사용자에게 어떤 패턴을 원하는지 확인 | 자동 판단 위험 |

### 4-A. 트래킹 브랜치: reset

```bash
git reset --hard upstream/<현재 브랜치명>
```

이 명령은 로컬 브랜치를 upstream과 정확히 동일한 커밋으로 맞춘다. fork(`origin`)에도 변경이 push되어 있다면 origin과 upstream의 차이가 없어진다.

origin이 upstream보다 앞서 있는(ahead) 비정상 상태라면 reset 전에 사용자에게 알린다 — 의도치 않은 fork 측 커밋이 있을 수 있다:

```bash
git log --oneline upstream/<branch>..origin/<branch>
```

### 4-B. 작업 브랜치: rebase

베이스 브랜치 위에 내 커밋을 다시 얹는다. 베이스는 보통 작업이 분기된 트래킹 브랜치(`alpha`가 일반적):

```bash
git rebase upstream/<base-branch>
```

충돌 발생 시 사용자에게 알리고 해결 방법 안내(`git status`로 충돌 파일 확인, 수정 후 `git add` → `git rebase --continue`).

rebase 성공 후 fork에 이미 push된 상태였다면 force-push 필요:

```bash
git push --force-with-lease origin <현재 브랜치명>
```

`--force-with-lease`는 다른 사람이 그 브랜치에 추가 push해 놓은 경우를 감지해 덮어쓰기를 막는다. **단순 `--force`는 사용하지 않는다** — 협업 안전성 차원.

### 5. 결과 확인

```bash
git log --oneline -5
git status
```

기대 상태:
- 트래킹 브랜치: `Your branch is up to date with 'origin/<branch>'.` 또는 동일 커밋
- 작업 브랜치: 내 커밋이 새 베이스 위에 올라가 있음

## 흔한 함정

- **master에서 reset하면 fork master가 upstream과 같아진다.** 이게 원하는 동작인지 확인. fork master에 별도 작업이 있는 경우는 거의 없지만, 있다면 reset 전에 사용자 컨펌.
- **rebase 중 충돌이 누적**되면 `git rebase --abort`로 안전하게 원상복구할 수 있다. 무리하게 진행하지 말 것.
- **`upstream` remote 이름이 `base`나 `origin-upstream`처럼 다를 수 있다.** 가정하지 말고 `git remote -v`로 확인 후 진행.
- **detached HEAD 상태에서 fetch만 하고 끝나면** 무엇도 변하지 않은 것처럼 보인다. 분기 판단 전에 반드시 작업 브랜치로 checkout.

## 원본 저장소 정보

- 저장소: `TOAST-DOCS/OCR`
- SSH: `git@github.com:TOAST-DOCS/OCR.git`
- HTTPS: `https://github.com/TOAST-DOCS/OCR.git`
