# Bilingual Prompt Coach

[English](README.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Español mexicano](README.es-MX.md) | [Português (Brasil)](README.pt-BR.md) | [Türkçe](README.tr.md)

Practica un idioma mientras haces tu trabajo. Este Skill de Codex se activa de forma explícita: ofrece comentarios breves sobre tu redacción antes de atender tu solicitud y agrega explicaciones en tu idioma de apoyo solo cuando son útiles.

La configuración predeterminada es chino como idioma de apoyo e inglés estadounidense claro de nivel B2–C1 como idioma de práctica. Puedes elegir ambos idiomas, la variante y el nivel del idioma de práctica, el detalle de las correcciones y la proporción de cada idioma.

Los enlaces de arriba solo cambian el idioma de la documentación. No modifican la configuración de práctica; indica tus preferencias en la conversación.

![Ejemplo en inglés con las correcciones en negritas](docs/output-example.png)

*La imagen muestra un ejemplo de respuesta en inglés. Solo los cambios de la corrección mínima aparecen en negritas.*

![Diagrama en inglés para decidir cuándo dar comentarios](docs/decision-map.jpg)

*Este diagrama está en inglés y muestra cuándo se ofrecen comentarios sobre el idioma.*

## Descripción

Haz tus solicitudes habituales de estudio, investigación, programación o trabajo cotidiano y aprende con comentarios breves que puedas aplicar después. La respuesta a tu solicitud original aparece a continuación.

- Los textos en inglés u otro idioma de práctica reciben una corrección mínima y una versión natural cuando resulta útil.
- Los textos escritos por completo en tu idioma principal reciben una versión natural en el idioma de práctica.
- Los textos que mezclan idiomas se convierten al idioma de práctica sin cambiar su significado.
- Si el texto ya es claro y natural, se agrega una nota breve en lugar de reescribirlo sin necesidad.
- Los pasajes difíciles pueden incluir una explicación breve en el idioma de apoyo justo debajo. Las respuestas habituales no se traducen párrafo por párrafo.

## Instalación

Pídele a Codex que use su instalador integrado:

```text
Use $skill-installer to install the skill from https://github.com/aolongsun/bilingual-prompt-coach.
```

También puedes clonar el repositorio en tu directorio personal de skills:

```bash
git clone https://github.com/aolongsun/bilingual-prompt-coach ~/.agents/skills/bilingual-prompt-coach
```

Reinicia Codex si el skill no aparece de inmediato.

## Uso

Invoca el skill de forma explícita junto con una solicitud concreta:

```text
$bilingual-prompt-coach I read a paper yesterday. Can you help me understand its main argument?
```

La práctica sigue activa durante la tarea actual sin tener que invocar el skill otra vez. Cada tarea nueva empieza con el modo de práctica desactivado. Puedes desactivarlo con cualquiera de estas expresiones:

```text
off
OFF!
stop coaching
Desactiva la práctica de idiomas.
```

También puedes pedirlo en tu propio idioma. Una instrucción no relacionada, como `turn the server off`, no desactiva los comentarios sobre el idioma.

## Elige tus idiomas y los comentarios

El idioma principal o de apoyo y el idioma que quieres practicar son dos ajustes independientes. Puedes indicarlos con tus propias palabras, incluso al activar el skill:

```text
$bilingual-prompt-coach Mi idioma principal es el japonés y quiero practicar inglés.
Mi idioma principal es el chino y quiero practicar japonés.
Usa inglés británico de nivel B1.
Solo inglés.
Incluye más chino, por favor.
Sin notas sobre las correcciones.
No resaltes los cambios.
Corrige el texto completo.
```

En la tarea actual se aplica la última preferencia explícita. Si no indicas otra cosa, se mantienen el apoyo en chino y la práctica de inglés estadounidense B2–C1. Cambiar de README no configura ninguno de los dos idiomas.

Si pides un idioma específico para el resultado, se usa ese idioma en la respuesta a la tarea. Por ejemplo, “Responde esta pregunta en chino” genera una respuesta en chino y conserva el bloque de práctica cuando corresponde. Las notas `Why` normalmente se escriben en el idioma de práctica, con apoyo en el idioma principal solo cuando hace falta.

## Ejemplo

Entrada:

```text
$bilingual-prompt-coach I want practice English while I work. Can you helps me?
```

Ejemplo de respuesta, conservado en inglés para mostrar las correcciones:

> ### Language practice
>
> Minimal correction: I want **to** practice English while I work. Can you **help** me?
>
> Natural phrasing: I'd like to practice English as I work. Can you help me?
>
> Why: Use “want to” before a verb. After “can,” use the base form “help.”
>
> Yes. Send your next work-related request, and I'll give brief language feedback before answering it.

Solo las inserciones y sustituciones de `Minimal correction` aparecen en negritas. `Natural phrasing` y la respuesta a la tarea no resaltan cambios. Las eliminaciones se quitan del texto; no se usan tachado, colores HTML ni formato diff de manera predeterminada. Puedes pedir correcciones sin resaltado.

Si todo el texto está en tu idioma principal, el bloque usa `Natural version` en lugar de `Minimal correction` y `Natural phrasing`.

## Límites de funcionamiento

- Los comentarios aparecen como máximo una vez por turno, al inicio de la respuesta final. No aparecen en los avances ni en la planificación intermedia. Los requisitos de salida, como entregar solo JSON o código, tienen prioridad.
- Se omiten en saludos, confirmaciones, selección de opciones, archivos adjuntos sin texto sustantivo y mensajes breves como “continúa” o “implementa el plan”.
- Se excluyen citas, fuentes pegadas, código, comandos, registros, nombres de archivo y datos, salvo que pidas editarlos.
- Si la corrección, reescritura o traducción es el resultado solicitado, no se agrega otro bloque de comentarios salvo que lo pidas.
- Para textos de más de 150 palabras, se eligen hasta tres fragmentos útiles en lugar de repetir todo el texto dos veces. Puedes pedir una corrección completa para cambiar este comportamiento.
- Las versiones conservan el significado, el tono, las afirmaciones y el grado de detalle. No agregan ideas ni hacen la solicitud más fuerte o más débil.

Este skill contiene solo instrucciones: no tiene scripts de ejecución, dependencias de herramientas externas ni memoria oculta entre tareas. El modo de práctica depende de la conversación actual. [SKILL.md](SKILL.md) contiene el único conjunto de instrucciones, escrito en inglés; los README traducidos explican el mismo skill y no son versiones independientes. La [lista de verificación de comportamiento](tests/behavior-cases.md) documenta los escenarios de validación.

## Licencia

[MIT](LICENSE)
