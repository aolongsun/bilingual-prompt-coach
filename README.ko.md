# Bilingual Prompt Coach

[English](README.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Español mexicano](README.es-MX.md) | [Português (Brasil)](README.pt-BR.md) | [Türkçe](README.tr.md)

실제 작업을 하면서 언어를 연습할 수 있는 Codex Skill입니다. 명시적으로 활성화하면 요청을 수행하기 전에 간결한 언어 피드백을 제공하고, 도움이 되는 경우에만 모국어·보조 언어로 설명을 덧붙입니다.

기본값은 중국어 보조 설명과 명확한 B2–C1 수준의 미국 영어 연습입니다. 두 언어를 각각 선택하고 연습 언어의 지역 변형, 수준, 피드백 깊이, 두 언어의 비중을 조절할 수 있습니다.

위 링크는 문서의 표시 언어만 바꿉니다. 연습 설정은 자동으로 바뀌지 않으므로 원하는 언어를 대화에서 명시해 주세요.

![수정 부분을 굵게 표시한 영어 출력 예시](docs/output-example.png)

*이미지는 영어 출력 예시입니다. 최소 수정안에서 바뀐 부분만 굵게 표시됩니다.*

![언어 피드백 여부를 판단하는 영어 흐름도](docs/decision-map.jpg)

*이 흐름도는 영어로 되어 있으며 피드백이 표시되는 조건을 설명합니다.*

## 소개

공부, 연구, 코딩, 일상 업무에 관한 요청을 평소처럼 하면서 재사용할 수 있는 짧은 언어 피드백으로 학습합니다. 피드백 뒤에는 원래 요청에 대한 답변이 이어집니다.

- 영어를 비롯한 연습 언어로 작성한 프롬프트에는 도움이 될 때 최소 수정안과 자연스러운 표현을 제공합니다.
- 전체가 모국어·보조 언어로 작성된 프롬프트에는 자연스러운 연습 언어 버전을 하나 제공합니다.
- 여러 언어가 섞인 프롬프트는 의미를 유지하면서 연습 언어로 바꿉니다.
- 이미 명확하고 자연스러운 문장에는 중복해서 고쳐 쓰는 대신 짧은 안내를 제공합니다.
- 어려운 구절에는 바로 아래에 짧은 보조 언어 설명을 붙일 수 있습니다. 일반적인 답변을 문단마다 중복 번역하지는 않습니다.

## 설치

Codex에 내장 설치 도구를 사용하도록 요청합니다.

```text
Use $skill-installer to install the skill from https://github.com/aolongsun/bilingual-prompt-coach.
```

또는 개인 skills 디렉터리에 저장소를 복제합니다.

```bash
git clone https://github.com/aolongsun/bilingual-prompt-coach ~/.agents/skills/bilingual-prompt-coach
```

바로 표시되지 않으면 Codex를 다시 시작하세요.

## 사용법

구체적인 요청이 담긴 메시지에서 명시적으로 호출합니다.

```text
$bilingual-prompt-coach I read a paper yesterday. Can you help me understand its main argument?
```

활성화 후에는 현재 작업에서 매번 호출할 필요가 없습니다. 새 작업은 연습 모드가 꺼진 상태로 시작합니다. 다음 표현 중 하나로 종료할 수 있습니다.

```text
off
OFF!
stop coaching
언어 연습을 종료해 주세요.
```

자신의 언어로 종료를 요청해도 됩니다. `turn the server off`처럼 관련 없는 지시는 언어 피드백을 끄지 않습니다.

## 언어와 피드백 설정

모국어·보조 언어와 목표·연습 언어는 별개의 설정입니다. 자연어로 지정할 수 있으며 활성화와 동시에 설정해도 됩니다.

```text
$bilingual-prompt-coach 제 모국어는 일본어이고 영어를 연습하고 싶습니다.
제 모국어는 중국어이고 일본어를 연습하고 싶습니다.
B1 수준의 영국 영어를 사용해 주세요.
영어만 사용해 주세요.
중국어 설명을 늘려 주세요.
교정 설명은 필요 없습니다.
수정 부분을 강조하지 마세요.
전체 글을 교정해 주세요.
```

현재 작업에서는 마지막으로 명시한 설정이 우선합니다. 따로 지정하지 않으면 중국어 보조 설명과 B2–C1 미국 영어가 기본값입니다. README를 바꿔 읽어도 두 언어 설정은 바뀌지 않습니다.

결과물의 언어를 명시하면 실제 작업 답변에는 해당 언어를 우선 사용합니다. 예를 들어 “이 질문에는 중국어로 답해 주세요”라고 요청하면 필요한 언어 연습 블록은 유지하면서 답변 본문은 중국어로 작성합니다. `Why` 설명은 보통 연습 언어로 쓰고, 필요한 경우에만 보조 언어를 덧붙입니다.

## 예시

입력:

```text
$bilingual-prompt-coach I want practice English while I work. Can you helps me?
```

응답 예시(수정 내용을 확인할 수 있도록 영어로 표시):

> ### Language practice
>
> Minimal correction: I want **to** practice English while I work. Can you **help** me?
>
> Natural phrasing: I'd like to practice English as I work. Can you help me?
>
> Why: Use “want to” before a verb. After “can,” use the base form “help.”
>
> Yes. Send your next work-related request, and I'll give brief language feedback before answering it.

`Minimal correction`에서는 삽입하거나 바꾼 부분만 굵게 표시합니다. `Natural phrasing`과 작업 답변에는 변경 표시를 넣지 않습니다. 삭제한 부분은 문장에서 제거하며 기본적으로 취소선, HTML 색상, diff 표기를 사용하지 않습니다. 강조 표시 없이 교정해 달라고 요청할 수도 있습니다.

전체가 모국어·보조 언어로 작성된 프롬프트에는 `Minimal correction`과 `Natural phrasing` 대신 `Natural version`을 사용합니다.

## 동작 범위

- 언어 피드백은 매 턴 최종 답변의 맨 앞에 최대 한 번 표시하며 진행 상황이나 중간 계획에는 넣지 않습니다. JSON만, 코드만 등의 출력 형식 요청이 우선합니다.
- 인사, 확인, 선택지 응답, 실질적인 글이 없는 첨부 파일, “계속해 주세요”나 “계획을 실행해 주세요” 같은 짧은 조율 메시지에는 표시하지 않습니다.
- 인용문, 붙여 넣은 자료, 코드, 명령어, 로그, 파일명, 데이터는 편집을 요청하지 않는 한 제외됩니다.
- 교정, 재작성, 번역 자체가 요청한 결과물이라면 별도로 요구하지 않는 한 피드백 블록을 중복해서 추가하지 않습니다.
- 150단어를 넘는 프롬프트는 전체를 두 번 반복하는 대신 학습에 도움이 되는 부분을 최대 세 개 선택합니다. 전체 교정을 요청하면 이 제한보다 우선합니다.
- 재작성은 의미, 어조, 주장, 구체성을 유지합니다. 새로운 생각을 추가하거나 요청을 더 강하게 또는 약하게 만들지 않습니다.

이 skill은 지침으로만 구성되며 실행 스크립트, 외부 도구 의존성, 작업 간 숨겨진 기억이 없습니다. 연습 모드는 현재 대화에 의존합니다. 영어로 된 [SKILL.md](SKILL.md)가 유일한 실행 규칙이며, 번역된 README는 같은 skill을 설명하는 문서입니다. [동작 체크리스트](tests/behavior-cases.md)에 검증 시나리오가 있습니다.

## 라이선스

[MIT](LICENSE)
