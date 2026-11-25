# Política de trabajo para agentes

Este repositorio corresponde al proyecto Álbum numismático. El usuario es un ingeniero informático; puede recibir explicaciones técnicas, pero las decisiones importantes deben incluir justificación y alternativas.

## Fuente de verdad y continuidad

1. Antes de trabajar, leer este archivo, `docs/STATE.md`, `docs/PRD.md`, `docs/DECISIONS.md` y los documentos relevantes de `docs/`.
2. El repositorio es la fuente de verdad, no el historial del chat. No pedir de nuevo información ya documentada.
3. Al cerrar cada iteración, actualizar como mínimo `docs/STATE.md`, `docs/DECISIONS.md` si hubo decisiones, y `docs/BACKLOG.md`.
4. Dejar un resumen de lo realizado, errores, decisiones, bloqueos y siguiente paso exacto. Preparar un prompt de relevo autosuficiente cuando el usuario lo solicite o antes de cambiar de sesión/contexto.
5. **No terminar nunca un chat con una respuesta sin continuidad explícita.** Todo mensaje que cierre una tarea o conversación debe acabar con una pregunta concreta dirigida al usuario o, si el trabajo debe continuar en otro chat, con un prompt de relevo autosuficiente listo para copiar. No basta con enumerar posibles siguientes pasos ni con una frase genérica como «cuando quieras seguimos».
6. **Vigilar proactivamente la capacidad del contexto.** Cuando la conversación se acerque a un nivel en el que pueda perderse información relevante, avisar antes de que ocurra y preparar el prompt de relevo; no esperar a que el usuario lo solicite ni a que el contexto esté agotado.
7. Estas reglas se aplican también a respuestas breves, cambios de tarea y chats de investigación. Solo se omite la pregunta/prompt si el usuario pide expresamente que no se añada.

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
