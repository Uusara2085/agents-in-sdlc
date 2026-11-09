---
title: "Ejercicio 5 - Supervisar y gestionar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Ejercicio anterior: Agentes personalizados][previous-lesson] |
|:--|

Cuando utilizas el modo agente de GitHub Copilot, Copilot explora el código, propone cambios, edita archivos y ejecuta comandos de forma autónoma. Como el trabajo se realiza en tu equipo y en tiempo real, Copilot Chat en VS Code muestra cada llamada a herramientas y cada edición. Puedes revisar las diferencias en línea, aceptar o rechazar cambios y orientar la conversación con prompts adicionales sin salir del editor.

En este ejercicio:

- supervisarás en tiempo real el trabajo del agente de accesibilidad.
- revisarás y aceptarás los cambios propuestos en los archivos.
- orientarás al agente durante la sesión para que añada un control del modo claro además del modo de alto contraste.

## Escenario

El agente personalizado de accesibilidad del [ejercicio 4][previous-lesson] está implementando el modo de alto contraste. Mientras trabaja, el equipo de diseño pide añadir también un modo claro para las personas a quienes les resulta demasiado oscuro el tema predeterminado. En lugar de iniciar otra conversación, ampliarás el trabajo de la sesión actual.

## Supervisa el progreso de Copilot

La vista Copilot Chat muestra cada paso del agente: los archivos que explora, los comandos que ejecuta y las ediciones que propone. Las ediciones aparecen en el chat con sus diferencias y los controles **Keep** y **Undo**.

1. Vuelve a la vista Copilot Chat del ejercicio 4.
2. Mientras trabaja el agente, desplázate por el chat para observar las llamadas a herramientas, las lecturas y ediciones de archivos y los comandos de terminal que solicita ejecutar.
3. Cuando proponga una edición, revisa las diferencias en línea:
   - Selecciona **Keep** para aceptar el cambio.
   - Selecciona **Undo** para revertirlo y permitir que el agente vuelva a intentarlo.
4. También puedes abrir el indicador **Files changed** en la parte superior del chat para revisar todos los archivos modificados durante la sesión.

> [!NOTE]
> Si una llamada a herramientas requiere permiso, por ejemplo, para ejecutar un comando de terminal, el agente se detendrá y mostrará una solicitud **Allow**. Aprueba solo los comandos que te parezcan adecuados.

5. Espera a que el agente termine de implementar el modo de alto contraste. Debería mostrar un mensaje con un resumen de los cambios.

## Pide al agente que añada el modo claro

Cuando esté implementado el modo de alto contraste, ampliarás la misma conversación para añadir un control del modo claro. Como continuarás en la misma sesión, el agente conservará el contexto del trabajo anterior, incluidos los componentes y estilos modificados y el método usado para guardar la preferencia en el almacenamiento local.

1. En el campo de Copilot Chat, envía este prompt:

   ```plaintext
   Nice work! Now add a light-mode toggle alongside the high-contrast toggle. Light mode should follow the same pattern — persist via local storage and be accessible from the same area of the UI. The user should be able to enable high-contrast and light mode independently.
   ```

2. El agente continuará desde el punto anterior, revisará los cambios y propondrá añadir el modo claro.
3. Revisa cada edición, como hiciste con el modo de alto contraste. Selecciona **Keep** o **Undo** para cada diferencia.
4. Si el agente toma una dirección que no quieres —por ejemplo, intenta reorganizar los controles de modo—, detenlo con **Stop**, junto al campo de chat, y envía una indicación para aclarar lo que necesitas.

> [!TIP]
> Orientar una sesión en curso es más rápido que empezar de nuevo. Utiliza prompts adicionales para pedir ajustes, corregir el enfoque o ampliar el alcance; por ejemplo, para simplificar el CSS con variables, integrar el modo claro en el panel existente o añadir atajos de teclado.

## Revisa los cambios

Antes de confirmar el trabajo, revisa todos los archivos modificados por el agente.

1. Abre la vista **Source Control** en VS Code.
2. Revisa la lista completa de archivos modificados. Deberías ver cambios en componentes Astro, estilos y pruebas relacionadas.
3. Abre algunos archivos y revisa las diferencias. Comprueba los patrones de accesibilidad del agente personalizado: atributos de aplicaciones de Internet enriquecidas accesibles (ARIA), navegación con teclado, lenguaje de marcado de hipertexto (HTML) semántico y persistencia en el almacenamiento local.
4. Cuando estés conforme, prepara y confirma los cambios desde el panel **Source Control**. Los publicarás en el [siguiente ejercicio][next-lesson].

## Resumen y pasos siguientes

Has utilizado el modo agente de Copilot Chat para supervisar y orientar una sesión en curso: has revisado cada edición, aceptado o rechazado cambios y enviado prompts adicionales para ampliar el trabajo sin perder el contexto.

Has supervisado el trabajo del agente en tiempo real, aceptado o rechazado cambios individuales y orientado la sesión con prompts adicionales.

En el [siguiente ejercicio][next-lesson] publicarás el trabajo de accesibilidad como una solicitud de incorporación de cambios y revisarás los cambios del agente local personalizado realizados durante el laboratorio.

## Recursos

- [Copilot Chat en VS Code][copilot-chat-vscode]
- [Uso del modo agente][agent-mode]

---

| [← Ejercicio anterior: Agentes personalizados][previous-lesson] | [Siguiente ejercicio: Iterar sobre el trabajo de Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
