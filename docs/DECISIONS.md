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


## D-011 — El feedback del prototipo no bloquea la Fase 0

- **Estado:** Aprobada (2026-11-26).
- **Decisión:** continuar las tareas de descubrimiento aunque el feedback del prototipo UX todavía no haya llegado. La revisión UX se difiere y deja de ser una dependencia para avanzar en modelo, catálogo, fuentes e infraestructura.
- **Alcance de la decisión:** no se cancela la revisión. Cuando el usuario y su amigo aporten feedback, se analizará y se utilizará para ajustar UX y alcance V1. La revisión propia en Android y escritorio también sigue pendiente.
- **Prioridad inmediata:** validar estructuralmente `docs/DATA_MODEL.md` con Andorra, Cuba CUP/CUC, Ecuador, euro, XOF/XAF y peseta, contrastando los requisitos con `docs/CATALOG_SOURCES.md`.
- **Límites:** Fase 0 permanece abierta; esta decisión no aprueba su cierre ni autoriza código de producto/MVP. D-008 sigue vigente. La investigación CELLAR queda aparcada salvo petición expresa.
- **Motivo:** el feedback visual puede recogerse sobre una versión funcional más adelante y no justifica detener la reducción de riesgos de catálogo y modelo.

## D-012 — Autoridad monetaria independiente

- **Estado:** Aprobada (2026-11-26).
- **Decisión:** modelar `monetary_authority` como entidad institucional independiente de `issuer`, relacionada con monedas mediante relaciones temporales y tipadas que identifiquen sus funciones (política monetaria, autoridad monetaria o emisión de billetes).
- **Límites:** no sustituye al emisor político/legal de una pieza. Cecas e imprentas son productores físicos, no autoridades por fabricar. No exigir poblar autoridades históricas sin fuentes suficientes.
- **Motivo:** representar BCEAO/BEAC, BCE/Eurosistema, bancos centrales nacionales y autoridades históricas sin confundir institución, territorio y emisor.

## D-013 — Roles temporales de la relación emisor-moneda

- **Estado:** Aprobada (2026-11-26).
- **Decisión:** sustituir `issuer_currency.issues_own` por roles tipados y temporalmente delimitados. Roles iniciales: `uses`, `legally_issues` y `has_authorized_coinage`; un emisor puede tener varios roles documentados.
- **Límites:** uso no implica competencia legal de emisión. Acuñación/impresión física y membresía en una unión monetaria se modelan por separado. Cada rol requiere procedencia.
- **Motivo:** distinguir estados usuarios, emisores legales y estados autorizados a emitir moneda propia dentro de una moneda compartida.

## D-014 — Cronología de estados monetarios

- **Estado:** Aprobada (2026-11-26).
- **Decisión:** representar cambios legales/económicos mediante eventos tipados, fechados y asociados al ámbito afectado (moneda, relación emisor-moneda o emisión y, cuando proceda, jurisdicción). Tipos iniciales: introducción, inicio de circulación/curso legal, fin de curso legal, retirada de circulación, fin de canje y desmonetización.
- **Límites:** no usar un único estado global como verdad primaria. Una etiqueta podrá derivarse o ser descriptiva. No inventar fechas ausentes. «Conmemorativa» o «no destinada a circulación» es característica de emisión, no estado legal de moneda.
- **Motivo:** distinguir coexistencia, retirada, canje y desmonetización, que pueden ocurrir en fechas diferentes y afectar a ámbitos distintos.

## D-015 — Reutilización de caras en diseños

- **Estado:** Aprobada (2026-11-26).
- **Decisión:** permitir caras/anversos/reversos reutilizables mediante `design_side`; `catalog_design` referencia la pareja concreta de caras.
- **Límites:** identidad visual sigue siendo la combinación de anverso y reverso conforme a D-002. Compartir una cara no fusiona diseños ni crea fichas por cara. La reutilización de imágenes sigue sujeta a D-008.
- **Motivo:** evitar duplicación de caras comunes, especialmente en monedas euro, sin alterar la identidad del álbum.

## D-016 — Transiciones monetarias tipadas

- **Estado:** Aprobada (2026-11-26).
- **Decisión:** representar relaciones dirigidas entre monedas mediante `currency_transition`, con tipo inicial `replacement` o `redenomination`, periodo y factor exacto opcional (unidades destino por unidad origen).
- **Límites:** no asumir que sustitución implica conversión fija. La coexistencia ordinaria se representa con periodos/eventos de uso y estado, no como transición. Registrar circulación paralela solo si existe régimen transitorio específico documentado. XOF y XAF siguen siendo monedas distintas.
- **Motivo:** distinguir sustitución, redenominación y coexistencia sin relaciones ambiguas.

## D-017 — Denominaciones y valores faciales exactos

- **Estado:** Aprobada (2026-11-26).
- **Decisión:** conservar denominación original y añadir, cuando esté documentado, valor facial normalizado como racional exacto (numerador/denominador enteros) respecto de la unidad principal. Se podrá conservar etiqueta de unidad/subunidad.
- **Límites:** no usar coma flotante ni crear monedas independientes para subunidades sin existencia monetaria/legal propia. Para sistemas históricos no decimales o datos incompletos, conservar texto y normalizar solo con equivalencia acreditada.
- **Motivo:** permitir ordenación/comparación fiables sin confundir subunidades —como el centavo ecuatoriano— con monedas independientes.


## D-018 — Atribución de autoridad monetaria por emisión

- **Estado:** Aprobada (2026-11-26).
- **Decisión:** permitir una relación opcional y temporal entre `catalog_issue` y `monetary_authority`, con rol controlado y procedencia. Roles iniciales: `legal_issuer` (competencia/responsabilidad legal de emisión) y `operational_issuer` (ejecución o puesta en circulación).
- **Límites:** no exigir la relación cuando no aporte precisión o falte evidencia. Cecas e imprentas siguen siendo productores físicos, no autoridades. No confundir emisión legal con puesta en circulación.
- **Motivo:** atribuir responsabilidades institucionales a emisiones concretas cuando una moneda y periodo incluyen varias autoridades o funciones.

## D-019 — Intención de circulación y unidades nominales de colección

- **Estado:** Aprobada (2026-11-26).
- **Decisión:** incorporar en `catalog_issue` un atributo opcional y controlado de intención de circulación, con valores iniciales `intended_for_circulation` y `not_intended_for_circulation`. Conservar denominaciones y unidades nominales originales de piezas de colección aunque la unidad no sea una moneda oficial independiente.
- **Límites:** ausencia del atributo significa desconocido; no inferir que una pieza no circuló por falta de evidencia. Las categorías de prueba/patrón quedan separadas. No crear una entidad `currency` para una unidad nominal no oficial (por ejemplo, diners) por el mero hecho de aparecer en una pieza. Normalizar solo cuando exista una unidad de referencia documentada.
- **Motivo:** representar emisiones no circulantes y piezas de colección sin inventar monedas legales ni mezclar intención con estado jurídico efectivo.

## D-020 — Naturaleza oficial o de facto del uso monetario

- **Estado:** Aprobada (2026-11-26).
- **Decisión:** añadir a `issuer_currency` un calificador opcional `use_basis`, con valores iniciales `official` y `de_facto`, independiente del rol temporal `uses`.
- **Límites:** registrar el calificador solo cuando exista evidencia suficiente. No deducir curso legal, adopción oficial ni competencia de emisión a partir del uso de facto; los eventos jurídicos y los demás roles de D-013 permanecen independientes.
- **Motivo:** distinguir la adopción oficial de la circulación de facto de monedas extranjeras, como en Andorra antes del euro.
