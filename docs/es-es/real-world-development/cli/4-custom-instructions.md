---
title: "Lección 4 - Guiar a Copilot con instrucciones personalizadas"
description: "Explora las instrucciones del repositorio, añade un estándar de documentación y aplícalo al código de filtrado."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

El contexto es fundamental al trabajar con inteligencia artificial generativa. Si una tarea debe realizarse de una forma concreta, proporciona a Copilot las instrucciones necesarias. Los [archivos de instrucciones][instruction-files] describen tanto qué código quieres como cómo debe estructurarse. Ahora que has creado el filtrado, explorarás las instrucciones utilizadas por Copilot, añadirás un estándar de documentación y lo aplicarás al código.

En esta lección:

- explorarás cómo llegan al agente las instrucciones del repositorio y las instrucciones específicas de rutas.
- actualizarás el archivo de instrucciones para que se sigan los estándares de código.
- comprobarás el efecto de los archivos de instrucciones en el código.

## Escenario

Tailspin Toys tiene pautas y requisitos para las prácticas de desarrollo:

- Los comentarios deben explicar la intención y las decisiones que no resulten evidentes, no repetir el código.
- Las funciones exportadas de `db/` y `src/lib/` deben documentar su propósito, parámetros y valores devueltos mediante comentarios de documentación de TypeScript (TSDoc) o JavaScript (JSDoc), incluido el argumento `db` inyectable cuando corresponda.
- Los componentes Astro reutilizables deben documentar los contratos de `Props`, y los comentarios deben mantenerse actualizados cuando cambie el código relacionado.
- Se deben conservar las pautas de formato y lint existentes.

Utilizarás archivos de instrucciones para proporcionar a Copilot el contexto necesario para seguir estas prácticas.

## Archivos de instrucciones

Las instrucciones personalizadas proporcionan a Copilot contexto y preferencias para que comprenda mejor tu estilo y requisitos de programación. Puedes indicar convenciones de código, bibliotecas y comentarios. Hay dos tipos:

- `.github/copilot-instructions.md` es un único archivo que se envía a Copilot en **todas** las solicitudes del repositorio. Debe contener información general aplicable a la mayoría de las solicitudes.
- Los archivos `.github/instructions/*.instructions.md` proporcionan pautas para lenguajes, tipos de archivo o tareas concretos.

> [!NOTE]
> Los formatos de instrucciones adicionales y su compatibilidad varían según el entorno. Consulta la [referencia de compatibilidad de instrucciones personalizadas][custom-instructions-support] antes de depender de un formato concreto.

## Explora los archivos de instrucciones personalizadas del proyecto

El proyecto inicial ya incluye varios archivos de instrucciones. Revisa los existentes antes de modificarlos para poder observar el efecto del cambio.

1. Vuelve al codespace.
2. En el editor de Codespaces, no en el terminal, abre `.github/copilot-instructions.md`.
3. Revisa la descripción breve del proyecto y las pautas de código. Estas instrucciones se aplican a todas las interacciones con Copilot en este repositorio.
4. Abre la carpeta `.github/instructions` y explora los archivos. Hay instrucciones para Astro, la capa de datos Drizzle, las pruebas y más.
5. Abre `.github/instructions/unit-tests.instructions.md`. Observa el campo `applyTo` del principio, que define las rutas de archivo a las que se aplican las instrucciones.
6. Abre `.github/instructions/drizzle.instructions.md` y revisa sus enlaces a otros archivos de instrucciones y a archivos existentes del proyecto. Así puedes dividir las instrucciones extensas en archivos reutilizables y proporcionar a Copilot ejemplos.

## Actualiza las instrucciones para reflejar las pautas del equipo

Los archivos actuales son un buen punto de partida, pero falta una pauta. Añade al archivo `copilot-instructions.md` una regla para incluir comentarios TSDoc en el nuevo código TypeScript.

1. En `.github/copilot-instructions.md`, busca la sección **Code formatting guidance**, que debería estar cerca de la línea 35.
2. Añade este elemento al final de la lista:

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

El archivo se guardará automáticamente.

## Utiliza las instrucciones actualizadas

Copilot CLI carga las instrucciones del repositorio cuando comienza una conversación. Después de guardar el cambio, sal de la conversación de filtrado y reanúdala para que Copilot lea las instrucciones nuevas sin perder el contexto de la funcionalidad.

1. Si la conversación de filtrado sigue abierta, introduce `/exit` para cerrarla. Copilot CLI guarda las conversaciones automáticamente.
2. Desde la raíz del repositorio en la rama `game-filters-cli`, reanuda la conversación guardada:

   ```bash
   copilot --resume
   ```

   Si se te solicita, selecciona la conversación de filtrado y confirma que está activa la rama `game-filters-cli`.
3. Pide a Copilot que aplique las instrucciones actualizadas:

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

4. Introduce `/diff` y revisa los archivos TypeScript modificados. Observa los comentarios TSDoc nuevos y confirma que describen el código correctamente.

## Resumen y pasos siguientes

Has explorado cómo Copilot CLI utiliza el contexto de los archivos de instrucciones y has aplicado un estándar nuevo a la funcionalidad. En esta lección:

- has explorado cómo llegan al agente las instrucciones del repositorio y las instrucciones específicas de rutas.
- has actualizado el archivo de instrucciones para que se sigan los estándares de código.
- has comprobado el efecto de los archivos de instrucciones en el código.

A continuación, [personalizarás y ejecutarás la habilidad reutilizable quality-checks][next-lesson] para aplicar de forma coherente las comprobaciones de lint y las pruebas.

## Recursos

- [Añadir instrucciones personalizadas para Copilot CLI][instruction-files]
- [Compatibilidad con instrucciones personalizadas][custom-instructions-support]
- [Prácticas recomendadas para crear instrucciones personalizadas][instructions-best-practices]
- [Awesome Copilot: colección de archivos de instrucciones y otros recursos][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
