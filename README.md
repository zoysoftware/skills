# Skills de Zoy

Skills compartidas para crear documentos HTML visuales y escribir con claridad.
Se pueden instalar globalmente en Windows, Linux y macOS mediante
[`npx skills`](https://github.com/vercel-labs/skills).

| Skill | Para qué sirve |
| --- | --- |
| [html-communication](skills/html-communication/SKILL.md) | Explicar especificaciones, planes y alternativas en un HTML autónomo, visual y legible, con diagramas y comparaciones cuando ayuden. |
| [unslop](skills/unslop/SKILL.md) | Eliminar frases vacías, adornos y patrones de escritura artificial. |

`html-communication` usa `unslop`; instalar ambas. Las skills contienen solamente
instrucciones y no ejecutan scripts de validación.

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
Usa $html-communication para comparar estas opciones en un documento HTML.
Usa $unslop para revisar la redacción.
```

El HTML generado es un único archivo con estilos y recursos incorporados,
sin JavaScript ni dependencias de red. La skill guía la revisión del contenido,
la entrega y la comprobación del diseño en escritorio y pantalla estrecha.

## Mejorar las skills

Cada skill vive en `skills/<nombre>/SKILL.md`, con `name` y `description` en el
frontmatter. Editar la fuente, revisar el cambio y publicarlo en la rama `main`.
Los demás reciben los cambios publicados al actualizar. No añadir rutas de
equipos personales, secretos ni instrucciones que dependan del monorepo privado.
