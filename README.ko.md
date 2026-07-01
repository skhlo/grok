# grok

[English](README.md) | 한국어

AI의 설명은 유용하지만, 대개 대화 속에 묻혀 사라지곤 합니다.

`grok`은 그중에서 다시 볼 만한 설명을 재사용할 수 있는 노트로 남겨 줍니다. 어시스턴트에게 개념을 물어보면 grok이 직접 검색한 출처를 바탕으로 짧게 설명하고, 간직하고 싶은 내용만 개인 학습 폴더에 일반 Markdown 노트로 저장합니다.

다음에 같은 주제가 나오면, 어시스턴트가 이미 배운 내용을 읽고 처음부터 다시 시작하는 대신 그 지점부터 이어서 도와줍니다.

**Claude Code**와 **Codex**에서 쓸 수 있습니다.

## 왜 쓸까요?

AI 어시스턴트에게 무언가를 설명해 달라고 했을 때 이런 생각이 든다면 `grok`을 쓰면 됩니다.

> 이거 나중에 또 필요하겠는데.

그 설명을 대화 기록 속에 흘려보내는 대신, `grok`은 다음을 저장합니다.

- 그 개념이 무엇인지
- 왜 그 개념이 나왔는지
- 어디까지 이해했는지
- 어떤 출처를 참고했는지
- 다음에 어디서부터 이어가면 될지

한 번 찾고 마는 단편 정보가 아니라, 두고두고 다시 볼 개념을 위한 도구입니다.

## 실제로 써 보면

작업을 하다가 어렴풋이만 아는 개념을 만났다고 해 봅시다.

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

저장된 노트는 그냥 Markdown 파일입니다. 읽고, 검색하고, 직접 고칠 수 있으며, 다시 필요해질 때까지 그냥 두어도 됩니다.

## 기본 흐름

1. **하던 일을 잠깐 멈춥니다.** 코딩, 리서치, 글쓰기 중에 개념 하나가 걸립니다.
2. **그 개념을 grok합니다.** `/grok <concept>`라고 입력하면 됩니다.
3. **짧은 설명을 받습니다.** grok은 현재 수준에 맞춰 설명하고, 직접 검색한 출처를 활용합니다.
4. **쓸모 있을 때만 저장합니다.** 사용자가 동의해야만 vault에 기록합니다.
5. **나중에 이어서 봅니다.** 다음에 같은 주제를 grok하면 저장해 둔 노트를 먼저 찾습니다.

쓰는 도구가 세션 분기를 지원한다면, 이를 활용해 학습 곁길을 원래 작업과 떼어 놓는 것이 좋습니다.

- Claude Code: `/branch`를 사용합니다.
- Codex: `/fork`를 사용하고, 짧은 곁길이면 `/side`를 사용합니다.

개념을 다 파악했으면 원래 세션으로 돌아오면 됩니다.

## 무엇이 저장되나요?

기본적으로 grok은 다음 폴더를 사용합니다.

```text
~/Vault/grok/
```

이 폴더를 나만의 학습 공간이라고 생각하면 됩니다. 주제마다 폴더가 하나씩 생깁니다.

```text
~/Vault/grok/ai-inference-and-tokens/
  INDEX.md        개념의 의미와 현재 이해 상태
  CHECKPOINT.md   어디서 멈췄고 어떻게 이어갈지
  HISTORY.md      다시 볼 때마다 쌓이는 기록
  REFERENCES.md   grok이 참고한 출처
```

주제에 따라 다음 파일도 생길 수 있습니다.

```text
PRIMER.md        다시 읽기 좋게 정리한 설명
GLOSSARY.md      핵심 용어와 정의
```

파일은 도움이 될 때만 만들어집니다. 작은 주제는 작은 채로 남아 있어도 괜찮습니다.

## 실제 저장 예시 보기

이 저장소에는 grok으로 저장한 예시가 들어 있습니다.

[examples/ai-inference-and-tokens](examples/ai-inference-and-tokens)

실제 checkpoint가 만들어 내는 파일들을 볼 수 있습니다.

- `INDEX.md`: 오래 남길 이해 상태
- `CHECKPOINT.md`: 어디서 멈췄고 어떻게 이어갈지
- `PRIMER.md`: 다시 읽기 좋게 정리한 설명
- `REFERENCES.md`: 검색한 출처와 그 출처가 유용했던 이유
- `HISTORY.md`: 학습 흐름 기록

핵심은 학습이 점진적이라는 점입니다. 한 번에 전부 이해할 필요는 없습니다. grok은 지금 이해한 만큼만 저장해 두었다가, 더 깊이 파고들 필요가 생기면 그 지점부터 이어갈 수 있습니다.

## 일반 채팅과 무엇이 다른가요?

일반 채팅에서 설명은 일시적입니다. 스크롤 기록 안에만 있어서, 세션이 끝나거나 압축되거나 다른 작업으로 넘어가면 쉽게 사라집니다.

`grok`은 쓸모 있는 설명을 오래 남게 만듭니다.

- **수준을 기억합니다.** 저장된 노트에 지금 무엇을 이해했는지가 담깁니다.
- **이유를 남깁니다.** 그 개념이 왜 나왔는지 기록합니다.
- **출처를 저장합니다.** 다음 설명은 이미 찾아 둔 출처 위에서 이어질 수 있습니다.
- **이어서 시작합니다.** 어시스턴트가 저장된 중단 지점부터 이어갈 수 있습니다.
- **프로젝트를 넘나듭니다.** vault는 특정 저장소에 묶이지 않은 전역 폴더입니다.

목표는 단순합니다. 같은 것을 매번 처음부터 다시 배우지 않는 것입니다.

## 설치

### Claude Code

이 저장소를 플러그인 마켓플레이스로 추가한 뒤 플러그인을 설치합니다.

```text
/plugin marketplace add skhlo/grok
/plugin install grok@grok
```

볼트 폴더는 처음 저장할 때 자동으로 만들어집니다.

### Codex

이 저장소를 플러그인 마켓플레이스로 추가합니다.

```text
codex plugin marketplace add skhlo/grok
```

그런 다음 Codex에서 `/plugins`를 열고 **grok** 마켓플레이스를 선택해 grok 플러그인을 설치합니다.

### 사용하기

이렇게 실행합니다.

```text
/grok <concept>
```

또는 그냥 무언가를 grok해 달라고 말해도 됩니다.

## 기술 독자를 위한 설명

`grok`은 다른 작업 중에 생기는 학습 곁길을 빠르게 처리하고 다시 이어갈 수 있게 해 주는, 여러 도구에서 쓸 수 있는 Agent Skill입니다. 설명하기 전에 신뢰할 만한 출처를 검색하고, 사용자가 명시적으로 동의할 때만 기록하며, 학습 상태를 YAML frontmatter가 포함된 Markdown으로 저장합니다.

vault는 두 종류의 독자를 위한 것입니다.

- Markdown 노트를 직접 훑어보는 사용자
- 이미 아는 내용을 복원한 뒤 이어서 설명하는 AI 어시스턴트

각 주제의 `INDEX.md`가 유일한 기준입니다. 루트의 `~/Vault/grok/INDEX.md`는 모든 주제를 자동 생성한 요약이므로, 직접 수정하지 마세요.

vault 위치나 시간대를 바꾸려면 [`skills/grok/SKILL.md`](skills/grok/SKILL.md)에 있는 `~/Vault/grok`와 `KST` 관련 부분을 수정하면 됩니다.

전체 파일 형식은 [`VAULT-SCHEMA.md`](VAULT-SCHEMA.md)를 참고하세요.

## 배경

`grok`은 Matt Pocock의 [`/teach` skill](https://github.com/mattpocock/skills/tree/main/skills/productivity/teach)에서 갈라져 나왔습니다.

`/teach`는 더 깊이 들어가는 강의형 워크플로입니다. `grok`은 그 학습 원칙은 그대로 두되 형태를 바꿨습니다. 앉아서 한 주제를 깊이 파는 것이 아니라, 무언가를 하는 도중에 지금 당장 개념 하나를 이해해야 하는 순간을 위한 것입니다.

| | `/teach` | `grok` |
|---|---|---|
| 시점 | 계획적인 깊은 학습 | 작업 중간의 개념 곁길 |
| 결과물 | 강의형 작업 공간 | Markdown checkpoint |
| 상태 저장 위치 | 현재 프로젝트 작업 공간 | 전역 학습 vault |
| 기록 방식 | 학습 산출물 생성 | 확인 후에만 기록 |

이어받은 원칙은 다음과 같습니다.

- 현재 수준보다 한 걸음 앞선 내용을 가르치기
- 지금 하는 일에서 그 개념이 왜 중요한지 설명하기
- 기억에만 의존하지 않고 신뢰할 만한 출처 사용하기
- "이해됐다"와 "나중에도 기억한다"를 구분하기
- 필요할 때 오해와 바로잡은 가정도 저장하기

## 라이선스

MIT - [LICENSE](LICENSE)를 참고하세요.
