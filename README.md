# professor

연구가 막힐 때, 글이 잘 안 써질 때, 발표가 어딘가 어색할 때.
`professor`에게 한마디를 듣고, 그 답변을 목소리로 읽어보는 실습입니다.

## 시작하기

```bash
git clone https://github.com/jumincho/AI-JBNU-2026.git
cd AI-JBNU-2026
code .
```

VSCode에서 이 폴더를 열고 Codex 또는 Claude Code의 새 대화를 시작하세요.

**Codex**

```text
$professor 교수님, 연구가 너무 하기 싫어요.
```

**Claude Code**

```text
/professor 교수님, 연구가 너무 하기 싫어요.
```

문제부터 짚고, 이유를 묻고, 지금 해볼 수 있는 작은 행동을 함께 정리합니다.

## 목소리로 들어보기

[실습 노트북 열기](notebooks/professor_voice_lab.ipynb)

노트북을 VSCode/Jupyter에서 열거나, Colab의 파일 → 노트북 열기 → GitHub에서 이 저장소를 선택하세요.
CUDA GPU가 연결된 커널을 사용합니다. Colab 사용 시에는 [런타임 이용 범위](https://research.google.com/colaboratory/faq.html)를 확인하세요.

1. 실행 환경을 확인하고 패키지를 설치합니다.
2. 저장소에 포함된 [`voice_sample.mp3`](voice_sample.mp3)를 사용합니다. Colab에서는 노트북이 자동으로 가져옵니다.
3. OmniVoice 모델과 목소리를 한 번 불러옵니다.
4. VSCode 에이전트에서 `professor` 스킬로 짧은 답변을 만듭니다.
5. 답변을 노트북에 붙여넣고 합성·재생합니다.
6. WAV와 답변 TXT를 함께 받습니다.

언어·스타일·속도 같은 생성 옵션은 건드리지 않고 기본값을 사용합니다.
참조 음성은 저장소의 `voice_sample.mp3`를 사용합니다. 생성된 결과는 GitHub에 올리지 않고, 노트북을 공유할 때는 실행 출력을 지워주세요.

음성용 답변은 이렇게 요청하면 됩니다.

```text
$professor 음성용으로 2~4문장만 답해주세요. 교수님, 모델을 세 개 붙이면 연구가 될까요?
```

Claude Code에서는 `$professor` 대신 `/professor`를 사용합니다.
새 답변을 읽을 때는 모델을 다시 받을 필요 없이 노트북의 7~10번만 반복하면 됩니다.

## 파일

| 파일 | 용도 |
| --- | --- |
| `.agents/skills/professor/SKILL.md` | Codex 스킬 |
| `.claude/skills/professor/SKILL.md` | Claude Code 스킬 |
| `notebooks/professor_voice_lab.ipynb` | 음성 합성 실습 |
| `voice_sample.mp3` | 실습용 참조 음성 |

스킬은 [Distilly](https://github.com/titanwings/distilly)로 만들었고, 음성 합성에는
[OmniVoice](https://github.com/k2-fsa/OmniVoice)를 사용합니다.
모델 이용 조건은 [모델 카드](https://huggingface.co/k2-fsa/OmniVoice#license),
관련 소프트웨어 안내는 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)에서 확인할 수 있습니다.
