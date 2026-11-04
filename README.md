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

## VSCode에서 Colab GPU 연결하기

노트북의 Python 코드는 선택한 커널에서 실행됩니다. Colab GPU 커널을 연결하면 패키지 설치·모델 로딩·음성 합성은 Colab 서버에서 진행되므로 PC에 NVIDIA GPU를 따로 준비할 필요가 없습니다.

1. VSCode 확장 화면(`Ctrl + Shift + X`)에서 [Google Colab](https://marketplace.visualstudio.com/items?itemName=google.colab)을 설치합니다. 확장 ID는 `google.colab`입니다. 기반이 되는 [Jupyter](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter) 확장도 설치·활성화되어 있어야 합니다.
2. 이 저장소 폴더에서 `notebooks/professor_voice_lab.ipynb`를 엽니다.
3. 노트북 오른쪽 위의 **Select Kernel(커널 선택)**을 누릅니다. 메뉴가 한 단계 더 나오면 **Select Another Kernel**을 거쳐 **Colab**을 선택합니다.
4. **New Colab Server**를 선택하고 Google 계정에 로그인합니다. 로그인 화면이 나오면 브라우저에서 승인한 뒤 VSCode로 돌아옵니다.
5. 서버 종류에서 **GPU**, 가속기에서 **T4 등 계정에 제공되는 GPU**를 선택합니다. 추가로 런타임 버전·메모리·서버 이름을 묻는 화면이 나올 수 있습니다. 기본값을 사용해도 되며 GPU 종류만 꼭 확인합니다.
6. 생성한 서버의 Python 커널을 선택한 뒤 노트북 **1번 셀**을 실행합니다. GPU 이름과 메모리가 출력되면 연결된 것입니다.
7. 나머지 셀을 순서대로 실행합니다. 기본 참조 음성은 저장소에서 자동으로 가져오므로 별도 업로드 없이 진행할 수 있습니다.

`Auto Connect`는 기본 서버에 연결하는 기능입니다. GPU 실습에서는 서버 종류를 직접 고르고, 1번 셀에서 CUDA GPU가 잡혔는지 확인하세요. GPU 목록과 할당 가능 여부는 계정·사용량·자원 상황에 따라 달라집니다.

| 작업 | 실행 위치 |
| --- | --- |
| 코드·노트북 편집과 스킬 호출 | PC의 VSCode |
| 패키지 설치·OmniVoice 모델 로딩·음성 합성 | 연결한 Colab GPU 서버 |
| 생성된 WAV·TXT·ZIP 파일 | Colab 서버의 `_professor_lab` 폴더 |

답변은 VSCode의 Codex/Claude Code 대화창에서 생성해 노트북에 붙여넣습니다. 이 실습에서는 Colab MCP를 추가로 설정할 필요가 없습니다.

결과는 VSCode 왼쪽 **Colab → Contents**에서 찾을 수 있습니다. 노트북이 출력한 경로의 ZIP 파일을 찾아 우클릭하고 **Download...**로 PC에 저장합니다. 목록에 보이지 않으면 새로고침하세요. 다른 참조 음성을 쓰고 싶으면 로컬 파일을 우클릭해 **Upload to Colab**으로 올리고 서버 경로를 입력할 수 있습니다.

실습을 마치면 `Ctrl + Shift + P`에서 **Colab: Remove Server**를 실행해 서버를 정리합니다. 새 서버에 연결하면 설치한 패키지와 모델 준비 단계를 다시 실행해야 합니다.

메뉴가 보이지 않으면 Colab·Jupyter 확장이 활성화되어 있는지 확인하고 VSCode 창을 다시 불러오세요. 연결 과정이 잘 안 되면 [브라우저 Colab에서 같은 노트북을 열어](https://colab.research.google.com/github/jumincho/AI-JBNU-2026/blob/main/notebooks/professor_voice_lab.ipynb) 런타임의 하드웨어 가속기를 GPU로 선택해 진행할 수 있습니다.

자세한 화면은 [Google Colab 확장 공식 사용 안내](https://github.com/googlecolab/colab-vscode/wiki/User-Guide)를 참고하세요.

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
