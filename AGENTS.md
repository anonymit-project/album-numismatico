# Política de trabajo para agentes

Este repositorio corresponde al proyecto Álbum numismático. El usuario es un ingeniero informático; puede recibir explicaciones técnicas, pero las decisiones importantes deben incluir justificación y alternativas.

## Fuente de verdad y continuidad

1. Antes de trabajar, leer este archivo, `docs/STATE.md`, `docs/PRD.md`, `docs/DECISIONS.md` y los documentos relevantes de `docs/`.
2. El repositorio es la fuente de verdad, no el historial del chat. No pedir de nuevo información ya documentada.
3. Al cerrar cada iteración, actualizar como mínimo `docs/STATE.md`, `docs/DECISIONS.md` si hubo decisiones, y `docs/BACKLOG.md`.
4. Dejar un resumen de lo realizado, errores, decisiones, bloqueos y siguiente paso exacto.
5. **Cierre obligatorio de cada chat:** nunca terminar una respuesta que cierre el trabajo o la conversación de forma ambigua. El último mensaje del chat debe acabar siempre con una de estas dos opciones: (a) una pregunta concreta y útil dirigida al usuario, si hace falta una respuesta o decisión suya; o (b) un prompt de relevo autosuficiente, listo para copiar en un nuevo chat, si el siguiente paso es continuar el trabajo sin necesitar una decisión. No basta con enumerar tareas pendientes ni con decir «cuando quieras seguimos». Si el trabajo continúa en el mismo chat, no es necesario forzar un cierre intermedio.
6. El prompt de relevo debe indicar objetivo, contexto imprescindible, documentos/rama/PR relevantes, restricciones vigentes, trabajo ya realizado y siguiente acción concreta. No debe pedir al usuario que repita información ya documentada.

## Reglas de producto

- Priorizar la fiabilidad y trazabilidad del catálogo sobre la amplitud o las funciones vistosas.
- Presupuesto objetivo: 0 €. Advertir claramente si una función depende de servicios de pago, cuotas gratuitas limitadas o condiciones cambiantes.
- Catálogo mundial progresivo; nunca prometer exhaustividad mundial.
- No comenzar código de producto/MVP hasta que el usuario apruebe expresamente el cierre de Fase 0.
- Mantener separadas entidad emisora, moneda, diseño visual, emisión y posesión del usuario.
- Colecciones privadas por defecto. Compartición futura solo voluntaria y de solo lectura.
- Las imágenes requieren licencia/permiso verificado; usar placeholder cuando no exista imagen reutilizable.

## Verificación

- Verificar en fuentes oficiales cualquier dato que pueda cambiar: precios, cuotas, licencias, APIs, versiones y políticas.
- No presentar como verificado lo que solo sea una hipótesis o recuerdo; etiquetar lo pendiente como `VERIFICAR`.
- Distinguir datos de fuentes, decisiones del usuario, recomendaciones y propuestas aún no aprobadas.

## Flujo de Git

- Trabajar en ramas descriptivas, nunca directamente en `main`.
- Proponer cambios mediante pull request.
- No fusionar PR ni modificar `main` sin autorización explícita.
- Revisar el contenido actual antes de reemplazar un archivo; evitar sobrescribir trabajo ajeno.
- Mantener commits pequeños y con mensajes claros.

## Calidad y comunicación

- Responder en español, de forma directa y concisa.
- Ser crítico: señalar riesgos, contradicciones y alternativas; no dar la razón por defecto.
- No afirmar que un cambio se ha aplicado hasta recibir confirmación de GitHub.
- No simular pruebas ni ejecución local si no se han realizado.
