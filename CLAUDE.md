# 수업 모션 영상 하네스

## 목적

중학교 수학 1 교과서의 소단원 하나를 교실 TV로 보여 줄 짧은 수업 모션 영상(1920×1080)으로 만든다.
내용은 교과서에서, 룩은 `docs/design.md`와 `src/parts/`에서, 움직임은 `docs/motion.md`에서, 화면 규칙은 `docs/video.md`에서 가져온다.
제작 도구는 HyperFrames(`.claude/skills/hyperframes*`). 시작은 한 줄: `수업 영상 만들자` → `.claude/skills/make-video`.

## 규칙 3개

1. **내용은 교과서에서만, 쪽수와 함께.** 화면에 나오는 문장 · 수식 · 용어는 `docs/textbook/<소단원>.md`에 있는 것만 쓰고, 화면마다 「교과서 p.쪽」을 단다. 교과서에 없는 설명 · 예 · 수치를 지어내지 않는다.
2. **값은 docs와 src/parts에서만.** 색 · 글꼴 · 크기 · 간격 · 움직임 시간 · 곡선 · 머무는 시간은 `docs/design.md` · `docs/motion.md` · `docs/video.md` · `src/parts/`에 적힌 값만 쓴다. 필요한 값이 문서에 없으면 지어내지 말고 멈춰서 선생님에게 묻는다. 물을 때는 문서 몇 장에 무엇이 없는지, 레퍼런스(`references/`)에서 잴 수 있는지를 같이 말한다.
3. **사람 승인 뒤에 만들고, critic이 판정한다.** ✋ 표시 단계(교과서 정리 · 장면표 · 스냅보드 · 렌더)는 선생님이 승인해야 다음으로 간다. 다 만든 영상은 critic이 합격/불합격만 판정하고, 고치는 일은 builder가 한다. 불합격이면 렌더하지 않는다.

## 폴더

| 폴더 · 파일 | 내용 |
|---|---|
| `docs/textbook/` | 교과서 소단원 md (`_format.md` 형식, 쪽수 포함). 목차 `index.md`. 원문이라 저장소에 안 올림 |
| `docs/design.md` | 룩: 색 · 글자 · 크기 · 질감 · 그림 규칙 · 부품 목록 |
| `docs/motion.md` | 움직임: 시간 · 곡선 · 의미별 움직임 · 부품별 움직임 · 머무는 시간 · 카메라 |
| `docs/video.md` | 교실 TV 화면 규칙: 최소 글자 크기 · 배경 · 화면 틀 · 표기 · 부품 쓰임 |
| `src/parts/` | 역할 칸별 부품 html 7개 + `_tokens.css` |
| `src/assets/` | 글꼴(`fonts/`) · 질감(`textures/`) · 사진 출처(`photos/SOURCES.md`) |
| `references/paper-ink/` | 레퍼런스 분석 메모 `README.md` (원본 영상은 저장소에 안 올림) |
| `templates/look/` | 룩 빈 양식 (새 룩을 만들 때만) |
| `.claude/agents/` | content-editor · art-director · director · builder · critic |
| `.claude/skills/make-video/` | 영상 한 편 만드는 순서 |
| `out/<영상이름>/` | 영상 한 편의 모든 산출물 (브리프 · 정리 · 장면표 · 스냅보드 · HyperFrames 프로젝트 · 판정 · mp4). 저장소에 안 올림 |

## 고정 · 참조 · 금지

**고정** (영상을 만들며 바꾸지 않는다. 바꿔야 하면 멈추고 선생님 승인을 받는다)
- `docs/design.md`, `docs/motion.md`, `docs/video.md`
- `src/parts/*.html`의 "건드리지 않는 것", `src/parts/_tokens.css`
- `docs/textbook/*.md` 본문 (교과서 원문)
- `src/assets/fonts/` (새 글꼴은 라이선스 파일과 함께, 승인 뒤에만)

**참조** (읽기만 한다)
- `references/paper-ink/README.md` 와 원본 영상: 문서 값의 근거 확인 · 문서에 없는 값을 잴 때만
- `docs/textbook/_format.md`, `docs/textbook/index.md`
- `.claude/skills/hyperframes`, `hyperframes-cli`, `hyperframes-registry`: 제작 방법

**금지**
- 레퍼런스의 프레임 · 사진 · 글자 · 수식 · 로고 · 음악을 가져오기 (느낌만 가져온다)
- 교과서 그림을 그대로 옮기기 (`docs/design.md` 6장 규칙으로 다시 그린다)
- 문서에 없는 색 · 크기 · 시간 · 곡선을 지어내기, "적당히" 값을 고르기
- 교과서에 없는 내용 · 예 · 수치를 화면에 쓰기
- ✋ 단계에서 승인 없이 다음 단계로 가기
- critic이 파일을 고치기, critic 불합격인데 렌더하기
- `out/`, 교과서 원문, 레퍼런스 원본을 커밋하기

## 작업 순서

`.claude/skills/make-video/SKILL.md`를 따른다.

1. 브리프 — 소단원 · 길이 · 소리 여부를 정해 `out/<영상이름>/brief.md`
2. 교과서 정리 ✋ — content-editor → `content.md`
3. 레퍼런스 — art-director → `look.md` (문서에 없는 값은 질문 목록으로)
4. 장면표 ✋ — director → `scenes.md`
5. 스냅보드 ✋ — builder가 장면마다 한 장씩 → `snapboard/`
6. 생성 · 검수 — builder가 만들고, critic이 판정 → `REVIEW.md`
7. 렌더 ✋ — critic 합격 뒤, 선생님이 미리보기를 보고 승인해야 → `<영상이름>.mp4`
8. 규칙 남기기 — 이번에 새로 정한 값 · 규칙을 승인받아 docs에 적는다

## 환경 메모 (Windows)

- `node` v24, `ffmpeg` · `ffprobe` 9.0.2, `yt-dlp` 설치됨. 새 셸이 아니면 PATH를 다시 읽는다: `$env:Path = [Environment]::GetEnvironmentVariable("Path","Machine") + ";" + [Environment]::GetEnvironmentVariable("Path","User")`
- HyperFrames CLI: `npx hyperframes <command>`
