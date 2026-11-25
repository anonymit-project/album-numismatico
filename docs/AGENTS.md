# POLÍTICA DE TRABAJO CON IA · App de colección numismática

> Guárdalo en el repo como `AGENTS.md` (o `CLAUDE.md`). Es corto a propósito: se pega o se lee al inicio de **cada** chat. El detalle del proyecto vive en `docs/` (el prompt maestro pasa a ser `docs/PRD.md`).

## 1. Principios

1. **El repo es la memoria, el chat no.** Lo que no está en el repo no existe para la próxima sesión.
2. **Un chat = una micro-tarea** con objetivo y criterio de "hecho" claros. Si se alarga o cambia de tema, se cierra y se abre otro.
3. **La IA pregunta antes de asumir.** Ante cualquier duda de alcance, datos, diseño o licencias, pregunta (agrupado, con su recomendación por defecto). No rellena huecos por su cuenta.
4. **Lo verificable se verifica.** Cuotas gratuitas, precios, licencias, versiones de librerías y APIs se comprueban en fuentes oficiales con fecha; si no se puede, se marca `VERIFICAR`.
5. **Presupuesto 0 €.** Si algo requiere pagar, la IA avisa antes de proponerlo.
6. **Cambios pequeños y desplegables.** Cada micro-tarea deja el proyecto funcionando y con tests en verde.
7. **Nada de decisiones silenciosas.** Toda decisión relevante se registra en `docs/DECISIONS.md` (fecha, contexto, opciones, elegida, motivo).

## 2. Ciclo de una micro-tarea

1. **Inicio:** el usuario abre chat nuevo con la plantilla A (abajo) + este fichero + `docs/STATE.md` + la tarea.
2. **Comprensión:** la IA resume la tarea en 3-5 líneas, lista supuestos y preguntas. **No empieza hasta que el usuario responde o dice "adelante".**
3. **Ejecución:** entrega por pasos pequeños, con ficheros completos (rutas exactas) y cómo probarlos.
4. **Verificación:** la IA indica qué tests ejecutar y qué debe verse. El usuario confirma el resultado.
5. **Cierre:** la IA entrega (plantilla B) las actualizaciones de `STATE.md`, `DECISIONS.md`, `BACKLOG.md` y `CHANGELOG.md`, y el mensaje de commit sugerido.
6. **Commit:** el usuario sube todo al repo (o el agente, si tiene acceso). Solo entonces se da por cerrada la tarea.

## 3. Reglas de calidad

- Tests para toda lógica nueva (Vitest) y e2e para flujos críticos (Playwright); CI en verde antes de cerrar.
- Código tipado (TypeScript), sin dependencias nuevas sin justificarlas (licencia, mantenimiento, peso).
- Migraciones de BD siempre versionadas en el repo; nada de cambios manuales en producción sin dejarlos escritos.
- Datos de catálogo: siempre con `source`, `verification_status` y licencia de la imagen.
- Secretos (claves de API) nunca en el repo ni en el frontend.

## 4. Si la IA no tiene acceso al repo (chat normal)

- El usuario pega: `AGENTS.md`, `docs/STATE.md` y solo los ficheros que la tarea toque.
- La IA devuelve **ficheros completos** o diffs claros, nunca fragmentos ambiguos.
- La IA nunca afirma haber "actualizado el repo": entrega el contenido y el usuario lo sube.

## 5. Plantilla A · Inicio de micro-tarea (copiar y rellenar)

```
Lee y sigue la política de trabajo adjunta (AGENTS.md) y el estado actual (STATE.md).

TAREA: <una frase>
OBJETIVO / "HECHO CUANDO": <criterios verificables>
FUERA DE ALCANCE: <lo que NO quiero que toques>
FICHEROS RELEVANTES: <rutas o pegados abajo>

Antes de hacer nada: resume la tarea en 3-5 líneas, lista tus supuestos
y hazme las preguntas necesarias. No escribas código hasta que te diga "adelante".
```

## 6. Plantilla B · Cierre de micro-tarea (pedírselo a la IA)

```
Cierra la tarea. Entrégame, listos para pegar en el repo:
1. docs/STATE.md actualizado (qué está hecho, qué falla, siguiente paso exacto).
2. Entrada nueva para docs/DECISIONS.md (si hubo decisiones).
3. Cambios en docs/BACKLOG.md.
4. Entrada para docs/CHANGELOG.md.
5. Mensaje de commit (convencional) y lista de ficheros modificados.
6. Preguntas pendientes para mí.
```

## 7. Plantilla C · Retomar tras corte o límite de uso

```
Se cortó la sesión. Aquí está STATE.md y el último estado de los ficheros.
Resume en 5 líneas dónde estábamos, qué falta y cuál es el siguiente paso.
Pregúntame solo lo imprescindible para continuar.
```

## 8. Qué NO debe hacer la IA

- Empezar a programar sin haber confirmado el alcance.
- Inventar datos de catálogo, cuotas, precios o licencias.
- Mezclar varias tareas en un mismo chat o ampliar el alcance por su cuenta.
- Dar por buena una decisión abierta (ver "Decisiones abiertas" del PRD).
- Cerrar una tarea sin dejar la documentación actualizada.
