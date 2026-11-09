---
title: "Ejercicio 5: Iterar sobre el trabajo de GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Ejercicio anterior: Gestión de agentes][previous-lesson] |
|:--|

## Revisa el trabajo

En este laboratorio has trabajado con GitHub Copilot en varias tareas para mejorar la experiencia de usuario y añadir funcionalidades. Le has pedido que documente el código, cree una sección de juegos relacionados y añada funciones de accesibilidad con modos de alto contraste y claro. Ahora revisarás los cambios y, si es necesario, pedirás a Copilot que los mejore.

### Escenario

Los fundamentos del diseño de software y el desarrollo y operaciones (DevOps) no cambian al añadir IA generativa. Hay que revisar el código generado y seguir el proceso habitual. Revisarás las propuestas de Copilot para documentar el código, mostrar juegos relacionados y añadir las funciones de accesibilidad antes de activar la revisión para el resto del equipo.

## Seguridad y agente en la nube de GitHub Copilot

El agente en la nube de Copilot trabaja de forma asíncrona y sin supervisión directa. Para proteger el entorno:

- Copilot solo tiene acceso de lectura al repositorio y acceso de escritura **únicamente** a la rama que utiliza para el código.
- El agente se ejecuta en GitHub Actions, dentro de un entorno independiente y efímero.
- Una persona debe aprobar los flujos de trabajo de GitHub Actions antes de que se ejecuten.
- De forma predeterminada, el [acceso a recursos externos está limitado](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall), incluidos los servidores del Model Context Protocol (MCP).

## Revisa la documentación generada

Empieza por la primera solicitud de incorporación de cambios (PR) creada por el agente en la nube: la que añade documentación al código. Utilizarás la interfaz habitual de PR de GitHub.com.

> [!NOTE]
> Es posible que la PR muestre un aviso de que el cortafuegos bloquea GitHub Copilot. Es lo esperado: el acceso del agente a recursos externos, incluidas las llamadas a servidores del Model Context Protocol (MCP), está limitado de forma predeterminada. Si quieres, puedes [personalizar o desactivar el cortafuegos del agente en la nube][agent-firewall].

1. Vuelve al repositorio en github.com.
2. Selecciona **Pull Requests** para abrir la lista de solicitudes.
3. Abre la solicitud cuyo título sea parecido a **Add missing documentation**.

> [!NOTE]
> Si Copilot sigue trabajando, la PR incluirá la etiqueta **[WIP]**. Espera a que termine; puede tardar varios minutos.

4. Cuando la PR esté lista, selecciona **Files changed** y revisa los cambios.

    ![Pestaña Files changed](../../../_images/shared-pr-files-changed.png)

5. Examina el código actualizado, que incluye comentarios TSDoc y otra documentación. Los cambios concretos pueden variar. Comprueba las convenciones de TypeScript y los encabezados de comentario: proceden de los archivos de instrucciones que revisaste al principio del ejercicio 2.
6. Cuando hayas revisado los cambios, vuelve a la pestaña **Conversation** y desplázate hacia abajo.
7. Comprueba si hay flujos de trabajo pendientes de aprobación.
8. Si los hay, selecciona **Approve and run workflows**.

    ![Botón Approve and run workflows](../../../_images/shared-approve-workflows.png)

9. Comprueba que los flujos aparecen en la sección de verificaciones de la PR. Si todo va bien, las comprobaciones del proyecto para la aplicación Astro deberían superarse. Puede tardar varios minutos.

## Pide cambios a GitHub Copilot

Puedes mencionar a Copilot en un comentario de la PR o en un comentario en línea del código, igual que a otra persona del equipo. Copilot verá el comentario e iniciará otra sesión para resolverlo. Como los resultados son probabilísticos, no hay un prompt único que debas utilizar. Puedes pedir, por ejemplo:

- añadir encabezados de comentario al principio de cada archivo de código para explicar su propósito.
- añadir comentarios TSDoc a archivos TypeScript y Astro.
- crear un README que describa la estructura de la aplicación Astro.

1. Añade un comentario que solicite un cambio en la documentación generada y menciona a **@copilot**. Puedes utilizar una de las ideas anteriores u otra mejora que quieras solicitar.
2. Selecciona **View Session** para observar el trabajo. Copilot iniciará una sesión nueva para realizar los cambios.
3. Para volver a la solicitud, selecciona **Back to pull request**.

    ![Botón Back to pull request](../../../_images/ex7-back-to-pr.png)

4. Cuando Copilot termine, comprueba que la PR contiene un commit nuevo.
5. Selecciona **Files changed** y revisa los cambios.

Puedes seguir iterando hasta que estés conforme. Después, convierte la PR de borrador en lista para revisión y combínala.

![Opción para convertir la PR en lista para revisión](../../../_images/ex7-ready-for-review.png)

## Revisa la funcionalidad de juegos relacionados

Ahora revisarás la PR creada por Copilot para la incidencia sobre los juegos relacionados en la página de detalles.

1. Vuelve al repositorio en GitHub.com.
2. Selecciona la pestaña **Pull Requests**.
3. Selecciona la PR cuyo título sea parecido a **Show related games on the game details page**.
4. Selecciona **Files changed** y revisa el código generado.
5. Cuando hayas revisado los cambios, vuelve a **Conversation** y desplázate hacia abajo.
6. Comprueba si hay flujos de trabajo pendientes de aprobación.
7. Si los hay, selecciona **Approve and run workflows**.

    ![Botón Approve and run workflows](../../../_images/shared-approve-workflows.png)

8. Comprueba que los flujos aparecen en la sección de verificaciones y que las comprobaciones de la aplicación Astro se superan. Puede tardar varios minutos.
9. **Opcional:** cambia a esta rama en el codespace para probar manualmente la funcionalidad. Abre el terminal y ejecuta estos comandos; sustituye `<branch-name>` por la rama creada por Copilot, por ejemplo, `copilot/fix-8`:

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

Copilot ha creado la funcionalidad de juegos relacionados. Puedes pedirle cambios mediante un comentario nuevo en la pestaña **Conversation**; por ejemplo, ajustar cuántos juegos se muestran o añadir encabezados de comentario y comentarios TSDoc. Ten en cuenta que esta tarea se asignó antes de actualizar las instrucciones personalizadas.

## Revisa las funciones de accesibilidad

Por último, revisarás la PR de accesibilidad creada con el agente personalizado. Debe incluir el modo de alto contraste que pediste en el ejercicio 3 y el modo claro que solicitaste desde el panel de agentes en el ejercicio 4.

1. Vuelve al repositorio en GitHub.com.
2. Selecciona la pestaña **Pull Requests**.
3. Abre la PR cuyo título sea parecido a **Add high contrast mode to website**.

> [!NOTE]
> Si Copilot todavía trabaja en la tarea, la PR incluirá la etiqueta **[WIP]**. Espera a que termine; puede tardar varios minutos.

4. Selecciona **Files changed** y revisa el código generado.
5. Revisa la implementación y presta atención a:
   - los controles para cambiar de modo.
   - el uso del almacenamiento local para conservar las preferencias.
   - los cambios de hojas de estilo en cascada (CSS) para los modos de alto contraste y claro.
   - los atributos de accesibilidad, como las etiquetas de aplicaciones de Internet enriquecidas accesibles (ARIA) y la navegación con teclado.
   - el código JavaScript o TypeScript que gestiona los modos.

6. Cuando termines la revisión, vuelve a **Conversation** y desplázate hacia abajo.
7. Comprueba si hay flujos de trabajo pendientes de aprobación.
8. Si los hay, selecciona **Approve and run workflows**.

    ![Botón Approve and run workflows](../../../_images/shared-approve-workflows.png)

9. Comprueba que los flujos aparecen en la sección de verificaciones y que las comprobaciones de la aplicación Astro se superan. Puede tardar varios minutos.
10. **Opcional:** cambia a esta rama en el codespace para probar manualmente las funciones de accesibilidad. Abre el terminal y ejecuta estos comandos; sustituye `<branch-name>` por la rama que creó Copilot:

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    Inicia la aplicación y prueba los controles de alto contraste y modo claro en el navegador. Comprueba que funcionan y que las preferencias se conservan al volver a cargar la página.

El agente personalizado de accesibilidad ha orientado a Copilot para que implemente estas funciones siguiendo las prácticas recomendadas. Si detectas problemas de accesibilidad o posibles mejoras, menciona a **@copilot** en un comentario y solicita los cambios.

## Ejercicio opcional: sigue delegando

El agente en la nube resulta útil para delegar tareas reales de la lista de trabajo pendiente y ocuparte de otra cosa. Para practicarlo, crea más incidencias en el repositorio y asígnalas a Copilot. Algunas ideas:

- crear un formulario para que las personas que respaldan un juego expresen su interés en la página de detalles.
- añadir paginación a la lista de juegos.
- añadir validación de entradas y gestión de errores a las funciones de acceso a datos.

## Resumen

Has completado el recorrido del agente en la nube. En estos ejercicios:

- has inspeccionado los archivos de instrucciones personalizadas del repositorio para reconocer su efecto en el trabajo del agente.
- has asignado incidencias al agente en la nube y observado cómo prepara el entorno, planifica y trabaja de forma asíncrona.
- has creado y utilizado un agente personalizado de accesibilidad para añadir modos de alto contraste y claro.
- has utilizado la página de agentes de Copilot para supervisar y orientar la sesión de accesibilidad mientras estaba en curso.
- has revisado e iterado sobre las solicitudes de incorporación de cambios del agente en la nube, has mencionado a `@copilot` para pedir cambios y has aprobado los flujos de trabajo.

## Revisión y pasos siguientes

Si quieres seguir explorando, los otros recorridos complementan lo que has practicado:

- 🖥️ **[Recorrido de VS Code](../../vscode/)**: explora el modo agente de Copilot Chat y la integración de MCP desde el IDE.
- 💻 **[Recorrido de CLI](../../cli/)**: entrega dos cambios revisados desde el terminal con Plan y Autopilot, habilidades de agente, un agente de QA, Playwright MCP, Agent Merge y el puente opcional `/delegate` al agente en la nube.

En tu propio repositorio, prueba estas ideas:

- asigna al agente en la nube una incidencia de refactorización o cobertura de pruebas.
- crea un agente personalizado para otro ámbito.
- configura `copilot-setup-steps.yml` para otra pila tecnológica.

## Recursos

- [GitHub Copilot][github-copilot]
- [Acerca de los agentes de Copilot][copilot-agents]
- [Asignar incidencias de GitHub a Copilot][assign-issue]
- [Prácticas recomendadas para el flujo de configuración del agente en la nube][cloud-agent-best-practices]
- [Configurar el cortafuegos del agente en la nube][agent-firewall]

---

| [← Ejercicio anterior: Gestión de agentes][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall
[previous-lesson]: ../4-managing-agents/
