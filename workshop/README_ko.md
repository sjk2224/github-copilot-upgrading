## GitHub Copilot으로 레거시 프로젝트 업그레이드하기

레거시(구식) Python 애플리케이션을 최신 버전의 Python으로 업그레이드하는 과정을 GitHub Copilot의 도움을 받아 단계별로 진행해봅니다.

> [!NOTE]
> 이 저장소는 **GitHub Copilot**의 다양한 기능(예: **Copilot Chat**, **인라인 채팅**)을 소개하기 위한 것입니다. 아래 단계별 가이드에는 필요한 작업의 일반적인 설명이 포함되어 있으며, Copilot Chat 또는 인라인 채팅을 통해 필요한 명령을 생성할 수 있습니다.
>
> 각 단계(해당되는 경우)에는 Copilot의 제안을 올바른 명령과 비교할 수 있는 `Cheatsheet`도 포함되어 있습니다.
>
> 💡 다양한 프롬프트를 시도해 보며 Copilot 제안의 정확도가 어떻게 달라지는지 확인해보세요. 예를 들어, 인라인 채팅을 사용할 때 추가 프롬프트를 통해 응답을 더 세밀하게 조정할 수 있습니다.

## 학습 목표

이 워크숍에서 여러분은 다음을 수행합니다:

  - 레거시 프로젝트를 다루기 위한 GitHub Copilot의 고급 상호작용 기법 사용
  - 레거시 프로젝트를 업그레이드하고 정확성을 검증하기 위해 반복, 검증, 개선
  - 더 나은 결과를 얻을 수 있는 다양한 전략을 적용
  - 업그레이드 후 프로젝트의 최종 상태를 검증할 수 있는 철저한 테스트 전략 구축

## :mega: 사전 준비 사항

워크숍에 참여하기 전, 공개 GitHub 계정이 필요합니다. 모든 리소스, 의존성, 데이터는 저장소에 포함되어 있습니다. GitHub Copilot 라이선스, 체험판 또는 무료 버전을 준비하세요.

## 워크숍 특징

### 1. 에이전트를 사용해 프로젝트 탐색

`@workspace` 에이전트를 사용해 프로젝트의 동작을 설명해보세요.

- GitHub Copilot Chat을 열고 프롬프트 앞에 `@workspace`를 붙이세요.
- 예시: "이 프로젝트는 어떻게 의존성을 설치하나요?" 등

### 2. 레거시 및 포팅 문제 파악

Python 애플리케이션의 테스트를 실행해보세요. 사전 설치된 `pytest`를 사용해 결과를 확인하세요.

- `@workspace`에게 "이 코드를 최신 Python으로 포팅할 때 발생할 수 있는 문제는?" 등 질문
- 가상환경을 만들어 의존성 설치 시도

> [!NOTE]
> 왜 설치가 실패할 수 있을까요? 레거시 Python에서 더 이상 지원되지 않는 `distribute`를 사용하기 때문입니다.
> Copilot에게 의존성 설치의 다른 방법을 제안받으세요.

### 3. 모든 코드를 업그레이드 디렉터리로 복사

코드를 포팅하려면 모든 코드를 `upgraded` 디렉터리로 복사해야 합니다. 이곳에서 작업을 진행합니다.

- 기능 테스트를 활용해 집중할 기능 범위를 정하세요.

> [!NOTE]
> 비즈니스 로직에 따라 일부 컴포넌트가 명확하지 않을 수 있습니다.

### 4. 프로젝트 설치

가상환경을 만들고 프로젝트를 설치하세요. `python setup.py develop`을 실행하고 오류를 분석하세요.

- Copilot Chat에 오류를 붙여넣고 안내를 받으세요.
- 파일을 컨텍스트로 추가하세요(`#file:setup.py`).
- Copilot의 제안대로 오류를 수정하고 설치를 완료하세요.

### 5. 테스트 실행

`pytest` 프레임워크와 명령줄 도구가 설치되어 있습니다. 유닛 테스트를 실행하고 오류를 확인하세요.

- 오류 출력을 Copilot에 붙여넣어 도움을 받으세요(`#terminalSelection`).
- Copilot의 답변을 검토하고 필요시 추가 질문
- *아직 코드를 수정하지 마세요.*

> [!NOTE]
> 오류가 즉시 이해되지 않을 수 있습니다. 추가 질문을 통해 전략을 세우세요. 프로젝트가 오래된 Python 버전을 사용했음을 Copilot에 알릴 수도 있습니다.

### 6. try/except 오류 수정

기능 테스트를 활용해 집중할 기능 범위를 정하고, try/except 오류를 수정하세요.

- Copilot에게 실제 문제 해결을 요청하세요. 오래된 Python 버전임을 언급하세요.
- 모든 try/except 오류를 수정하고 테스트를 반복 실행하세요.

> [!NOTE]
> 예외 외에도 다른 오류가 있을 수 있습니다. try/except 오류를 모두 해결한 후 다음 단계로 진행하세요.

### 7. ConfigParser 문제 해결

다음 문제는 `ConfigParser`가 사용 불가한 경우입니다. Copilot에게 해결 전략을 요청하세요.

- "이 프로젝트는 Python 2.5로 작성되었고, Python 3.9에서 다음과 같은 오류가 발생합니다:"라고 질문하고 테스트 출력을 붙여넣으세요.
- 간단한 해결책을 선택하고 즉시 검증하세요.
- 테스트를 실행해 변경 사항이 올바른지 확인하세요.

[!NOTE]
> 모든 테스트가 통과해야 합니다. 그렇지 않으면 Copilot에게 다시 질문하고 이전 단계를 검토하세요.

### 8. 테스트를 Pytest로 포팅

Pytest는 가장 강력한 Python 테스트 프레임워크입니다. 레거시 코드는 `unittest`를 사용하므로, 모든 테스트를 `pytest`로 포팅하세요.

- 테스트 파일에서 `@workspace` 에이전트로 포팅 방법을 질문하세요.
- 테스트 함수로 하나의 테스트를 작성해보세요(클래스 대신 함수 사용 권장).
- 하나의 테스트를 작성한 후 Copilot에게 다음 테스트 생성을 요청하세요.

> [!NOTE]
> Pytest는 `unittest` 테스트도 실행할 수 있지만, 향후 확장성과 유지보수를 위해 pytest 스타일로 포팅하는 것이 좋습니다.

### 9. 최신 패키징 사용

레거시 코드는 여전히 `setuptools`와 `setup.py`를 사용합니다. 최신 표준인 `pyproject.toml`로 패키징하세요.

- Copilot에게 `pyproject.toml` 파일 생성 방법을 질문하세요. `setup.py` 파일을 열어두세요.
- 새 `pyproject.toml` 파일을 만들고 Copilot의 제안으로 내용을 채우세요.
- `pip install .` 명령으로 프로젝트를 설치하세요.

> [!NOTE]
> Python 패키징은 여전히 도전적인 주제입니다. Copilot의 제안을 검증하고 설치를 테스트하세요.

### 10. GitHub Actions로 자동화

레거시 프로젝트에는 자동화가 없습니다. GitHub Actions로 테스트 및 검증을 자동화하세요.

- Copilot에게 GitHub Actions 워크플로우 생성 방법을 질문하세요.
- 필요한 파일과 디렉터리를 생성하세요.
- 변경 사항을 푸시해 GitHub Actions가 동작하는지 확인하세요.

> [!NOTE]
> 자동화 구축은 시간이 걸릴 수 있습니다. 인내심을 갖고 Copilot의 도움을 받아 진행하세요.

## 주요 포인트

- Copilot의 다양한 기능을 실습하며 레거시 코드를 최신 Python으로 업그레이드하는 전체 과정을 경험할 수 있습니다.
- 각 단계에서 Copilot의 제안을 적극적으로 활용하고, 오류나 문제 발생 시 반복적으로 질문하며 해결책을 찾아보세요.

## :books: 참고 자료

이 워크숍에서 다루는 일부 기능은 다음 Microsoft Learning 모듈에서 확인할 수 있습니다:

- [GitHub Codespaces로 코드 작성하기](https://learn.microsoft.com/training/modules/code-with-github-codespaces/)
- [고급 GitHub Copilot 기능 사용하기](https://learn.microsoft.com/training/modules/advanced-github-copilot/)

## 기여하기

이 프로젝트는 기여와 제안을 환영합니다. 대부분의 기여는 Contributor License Agreement(CLA)에 동의해야 합니다. 자세한 내용은 https://cla.opensource.microsoft.com 을 참고하세요.

풀 리퀘스트를 제출하면 CLA 봇이 자동으로 확인하고 안내합니다. 한 번만 동의하면 됩니다.

이 프로젝트는 [Microsoft 오픈 소스 행동 강령](https://opensource.microsoft.com/codeofconduct/)을 채택하고 있습니다. 자세한 내용은 [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/)를 참고하거나 [opencode@microsoft.com](mailto:opencode@microsoft.com)으로 문의하세요.

## 상표

이 문서에 언급된 모든 상표는 각 소유자의 자산입니다.
