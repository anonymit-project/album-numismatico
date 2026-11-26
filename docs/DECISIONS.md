# Registro de decisiones

Registro vivo de decisiones de producto. Las propuestas no aprobadas se etiquetan como **PENDIENTE**.

## D-001 — Alcance del catálogo progresivo

- **Estado:** Aprobada.
- **Decisión:** catálogo mundial progresivo; no se promete exhaustividad global. El MVP cubre España (pesetas y euros, incluidas conmemorativas) y algunos emisores adicionales.
- **Motivo:** priorizar fiabilidad y validar el modelo antes de escalar cobertura.

## D-002 — Identidad de una pieza del álbum

- **Estado:** Aprobada.
- **Decisión:** anverso y reverso determinan la identidad visual base. Diferencias de diámetro o composición, por sí solas, no crean otra ficha de álbum; se distinguen cuando el cambio es visualmente relevante o el usuario quiere controlar esa variante.
- **Motivo:** evitar fragmentar el álbum por variantes técnicas que no aportan valor al inventario inicial.

## D-003 — Separación entre diseño, emisión y ejemplar

- **Estado:** Aprobada.
- **Decisión:** modelar por separado el diseño/pieza visual, sus emisiones y los ejemplares/posesiones de cada usuario. El año no genera una ficha visual distinta automáticamente.
- **Motivo:** mantener una identidad estable aunque existan años, acuñaciones o tiradas diferentes.

## D-004 — Privacidad y compartición

- **Estado:** Aprobada.
- **Decisión:** cada usuario tiene inventario independiente y privado por defecto. Puede compartir voluntariamente la colección o partes de ella en modo solo lectura. Nadie puede modificar el inventario de otro usuario.
- **Fuera de alcance:** marketplace y red social.

## D-005 — Imágenes ausentes

- **Estado:** Aprobada.
- **Decisión:** una pieza puede existir sin fotografía. Se mostrará una ilustración/silueta neutra hasta disponer de imagen propia o de una fuente con licencia compatible.
- **Motivo:** no bloquear el catálogo por derechos de imagen.

## D-006 — Comportamiento del álbum y preferencias

- **Estado:** Aprobada.
- **Decisión:** mostrar un selector visible de emisor/país; ordenar por denominación por defecto; permitir filtrar por monedas y billetes; conservar filtros y preferencias por usuario entre sesiones y dispositivos.
- **UX adicional:** controles «Lo tengo / Me falta» y piezas faltantes atenuadas, estilo álbum de cromos.
- **Motivo:** hacer descubrible la navegación y evitar reaplicar filtros en cada visita.

## D-007 — Trabajo en ramas

- **Estado:** Aprobada.
- **Decisión:** trabajar en ramas y proponer cambios mediante pull request; no modificar `main` directamente ni fusionar sin autorización explícita.


## D-008 — Política conservadora de fuentes y reutilización

- **Estado:** Aprobada.
- **Decisión:** utilizar únicamente datos, imágenes y materiales cuya reutilización en el proyecto esté respaldada por una licencia abierta explícita, dominio público verificable o permiso ya concedido. No contactar con proveedores ni titulares para solicitar excepciones o aclaraciones. Si las condiciones son ambiguas, restrictivas o no se pueden comprobar, no incorporar el material; usar la fuente solo como referencia bibliográfica/enlace o dejar un placeholder.
- **Aplicación:** Wikidata para datos estructurados CC0; Wikimedia Commons solo para archivos cuya licencia individual permita el uso previsto y tras registrar atribución y condiciones; Natural Earth para cartografía en dominio público; fuentes oficiales para verificar hechos, sin reutilizar automáticamente sus imágenes o textos protegidos. Numista queda excluida como fuente de importación o integración mientras no exista una licencia pública inequívoca compatible con el uso previsto.
- **Motivo:** evitar riesgos contractuales y de propiedad intelectual, mantener el presupuesto objetivo de 0 € y no añadir decisiones legales innecesarias al usuario.
- **Consecuencia:** primar catálogo pequeño y fiable, aunque haya menos imágenes o cobertura; las fichas sin imagen usarán placeholder.


## D-009 — Prototipo interactivo previo al cierre de Fase 0

- **Estado:** Aprobada.
- **Decisión:** se autoriza construir un prototipo desechable de validación UX antes de aprobar el cierre de Fase 0. Debe ser web responsive, móvil primero y usable también en ordenador. Se probará en navegador móvil Android y escritorio.
- **Alcance:** navegación y flujos simulados con datos ficticios claramente identificados; álbum, emisores/monedas/series, ficha, marcar posesión y faltantes, cantidades, búsqueda, filtros, orden, indicadores básicos, simulación de alta/edición e importación y ajustes cuando aporten valor a la validación.
- **Límites:** sin backend, autenticación real, sincronización, persistencia de servidor, catálogo real, importación efectiva, servicios externos ni imágenes de terceros. Los cambios solo se conservan durante la sesión del prototipo. No crear arquitectura de producción ni reutilizar el prototipo como base automática del MVP.
- **Separación de Fase 0:** esta autorización es una excepción limitada para validar experiencia de uso y viabilidad de interfaz; **no** supone cierre de Fase 0, aprobación del modelo de datos, autorización para iniciar el MVP ni permiso para incorporar código de producto.
- **Criterio de salida:** el usuario y su amigo pueden recorrer los flujos principales en móvil y escritorio, registrar problemas y decidir qué ajustar antes de cerrar Fase 0.
- **Motivo:** reducir incertidumbre de diseño y usabilidad antes de comprometer arquitectura y desarrollo de producto.


## D-010 — Alcance visual del prototipo UX

- **Estado:** Aprobada (aclaración de D-009, 2026-11-26).
- **Decisión:** el prototipo será ante todo una maqueta visual interactiva, móvil primero y responsive, para validar aspecto, navegación y usabilidad de las funcionalidades principales. No se pretende simular fielmente toda la lógica ni los procesos operativos del futuro producto.
- **Interacciones suficientes:** navegación entre inicio, emisor, moneda, serie, álbum y ficha; marcar/desmarcar posesión; ajustar una cantidad sencilla; observar progreso; búsqueda, filtros y orden básicos con respuesta visible.
- **No requerido:** formularios completos de administración, alta/edición funcionales, carga/importación simulada, validación de ficheros, persistencia, lógica de negocio exhaustiva, backend o arquitectura de producción. Se pueden representar visualmente como elementos estáticos o dejarse fuera si no ayudan a validar UX.
- **Datos y recursos:** datos ficticios y placeholders propios/neutros; sin material de terceros no autorizado, conforme a D-008.
- **Tecnología:** priorizar la vía más rápida y sencilla que permita una demo navegable en navegador Android y escritorio. No imponer framework ni modularidad de producción; decidir tras inspeccionar el repositorio.
- **Separación:** mantiene íntegramente los límites de D-009. No cierra Fase 0, no aprueba el modelo ni autoriza el MVP.
- **Motivo:** el objetivo es obtener feedback temprano de diseño y usabilidad, no construir una aplicación simulada.
