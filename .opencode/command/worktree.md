---
description: Crea un git worktree en .worktrees/ con un nombre derivado del argumento.
agent: build
---

El usuario invocó `/worktree` con este argumento (puede contener espacios o ser descriptivo):

$ARGUMENTS

Tu única tarea es crear un git worktree. Sigue estos pasos:

1. Analiza `$ARGUMENTS` y deriva un **slug kebab-case corto y contextual** que represente la feature. Acorta y normaliza, no copies literal:
   - "triple shot" → `triple-shot`
   - "sistema de skins" → `skins`
   - "power up de escudo" → `shield`
   - "power up de velocidad" → `speed`
   El slug debe ser breve (idealmente 1-2 palabras), en minúsculas, sin tildes ni caracteres especiales.

2. Ejecuta **exactamente** este comando con la herramienta bash, **sin cambiar de directorio** (usa el directorio de trabajo actual):
   ```
   git worktree add .worktrees/<slug>
   ```

3. Muestra la salida de git como confirmación (ruta del worktree + rama creada).

No hagas nada más: no crees commits, no crees archivos extra, no modifiques nada, no cambies de directorio.
