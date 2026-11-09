---
title: "Ejercicio 2 - Añadir funcionalidades con el modo agente de Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Incluso los cambios sencillos de una aplicación pueden requerir modificar varios archivos y ejecutar pruebas. Como desarrollador, tendrás que localizar los archivos adecuados, realizar los cambios, ejecutar las pruebas, depurar los fallos y volver a modificar el código si falta algo.

El modo agente de Copilot puede explorar la estructura del proyecto, modificar varios archivos, ejecutar tareas como las pruebas y corregir los errores que detecta. En este ejercicio lo utilizarás para añadir una funcionalidad al sitio.

> [!NOTE]
> Aunque los nombres se parecen, el modo agente y el agente en la nube ofrecen experiencias distintas. El modo agente trabaja en tu IDE y permite ciclos de respuesta rápidos. El agente en la nube trabaja de forma asíncrona, como un miembro del equipo, y se comunica contigo mediante incidencias y solicitudes de incorporación de cambios.

En este ejercicio:

- utilizarás el modo agente para explorar el proyecto, localizar archivos y coordinar cambios.
- implementarás una funcionalidad en la interfaz y la capa de datos.
- revisarás los cambios y las pruebas antes de combinarlos.

## Escenario

El catálogo de juegos crece y quieres que los usuarios puedan filtrarlo por categoría y editor. En el ejercicio anterior ya creaste un helper de editores. Ahora completarás el trabajo restante en la capa de datos, la interfaz y las pruebas con el modo agente de Copilot.

## Ejecuta el sitio de Tailspin Toys

Antes de hacer cambios, explora el sitio para conocer su comportamiento actual.

Tailspin Toys es una plataforma de financiación colectiva de juegos de mesa con un tema de desarrollo de software. Permite consultar juegos y sus detalles. El sitio es una única aplicación Astro que genera páginas HTML estáticas durante la compilación. Las páginas consultan directamente una base de datos SQLite local mediante Drizzle ORM; no hay una API independiente ni un framework de interfaz en el cliente. Los helpers de acceso a datos se encuentran en `src/lib/`, y la interactividad se implementa con scripts Astro pequeños y acotados que utilizan interfaces de programación de aplicaciones (API) estándar del modelo de objetos del documento (DOM).

### Inicia el sitio

La tarea `npm run dev` inicia el único servidor de desarrollo Astro. Puedes ejecutarla en el codespace:

1. Vuelve al codespace. Deberías estar en `main` después del ejercicio anterior.
2. Abre un terminal con <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
3. Actualiza `main` y crea una rama para el filtrado:

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. Inicia el sitio:

   ```bash
   npm run dev
   ```

Cuando el servidor esté listo, debería mostrar un mensaje con la URL, parecido a este:

```bash
🚀 Tailspin Toys is ready!
   Astro server: http://localhost:4321
   Press Ctrl-C to stop.
```

> [!NOTE]
> Si aparece un cuadro de diálogo para abrir `http://localhost:4321` en un navegador, ciérralo seleccionando **x**.

5. Mantén pulsada la tecla <kbd>Command</kbd> (Mac) o <kbd>Ctrl</kbd> (Windows/Linux) y selecciona `http://localhost:4321` en el terminal.

> [!NOTE]
> En un codespace, el enlace de localhost se redirige automáticamente a `https://<your-codespace-name>-4321.app.github.dev/`, un túnel privado al servidor del codespace.

### Explora el sitio

Cuando el sitio esté en ejecución, explora sus funciones principales:

- **Home Page** muestra juegos de mesa, con sus títulos, imágenes y descripciones.
- **Game Details Page** muestra información de un juego, como el título, la descripción, el editor y la categoría.

## Explora la lista de trabajo pendiente con Copilot

> [!TIP]
> **Abre Copilot Chat**
>
> Antes de continuar, vuelve al codespace, abre el panel Copilot Chat y selecciona **New Chat** para iniciar una conversación nueva. El modo y el modelo varían según el ejercicio; cada paso indica cuál debes utilizar.

La plantilla del proyecto creó incidencias automáticamente. Pide a GitHub Copilot que te muestre esos elementos.

1. En el selector de agentes de la vista Chat, selecciona **Agent**. El agente planifica y aplica cambios en varios archivos, ejecuta comandos y utiliza herramientas.

   ![Selector de agentes en la vista Chat](../../../_images/shared-chat-mode-selector.png)

2. Selecciona **Claude Sonnet 4.5** en la lista de modelos disponibles.

> [!CAUTION]
> Los autores no recomiendan un modelo sobre otro. Se incluye Claude Sonnet 4.5 porque se utilizó al crear el taller, con la intención de mantener una experiencia coherente. Los modelos de lenguaje grandes (LLM) son probabilísticos y pueden producir resultados distintos a los ejemplos. Es normal.

> [!NOTE]
> Copilot puede utilizar un comando MCP diferente y aun así completar la tarea.

3. Envía este prompt:

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. Selecciona **Continue** para permitir que enumere las incidencias.
5. Revisa la lista generada.

## Revisa los archivos de instrucciones

Antes de generar código, revisa el archivo de instrucciones de interfaz de usuario, que proporciona contexto sobre cómo añadir funcionalidades al sitio.

1. En el codespace, abre `.github/instructions/ui.instructions.md`.
2. Revisa la arquitectura, los principios de diseño de componentes, las pautas de pruebas y accesibilidad y los enlaces a instrucciones para Astro, Tailwind CSS y Drizzle.

> [!TIP]
> Los archivos de instrucciones pueden enlazar a otros archivos de instrucciones y a archivos del proyecto. Las rutas son relativas al archivo de instrucciones, lo que permite reutilizar contenido, dividir pautas extensas y proporcionar ejemplos.

## Implementa el filtrado

Para completar el filtrado tendrás que añadir o ajustar la lógica de acceso a datos en `src/lib/`, crear o actualizar pruebas y añadir la interfaz de filtrado a la página de listado de juegos. Copilot puede realizar este trabajo y ejecutar las pruebas.

1. Continúa en la conversación actual o selecciona **New Chat**.
2. Selecciona **Add Context**, **Instructions** y **ui** para añadir el archivo de instrucciones.

   ![Selección del archivo de instrucciones de interfaz de usuario](../../../_images/ex3-select-instructions-file.png)

3. Confirma que **Agent** está seleccionado en el selector de agentes.

   ![Selector de agentes en la vista Chat](../../../_images/shared-chat-mode-selector.png)

4. Confirma que el modelo seleccionado es **Claude Sonnet 4.5**.
5. Pide a Copilot que implemente la incidencia relacionada:

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. Observa cómo Copilot explora el proyecto, localiza los helpers de datos, la interfaz y las pruebas, y modifica los archivos.

   ![Copilot explora los archivos del proyecto](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot puede tardar varios minutos en explorar, modificar archivos y ejecutar pruebas. Durante el proceso pueden aparecer los controles **Keep** y **Undo**. Cuando termine, podrás aceptar o revertir cada cambio; no hace falta seleccionarlos mientras el agente sigue trabajando.

7. Cuando Copilot lo solicite, selecciona **Continue** para ejecutar las pruebas.

   ![Cuadro de Copilot Chat que solicita confirmación para ejecutar pruebas](../../../_images/ex3-agent-mode-run-tests.png)

8. Es normal que el proceso incluya pausas o que fallen algunas pruebas. Copilot puede alternar entre generar código y ejecutar pruebas hasta que termine y no detecte errores.

   ![Sesión de Copilot Chat terminada con cambios propuestos](../../../_images/ex3-agent-mode-proposed-changes.png)

9. Revisa el código generado para detectar posibles problemas.

> [!CAUTION]
> Revisa siempre el código generado por Copilot o cualquier otra herramienta de IA.

10. Vuelve al navegador con el sitio en ejecución y explora la nueva funcionalidad.
11. Cuando hayas revisado el código y confirmado que funciona, selecciona **Keep** en Copilot Chat.

## Resumen y pasos siguientes

Has utilizado el modo agente de GitHub Copilot para desarrollar el sitio Tailspin Toys. En este ejercicio:

- has explorado el proyecto, identificado archivos relevantes y coordinado cambios.
- has implementado una funcionalidad en la interfaz y la capa de datos.
- has revisado los cambios y las pruebas antes de integrarlos.

A continuación, [probarás la funcionalidad con el servidor Playwright MCP][next-lesson] y abrirás una solicitud de incorporación de cambios.

### Ejercicio adicional: implementar paginación

Cuando crezca la lista de juegos, puede ser necesario añadir paginación. Utiliza lo aprendido para pedir a Copilot que la implemente. Sigue las instrucciones existentes, decide si los usuarios podrán elegir el tamaño de página y aporta a Copilot el contexto necesario. Es posible que tengas que iterar y aclarar la petición; es una parte normal del trabajo.

## Recursos

- [Modos ask, edit y agent de Copilot: qué hacen y cuándo utilizarlos][choose-mode]
- [Modo agente en VS Code][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
