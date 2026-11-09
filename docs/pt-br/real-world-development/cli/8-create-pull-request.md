---
title: "Lição 8 - Criar e integrar o pull request (PR) do recurso"
description: "Revise a filtragem, as instruções, a atualização da skill, o perfil de QA e os testes; depois, crie um PR e use o Agent Merge."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

A implementação da filtragem, as atualizações das instruções, a atualização da skill, o perfil de garantia de qualidade (QA) e os testes estão salvos em uma única branch. Agora, revise o conjunto e abra um pull request. Você integrou manualmente o pull request (PR) de avaliações por estrelas; desta vez, deixe que o **Agent Merge** gerencie o processo.

> [!NOTE]
> Normalmente, dividiríamos o recurso, as atualizações das instruções, a atualização da skill e o agente de QA em alguns PRs. Para simplificar o workshop, mantivemos todo o fluxo de filtragem e qualidade em uma conversa e branch, e incluiremos o trabalho neste PR.

Nesta lição, você vai:

- entender o que é o Agent Merge e como ele automatiza o ciclo de merge;
- inspecionar toda a alteração do recurso e as evidências de verificação;
- criar o PR da filtragem;
- habilitar o Agent Merge somente depois da revisão e confirmar que o PR foi integrado.

## Cenário

Durante o fluxo de filtragem, você usou o Copilot para planejar, implementar e verificar um recurso. Agora a Tailspin Toys quer automatizar o trabalho restante do PR, mantendo a autorização para o merge sob controle da pessoa desenvolvedora.

## Introdução ao Agent Merge

O **Agent Merge** automatiza o trabalho restante para integrar um pull request. Quando habilitado, o Copilot resolve os impedimentos do PR — corrige verificações de integração contínua (CI) com falha, responde aos comentários de revisão e atualiza a branch quando necessário — e, em seguida, habilita o merge automático do GitHub se o repositório permitir.

Até agora, você mesmo selecionou **Merge pull request**. O Agent Merge pode assumir essa responsabilidade. Revise o trabalho e confirme que ele está pronto antes de habilitar o Agent Merge.

## Usar o Agent Merge para gerenciar o PR

Com todo o código pronto, revise as alterações, crie o PR e deixe o Agent Merge cuidar das etapas restantes.

1. Volte ao Codespace.
2. Abra a caixa de diálogo de agente digitando `/agent`.
3. Selecione **Default** na lista e pressione <kbd>Enter</kbd>.
4. Crie um novo PR com o comando `/pr create`.
5. Ative o Agent Merge com `/pr agentmerge`.
6. O Copilot acompanhará o processo de integração contínua do PR. Quando tudo for aprovado, ele fará o merge.
7. Confirme que você recebeu uma mensagem do Copilot semelhante a `PR #14 was squash-merged successfully.`

> [!IMPORTANT]
> O Agent Merge não ignora aprovações obrigatórias, proteção de branch, filas de merge, configurações do repositório nem permissões ausentes. Se o processo for bloqueado, leia o motivo informado e faça o merge manualmente depois da revisão, quando o repositório permitir.

## Resumo e próximos passos

Você automatizou várias etapas do desenvolvimento: geração de código, testes e validação e, agora, o processo do pull request. Nesta lição, você:

- entendeu o que é o Agent Merge e como ele automatiza o ciclo de merge;
- inspecionou a alteração completa do recurso e as evidências de verificação;
- criou o PR da filtragem;
- habilitou o Agent Merge somente depois da revisão e confirmou que o PR foi integrado.

Em seguida, [explore outros comandos slash úteis do Copilot CLI][next-lesson] para contexto, modelos, compartilhamento e delegação opcional para a nuvem.

## Recursos

- [Gerenciar pull requests com o Copilot CLI][manage-prs]
- [Referência de comandos do Copilot CLI][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
