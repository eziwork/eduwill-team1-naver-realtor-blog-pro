# Naver Realtor Blog Pro v0.3

매물번호·링크·설명·사진으로 고객과 검색 의도에 맞는 전략을 추천하고, 사용자 확정 후 네이버 블로그 글을 작성·임시저장·재열람 검수하는 Codex 스킬입니다.

## 작업 흐름

1. 매물 정보와 사진을 살펴보고 사실마다 출처를 기록합니다.
2. 관련 상담 노하우를 읽고, 필요한 정보가 부족하거나 서로 다르면 **작성 전에 Codex 질문으로 사용자에게 확인**합니다. 현장 설명이 부족할 때만 추천 이유·고객 반응을 최대 2개 질문하며, 사실 확인과 함께 한 번에 묻습니다. 답이 없는 항목은 고객용 글에서 제외합니다.
3. 타겟·검색 의도·검색어 후보·후킹·글 구성·상담 유도를 담은 전략 한 안을 보여주고 실제 확정 응답을 받습니다.
4. 블로그별 저장 문체를 적용합니다. 문체가 없으면 공개 매물 글 최대 5개를 읽고, 사용자가 직접 지정한 말투와 형식을 우선합니다.
5. 원고·조건표·썸네일·사진·상담 배너를 만들고 로컬에서 검증합니다.
6. Codex 내장 브라우저에서 네이버 편집기에 입력하고 임시저장합니다.
7. **같은 임시저장 글을 다시 열어** 제목·본문·이미지·표·지도·연락처를 원본과 대조합니다.

정보가 없다는 수집 상태를 본문·표·캡션·이미지·상담 문구에 적지 않습니다. 필요한 사실은 미리 질문하고, 확인되지 않은 항목은 제외합니다. 확인된 중요한 제약은 사실대로 설명합니다.

기본 형식은 친숙한 존댓말, 한 문장당 한 문단, 문장 사이 빈 줄 한 줄, 가운데 정렬입니다. 사용자의 직접 요청이 기본 형식보다 우선합니다.

## 현장 포인트와 사무소 상담 노하우

- 이미 추천 이유나 고객 반응을 충분히 설명했다면 다시 묻지 않습니다. 현장 질문을 건너뛰어도 확보된 사실로 전략을 추천합니다.
- 답변은 매물 사실·중개사 평가·전달받은 고객 반응으로 나눕니다. 평가와 반응을 객관적인 매물 조건이나 후기처럼 쓰지 않습니다.
- “우리 파주 창고 임대 고객은 차량 진입부터 물어요”처럼 반복 적용 의도가 명확한 상담 경험은 자동으로 기억하고 짧게 알립니다. 같은 유형·지역·거래 조건의 다음 전략에서 설명 순서·상담 제안에 반영합니다.
- 개별 매물의 고객 반응이나 AI의 타겟 가설은 사무소 노하우로 저장하지 않습니다. 고객 이름·연락처도 저장하지 않습니다.
- 같은 내용은 중복 저장하지 않고, 명시적인 수정은 기존 내용을 대체합니다. 모호한 충돌은 확인될 때까지 보류하며 “이건 잊어줘”로 이후 적용을 중단합니다.
- 노하우는 profile.yaml과 같은 폴더의 office-knowledge.json에 저장하며 블로그 문체와 분리합니다. 이미 확정된 전략은 새 기억만으로 바뀌지 않습니다.

기존 호출명·입력 방식·프로필·전략 확정 절차를 유지합니다. 새 항목이 없는 기존 작업도 계속 읽습니다.

## 설치

**Node.js 20 이상**, Git, 스킬과 내장 브라우저를 사용할 수 있는 Codex가 필요합니다. 썸네일·배너 제작에는 현재 환경에서 제공되는 이미지 제작 기능을 사용합니다.

Codex에 다음처럼 요청하세요.

> https://github.com/eziwork/eduwill-team1-naver-realtor-blog-pro 저장소의 naver-realtor-blog-pro 폴더를 Codex 스킬로 설치해줘. 기존 설치와 사무소 프로필이 있으면 보존하고 업데이트해줘.

직접 설치할 때는 저장소를 내려받고 내부 스킬 폴더를 연결합니다.

```bash
git clone https://github.com/eziwork/eduwill-team1-naver-realtor-blog-pro.git
cd eduwill-team1-naver-realtor-blog-pro
```

macOS / Linux:

```bash
mkdir -p ~/.codex/skills
ln -s "$(pwd)/naver-realtor-blog-pro" ~/.codex/skills/naver-realtor-blog-pro
```

Windows PowerShell:

```powershell
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.codex\skills" | Out-Null
New-Item -ItemType Junction `
  -Path "$env:USERPROFILE\.codex\skills\naver-realtor-blog-pro" `
  -Target (Resolve-Path .\naver-realtor-blog-pro)
```

이미 같은 경로에 스킬이 있으면 중복 연결을 만들지 말고 기존 설치를 업데이트하세요. `CODEX_HOME`을 별도로 쓰는 환경에서는 해당 스킬 위치를 사용합니다.

매물번호 수집 기능을 사용하려면 **스킬 폴더에서** 다음 명령을 실행합니다. lockfile에 고정된 Playwright와 Chromium을 설치합니다.

```bash
cd naver-realtor-blog-pro
npm ci
```

상태 관리·문체·원고 검증 도구는 Node 내장 모듈만 사용합니다. 네이버 로그인과 글 입력은 Codex 내장 브라우저에서 진행합니다.

## 사용 예시

```text
$naver-realtor-blog-pro
매물번호: <매물번호>
내 블로그: https://blog.naver.com/<블로그ID>
이 매물의 고객과 검색 의도에 맞는 전략을 추천해줘.
내가 확정하면 내 문체로 작성하고 임시저장·검수해줘.
```

번호 대신 매물 설명과 사진을 제공해도 됩니다. 사무소명·담당자명·공개 상담 연락처는 처음에 등록하고 이후 재사용합니다.

사무소 프로필의 기본 위치는 `~/.codex/naver-realtor-blog/profile.yaml`, 블로그별 문체는 같은 폴더의 `blog-styles.json`입니다. 계정별 프로필·로그인 데이터·매물 작업 결과는 저장소에 올리지 않습니다.

## 저장과 검수

이 스킬은 네이버 **임시저장까지** 수행합니다. 공개 발행·예약 발행·공개 범위 변경·기존 글 삭제는 포함하지 않습니다. 로그인은 사용자가 네이버 화면에서 직접 합니다.

| 저장 상태 | 의미 |
|---|---|
| `SAVED` | 저장 신호와 저장본 식별이 확인됨 |
| `BLOCKED` | 로그인 등 선행 작업이 필요함 |
| `UNVERIFIED` | 저장 여부를 확인할 충분한 근거가 없음 |
| `FAILED` | 작업 실패가 확인됨 |

완성도는 `완료 / 보완 필요 / 확인 불가`로 따로 기록합니다. 저장 후 같은 글을 재열람하여 모든 항목을 대조해야 `완료`로 보고합니다. 중단 후 재개할 때는 임시저장 목록을 먼저 확인해 중복 글 생성을 방지합니다.

검색어는 실시간 검색량·순위 분석 결과가 아닌 추천 후보입니다. 실제 유입과 문의 성과는 발행 후 확인합니다.

## 파일 구성과 검증

- [SKILL.md](naver-realtor-blog-pro/SKILL.md): 현재 작업 지침
- [전략 가이드](naver-realtor-blog-pro/references/strategy-guide.md): 타겟·검색 의도·문의 유도
- [콘텐츠 형식](naver-realtor-blog-pro/references/content-format.md): 원고·사진·표·상담 배너
- [파일 계약과 CLI](naver-realtor-blog-pro/references/workflow-contract.md): 사실·전략·확정·원고·전송 상태
- [브라우저 전송 계약](naver-realtor-blog-pro/references/transfer-contract.md): 입력·임시저장·재열람 검수
- [수동 평가 기준](naver-realtor-blog-pro/references/evaluation-cases.md): 유형별 확인 항목
- [현장 포인트·상담 노하우 계약](naver-realtor-blog-pro/references/broker-knowledge.md): 분류·범위·기억·수정·잊기 명령
- [구현 검증 기록](naver-realtor-blog-pro/docs/implementation-validation.md): 연속 두 매물의 정보 분리와 검증 범위

저장소 루트에서 실행합니다.

```bash
npm test
node naver-realtor-blog-pro/scripts/check-core.mjs
```

자동 테스트는 번들 구성·전략 확정·문체·원고·전송 상태와 현장 질문·노하우의 범위·중복·수정·비활성화를 확인합니다. 연속 두 매물에서 상담 우선순위만 재사용되고 개별 매물 조건이 섞이지 않는지도 검증합니다. 네이버 실제 로그인·자연어 의미 판단·브라우저 저장 결과를 자동 테스트만으로 보증하지 않습니다. 개별 작업에서 원문과 화면 검수를 수행합니다.

`scripts/post-draft.mjs`와 `scripts/login-setup.mjs`는 이전 전송기 호환용 파일입니다. 현재 흐름은 내장 브라우저를 사용하며 해당 스크립트로 자동 전환하지 않습니다. `docs/`의 정적 도식과 예전 화면 예시는 이전 버전 자료로, 현재 실행 절차는 `SKILL.md`와 `references/`를 따릅니다.

## 출처

이 저장소는 [Dr-Min/naver-realtor-blog-pro](https://github.com/Dr-Min/naver-realtor-blog-pro)의 기존 구조를 바탕으로, Eziwork에서 전략 확정·블로그별 문체·내장 브라우저 검수 흐름을 보완한 배포본입니다.
