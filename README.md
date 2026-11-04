# 내 스킬과 내 목소리로 듣는 한마디

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/jumincho/AI-JBNU-2026/blob/main/notebooks/my_voice_lab.ipynb)

**VSCode 없이 바로 해 보려면 위 Open In Colab 버튼을 누르세요.** 내 목소리 녹음 파일을 올리고 **런타임 > 모두 실행**을 누르면, 입력한 문장을 내 목소리로 들을 수 있습니다.

[Distilly](https://github.com/titanwings/distilly)로 나만의 페르소나 스킬을 만들고, 그 스킬의 답변을 [OmniVoice](https://github.com/k2-fsa/OmniVoice)로 복제한 내 목소리로 들어 보는 실습입니다. 스킬도, 목소리 샘플도 직접 만듭니다.

```text
질문 ──▶ 내 스킬 (Codex / Claude Code) ──▶ 답변 텍스트 ──▶ OmniVoice (Colab GPU) ──▶ 내 목소리
```

| 방법 | 필요한 것 | 답변 텍스트 |
| --- | --- | --- |
| **A. Colab만으로** | Google 계정, 내 목소리 녹음 | 직접 입력합니다 |
| **B. VSCode와 함께** | VSCode, Codex 또는 Claude Code, Google 계정, 내 목소리 녹음 | Distilly로 만든 내 스킬이 만들어 줍니다 |

강의 자료는 [`AI-JBNU-2026-jumincho.pptx`](AI-JBNU-2026-jumincho.pptx)에 있습니다. GitHub에서 내려받기 어려우면 [Google Drive에서 받기](https://drive.google.com/uc?export=download&id=1ZDCGtFEGbVQnbFs1ScRPzzUBe4a-W6bT)를 누르세요.

## 0. 내 목소리 녹음하기 (A, B 공통)

- 휴대폰 음성 메모나 PC 녹음기 앱으로 **3~10초** 동안 한두 문장을 평소 말투로 읽습니다.
- 조용한 곳에서 녹음하고, 음악이나 다른 사람 목소리가 섞이지 않게 합니다.
- 말을 시작하기 전과 끝낸 뒤에 잠깐 조용히 두고, 문장을 끝까지 말합니다. 말 중간에 잘린 녹음은 합성 결과가 불안정할 수 있습니다.
- 파일 형식은 WAV, MP3, M4A 모두 괜찮습니다. 노트북이 알아서 변환합니다.
- **본인 목소리만 사용하세요.**

## A. Colab만으로 하기 (VSCode 없이, 10분)

1. 위의 **Open In Colab** 버튼을 누르고 Google 계정으로 로그인합니다.
2. 메뉴 **런타임 > 런타임 유형 변경**에서 하드웨어 가속기가 **T4 GPU**인지 확인하고 저장합니다.
3. 왼쪽 **폴더 아이콘**을 누르고, 녹음 파일을 그 안으로 끌어다 놓아 올립니다.
4. 메뉴 **런타임 > 모두 실행**을 누릅니다. Google이 만든 노트북이 아니라는 경고가 나오면 **계속 실행**(Run anyway)을 누릅니다.
5. 처음에는 설치와 모델 다운로드 때문에 5~10분 정도 걸립니다. 끝나면 **7. 음성 합성하고 듣기** 셀에서 기본 문장을 내 목소리로 들을 수 있습니다.
6. **6. 읽을 문장** 셀의 입력 칸에 원하는 문장을 적고, 6번과 7번 셀만 다시 실행합니다.
7. **8. 파일로 받기** 셀의 링크를 누르면 WAV 파일을 내려받습니다.

## B. VSCode에서 Codex나 Claude Code와 함께 하기

### 준비물

| 항목 | 설명 |
| --- | --- |
| [VSCode](https://code.visualstudio.com/) | 코드 편집기 |
| Codex 또는 Claude Code 확장 | VSCode 확장 화면(`Ctrl + Shift + X`)에서 설치하고 로그인합니다 |
| [Jupyter](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter) 확장 | 노트북 실행 |
| [Colab](https://marketplace.visualstudio.com/items?itemName=google.colab) 확장 | Colab GPU 서버 연결 |
| Google 계정 | Colab 로그인 |
| 내 목소리 녹음 | 0번 안내대로 녹음한 파일 |

### 1. 저장소 내려받기

```bash
git clone https://github.com/jumincho/AI-JBNU-2026.git
cd AI-JBNU-2026
code .
```

git이 없다면 VSCode에서 `Ctrl + Shift + P`를 누르고 **Git: Clone**에 저장소 주소를 붙여넣어도 됩니다.

### 2. Distilly로 내 스킬 만들기

[Distilly](https://github.com/titanwings/distilly)는 한 사람의 경험, 판단, 말투, 일하는 방식을 에이전트가 쓰는 스킬(Person Profile)로 정리해 주는 오픈소스 프로젝트입니다. 만들 수 있는 유형은 세 가지입니다.

| 유형 | 대상 | 이런 스킬을 만들어 보세요 |
| --- | --- | --- |
| `colleague` | 동료, 선배, 멘토 | 성격과 말투 설명만으로 만드는 가상의 연구실 선배 |
| `relationship` | 가족, 친구 | 허락을 받은 친구의 대화로 만드는 말벗 |
| `celebrity` | 공개 인물, 가상 인물 | 좋아하는 작가나 연구자, 소설 속 인물 |

1. **Distilly 설치하기.** 에이전트 대화창에 아래 문장을 보냅니다. 설치가 끝나면 새 대화를 엽니다.

   ```text
   https://github.com/titanwings/distilly 에서 Distilly를 설치하고 이 호스트가 인식하는지 확인해 줘.
   ```

   직접 설치하려면 저장소 폴더에서 쓰는 에이전트에 맞는 명령을 실행합니다.

   ```bash
   # Claude Code
   git clone https://github.com/titanwings/distilly .claude/skills/distilly
   # Codex
   git clone https://github.com/titanwings/distilly .agents/skills/distilly
   ```

2. **스킬 만들기.** 새 대화에서 Claude Code는 `/distilly`, Codex는 `$distilly`를 입력합니다. 유형을 고르고 이름과 설명, 자료(직접 쓴 글, 대화, 기록 등)를 넣은 뒤 미리보기를 확인합니다. 이름 말고는 모두 건너뛸 수 있어서 설명만으로도 만들 수 있지만, 자료가 좋을수록 스킬도 좋아집니다.
3. **에이전트에 설치하기.** "만든 스킬을 Claude Code에 설치해 줘" 또는 "Codex에 설치해 줘"라고 요청합니다. 스킬 이름은 `유형-이름` 꼴(예: `colleague-mentor`)이고, 설치한 뒤에는 새 대화를 엽니다.

> 유형에서 나 자신(`owner`)을 고르면 스킬 대신 에이전트가 나를 알기 위한 프로필이 만들어집니다. 이 실습에서는 위 세 유형 중 하나를 고르세요.

Distilly는 만든 스킬의 원본을 자료와 함께 작업 폴더의 `skills/` 아래에 저장합니다. 이 폴더와 저장소 안에 설치한 Distilly는 `.gitignore`에 들어 있어서 커밋되지 않습니다.

### 3. 내 스킬에게 물어보기

새 대화를 열고 내 스킬 이름으로 시작해서 묻습니다. 아래 예시의 `colleague-mentor` 자리에 내 스킬 이름을 넣으세요.

| 에이전트 | 입력 |
| --- | --- |
| Codex | `$colleague-mentor 요즘 공부가 손에 안 잡혀요.` |
| Claude Code | `/colleague-mentor 요즘 공부가 손에 안 잡혀요.` |

목소리로 들을 답변은 짧게 받습니다. Claude Code에서는 `$` 대신 `/`를 씁니다.

```text
$colleague-mentor 음성용으로 제목과 목록 없이 2~4문장만 답해 주세요. 요즘 공부가 손에 안 잡혀요.
```

### 4. 노트북을 Colab GPU에 연결하기

1. `notebooks/my_voice_lab.ipynb`를 엽니다.
2. 오른쪽 위 **Select Kernel**을 누르고 **Colab**을 고릅니다.
3. **New Colab Server**를 고르고, 차례로 나오는 선택 창에서 **GPU**(Select a variant)와 **T4**(Select an accelerator)를 고릅니다. 이어서 나오는 기기 사양, 런타임 버전, 서버 이름은 기본값 그대로 Enter를 누르면 됩니다. (**Auto Connect**는 GPU가 없는 기본 서버에 연결될 수 있습니다.)
4. Google 로그인 안내가 나오면 **Allow**를 누르고 브라우저에서 로그인한 뒤 VSCode로 돌아옵니다.
5. 만든 서버의 Python 커널을 고르고 **1. GPU 확인** 셀을 실행합니다. GPU 이름이 나오면 연결된 것입니다.

코드는 PC가 아니라 Colab 서버에서 실행되므로 PC에 NVIDIA GPU가 없어도 됩니다.

| 작업 | 실행 위치 |
| --- | --- |
| 스킬 만들기와 호출, 노트북 편집 | 내 PC의 VSCode |
| 설치, 모델 로딩, 음성 합성 | 연결한 Colab GPU 서버 |
| 올린 녹음 파일과 만든 WAV 파일 | Colab 서버의 `/content` 폴더 |

### 5. 녹음 파일 올리고 실행하기

1. 녹음 파일을 저장소 폴더에 넣고, 탐색기에서 우클릭한 뒤 **Upload to Colab**을 누릅니다. 녹음 파일은 `.gitignore`에 들어 있어서 커밋되지 않습니다.
2. 1번부터 5번 셀을 차례로 실행합니다. 처음에는 설치와 모델 다운로드 때문에 5~10분 정도 걸립니다.
3. 3단계에서 받은 답변을 **6. 읽을 문장** 셀의 `TEXT`에 붙여넣고 6번과 7번 셀을 실행합니다.
4. 새 답변을 들을 때는 6번과 7번 셀만 다시 실행합니다. 모델과 목소리는 다시 준비하지 않아도 됩니다.

### 6. 결과 받고 정리하기

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

## 내 스킬 위치

| 에이전트 | 이 저장소에서만 쓸 때 | 모든 프로젝트에서 쓸 때 | 부르는 법 |
| --- | --- | --- | --- |
| Codex | `.agents/skills/<스킬 이름>/SKILL.md` | `~/.agents/skills/<스킬 이름>/SKILL.md` | `$<스킬 이름>` |
| Claude Code | `.claude/skills/<스킬 이름>/SKILL.md` | `~/.claude/skills/<스킬 이름>/SKILL.md` | `/<스킬 이름>` |

같은 `SKILL.md`를 두 에이전트의 위치에 함께 넣으면 Codex와 Claude Code에서 모두 쓸 수 있습니다.

## 저장소 구성

```text
AI-JBNU-2026/
├── AI-JBNU-2026-jumincho.pptx      강의 자료
├── notebooks/my_voice_lab.ipynb    내 목소리 합성 실습
└── THIRD_PARTY_NOTICES.md          사용한 오픈소스 고지
```

## 막힐 때

| 증상 | 해결 |
| --- | --- |
| GPU가 연결되지 않았다는 오류 | Colab: 런타임 > 런타임 유형 변경 > T4 GPU / VSCode: New Colab Server에서 GPU 선택 |
| GPU를 할당받지 못했다는 안내 | 무료 GPU는 사용량이 많으면 잠시 막힐 수 있습니다. 잠시 뒤 다시 시도합니다 |
| 녹음 파일을 찾지 못했다는 오류 | 녹음 파일을 올린 뒤 3번 셀부터 차례로 다시 실행합니다 |
| 설치 뒤 import 오류 | 런타임 > 세션 다시 시작을 누른 뒤 모두 실행 |
| 첫 실행이 오래 걸림 | 모델(약 5GB)을 내려받는 중입니다. 두 번째부터는 빠릅니다 |
| 문장 일부가 빠지거나 어색하게 읽힘 | 7번 셀만 다시 실행합니다. 계속 어색하면 조용한 곳에서 다시 녹음합니다 |
| 에이전트가 Distilly나 내 스킬을 못 찾음 | 설치한 뒤 새 대화를 엽니다. 스킬 폴더 안에 `SKILL.md`가 있는지 확인합니다 |
| VSCode에 Colab 메뉴가 없음 | Colab, Jupyter 확장이 켜져 있는지 확인하고 VSCode를 다시 엽니다 |

## 주의

- 녹음은 본인 목소리만 사용하세요. 만든 음성으로 다른 사람을 흉내 내거나 속이면 안 되고, 다른 사람에게 들려줄 때는 합성 음성이라고 밝혀 주세요.
- 다른 사람의 글이나 대화로 스킬을 만들 때는 그 사람의 허락을 받으세요. 원자료는 저장소에 올리지 마세요.
- 노트북을 공유할 때는 실행 결과(음성 포함)를 지우고 저장하세요.
- Colab 무료 GPU는 사용량 제한이 있습니다. [Colab 런타임 이용 범위](https://research.google.com/colaboratory/faq.html)를 확인하세요.

## 사용한 프로젝트

- [Distilly](https://github.com/titanwings/distilly): 페르소나 스킬 생성 (MIT License, [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md))
- [OmniVoice](https://github.com/k2-fsa/OmniVoice): 음성 복제와 합성. 코드는 Apache 2.0, 사전학습 모델은 [CC BY-NC](https://huggingface.co/k2-fsa/OmniVoice#license)라서 비상업 용도로만 쓸 수 있습니다.
