---
title: "Lección 6 - Validar la funcionalidad con Playwright MCP"
description: "Comprueba la configuración de Playwright MCP en Copilot CLI y utilízala para explorar el filtrado en un navegador."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Como ya hemos comentado, desarrollar no consiste solo en escribir código. También hay que trabajar con datos y servicios externos, y ampliar las automatizaciones disponibles para Copilot. Los servidores del Model Context Protocol (MCP) permiten que Copilot CLI utilice más herramientas y servicios.

En esta lección:

- conocerás el Model Context Protocol (MCP) y cómo lo utiliza Copilot CLI.
- añadirás el servidor Playwright MCP si todavía no está disponible.
- pedirás al agente que maneje un navegador para explorar el filtrado.

## Escenario

Las pruebas unitarias y de extremo a extremo son importantes, pero para validar cambios en la interfaz hay que interactuar con ella. Permitirás que Copilot utilice el sitio como lo haría una persona y automatice más comprobaciones para aumentar la confianza en el resultado.

## Qué es el Model Context Protocol (MCP)

El [Model Context Protocol (MCP)][mcp-blog-post] permite que los agentes de IA se comuniquen con herramientas y servicios externos. Así pueden acceder a información actualizada y realizar acciones en tu nombre.

Los agentes acceden a estas herramientas y recursos mediante un servidor MCP, que actúa como puente entre el agente y las herramientas y servicios externos. Cada servidor ofrece un conjunto distinto de herramientas y recursos.

Algunos servidores MCP populares son:

- **[GitHub MCP Server][github-mcp]**: proporciona acceso a interfaces de programación de aplicaciones (API) para gestionar repositorios, incidencias y solicitudes de incorporación de cambios de GitHub.
- **[Playwright MCP Server][playwright-mcp-server]**: proporciona automatización del navegador mediante Playwright.

Hay muchos otros servidores MCP disponibles. GitHub aloja un [registro de MCP][mcp-registry] para facilitar su descubrimiento y las contribuciones al ecosistema.

> [!CAUTION]
> Trata los servidores MCP como cualquier otra dependencia del proyecto. Antes de utilizar uno, revisa su código fuente, comprueba quién lo publica y considera las implicaciones de seguridad.

## Añade el servidor Playwright MCP

Si Playwright MCP todavía no está disponible, añádelo para que Copilot pueda interactuar con el sitio.

> [!NOTE]
> Si Playwright MCP ya está configurado en Copilot CLI, omite estos pasos y continúa con la sección siguiente.

1. Vuelve al codespace.
2. En Copilot CLI, introduce este comando para abrir el cuadro de diálogo de configuración:

   ```plaintext
   /mcp add
   ```

3. En el campo de nombre, escribe `playwright` y pulsa <kbd>Tab</kbd>.
4. Confirma el tipo de servidor **STDIO** con <kbd>Enter</kbd> y pulsa <kbd>Tab</kbd>.
5. Pega lo siguiente en el cuadro **Command**:

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. Pulsa <kbd>Control</kbd>+<kbd>S</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>S</kbd> (Windows/Linux) para guardar el servidor MCP.
7. Pulsa <kbd>Esc</kbd> para cerrar el cuadro de diálogo MCP.

## Pide a Copilot que explore la funcionalidad con Playwright

Ya has comprobado manualmente que la funcionalidad funciona. Ahora pedirás a Copilot que haga lo mismo con el servidor Playwright MCP.

1. Envía este prompt para pedir a Copilot que valide la funcionalidad con el servidor:

   ```plaintext
   Start the app and use Playwright MCP to check filtering against the issue and our plan. Tell me what works and what doesn't, without making changes. Stop the server you started when you're done.
   ```

> [!NOTE]
> No es imprescindible indicar a Copilot que utilice el servidor MCP; normalmente lo detectará. Aun así, especificar la herramienta puede hacer que el resultado sea más coherente y reducir el uso de tokens.

2. Observa los pasos que Copilot realiza en el navegador para comprobar la funcionalidad.
3. Lee el informe y confirma que todo se comporta como esperas.

Copilot iniciará el servidor, utilizará Playwright para interactuar con el sitio, detendrá el servidor y te entregará un informe.

## Resumen y pasos siguientes

Has utilizado Playwright MCP para explorar la funcionalidad en un navegador real desde Copilot CLI. En esta lección:

- has conocido el Model Context Protocol (MCP) y cómo lo utiliza Copilot CLI.
- has añadido el servidor Playwright MCP si todavía no estaba disponible.
- has pedido al agente que maneje un navegador para explorar el filtrado.

A continuación, [crearás un agente de control de calidad (QA)][next-lesson] que combinará la habilidad y las herramientas del navegador en un rol especializado.

## Recursos

- [Qué es MCP y por qué se habla tanto de él][mcp-blog-post]
- [Servidor Playwright MCP de Microsoft][playwright-mcp-server]
- [Añadir servidores MCP a Copilot CLI][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
