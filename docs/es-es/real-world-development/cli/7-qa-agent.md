---
title: "Lección 7 - Crear y utilizar un agente de QA"
description: "Crea un agente de QA que combine los requisitos de la incidencia, la habilidad quality-checks y Playwright MCP."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Has utilizado la habilidad `quality-checks` para ejecutar comprobaciones automatizadas y el servidor Playwright del Model Context Protocol (MCP) para observar el filtrado en un navegador. Ahora reunirás estas capacidades en un agente personalizado con un proceso de control de calidad (QA) definido.

En esta lección:

- explorarás cómo un agente personalizado utiliza instrucciones, habilidades y herramientas MCP.
- crearás y revisarás un perfil de control de calidad reutilizable.
- seleccionarás el agente de QA y revisarás sus conclusiones respecto a la incidencia de filtrado.

## Escenario

Tailspin Toys quiere revisar de forma coherente los requisitos, la calidad del código, las comprobaciones automatizadas, la cobertura de pruebas y el comportamiento en el navegador antes de abrir una solicitud de incorporación de cambios (PR). Un agente personalizado puede coordinar el proceso de QA y proporcionar un informe reutilizable.

## Qué es un agente personalizado

Un agente personalizado es una versión especializada de Copilot definida en un perfil Markdown. El perfil describe el propósito, las instrucciones y las herramientas disponibles para el agente. En este taller, crearás el rol de QA en `.github/agents/qa.agent.md` y lo seleccionarás en Copilot CLI.

Cada personalización cumple una función distinta. Las instrucciones del repositorio describen los estándares del equipo; la habilidad `quality-checks` reúne comprobaciones repetibles; Playwright MCP proporciona herramientas de navegador; y el perfil de QA indica a Copilot cómo utilizar esas capacidades para revisar los requisitos y comunicar los resultados. El perfil no sustituye a las otras personalizaciones ni requiere otra conversación.

## Crea el perfil de QA

Antes de abrir la PR de la funcionalidad, pedirás a Copilot que cree un perfil de QA reutilizable. El perfil definirá las comprobaciones y los límites que debe respetar.

1. Vuelve al codespace y confirma que la conversación de filtrado está en modo Interactive.
2. Pide al agente predeterminado que cree el agente personalizado:

   ```plaintext
   Create a custom agent named QA in .github/agents/qa.agent.md. It should check features against their issues and agreed requirements, follow the repository instructions, run the quality-checks skill, use Playwright MCP to verify behavior, and add tests when coverage is missing.

   Have it report each requirement as pass, fail, or blocked with supporting evidence. It must ask before changing implementation code, and it must not commit changes or open pull requests.

   Just create the profile for now so I can review it.
   ```

## Revisa el perfil

Antes de utilizar el nuevo agente, revisa el perfil para confirmar que incluye el proceso de QA y sus límites. Así evitarás que un perfil incompleto o demasiado amplio modifique la funcionalidad cuando solo quieres verificarla.

1. Introduce `/diff` y abre `.github/agents/qa.agent.md`.
2. Lee el frontmatter. `description` es obligatorio; `name` es opcional, pero proporciona un nombre claro en la interfaz.
3. Comprueba que las instrucciones indican que QA debe partir de los requisitos, seguir las instrucciones del repositorio, ejecutar la habilidad `quality-checks` y utilizar Playwright MCP.
4. Confirma que el agente presenta pruebas que respaldan sus resultados, pide permiso antes de modificar el código de implementación y no crea commits ni solicitudes de incorporación de cambios.
5. Si faltan responsabilidades o límites, pide al agente predeterminado que revise el perfil antes de continuar.

## Ejecuta QA para la incidencia

Copilot CLI carga los agentes del proyecto al iniciar una conversación. Después de crear el perfil, reanuda la misma conversación de filtrado y selecciona QA para que pueda utilizar la incidencia y las decisiones de planificación que ya están en el contexto.

1. Activa el agente con este prompt:

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> Como acabas de crear el agente, es posible que no aparezca en la lista de agentes disponibles. El comando anterior lo activará.

2. Pide al agente de QA que revise la funcionalidad:

   ```plaintext
   Review the filtering feature against the issue and the decisions in our plan. Is it ready for a PR?
   ```

3. Deja que el agente de QA complete la revisión.
4. Lee el informe que genere.

## Resumen y pasos siguientes

Has añadido un rol especializado reutilizable y has revisado sus conclusiones. En esta lección:

- has explorado cómo un agente personalizado utiliza instrucciones, habilidades y herramientas MCP.
- has creado y revisado un perfil de control de calidad reutilizable.
- has seleccionado el agente de QA y revisado sus conclusiones respecto a la incidencia de filtrado.

Ya tienes la implementación, la actualización de la habilidad, el perfil de QA, las pruebas y el informe de verificación preparados para la revisión. A continuación, [los reunirás en una PR de la funcionalidad y utilizarás Agent Merge][next-lesson].

## Recursos

- [Crear agentes personalizados para Copilot CLI][create-agents]
- [Configuración de agentes personalizados][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
