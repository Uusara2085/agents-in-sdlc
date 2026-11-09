---
title: "Ejercicio 2 - Agente en la nube de GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Ejercicio anterior: Instrucciones personalizadas][previous-lesson] |
|:--|

Muy pocas organizaciones están libres de deuda técnica. Puede tratarse de problemas de seguridad sin resolver, código heredado que necesita actualizarse o solicitudes de funcionalidades que llevan tiempo en la lista de trabajo pendiente porque no ha habido tiempo para implementarlas. El agente en la nube de GitHub Copilot puede actualizar código y añadir funcionalidades de forma autónoma. Cuando termina, crea una solicitud de incorporación de cambios (PR) en borrador para que la revise un desarrollador. Así puedes delegar tareas tediosas, acelerar el desarrollo y centrarte en cuestiones de mayor alcance.

En este ejercicio explorarás:

- cómo personalizar el entorno de generación de código.
- cómo proteger las operaciones.
- la importancia de delimitar bien las incidencias.
- cómo asignar incidencias a Copilot.

## Escenarios

Tailspin Toys quiere resolver varios problemas de deuda técnica. La documentación del sitio está incompleta. Como primer paso, el equipo quiere añadir comentarios de documentación de TypeScript (TSDoc) a todas las funciones exportadas de la aplicación.

Además, el equipo de diseño quiere facilitar el descubrimiento de juegos. Quiere mostrar juegos relacionados —otros títulos de la misma categoría— en la página de detalles de cada juego para que los visitantes puedan seguir explorando. No necesita una implementación acabada; quiere algo que permita hacer pruebas de aceptación de la experiencia. Es un impedimento, aunque hay incidencias de mayor prioridad.

Son tareas que pueden quedar relegadas con facilidad y que se pueden asignar al agente en la nube de Copilot. Mientras el agente trabaja de forma asíncrona, el desarrollador puede ocuparse de otras tareas y volver después para revisar el resultado.

## Acerca del agente en la nube de GitHub Copilot

El [agente en la nube de GitHub Copilot](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) realiza tareas en segundo plano de forma parecida a un desarrollador. Por ejemplo, puedes [asignar una incidencia de GitHub a Copilot](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions). Después, Copilot crea una PR en borrador para seguir el progreso, prepara un entorno y empieza a trabajar. Puedes consultar la sesión mientras sigue en curso o después de que termine. Cuando la solución esté lista para revisión, Copilot te mencionará en la PR.

## La importancia de delimitar bien las tareas

GitHub Copilot no hace magia ni evita tener que pensar. Incluso las tareas aparentemente sencillas pueden volverse complejas al analizarlas en detalle. [Delimita cuidadosamente las tareas para el agente en la nube][cloud-agent-best-practices]. Utilízalo como compañero de programación con IA: trabaja por etapas, aprende, experimenta y adapta el enfoque. Los fundamentos del desarrollo de software no cambian al añadir IA generativa.

## Instrucciones personalizadas de este repositorio

En ejercicios anteriores has visto cómo las instrucciones personalizadas orientan a Copilot. Si ya has completado el ejercicio práctico sobre instrucciones, habrás visto `.github/copilot-instructions.md` en funcionamiento. Antes de asignar trabajo al agente en la nube, revisa los archivos de instrucciones que ya incluye este repositorio; así podrás reconocer más adelante su efecto.

Abre estos archivos en la interfaz web de GitHub o en un codespace que ya esté activo:

1. Abre `.github/copilot-instructions.md` y revisa **Code standards**, en especial las convenciones de TypeScript y los comentarios TSDoc.
2. Abre `.github/instructions/unit-tests.instructions.md` y observa el frontmatter `applyTo`, que aplica estas instrucciones a los archivos `**/*.test.ts`.

Cuando asignes al agente en la nube la incidencia `Code lacks documentation`, observa si la PR resultante incluye comentarios TSDoc, convenciones de TypeScript y encabezados de comentario. Estas pautas proceden de los archivos de instrucciones. Volverás a revisarlas al analizar las PR en un ejercicio posterior.

## Prepara el entorno de desarrollo del agente en la nube

El desarrollo de código suele requerir un entorno específico y scripts de configuración para instalar herramientas y dependencias. Lo mismo ocurre cuando asignas tareas a Copilot, que trabaja de forma parecida a un ingeniero de software (SWE).

El agente en la nube utiliza [GitHub Actions][github-actions] como entorno de trabajo. Puedes personalizarlo mediante un [flujo de trabajo de configuración][setup-workflow] especial, definido en `.github/workflows/copilot-setup-steps.yml`, que se ejecuta antes de que el agente empiece. El laboratorio ya incluye esta configuración. Proporciona Node.js, las dependencias del proyecto, los navegadores de Playwright para las pruebas de extremo a extremo y la base de datos SQLite migrada y precargada de la aplicación Astro:

```yaml
name: "Copilot Setup Steps"

# Allows you to test the setup steps from your repository's "Actions" tab
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # Set the lowest permissions needed for *your steps*. Copilot will be given its own token for its operations.
    permissions:
      # If you want to clone the repository as part of your setup steps, for example to install dependencies, you'll need the `contents: read` permission. If you don't clone the repository in these steps, Copilot will do this for you automatically after the steps complete.
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # Frontend / app setup - Node.js (the whole app is now Astro + Drizzle/libSQL)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # Migrate + seed the local SQLite database so builds and tests have data.
      - name: Set up the database
        run: npm run db:setup
```

El archivo se parece a cualquier otro flujo de trabajo de GitHub, pero tiene dos aspectos importantes:

- Incluye un único trabajo llamado `copilot-setup-steps`, que se ejecuta en GitHub Actions antes de que Copilot empiece a trabajar en la PR.
- El activador `workflow_dispatch` permite ejecutar manualmente el flujo desde la pestaña **Actions** del repositorio. Esto sirve para comprobar que funciona sin esperar a que Copilot lo ejecute.

## Añade documentación

Aunque la documentación es importante, muchos proyectos tienen información obsoleta o carecen de ella. Esta deuda técnica puede reducir la productividad y dificultar el mantenimiento del código o la incorporación de nuevos desarrolladores. Copilot puede generar documentación, por lo que esta es una buena tarea para asignarle. Más adelante revisarás el resultado.

1. Abre tu repositorio en github.com en una pestaña nueva del navegador.
2. Selecciona la pestaña **Issues**.
3. Selecciona **New issue** para abrir el cuadro de creación.
4. Selecciona **Blank issue**.
5. En **Title**, escribe `Code lacks documentation`.
6. En **Description**, escribe:

   ```plaintext
   Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
   ```

7. Selecciona **Create** para crear la incidencia.
8. A la derecha, selecciona **Assign to Copilot** para abrir el cuadro de asignación.

   ![Asignación de Copilot a una incidencia](../../../_images/shared-assign-copilot.png)

9. Selecciona **Assign**.

   ![Detalles de la asignación de Copilot](../../../_images/ex4-assign-copilot-details.png)

10. Selecciona la pestaña **Pull Requests**.
11. Abre la nueva PR, cuyo título será parecido a `[WIP]: Code lacks documentation`. Si todavía no aparece, espera un momento y vuelve a cargar la página.
12. Al cabo de unos minutos, Copilot debería crear una lista de tareas.

> [!NOTE]
> La lista puede tardar varios minutos en aparecer. Copilot está preparando el entorno mediante el flujo de trabajo descrito antes, analizando el proyecto y determinando cómo abordar la tarea.

13. Revisa la lista y las tareas que realizará Copilot.
14. Desplázate por la cronología de la PR y comprueba que Copilot ha empezado a trabajar en la incidencia.
15. Selecciona **View session**.

   ![Vista de la sesión de Copilot](../../../_images/ex4-view-session.png)

> [!CAUTION]
> Es posible que tengas que volver a cargar la página para ver el indicador actualizado.

16. Recorre la sesión en directo y observa cómo Copilot explora el código, analiza su estado, decide un plan y crea código.

La tarea puede tardar varios minutos. El agente en la nube permite trabajar de forma asíncrona y dedicarte a otras tareas. Aprovecharás esta función asignándole otra tarea y, mientras tanto, escribirás código para añadir funcionalidades a la aplicación.

## Añade una sección de juegos relacionados

Una ventaja del agente en la nube es que permite dividir el trabajo. Mientras Copilot trabaja en la sección de juegos relacionados que solicita el equipo de diseño, puedes ocuparte de otras tareas.

1. Vuelve al repositorio en github.com.
2. Selecciona la pestaña **Issues**.
3. Selecciona **New issue** para abrir el cuadro de creación.
4. Selecciona **Blank issue**.
5. En **Title**, escribe `Show related games on the game details page`.
6. En **Description**, escribe:

   ```markdown
   We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
   ```

7. Selecciona **Create** para crear la incidencia.
8. A la derecha, selecciona **Assign to Copilot** para abrir el cuadro de asignación.
9. Selecciona **Assign**.

Poco después, aparecerá un emoji 👀 en el primer comentario de la incidencia para indicar que Copilot está trabajando en ella.

![Copilot utiliza el emoji de ojos para indicar que está trabajando en la incidencia](../../../_images/ex4-issue-eyes-emoji.png)

Copilot ya está trabajando en la segunda solicitud. No es necesario que lo supervises continuamente; puedes revisar el resultado cuando termine. A continuación, crearás y utilizarás agentes personalizados.

## Resumen y pasos siguientes

Has explorado el agente en la nube de GitHub Copilot y cómo asignarle incidencias para que trabaje de forma asíncrona. Puede ayudar a resolver deuda técnica, crear funcionalidades o migrar código entre frameworks.

Has explorado el agente en la nube de GitHub Copilot y cómo asignarle incidencias para que trabaje de forma asíncrona. En este ejercicio:

- has personalizado el entorno de generación de código.
- has revisado cómo proteger las operaciones.
- has delimitado incidencias.
- has asignado trabajo a Copilot.

El agente en la nube también puede utilizar servidores del Model Context Protocol (MCP) y las instrucciones personalizadas que has explorado en ejercicios anteriores. Continúa con la creación y el uso de [agentes personalizados][next-lesson].

## Recursos

- [Acerca del agente en la nube de Copilot][copilot-agents]
- [Asignar incidencias de GitHub a Copilot][assign-issue]
- [Prácticas recomendadas para el flujo de configuración del agente en la nube][cloud-agent-best-practices]

| [Siguiente ejercicio: Agentes personalizados →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
