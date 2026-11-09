---
title: "Ejercicio 4 - Supervisar y gestionar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

En los ejercicios anteriores has pedido al agente en la nube de Copilot que se ocupe de tres tareas para mejorar la experiencia de usuario y añadir funcionalidades. Aunque el agente trabaja de forma asíncrona y autónoma, es importante poder supervisar estas tareas.

Puedes gestionar las tareas asignadas al agente en la nube con varias herramientas, incluida la [página de agentes][agents-page] de GitHub.com. Desde este panel puedes ver las tareas de los agentes que tienen solicitudes de incorporación de cambios abiertas, revisar las operaciones realizadas y orientar una sesión en curso.

En este ejercicio explorarás la página de agentes para supervisar tareas y orientar una sesión en curso con una petición adicional.

## Escenario

Después de asignar al agente la implementación de un modo de alto contraste, el equipo decide que también sería un buen momento para añadir un modo claro. Como ya se está actualizando el estilo del sitio y añadiendo controles de selección de modo, quieres orientar el trabajo del agente para que incluya ambas opciones.

## Revisa las tareas del agente en la nube

Consulta el estado de las tareas asignadas al agente en la nube de Copilot.

1. Abre la [página de agentes de Copilot](https://github.com/copilot/agents).
2. Revisa las tareas que aparecen en el panel principal y en el panel izquierdo. Deberías ver las tareas que asignaste a Copilot, entre ellas:
   - actualizar la documentación del código.
   - generar API para modificar juegos.
   - añadir un modo de alto contraste al sitio web.
3. Selecciona una tarea en curso y revisa las operaciones realizadas por Copilot. Pueden incluir:
   - obtener el código del repositorio.
   - preparar el entorno de trabajo de Copilot.
   - configurar servidores MCP.
   - realizar distintas tareas para completar el trabajo asignado.

> [!NOTE]
> Los pasos concretos varían según el estado del trabajo de Copilot y el enfoque utilizado.

4. Observa también el panel de solicitudes de incorporación de cambios de la derecha. Desde allí puedes consultar la solicitud y los archivos modificados.

## Orienta al agente en la nube

Ahora que conoces las tareas activas, pide a Copilot que añada el modo claro mientras trabaja en el modo de alto contraste.

1. Selecciona la sesión relacionada con el modo de alto contraste. El título exacto depende del nombre que Copilot haya elegido y del estado del trabajo.

    ![Sesión de accesibilidad en el panel de agentes](../../../_images/ex6-accessibility-session.png)

2. Espera unos minutos hasta que la sesión indique que la configuración ha terminado y que el trabajo ha empezado. Verás mensajes que indican ese cambio.
3. En el cuadro **Steer active session while Copilot is working**, escribe este prompt:

   ```plaintext
   While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
   ```

    ![Tarea del agente en la nube en la página de agentes con el cuadro Steer active session while Copilot is working resaltado](../../../_images/ex6-steer-cloud-agent-task.png)

4. Pulsa <kbd>Enter</kbd> para enviar el prompt.
5. Comprueba que Copilot confirma la petición y la incorpora al trabajo.

## Deja que Copilot trabaje

Copilot incorporará la nueva petición al flujo de trabajo cuando termine el paso que estaba ejecutando al recibir el mensaje. Esto puede tardar varios minutos; puedes aprovechar ese tiempo para repasar lo que has aprendido.

## Resumen y pasos siguientes

Has explorado la página de agentes de Copilot, el centro para supervisar y orientar las tareas del agente en la nube. Puedes seguir las tareas activas y completadas, revisar el trabajo y cambiar el alcance o aportar indicaciones adicionales a una sesión en curso.

Has utilizado el panel para supervisar una tarea y has enviado una petición adicional a una sesión en curso. Mientras Copilot termina el trabajo de accesibilidad, continúa con la [revisión de las solicitudes de incorporación de cambios que ha creado][next-lesson].

## Recursos

- [Página de agentes de Copilot][agents-page]
- [Acerca de los agentes personalizados][custom-agents]

---

| [← Ejercicio anterior: Agentes personalizados][previous-lesson] | [Siguiente ejercicio: Iterar sobre el trabajo de Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
