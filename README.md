# Skills de Zoy

Skills compartidas para crear documentos HTML visuales y escribir con claridad.
Se pueden instalar globalmente en Windows, Linux y macOS mediante
[`npx skills`](https://github.com/vercel-labs/skills).

| Skill | Para qué sirve |
| --- | --- |
| [html-communication](skills/html-communication/SKILL.md) | Explicar análisis y alternativas con HTML integrado en el chat de T3 Code o como archivo autónomo, con diagramas y comparaciones cuando ayuden. |
| [unslop](skills/unslop/SKILL.md) | Eliminar frases vacías, adornos y patrones de escritura artificial. |

`html-communication` usa `unslop`; instalar ambas. Incluye instrucciones,
una referencia del contrato de T3 Code y una plantilla HTML reutilizable.
La instalación no ejecuta scripts de validación ni añade las herramientas de T3.

## Instalar

Se necesita Git y una versión de Node.js compatible con el CLI `skills`.
El siguiente comando funciona en PowerShell y Bash. La opción `--copy` evita
necesitar permisos para enlaces simbólicos en Windows.

```sh
npx skills@latest add zoysoftware/skills --global --agent codex --skill html-communication unslop --copy
```

Para Cursor, sustituir `--agent codex` por `--agent cursor`.
Para instalar en ambos, usar `--agent codex cursor`.
Revisar el resumen antes de confirmar si ya existen skills con esos nombres.

Para ver las skills disponibles sin instalar:

```sh
npx skills@latest add zoysoftware/skills --list
```

## Actualizar

Repetir el comando de instalación obtiene el contenido actual del repositorio.
Para conservar explícitamente el agente y el modo de copia en cada actualización:

```sh
npx --yes skills@latest add zoysoftware/skills --global --agent codex --skill html-communication unslop --copy --yes
```

Usar los mismos agentes elegidos al instalar. La actualización puede reemplazar
las copias instaladas, por eso las mejoras se hacen en el repositorio.
La instalación no crea una sincronización automática. Se puede ejecutar este
comando antes de empezar una sesión o programarlo con las herramientas del
sistema operativo.

## Usar

En Codex, por ejemplo:

```text
Usa $html-communication para comparar estas opciones visualmente en el chat.
Usa $unslop para revisar la redacción.
```

Cuando T3 Code expone `html_preview` y `html_render`, la skill comprueba la
página y la muestra dentro de la conversación. El contenido hereda el tema,
las fuentes y el ancho del chat, sin un marco exterior ni fondo oscuro fijo.
La [referencia de T3](skills/html-communication/references/t3-code.md) documenta
los colores, tamaños y el flujo de entrega. La
[plantilla](skills/html-communication/assets/t3-inline.html) permite empezar
con comparaciones adaptables a escritorio y móvil.

Sin esas herramientas, o si se pide un archivo, entrega un HTML autónomo con
estilos y recursos incorporados. HTML, CSS y controles nativos son la base;
JavaScript inline queda reservado para interacciones locales que ayuden a
entender el contenido. Los datos y la explicación inicial siguen siendo legibles
sin ejecución ni red. Para pedir un documento estático explícitamente:

```text
Usa $html-communication para comparar estas opciones en un archivo HTML autónomo sin JavaScript.
```

La skill guía la revisión del contenido, contraste, foco y diseño en escritorio
y móvil. No depende del monorepo ni requiere un destino de hosting para entregar
el documento.

## Mejorar las skills

Cada skill vive en `skills/<nombre>/SKILL.md`, con `name` y `description` en el
frontmatter. Editar la fuente, revisar el cambio y publicarlo en la rama `main`.
Los demás reciben los cambios publicados al actualizar. No añadir rutas de
equipos personales, secretos ni instrucciones que dependan del monorepo privado.
