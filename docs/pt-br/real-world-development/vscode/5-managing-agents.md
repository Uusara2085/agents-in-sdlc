---
title: "Exercício 5 - Monitorar e gerenciar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lição anterior: Agentes personalizados][previous-lesson] |
|:--|

Quando você usa o GitHub Copilot no modo de agente, ele trabalha de forma autônoma: explora a base de código, propõe alterações, edita arquivos e executa comandos. Como esse trabalho acontece em tempo real no seu computador, o Copilot Chat no VS Code mostra cada chamada de ferramenta e edição de arquivo. Você pode revisar cada diff no chat, aceitar ou rejeitar alterações individuais e orientar a conversa com prompts de acompanhamento sem sair do editor.

Nesta lição, você vai:

- acompanhar em tempo real o trabalho do agente de acessibilidade;
- revisar e aceitar as edições de arquivos propostas;
- orientar o agente durante a sessão para adicionar um controle do modo claro junto com o modo de alto contraste.

## Cenário

O agente personalizado de acessibilidade usado na [Lição 4][previous-lesson] está implementando o modo de alto contraste. Enquanto o trabalho está em andamento, a equipe de design solicita também um controle do modo claro para quem considera o tema padrão escuro demais. Em vez de começar uma conversa nova, você orientará a sessão existente para ampliar o trabalho.

## Acompanhar o progresso do Copilot

A exibição Copilot Chat mostra cada etapa do agente: arquivos explorados, comandos executados e edições propostas. Cada edição de arquivo aparece no chat com um diff e os controles **Keep** e **Undo**.

1. Volte à exibição Copilot Chat da Lição 4.
2. Enquanto o agente trabalha, percorra o chat para acompanhar as chamadas de ferramentas. Você verá leituras e edições de arquivos e os comandos de terminal cuja execução foi solicitada.
3. Quando o agente propuser uma edição, o diff aparecerá no chat:
   - selecione **Keep** para aceitar a alteração;
   - selecione **Undo** para desfazê-la e permitir que o agente tente novamente.
4. Você também pode abrir o indicador **Files changed** no início do chat para ver todos os arquivos alterados pelo agente durante a sessão.

> [!NOTE]
> Se uma chamada de ferramenta solicitar permissão, por exemplo, para executar um comando de terminal, o agente pausará e exibirá uma solicitação **Allow**. Aprove apenas os comandos que considerar seguros.

5. Aguarde o agente concluir a implementação do modo de alto contraste. Você verá uma mensagem final que resume as alterações.

## Orientar o agente para adicionar o modo claro

Agora que o modo de alto contraste está pronto, amplie a mesma conversa para adicionar um controle do modo claro. Como você continuará na mesma sessão, o agente manterá o contexto do trabalho: os componentes alterados, a abordagem de estilo e o padrão de armazenamento local.

1. No campo de entrada do Copilot Chat, envie este prompt de acompanhamento:

    ```plaintext
    Nice work! Now add a light-mode toggle alongside the high-contrast toggle. Light mode should follow the same pattern — persist via local storage and be accessible from the same area of the UI. The user should be able to enable high-contrast and light mode independently.
    ```

2. O agente continuará o trabalho, explorando as alterações existentes e propondo as mudanças do modo claro.
3. Revise cada nova edição assim que aparecer, usando **Keep** ou **Undo** no diff.
4. Se o agente seguir uma direção indesejada, por exemplo, tentar refatorar os controles de uma maneira inadequada, interrompa-o com o botão **Stop** ao lado do campo de entrada e envie uma mensagem de esclarecimento.

> [!TIP]
> Orientar uma sessão em andamento é mais rápido do que começar de novo. Use prompts de acompanhamento para pedir ajustes, como "simplifique o CSS — use variáveis CSS em vez de duplicar seletores", corrigir a abordagem, como "não adicione um terceiro controle; integre o modo claro ao painel de configurações existente", ou ampliar o escopo, como "adicione também atalhos de teclado para os dois controles".

## Revisar o conjunto de alterações

Antes de fazer commit do trabalho, revise rapidamente tudo o que o agente alterou.

1. Abra a exibição **Source Control** no VS Code.
2. Revise a lista completa de arquivos alterados. Você deverá ver atualizações nos componentes Astro, nos estilos e nos testes relacionados.
3. Abra alguns arquivos alterados e examine os diffs. Confirme se eles seguem os padrões de acessibilidade do agente personalizado, incluindo:
   - os componentes de interface para alternar entre os modos;
   - o uso do armazenamento local para manter as preferências do usuário;
   - as alterações nas Folhas de Estilo em Cascata (CSS) ou nos estilos dos modos de alto contraste e claro;
   - os atributos de Accessible Rich Internet Applications (ARIA) e a navegação pelo teclado;
   - o HTML semântico e o código JavaScript/TypeScript que gerencia a alternância entre modos.
4. Quando estiver satisfeito, prepare e faça commit das alterações na exibição Source Control. Você as publicará na [próxima lição][next-lesson].

## Resumo e próximos passos

Você usou o modo de agente do Copilot Chat para acompanhar e orientar uma sessão em andamento: revisou cada edição, aceitou ou rejeitou alterações e enviou prompts de acompanhamento para ampliar o trabalho sem perder o contexto.

Nesta lição, você explorou:

- acompanhar o trabalho de um agente em tempo real;
- aceitar e rejeitar edições individuais;
- orientar uma sessão em andamento com prompts de acompanhamento.

Na [próxima lição][next-lesson], você publicará o trabalho de acessibilidade em um pull request e revisará as alterações produzidas pelo agente personalizado local durante o laboratório.

## Recursos

- [Copilot Chat no VS Code][copilot-chat-vscode]
- [Usar o modo de agente][agent-mode]

---

| [← Lição anterior: Agentes personalizados][previous-lesson] | [Próxima lição: Iterar sobre o trabalho do Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
