# professor에게 듣는 연구 한마디

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/jumincho/AI-JBNU-2026/blob/main/notebooks/professor_voice_lab.ipynb)

**VSCode 없이 바로 해 보려면 위 Open In Colab 버튼을 누르세요.** 메뉴에서 **런타임 > 모두 실행**만 누르면 교수님 목소리로 연구 한마디를 들을 수 있습니다.

연구가 막힐 때, 글이 잘 안 써질 때, 발표가 어딘가 어색할 때 `professor`에게 피드백을 받고, 그 답변을 교수님 목소리로 들어 보는 실습입니다.

```text
질문 ──▶ professor 스킬 (Codex / Claude Code) ──▶ 답변 텍스트 ──▶ OmniVoice (Colab GPU) ──▶ 교수님 목소리
```

| 방법 | 필요한 것 | 답변 텍스트 |
| --- | --- | --- |
| **A. Colab만으로** | Google 계정 | 직접 입력합니다 |
| **B. VSCode와 함께** | VSCode, Codex 또는 Claude Code, Google 계정 | professor 스킬이 만들어 줍니다 |

강의 자료는 [`AI-JBNU-2026-jumincho.pptx`](AI-JBNU-2026-jumincho.pptx)에 있습니다.

## A. Colab만으로 하기 (VSCode 없이, 10분)

1. 위의 **Open In Colab** 버튼을 누르고 Google 계정으로 로그인합니다.
2. 메뉴 **런타임 > 런타임 유형 변경**에서 하드웨어 가속기가 **T4 GPU**인지 확인하고 저장합니다.
3. 메뉴 **런타임 > 모두 실행**을 누릅니다. Google이 만든 노트북이 아니라는 경고가 나오면 **계속 실행**(Run anyway)을 누릅니다.
4. 처음에는 설치와 모델 다운로드 때문에 5~10분 정도 걸립니다. 끝나면 **7. 음성 합성하고 듣기** 셀에서 기본 문장을 들을 수 있습니다.
5. **6. 읽을 문장** 셀의 입력 칸에 원하는 문장을 적고, 6번과 7번 셀만 다시 실행합니다.
6. **8. 파일로 받기** 셀의 링크를 누르면 WAV 파일을 내려받습니다.

## B. VSCode에서 Codex나 Claude Code와 함께 하기

### 준비물

| 항목 | 설명 |
| --- | --- |
| [VSCode](https://code.visualstudio.com/) | 코드 편집기 |
| Codex 또는 Claude Code 확장 | VSCode 확장 화면(`Ctrl + Shift + X`)에서 설치하고 로그인합니다 |
| [Jupyter](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter) 확장 | 노트북 실행 |
| [Colab](https://marketplace.visualstudio.com/items?itemName=google.colab) 확장 | Colab GPU 서버 연결 |
| Google 계정 | Colab 로그인 |

### 1. 저장소 내려받기

```bash
git clone https://github.com/jumincho/AI-JBNU-2026.git
cd AI-JBNU-2026
code .
```

git이 없다면 VSCode에서 `Ctrl + Shift + P`를 누르고 **Git: Clone**에 저장소 주소를 붙여넣어도 됩니다.
저장소 폴더를 열어야 에이전트가 `professor` 스킬을 찾습니다.

### 2. professor에게 물어보기

에이전트 대화창에서 새 대화를 열고 물어봅니다.

| 에이전트 | 입력 |
| --- | --- |
| Codex | `$professor 교수님, 연구가 너무 하기 싫어요.` |
| Claude Code | `/professor 교수님, 연구가 너무 하기 싫어요.` |

목소리로 들을 답변은 짧게 받습니다.

```text
$professor 음성용으로 2~4문장만 답해 주세요. 교수님, 모델을 세 개 붙이면 연구가 될까요?
```

Claude Code에서는 `$professor` 대신 `/professor`를 씁니다. 답변은 문제부터 짚고, 이유를 묻고, 지금 해볼 수 있는 작은 행동으로 끝납니다.

### 3. 노트북을 Colab GPU에 연결하기

1. `notebooks/professor_voice_lab.ipynb`를 엽니다.
2. 오른쪽 위 **Select Kernel**을 누르고 **Colab**을 고릅니다.
3. **New Colab Server**를 고르고, 차례로 나오는 선택 창에서 **GPU**(Select a variant)와 **T4**(Select an accelerator)를 고릅니다. 이어서 나오는 기기 사양, 런타임 버전, 서버 이름은 기본값 그대로 Enter를 누르면 됩니다. (**Auto Connect**는 GPU가 없는 기본 서버에 연결될 수 있습니다.)
4. Google 로그인 안내가 나오면 **Allow**를 누르고 브라우저에서 로그인한 뒤 VSCode로 돌아옵니다.
5. 만든 서버의 Python 커널을 고르고 **1. GPU 확인** 셀을 실행합니다. GPU 이름이 나오면 연결된 것입니다.

코드는 PC가 아니라 Colab 서버에서 실행되므로 PC에 NVIDIA GPU가 없어도 됩니다.

| 작업 | 실행 위치 |
| --- | --- |
| 스킬 호출, 노트북 편집 | 내 PC의 VSCode |
| 설치, 모델 로딩, 음성 합성 | 연결한 Colab GPU 서버 |
| 만든 WAV 파일 | Colab 서버의 `/content` 폴더 |

### 4. 실행하고 듣기

1. 1번부터 5번 셀을 차례로 실행합니다. 처음에는 설치와 모델 다운로드 때문에 5~10분 정도 걸립니다.
2. 2단계에서 받은 답변을 **6. 읽을 문장** 셀의 `TEXT`에 붙여넣고 6번과 7번 셀을 실행합니다.
3. 새 답변을 들을 때는 6번과 7번 셀만 다시 실행합니다. 모델과 목소리는 다시 준비하지 않아도 됩니다.

### 5. 결과 받고 정리하기

- VSCode 왼쪽의 **Colab** 아이콘을 누르고 **Contents**에서 WAV 파일을 우클릭한 뒤 **Download...**를 누릅니다. VSCode에서는 Colab의 `files.download()`가 동작하지 않습니다.
- 다 끝나면 `Ctrl + Shift + P`에서 **Colab: Remove Server**를 실행해 서버를 반납합니다.

연결이 잘 안 되면 위의 Open In Colab 버튼으로 브라우저에서 같은 노트북을 열어 A 방법으로 진행하세요.
화면별 안내는 [Colab 확장 공식 사용 안내](https://github.com/googlecolab/colab-vscode/wiki/User-Guide)에 있습니다.

## 플러그인으로 더 해 보기 (선택)

강의에서 다룬 GitHub, Hugging Face 플러그인을 설치했다면 에이전트에게 이렇게 시켜 보세요.

| 플러그인 | 해 볼 요청 |
| --- | --- |
| GitHub | "jumincho/AI-JBNU-2026 저장소의 README를 읽고 실습 순서를 다섯 줄로 요약해 줘" |
| GitHub | "이 저장소를 내 계정으로 포크해 줘" |
| Hugging Face | "k2-fsa/OmniVoice 모델 카드에서 라이선스와 권장 참조 음성 길이를 알려 줘" |
| Hugging Face | "한국어를 지원하는 음성 합성 모델을 세 개 찾아서 비교해 줘" |

## professor 스킬

| 에이전트 | 위치 | 부르는 법 |
| --- | --- | --- |
| Codex | `.agents/skills/professor/SKILL.md` | `$professor` |
| Claude Code | `.claude/skills/professor/SKILL.md` | `/professor` |

두 파일의 내용은 같습니다. 오픈소스 프로젝트 [Distilly](https://github.com/titanwings/distilly)로 교수님의 연구 피드백 방식(PART A)과 말투(PART B)를 정리했습니다.
"음성용"이라고 요청하면 제목과 목록 없이 읽기 좋은 2~4문장으로 답합니다.

## 저장소 구성

```text
AI-JBNU-2026/
├── AI-JBNU-2026-jumincho.pptx          강의 자료
├── notebooks/professor_voice_lab.ipynb 음성 합성 실습
├── voice_sample.mp3                    참조 음성 (약 7초)
├── .agents/skills/professor/SKILL.md   Codex용 professor 스킬
├── .claude/skills/professor/SKILL.md   Claude Code용 professor 스킬
└── THIRD_PARTY_NOTICES.md              사용한 오픈소스 고지
```

## 막힐 때

| 증상 | 해결 |
| --- | --- |
| GPU가 연결되지 않았다는 오류 | Colab: 런타임 > 런타임 유형 변경 > T4 GPU / VSCode: New Colab Server에서 GPU 선택 |
| GPU를 할당받지 못했다는 안내 | 무료 GPU는 사용량이 많으면 잠시 막힐 수 있습니다. 잠시 뒤 다시 시도합니다 |
| 설치 뒤 import 오류 | 런타임 > 세션 다시 시작을 누른 뒤 모두 실행 |
| 첫 실행이 오래 걸림 | 모델(약 5GB)을 내려받는 중입니다. 두 번째부터는 빠릅니다 |
| 문장 일부가 빠지거나 어색하게 읽힘 | 7번 셀만 다시 실행합니다. 실행할 때마다 결과가 조금씩 달라집니다 |
| 에이전트가 `professor`를 못 찾음 | 저장소 폴더를 열었는지 확인하고 새 대화를 엽니다 |
| VSCode에 Colab 메뉴가 없음 | Colab, Jupyter 확장이 켜져 있는지 확인하고 VSCode를 다시 엽니다 |

## 주의

- 생성한 음성은 수업 실습용으로만 쓰고, 공개하거나 다른 용도로 쓰지 마세요.
- 다른 목소리를 쓸 때는 본인의 목소리나 동의를 받은 목소리만 사용하세요.
- 노트북을 공유할 때는 실행 결과(음성 포함)를 지우고 저장하세요.
- Colab 무료 GPU는 사용량 제한이 있습니다. [Colab 런타임 이용 범위](https://research.google.com/colaboratory/faq.html)를 확인하세요.

## 사용한 프로젝트

- [Distilly](https://github.com/titanwings/distilly): professor 스킬 생성 (MIT License, [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md))
- [OmniVoice](https://github.com/k2-fsa/OmniVoice): 음성 복제와 합성. 코드는 Apache 2.0, 사전학습 모델은 [CC BY-NC](https://huggingface.co/k2-fsa/OmniVoice#license)라서 비상업 용도로만 쓸 수 있습니다.
