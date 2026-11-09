---
title: "레슨 1 - GitHub Copilot app 설치"
description: "GitHub Copilot app을 설치하고 템플릿에서 만든 리포지토리를 연결한 다음 워크스페이스를 살펴보고 빠른 채팅을 사용해 봅니다."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

**[GitHub Copilot app][about-copilot-app]**은 에이전트 기반 개발을 위한 데스크톱 애플리케이션입니다. GitHub Copilot CLI를 기반으로 하며 GitHub와 기본적으로 통합되어 리포지토리, 브랜치, 지속적 통합(continuous integration, CI) 파이프라인을 바로 사용할 수 있습니다. 반복 작업을 자동화하고 각자 격리된 워크스페이스에서 여러 에이전트를 병렬로 지시하는 워크플로에 적합합니다. Node.js를 설치하고 프로젝트 복사본을 준비했으므로 이제 앱을 설치하고 리포지토리를 연결합니다.

이 레슨에서는 다음 작업을 수행합니다.

- GitHub Copilot app을 설치하고 로그인합니다.
- GitHub 리포지토리에서 프로젝트를 앱에 추가합니다.
- 템플릿에서 자동으로 만든 백로그를 포함해 워크스페이스를 살펴봅니다.
- 빠른 채팅으로 앱 자체에 관해 알아봅니다.

## 시나리오

팀에서는 늘어나는 백로그를 처리하기 위해 인공지능(artificial intelligence, AI) 에이전트를 도입하고 있습니다. Copilot app에서 이슈를 선택하고 에이전트를 실행하며 변경 내용을 검토하고 풀 리퀘스트를 병합할 수 있습니다. 이 레슨에서는 앱을 설치하고 프로젝트에 연결한 다음 프로젝트에 관해 대화를 시작하는 방법을 익힙니다.

> [!NOTE]
> Copilot Free, Copilot Student 또는 유료 플랜(Pro, Pro+, Business, Enterprise) 중 하나가 필요합니다. Copilot Business 또는 Copilot Enterprise를 사용하는 경우 관리자가 **GitHub Copilot app** 정책을 활성화해야 합니다.

## GitHub Copilot app 설치 및 구성

먼저 GitHub Copilot app을 설치하고 인증한 다음 Tailspin Toys 리포지토리를 추가합니다. Windows, macOS, Linux용 앱을 사용할 수 있습니다.

1. 브라우저에서 [GitHub Copilot app 랜딩 페이지][download-app]를 엽니다.
2. 사용 중인 플랫폼에 맞는 앱을 다운로드하고 랜딩 페이지의 안내에 따라 설치합니다.
3. 설치가 끝나면 앱을 엽니다.
4. **Sign in to GitHub**을 선택하고 안내에 따라 인증합니다. 데이터 레지던시가 적용되는 GitHub Enterprise Cloud를 사용한다면 **Use GitHub Enterprise**를 선택하고 메시지가 표시되면 `*.ghe.com` 호스트 이름을 입력합니다. GitHub Enterprise Server는 지원되지 않습니다.
5. 온보딩 중 리포지토리를 선택하라는 메시지가 표시되면 템플릿에서 만든 Tailspin Toys 리포지토리를 선택합니다. 리포지토리 선택을 건너뛰고 온보딩이 끝난 뒤 추가해도 됩니다.
6. 메시지가 표시되면 테마를 선택한 다음 온보딩을 완료합니다.
7. 사이드바의 **Sessions** 아래에서 리포지토리를 찾습니다. 이미 목록에 있으면 다시 추가할 필요가 없습니다.
8. 아직 리포지토리가 연결되지 않았다면 **Sessions** 옆의 **+**를 선택해 새 세션을 만든 다음 **Add GitHub repository**를 선택합니다. 필수 조건 레슨에서 기록한 소유자 이름과 리포지토리 이름을 입력합니다.
9. 리포지토리가 사이드바에 표시되는지 확인합니다. 여기에서 사용하는 레이아웃에서는 `tailspin-toys` 같은 리포지토리 폴더가 **Sessions** 아래에 그룹화되고 각 리포지토리 아래에 개별 세션이 표시됩니다.

## 워크스페이스 살펴보기

프로젝트를 연결했으므로 잠시 시간을 내어 워크스페이스를 살펴봅니다. 사이드바에는 다음 영역이 있습니다.

- **New** - 새 채팅 세션을 시작합니다.
- **Pull requests** - 앱의 GitHub 통합으로 풀 리퀘스트를 확인합니다. 앱을 벗어나지 않고 풀 리퀘스트를 찾아 필터링하고 지속적 통합(continuous integration, CI) 상태를 확인하고 검토할 수 있습니다.
- **Issues** - 이슈를 찾아 필터링하고 이슈에서 세션을 시작합니다.
- **Automations** — 일정에 따라 또는 요청 시 실행되는 에이전트 작업을 저장합니다. 할 일 목록 관리, 정기적인 프로젝트 유지 관리, 반복 작업 자동화에 유용합니다. 마무리에서 다음 단계로 소개하며 별도의 워크숍 실습으로 다루지는 않습니다.
- **Customize** - 모델 컨텍스트 프로토콜(Model Context Protocol, MCP) 서버, 플러그인, 스킬 및 기타 구성 요소를 추가해 Copilot app의 기능을 확장합니다. Playwright MCP를 구성할 때 사용합니다.
- **Chats** — 브랜치나 별도 워크스페이스가 필요하지 않은 질문과 브레인스토밍을 위한 가벼운 대화입니다. 첫 채팅을 시작한 후 이 영역이 표시됩니다. 표시되지 않으면 **Sessions** 옆의 **+**를 선택해 첫 채팅을 시작합니다.
- **Sessions** — 리포지토리 폴더와 해당 에이전트 세션을 그룹으로 표시합니다. `tailspin-toys` 같은 리포지토리 이름을 선택하면 리포지토리 화면이 열립니다. 리포지토리 아래의 세션을 선택하면 해당 대화로 돌아갑니다. 각 세션은 격리된 워크스페이스에서 실행되므로 변경 내용이 충돌하지 않게 여러 세션을 동시에 실행할 수 있습니다. 별점을 추가할 때 첫 세션을 시작합니다.

워크숍을 진행하면서 워크스페이스를 계속 살펴봅니다.

> [!TIP]
> 방법을 모르거나 가능한지 궁금한 작업이 있다면 Copilot에 질문해 안내를 받을 수 있습니다.

### 미리 생성된 백로그 찾기

Tailspin Toys 리포지토리를 만들 때 생성된 백로그를 살펴봅니다. 이슈 번호가 아니라 제목으로 대상 이슈를 찾습니다.

1. 사이드바의 **Sessions** 아래에서 개별 세션이 아닌 Tailspin Toys 리포지토리 폴더를 선택합니다. 그런 다음 리포지토리 상단 탐색에서 **Issues**를 선택합니다.
2. 다음 제목의 이슈를 찾습니다.

   - Allow users to filter games by category and publisher
   - Update our repository coding standards

3. 이슈를 선택해 세부 정보를 읽습니다. 각 이슈에서 에이전트 세션을 시작할 수 있습니다. 첫 변경을 마친 다음 필터링 이슈에서 작업을 시작합니다.

> [!NOTE]
> **Issues**와 **Pull requests**의 항목 목록에는 Copilot app에 추가한 리포지토리의 항목만 표시됩니다. 다른 리포지토리의 작업을 보려면 해당 리포지토리도 앱에 추가합니다.

## 빠른 채팅 사용해 보기

빠른 채팅은 앱 자체에 관한 질문이나 브레인스토밍에 적합합니다. 브랜치나 워크트리를 만들지 않으므로 세션이 필요 없는 간단한 질문에 사용할 수 있습니다.

1. 사이드바에서 **Chats** 옆의 **+**를 선택해 새 채팅을 엽니다. **Chats**가 아직 표시되지 않으면 **Sessions** 옆의 **+**를 선택해 첫 채팅을 시작합니다. 그러면 **Chats**가 표시됩니다.
2. 앱의 세션이 어떻게 작동하는지 질문합니다.

   ```plaintext
   How does the GitHub Copilot app use worktrees?
   ```

3. 대화 보기에서 응답을 읽습니다. 각 세션이 격리된 Git 워크트리에서 실행되므로 변경 내용이 충돌하지 않게 여러 에이전트를 병렬로 실행할 수 있음을 확인합니다. 대화를 계속하거나 언제든지 새 채팅을 시작할 수 있습니다.

## 요약 및 다음 단계

GitHub Copilot app을 설치하고 프로젝트를 연결한 다음 워크스페이스를 살펴봤습니다. 다음 작업을 수행했습니다.

- 앱을 설치하고 GitHub에 로그인했습니다.
- GitHub 리포지토리에서 프로젝트를 앱에 추가했습니다.
- 워크스페이스를 살펴보고 **Issues**에서 미리 생성된 백로그를 찾았습니다.
- 빠른 채팅으로 간단한 질문을 했습니다.

다음으로 [첫 번째 에이전트 세션을 시작][next-lesson]하고 게임 카드에 별점을 표시합니다.

## 리소스

- [GitHub Copilot app 정보][about-copilot-app]
- [GitHub Copilot app 시작하기][getting-started]
- [GitHub Copilot app에서 에이전트 세션 사용][agent-sessions]

[next-lesson]: ../2-add-star-rating/
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[getting-started]: https://docs.github.com/copilot/how-tos/github-copilot-app/getting-started
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
[download-app]: https://gh.io/app
