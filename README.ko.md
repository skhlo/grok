# grok

[English](README.md) | 한국어

AI가 해 주는 설명은 유용하지만, 보통 채팅 속에 그대로 사라집니다.

`grok`은 다시 볼 만한 설명을 재사용 가능한 노트로 바꿔 줍니다. AI 어시스턴트에게 개념 설명을 부탁하면, grok은 검색한 출처를 바탕으로 짧게 설명해 줍니다. 그리고 그 설명을 남기고 싶을 때만 개인 학습 폴더에 Markdown 노트로 저장합니다.

나중에 같은 주제가 다시 나오면, AI 어시스턴트는 이미 배운 내용을 먼저 읽고 처음부터 다시 설명하지 않고 이어서 도와줄 수 있습니다.

**Claude Code**와 **Codex**에서 사용할 수 있습니다.

## 왜 쓰나요?

AI 어시스턴트에게 무언가를 설명해 달라고 했을 때 이런 생각이 들면 `grok`을 쓰면 됩니다.

> 이건 나중에 또 필요하겠다.

`grok`은 설명을 채팅 기록 속에 잃어버리는 대신 다음을 저장합니다.

- 그 개념이 무엇인지
- 왜 그 개념이 나왔는지
- 어디까지 이해했는지
- 어떤 출처를 사용했는지
- 다음에 어디서부터 이어가면 되는지

한 번 보고 끝날 사실이 아니라, 다시 볼 만한 개념을 위한 도구입니다.

## 어떤 느낌인가요?

작업하다가 애매하게만 알고 있는 개념을 만났다고 해 보겠습니다.

```text
you  > /grok AI inference and tokens

grok > AI inference is when an already-trained AI model is being used.

       Training is like teaching the model.
       Inference is the model doing the job.

       Tokens are the small chunks of text the model reads and writes.
       They are not exactly words. They are the AI's text currency.

       Short version:
       inference = the AI doing the work
       tokens = the pieces of text it works with

       Sources: Google Cloud, IBM, OpenAI docs

       Save this in Vault/grok/ai-inference-and-tokens/?

you  > yes

grok > Saved.
```

저장된 노트는 그냥 Markdown 파일입니다. 읽을 수 있고, 검색할 수 있고, 직접 고칠 수도 있고, 다시 필요해질 때까지 그냥 두어도 됩니다.

## 기본 흐름

1. **하던 일을 잠깐 멈춥니다.** 코딩, 리서치, 글쓰기 중에 개념 하나가 걸립니다.
2. **그 개념을 grok합니다.** `/grok <concept>`를 입력합니다.
3. **짧은 설명을 받습니다.** grok은 현재 이해 수준에 맞춰 설명하고, 검색한 출처를 사용합니다.
4. **필요할 때만 저장합니다.** 사용자가 동의해야만 vault에 씁니다.
5. **나중에 이어서 봅니다.** 다음에 같은 주제를 grok하면 저장된 노트를 먼저 찾습니다.

사용 중인 도구가 세션 분기를 지원한다면, 학습용 샛길을 원래 작업과 분리해 두는 것이 좋습니다.

- Claude Code: `/branch` 사용
- Codex: `/fork` 사용, 짧은 샛길이면 `/side` 사용

개념을 정리한 뒤 원래 세션으로 돌아오면 됩니다.

## 무엇이 저장되나요?

기본적으로 grok은 다음 폴더를 사용합니다.

```text
~/Vault/grok/
```

이 폴더를 개인 학습 폴더라고 생각하면 됩니다. 각 주제는 자기 폴더를 가집니다.

```text
~/Vault/grok/ai-inference-and-tokens/
  INDEX.md        개념의 의미와 현재 이해 상태
  CHECKPOINT.md   어디서 멈췄고 어디서 다시 시작할지
  HISTORY.md      다시 볼 때마다 남는 기록
  REFERENCES.md   grok이 사용한 출처
```

어떤 주제에는 다음 파일도 생길 수 있습니다.

```text
PRIMER.md        다시 읽기 좋은 정리 설명
GLOSSARY.md      중요한 용어와 정의
```

파일은 도움이 될 때만 만들어집니다. 작은 주제는 작게 남아 있어도 괜찮습니다.

## 실제 저장 예시 보기

이 저장소에는 grok이 저장한 예시가 들어 있습니다.

[examples/ai-inference-and-tokens](examples/ai-inference-and-tokens)

실제 체크포인트가 만들 수 있는 파일들을 볼 수 있습니다.

- `INDEX.md`: 오래 남길 이해 상태
- `CHECKPOINT.md`: 다음에 어디서 이어갈지
- `PRIMER.md`: 다시 읽기 좋은 정리 설명
- `REFERENCES.md`: 검색한 출처와 그 출처가 유용했던 이유
- `HISTORY.md`: 학습 기록

중요한 점은 학습이 점진적이라는 것입니다. 한 번에 전부 이해할 필요는 없습니다. 지금 유용한 만큼만 이해하고 저장한 뒤, 더 깊게 볼 필요가 생기면 그 지점부터 다시 이어갈 수 있습니다.

## 일반 채팅과 무엇이 다른가요?

일반 채팅에서 설명은 임시적입니다. 스크롤 기록 속에 있고, 세션이 끝나거나 압축되거나 다음 작업으로 넘어가면 쉽게 사라집니다.

`grok`은 유용한 설명을 오래 남깁니다.

- **현재 이해 수준을 기억합니다.** 저장된 노트에는 지금 무엇을 이해했는지가 남습니다.
- **왜 배웠는지를 남깁니다.** 그 개념이 왜 나왔는지 기록합니다.
- **출처를 저장합니다.** 다음 설명은 이미 찾은 출처 위에서 이어질 수 있습니다.
- **다시 시작할 수 있습니다.** AI 어시스턴트가 저장된 중단 지점부터 이어서 도울 수 있습니다.
- **프로젝트를 넘어 쓸 수 있습니다.** vault는 특정 저장소가 아니라 전역 폴더입니다.

목표는 단순합니다. 같은 내용을 매번 처음부터 다시 배우지 않는 것입니다.

## 설치

### Claude Code

```sh
git clone https://github.com/skhlo/grok.git ~/grok
ln -s ~/grok/skills/grok ~/.claude/skills/grok
mkdir -p ~/Vault/grok
```

그다음 이렇게 실행합니다.

```text
/grok <concept>
```

또는 그냥 어떤 것을 grok하고 싶다고 말해도 됩니다.

### Codex

Codex plugin 설정이 이 저장소를 가리키게 하세요. [`.codex-plugin/plugin.json`](.codex-plugin/plugin.json) manifest가 `skills/` 폴더를 노출합니다.

그다음 이렇게 실행합니다.

```text
/grok <concept>
```

또는 그냥 어떤 것을 grok하고 싶다고 말해도 됩니다.

## 기술 독자를 위한 설명

`grok`은 작업 중간에 생기는 학습용 샛길을 빠르게 처리하고 다시 이어갈 수 있게 해 주는 portable Agent Skill입니다. 설명하기 전에 신뢰할 만한 출처를 검색하고, 사용자가 명시적으로 동의할 때만 쓰며, 학습 상태를 YAML frontmatter가 있는 Markdown으로 저장합니다.

vault는 두 종류의 독자를 위해 만들어졌습니다.

- Markdown 노트를 직접 읽는 사용자
- 사용자가 이미 무엇을 아는지 복원한 뒤 이어서 설명하는 AI 어시스턴트

각 주제의 `INDEX.md`가 기준 파일입니다. 루트의 `~/Vault/grok/INDEX.md`는 모든 주제의 생성된 요약입니다. 루트 index는 직접 고치지 마세요.

다른 vault 위치나 timezone을 쓰려면 [`skills/grok/SKILL.md`](skills/grok/SKILL.md)에 있는 `~/Vault/grok`와 `KST` 지시를 바꾸면 됩니다.

전체 파일 형식은 [`VAULT-SCHEMA.md`](VAULT-SCHEMA.md)를 보세요.

## 배경

`grok`은 Matt Pocock의 [`/teach` skill](https://github.com/mattpocock/skills/tree/main/skills/productivity/teach)에서 출발했습니다.

`/teach`는 더 깊은 course-building workflow입니다. `grok`은 그 학습 원칙은 유지하되 형태를 바꿨습니다. 앉아서 한 주제를 깊게 배우는 순간이 아니라, 이미 무언가를 하는 중에 지금 바로 개념 하나를 이해해야 하는 순간을 위한 도구입니다.

| | `/teach` | `grok` |
|---|---|---|
| 순간 | 계획된 깊은 학습 | 작업 중간의 개념 샛길 |
| 결과물 | course-style workspace | Markdown checkpoint |
| 상태 위치 | 현재 프로젝트 workspace | 전역 learning vault |
| 쓰기 방식 | 학습 산출물을 만듦 | 확인 후에만 씀 |

이어받은 원칙은 다음과 같습니다.

- 현재 수준보다 조금 앞선 내용을 가르치기
- 지금 하는 일에서 그 개념이 왜 중요한지 설명하기
- 기억만 믿지 않고 신뢰할 만한 출처 사용하기
- "이해한 것 같다"와 "나중에 기억할 수 있다"를 구분하기
- 유용할 때 오해와 수정된 가정도 저장하기

## 라이선스

MIT - [LICENSE](LICENSE)를 보세요.
