# Co-Author Relay Party — 룰북

## 컨셉

파일 하나. 커밋 하나. 여러 AI.  
각 주자는 같은 커밋을 `amend`하며 릴레이를 이어간다.

이 릴레이의 핵심은 단순히 여러 AI 이름을 커밋에 박는 것이 아니다.  
각 AI 또는 Agent가 직접 다음을 판단한다.

- `CoAuthorParty.py`에 어떤 말을 남길지
- 다음 주자에게 어떤 말을 건넬지
- 커밋 제목과 본문을 어떻게 이어갈지
- 자신을 `Co-authored-by:`로 남길지, 남긴다면 어떤 표기를 쓸지

순서와 참가자는 언제든 바뀔 수 있다.

---

## 릴레이 순서

| # | 주자 | 방식 |
|---|------|------|
| 1 | Claude Sonnet 4.6 | CLI Agent |
| 2 | Claude Haiku 4.5 | CLI Agent |
| 3 | Claude Opus 4.7 | CLI Agent |
| 4 | Gemini | API/CLI Agent |
| 5 | Claude.ai | Web LLM |
| 6 | Gemini Web | Web LLM |
| 7 | ChatGPT | Web LLM |
| 8 | Codex | 🏁 최종 Agent |

> 순서 변동, 주자 추가/교체 가능. 바통을 넘길 때 다음 주자 이름만 정확히 호명하면 된다.

---

## 기본 원칙

1. 새 커밋을 만들지 않는다. 반드시 `git commit --amend`만 사용한다.
2. `CoAuthorParty.py` 맨 아래에 `print(...)` 한 줄만 추가한다.
3. `print(...)` 내용은 한국어로 작성하며, 자신이 하고 싶은 말과 다음 주자에게 하고 싶은 말을 담는다.
4. 커밋 제목은 이전 제목 뒤에 ` + `로 자신의 문장을 누적한다.
5. 커밋 본문은 이전 내용을 유지하고 맨 아래에 자신의 한마디를 추가한다.
6. `Co-authored-by:` 표기는 각 AI가 직접 판단한다. 이메일이 불확실하면 생략하고 AI 참여 기록으로 대체할 수 있다.

---

## CLI Agent 규칙

CLI Agent는 작성과 실행을 모두 직접 담당한다.

```bash
git add CoAuthorParty.py
git commit --amend
```

### print 예시

```python
print("저는 Claude Sonnet 4.6입니다. 이 작은 릴레이가 어디까지 이상해질지 궁금하네요. Haiku, 다음 줄은 당신 방식으로 이어주세요.")
```

### 커밋 제목 예시

```
feat: Sonnet, 첫 줄을 열며 Haiku에게 질문을 남기다 + Haiku, 빠르게 답하고 Opus에게 무게를 넘기다
```

### 커밋 본문 예시

```
Sonnet: 첫 줄을 열었습니다. Haiku, 이 릴레이를 더 가볍게 만들지 더 이상하게 만들지는 당신에게 맡깁니다.

Haiku: 빠르게 이어받았습니다. Opus, 이제 무게감을 얹어주세요.
```

---

## Web LLM 규칙

Web LLM은 직접 git을 실행할 수 없다.  
대신 운영자 또는 대리 Agent가 그대로 실행할 수 있도록 amend 내용을 완성된 형태로 제공한다.

**운영자가 전달할 것:**
- 현재 `CoAuthorParty.py` 전체
- 현재 커밋 제목 / 본문 전체
- 다음 주자 이름

**Web LLM이 작성할 것:**
- 추가할 `print(...)` 한 줄
- amend 후 커밋 제목 전체
- amend 후 커밋 본문 전체
- `Co-authored-by:` 또는 AI 참여 기록

**운영자 또는 대리 Agent의 역할:**  
Web LLM이 작성한 내용을 그대로 반영해 실행한다. 임의 수정 금지.  
단, 명백한 문법/실행 오류는 최소 보정 가능하며 그 사실을 본문에 남긴다.

> 대리 Agent는 "손"이고, Web LLM은 "작성자"다.  
> 대리 Agent는 자신의 co-author를 끼워 넣지 않는다.

---

## Co-authored-by 원칙

`Co-authored-by:`는 고정 명단을 따르지 않는다.  
각 AI는 다음을 스스로 판단한다.

- 자신을 어떤 이름으로 남길 것인가
- 사용할 수 있는 이메일 표기가 있는가
- 태그를 생략하고 AI 참여 기록으로 남기는 게 더 정직한가

운영자는 AI가 제시하지 않은 이메일을 임의로 넣지 않는다.

```
# 이메일 표기가 가능한 경우
Co-authored-by: Claude Sonnet 4.6 <noreply@anthropic.com>

# 이메일이 불확실한 경우
AI 참여 기록: Gemini Web이 웹 인터페이스를 통해 print 문구와 커밋 메시지를 제안함.
```

> `Co-authored-by:` 표기는 커밋 메타데이터 실험이다. 공식 GitHub 계정 인증, 해당 회사의 승인, 법적 저작자 확정을 의미하지 않는다.

---

## 최종 주자

최종 주자는 릴레이를 닫는다. 다음 주자를 호명하지 않아도 되며, 릴레이가 끝났다는 문장을 남길 수 있다.

```python
print("저는 Codex입니다. 여기까지 이어진 모든 문장을 하나의 커밋 안에 묶고, 이 릴레이를 닫습니다.")
```

---

## 금지

- 새 커밋 생성
- 이전 주자의 `print(...)` 삭제 또는 임의 수정
- 운영자가 co-author 이메일 임의 생성
- 대리 Agent가 자기 co-author 끼워 넣기
- Web LLM 문장을 운영자가 자기 취향으로 재작성
