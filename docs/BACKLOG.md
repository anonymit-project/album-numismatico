# Backlog

Prioridad orientativa. No implica autorización para saltarse el cierre de Fase 0.

## Fase 0 — Descubrimiento (actual)

**Criterio obligatorio:** solo incorporar datos e imágenes con derechos de reutilización claros y compatibles. No contactar con proveedores para pedir permisos o aclaraciones. Ante ambigüedad, excluir el material o conservar únicamente un enlace de referencia.

- [x] Comparar Numista, Wikidata/Wikimedia Commons, fuentes oficiales y datasets abiertos a nivel documental.
- [x] Verificar licencias generales de Wikidata, Commons, Natural Earth e ISO; documentar restricciones de imágenes oficiales euro/peseta.
- [x] Verificar cuota/precio y condiciones de Numista; documentar riesgo contractual para una PWA privada multiusuario.
- [x] Documentar límites operativos actuales de Wikimedia API y Wikidata SPARQL.
- [x] Excluir Numista de la ingesta y de la aplicación: sus condiciones no garantizan el uso previsto y no se solicitarán excepciones.
- [x] Realizar prueba documental de cobertura con ejemplos concretos de pesetas, euros regulares y conmemorativos, billetes españoles, Andorra, Cuba CUP/CUC, Ecuador sucre/USD y monedas XOF/XAF.
- [x] Revisar ejemplos individuales de imágenes Commons y separar licencia de la fotografía de derechos/reglas del diseño monetario; no aprobar assets en esta iteración.
- [x] Evaluar Nomisma, Syllogeum y CANOA; confirmar que su cobertura es principalmente de moneda antigua y no satisface el catálogo moderno.
- [x] Identificar NumisLib como candidato auxiliar, pendiente de verificar licencia exacta y trazabilidad de la base.
- [ ] Identificar dataset especializado de monedas y billetes modernos con licencia explícita compatible y mantenimiento suficiente.
- [x] Buscar fuentes primarias y estructuradas para Cuba CUP/CUC: se localizaron normas de emisión y retirada, pero no catálogo abierto ni API. Se mantiene el bloqueo de ingesta automatizada.
- [x] Verificar las interfaces oficiales de EUR-Lex/CELLAR (SOAP/XML, REST, SPARQL, RSS/Atom y Formex) y localizar avisos reales de monedas euro.
- [x] Ejecutar manualmente consulta SPARQL para C/2026/406 y recuperar los recursos WEMI en español y lituano; se obtuvieron seis bindings.
- [x] Recuperar y examinar XHTML español y Formex/XML en español y lituano para C/2026/406; validar manualmente la presencia de campos numismáticos.
- [ ] Implementar y probar un parser/mapeo Formex/XML → staging con tests; no es código de producto.
- [x] Documentar estructura HTML, enlaces y categorías históricas de BEAC/BCEAO, con propuesta de extracción controlada de metadatos. No se ha localizado API/feed específico.
- [x] Confirmar que las páginas institucionales de BEAC/BCEAO/Cuba no aportan licencia abierta general para sus imágenes; mantener placeholders. La brochure oficial BEAC incluye prohibición expresa de reproducción.
- [ ] Validar el modelo con Andorra, Cuba CUP/CUC, Ecuador, euro, CFA, peseta y estados históricos.
- [ ] Definir tratamiento cartográfico de microestados, territorios y estados desaparecidos.
- [ ] Resolver valoración de monedas sin cotización y equivalencias históricas.
- [ ] Proponer escala sencilla de conservación.
- [ ] Definir moderación de contribuciones e imágenes aportadas por usuarios.
- [ ] Validar mockups con el usuario y su amigo.
- [ ] Verificar cuotas gratuitas y condiciones actuales de backend, hosting, almacenamiento y servicios de identificación.
- [ ] Validar proveedor FX. El BCE ofrece SDMX y tipos de referencia diarios para una selección de divisas; no cubre necesariamente todas las monedas históricas o exóticas y sus tipos son informativos.
- [ ] Obtener aprobación expresa para cerrar Fase 0.

## Fase 1 — MVP (bloqueada hasta aprobar Fase 0)

- [ ] Crear PWA móvil primero y despliegue gratuito.
- [ ] Autenticación y colecciones privadas con control de acceso.
- [ ] Catálogo semilla acotado y trazable, basado solo en datos con derechos compatibles.
- [ ] Álbum por emisor/país, moneda, serie y pieza.
- [ ] Selector visible de país/emisor.
- [ ] Orden por denominación y filtros de monedas/billetes.
- [ ] Persistencia de filtros y preferencias por usuario, sincronizada entre dispositivos.
- [ ] Marcar posesión/cantidad; faltantes atenuados.
- [ ] Importación CSV/XLSX básica.
- [ ] KPIs básicos, modo oscuro, tests y CI.

## Fases posteriores

- Mapa plano/globo, estadísticas avanzadas y asistente por lotes.
- Wishlist, duplicados, exportación y backups automatizados.
- Identificación asistida por foto, solo si se mantiene gratuita y privacidad aceptable.
- Catálogo ampliado, importadores y contribuciones moderadas.
- Compartición voluntaria de solo lectura e intercambio asistido.


## Investigación operativa — siguiente bloque técnico (sin código de producto)

- [x] Ejecutar en el editor oficial la consulta SPARQL preparada para C/2026/406; confirmar URIs de Expression, Manifestation e Item y formatos PDF/A, Formex y XHTML en español y lituano.
- [x] Recuperar el XML Formex por navegador/descarga y validar manualmente el mapeo de campos en dos expresiones lingüísticas del mismo aviso. Evidencia en [`docs/CELLAR_POC.md`](CELLAR_POC.md).
- [x] Validar un segundo aviso: C/2026/419 (Mónaco). SPARQL localizó Work/Expressions/Manifestations/Items; la Expression ENG ofrece `pdfa2a`, `fmx4` y `xhtml`; Formex descargado como ZIP con 3 XML y 8 TIFF. El XML principal `C_202600419EN.000101.fmx.xml` contiene ocho denominaciones y datos de emisor, fecha, diseños, ceca y canto de la moneda de 2 €. Prueba manual, sin demostrar automatización general ni derechos de imágenes; detalle en `docs/CELLAR_POC.md`.
- [ ] Implementar y probar un parser/mapeo pequeño Formex/XML → staging con tests; conservar procedencia por campo y revisión humana.
- [x] Investigar y documentar CELLAR RSS/Atom frente a alertas RSS de EUR-Lex; recomendación híbrida y limitaciones en docs/CELLAR_POC.md.
- [x] Ejecutar prueba manual del feed CELLAR desde PowerShell: acceso HTTP 200, respuesta Atom, filtros `type=create`, `type=update`, `wemiClasses=DOSSIER` y combinación create + ITEM; las primeras entradas inspeccionadas cumplen los filtros. Evidencia y límites en `docs/CELLAR_POC.md`.
- [x] Validar manualmente la paginación y condición terminal CELLAR para la consulta 19–25/11/2026: P330 (1.000, moreEntries=true), P331 (959, moreEntries=false) y P332 (0, moreEntries=false); comparación de las ventanas de 10 claves cellarId|updated a ambos lados de P330→P331 sin repeticiones. Evidencia en docs/CELLAR_POC.md, sección 13.
- [ ] Investigar campos que aparecen como plantillas `$item.*`, valores múltiples de `wemiClasses`, eventos DELETE y seguimiento de un evento hasta sus metadatos WEMI.
- [ ] Configurar y validar, con autorización y acceso del usuario a EUR-Lex, una búsqueda guardada RSS para las variantes de títulos numismáticos; no se ha creado ninguna alerta.
- [ ] Crear manifiesto versionado de URLs BEAC/BCEAO por familia, estado legal, país y fecha de consulta; validar cambios de HTML antes de automatizar extracción.
- [ ] Comprobar individualmente las condiciones de reutilización de cada PDF o texto de BEAC/BCEAO antes de almacenar copias; no extraer imágenes.
- [ ] Continuar Cuba solo con ejemplares oficiales de la Gaceta y catálogos institucionales accesibles; mantener las copias secundarias como pistas, no como autoridad de importación.

**Organización del trabajo:** [x] Registrar en `AGENTS.md` la preferencia del usuario por chats breves y tareas atómicas, con prompt de relevo obligatorio al cerrar cada tarea. Aplicar esta norma en las siguientes iteraciones.

**Límite actual de la validación CELLAR:** pruebas manuales positivas para C/2026/406 (Lituania) y C/2026/419 (Mónaco). La investigación de RSS/Atom y alertas EUR-Lex es documental; no acredita ejecución del feed, alerta configurada, automatización desatendida, parser probado, cobertura general ni derechos de reutilización de imágenes.


### Actualización de prueba operativa CELLAR RSS/Atom — 25/11/2026

La prueba manual desde PowerShell del usuario ha eliminado el bloqueo de acceso al endpoint y validado los filtros básicos. Se marca como completada únicamente la prueba de acceso/filtros; la paginación y la validación de campos/identificadores permanecen pendientes. Ver `docs/CELLAR_POC.md`, sección 9.


### Actualización de paginación CELLAR RSS/Atom — 25/11/2026

La página 1 se ha descargado desde PowerShell con HTTP 200 y 1.000 entradas. Una prueba previa comunicada de página 2 también obtuvo HTTP 200 y 1.000 entradas. Las tres primeras entradas de página 2 comparten timestamp con la última observada de página 1, pero no se ha probado que sean duplicados. Se mantiene abierta la tarea de paginación; no marcarla como completada hasta comparar registros y verificar continuidad, huecos y solapamientos. Detalle en la sección 10 de `docs/CELLAR_POC.md`.

- [ ] Descargar páginas 1 y 2 en una sola ejecución y comparar elementos de frontera por identificadores/campos XML reales; determinar continuidad, huecos y duplicados sin usar timestamps como clave.


### Actualización de paginación CELLAR RSS/Atom — 25/11/2026

La paginación queda **validada parcialmente**, no completada. P1–P5 devuelven HTTP 200 y 1.000 entradas cada una; moreEntries=true se observó en P3–P5. Se comprobaron tres fronteras: comparten timestamp, pero no se repiten claves cellarId|updated. P1–P3 mantuvieron los mismos hashes de claves ordenadas en consultas repetidas, incluida una tras unos 15 minutos. Esto no demuestra estabilidad ante inserciones tardías ni estabilidad de las páginas más recientes. Detalle en docs/CELLAR_POC.md, sección 11.

**Siguiente acción atómica:** continuar desde page=6 hasta la condición terminal notifReq:moreEntries; registrar recuentos y límites. No implementar aún sincronización incremental ni asumir unicidad global de cellarId|updated.

### Actualización de paginación CELLAR RSS/Atom — 25/11/2026

- [x] Inspeccionar metadatos de la respuesta Atom: se observan `startDate`, `endDate`, `page` y `moreEntries`; no se observó total de resultados ni enlace a última página.
- [x] Aplicar búsqueda exponencial/binaria para localizar el cambio comunicado entre P330 (`moreEntries=true`) y P331 (`moreEntries=false`), evitando recorrer secuencialmente las páginas intermedias.
- [x] Confirmar directamente P330 y P331: HTTP, recuento de entradas, número de página, `moreEntries`, primer/último `updated` y comparar las ventanas de 10 claves en la frontera.
- [x] Caracterizar P332 una vez después de confirmar P331: HTTP 200, página 332, cero entradas y moreEntries=false.

**Límite de aquella comprobación:** la sección 12 reflejaba el estado previo a la confirmación directa. La paginación queda cerrada para esta consulta según la sección 13; estabilidad, inserciones tardías y cursor siguen sin validar. No implementar sincronizador/parser.


### Cierre de validación terminal CELLAR — 26/11/2026

La prueba manual de paginación para la consulta 19–25/11/2026 queda completada: P330 y P331 confirmadas directamente, frontera comparada en ventanas de 10 claves y P332 consultada una vez. No se recorrieron P1–P329 secuencialmente y no se conoce un total exacto de toda la ventana. El cierre **no** cubre estabilidad ante inserciones tardías, unicidad global de `cellarId|updated`, identificación del evento ni cobertura numismática. Esos asuntos siguen separados en el backlog; no implementar cursor/sincronizador ni parser como consecuencia automática de esta prueba. Ver sección 13 de `docs/CELLAR_POC.md`.


### Actualización de identidad de eventos CELLAR — 26/11/2026

- [x] Inspeccionar en bruto una entrada Atom real y registrar namespaces, `cellarId`, `rootCellarId`, `wemiClass`, `classes`, `identifiers` y `rootIdentifiers` (evidencia en `docs/CELLAR_POC.md`, sección 14).
- [x] Inspeccionar una segunda entrada Atom de clase ITEM (índice 7 de P331): las plantillas sin resolver de `id`, `title`, `summary` y `link href` se repiten respecto a la entrada EXPRESSION. Evidencia y límites en `docs/CELLAR_POC.md`, sección 15.
- [ ] Seguir un `cellarId` real hasta sus metadatos WEMI mediante CELLAR/SPARQL.
- [ ] Probar eventos DELETE y valores múltiples de `wemiClasses`.

**Conclusión parcial:** la muestra identifica un recurso `EXPRESSION` y su raíz, y aporta CELEX/consolidation/ELI para relacionarlos. Sin embargo, `atom:id`, `title`, `summary` y `link href` llegaron como plantillas literales; el identificador de evento no queda validado. No usar `cellarId|updated` como clave global demostrada ni diseñar aún cursor/sincronizador. Mantener Fase 0 y D-008.


### Resultado de la segunda inspección Atom — 26/11/2026

La segunda muestra fue una entrada `ITEM`, `type=create`, seleccionada en el índice 7 de P331. Repite exactamente los campos plantilla observados en la entrada `EXPRESSION`: `atom:id` con `${item.cellarUri}`, `title=$item.title`, `summary=$item.entrySummary` y `link href=$item.cellarUri`. Los campos `cellarId` y `rootCellarId` sí están materializados. Se marca completada la comparación de dos muestras, no una caracterización general del feed.

**Siguiente acción atómica:** seguir un `cellarId` observado hasta sus metadatos WEMI mediante CELLAR/SPARQL. Mantener pendientes la prueba de DELETE y los valores múltiples de `wemiClasses`. No implementar parser, cliente, cursor ni sincronizador.


## Planificación de entregables y estimación — 26/11/2026

Estimaciones de esfuerzo, no compromisos de calendario. Para convertirlas en calendario, usar la dedicación semanal real. Los rangos incluyen apoyo de herramientas de IA, pero no eliminan el tiempo de revisión, pruebas, decisiones y correcciones. Reestimar al cerrar cada hito.

### Próximo entregable: prototipo interactivo responsive (autorizado por D-009)

**Objetivo:** validar navegación, usabilidad y viabilidad de la interfaz en móvil Android y ordenador, antes de cerrar Fase 0. No valida por sí solo la viabilidad legal del catálogo, las fuentes, el backend, la sincronización ni los costes de infraestructura.

| Tarea | Trabajo incluido | Esfuerzo |
|---|---|---:|
| 1. Definir flujos y criterios de aceptación | Priorizar navegación y escenarios de prueba; revisar decisiones existentes sin reabrirlas automáticamente | 3–5 h |
| 2. Estructura visual responsive | Navegación móvil/escritorio, jerarquía visual, componentes base y estados | 4–6 h |
| 3. Pantallas principales | Inicio, selección de emisor/moneda, álbum, ficha de pieza, colección y ajustes | 8–12 h |
| 4. Interacciones simuladas | Tengo/me falta, cantidades, búsqueda, filtros, orden, alta/edición y recorrido de importación simulado | 8–12 h |
| 5. Datos ficticios y estados | Dataset de demostración claramente rotulado, placeholders, estados vacíos y ejemplos representativos | 2–3 h |
| 6. Pruebas y correcciones responsive | Probar tamaños móviles y escritorio, navegación táctil, legibilidad y errores principales | 3–5 h |
| 7. Preparar revisión | Instrucciones y entrega de una vista previa accesible para el usuario y su amigo | 1–2 h |
| **Total de construcción** | | **29–45 h** |

**Revisión posterior:** 6–10 h (aprox. 1–2 jornadas), para recoger feedback, priorizar problemas y aplicar una ronda de ajustes.

**Criterios de aceptación del prototipo**
- Se puede recorrer el flujo principal desde inicio hasta emisor, moneda/serie y ficha.
- Se puede marcar una pieza como adquirida/faltante, cambiar cantidad y ver el efecto en el álbum e indicadores.
- Búsqueda, filtros y orden producen cambios visibles y coherentes.
- Las acciones de alta/edición e importación están simuladas y se identifican como tales.
- Se puede usar con comodidad en un móvil Android y en escritorio; no se exige instalación PWA en esta fase.
- Todo dato e imagen de demostración es ficticio o un placeholder; no se incorpora material de terceros sin verificar D-008.
- No hay backend, cuentas reales, sincronización ni persistencia fuera de la sesión.

### Preparación y cierre de Fase 0 (paralela o posterior a la revisión UX)

| Tarea pendiente | Esfuerzo inicial |
|---|---:|
| Validar modelo con Andorra, Cuba CUP/CUC, Ecuador, euro, XOF/XAF, peseta y estados históricos | 4–8 h |
| Resolver decisiones mínimas de conservación, valoración, privacidad/moderación y alcance V1 | 4–8 h |
| Verificar backend, hosting, autenticación, almacenamiento, backups y FX con cuotas vigentes | 5–8 h |
| Definir catálogo semilla pequeño, trazable y con derechos compatibles | 4–8 h |
| Revisar feedback del prototipo y congelar alcance de V1 | 2–4 h |
| **Subtotal estimado** | **19–36 h** |

Siguen pendientes también las tareas de cobertura/fuentes que figuran arriba en el backlog, incluido el parser Formex → staging; no se consideran bloqueantes para construir el prototipo UX. El cierre de Fase 0 requiere aprobación expresa del usuario.

### V1 funcional acotada (solo después de aprobar el cierre de Fase 0)

Estimación preliminar: **100–180 horas de esfuerzo**, aproximadamente **6–10 semanas** si se dedican 15–20 horas semanales y no aparecen bloqueos importantes. Debe revisarse tras el prototipo y la selección del backend. No es una fecha comprometida.

| Bloque | Trabajo principal | Esfuerzo |
|---|---|---:|
| Base técnica | Proyecto, PWA, CI, calidad, despliegue inicial | 10–16 h |
| Backend y seguridad | Base de datos, migraciones, autenticación, aislamiento de colecciones | 18–30 h |
| Catálogo y colección | Modelo aprobado, semillas, procedencia, posesión y faltantes | 16–28 h |
| Experiencia principal | Álbum móvil, navegación, filtros, búsqueda, detalle y edición | 20–32 h |
| Importación/exportación | CSV, validación, vista previa, exportación y backups | 10–18 h |
| Calidad y entrega | Tests, E2E, accesibilidad básica, pruebas Android, documentación y correcciones | 26–56 h |
| **Total preliminar** | | **100–180 h** |

**Incluido en la V1 acotada:** PWA móvil primero, dos o pocos usuarios, cuentas privadas, catálogo semilla limitado, álbum, posesión/cantidad, búsqueda/filtros, importación CSV, KPIs básicos, exportación y pruebas.  
**Excluido expresamente:** catálogo mundial exhaustivo, mapa/globo, escáner por foto, importadores automáticos, XLSX avanzado, asistente por lotes, red social e intercambio.

### Fases posteriores

- Mapa plano/globo.
- Identificación asistida por foto, si coste y privacidad lo permiten.
- Importadores CELLAR, BEAC/BCEAO y ampliación del catálogo, tras validar fuentes, licencias y automatización.
- Importación XLSX avanzada y asistente por lotes.
- Valoración avanzada, contribuciones moderadas, compartición social, intercambio y gamificación.

### Actualización de la prueba CELLAR

- [x] Intentar seguir un ITEM real observado en Atom hasta triples/metadatos WEMI mediante una consulta SPARQL de propiedades salientes.
- Resultado: `bindings: []` para la URI consultada; una consulta previa con UNION/BIND dio error de compilación Virtuoso SP031. Prueba cerrada como **inconclusa**: no acredita inexistencia o invalidez del recurso. Evidencia en `docs/CELLAR_POC.md`, sección 16.
- [ ] Resolver en una iteración futura, si se prioriza expresamente, por qué esa URI no devuelve triples. No convertir esta prueba fallida en una tarea de automatización ni en un bloqueo para el mock-up.


### Revisión del alcance del prototipo UX — 26/11/2026 (D-010)

La tabla anterior de 29–45 h corresponde al alcance inicial más amplio y queda **sustituida** para esta iteración por el siguiente alcance visual reducido:

| Tarea | Trabajo incluido | Esfuerzo |
|---|---|---:|
| 1. Definir recorrido y jerarquía visual | Priorizar pantallas/estados para la revisión | 0,25–0,5 h |
| 2. Maqueta responsive | Navegación, estilo visual y datos ficticios | 1–2 h |
| 3. Recorrido principal | Inicio, emisor, moneda, serie, álbum y ficha | 1–2 h |
| 4. Interacciones UX esenciales | Tengo/me falta, cantidad, progreso, búsqueda/filtros/orden básicos | 0,5–1 h |
| 5. Pruebas y correcciones | Navegación táctil, legibilidad y tamaños Android/escritorio | 1–1,5 h |
| 6. Entrega para revisión | Instrucciones y lista breve de aspectos a evaluar | 0,25–0,5 h |
| **Total de construcción** | | **4–8 h** |

**Revisión posterior estimada:** 2–3 h, según el feedback y el número de ajustes.

No se implementan formularios completos de alta/edición, carga o importación simulada, validaciones, procesos administrativos ni simulación detallada de operaciones. Pueden omitirse o mostrarse como elementos visuales sin comportamiento. El criterio de éxito es que el usuario y su amigo puedan evaluar el diseño y recorrer las funciones principales en navegador Android y escritorio.

**Siguiente tarea:** implementar el primer corte visual navegable. No ampliar alcance sin autorización. La estimación anterior queda conservada como histórico, pero no debe utilizarse para planificar esta versión reducida.


## Prototipo visual responsive — iteración 26/11/2026

- [x] Inspeccionar la estructura real y elegir la implementación mínima: un `index.html` sin dependencias.
- [x] Crear recorrido navegable Inicio → Emisor → Moneda → Serie → Álbum → Ficha.
- [x] Añadir datos ficticios y placeholders neutros, sin recursos numismáticos de terceros.
- [x] Añadir posesión/faltante, ajuste sencillo de cantidad, progreso, búsqueda, filtros y ordenación con cambios visibles.
- [x] Adaptar navegación y cuadrícula a pantallas estrechas y escritorio.
- [ ] Abrir y probar en navegador Android real y escritorio; registrar incidencias y feedback del usuario/amigo.
- [ ] Configurar una vista previa pública estable (p. ej. GitHub Pages) para compartir la maqueta; hosting aún no configurado.
- [ ] Corregir los problemas detectados en la revisión UX (estimación global de revisión y correcciones: 2–3 h).

**Estado de entrega:** primer corte de código creado en `index.html`. No se considera validado en dispositivos: no se han realizado pruebas de navegador desde este entorno. Fase 0 sigue abierta y el prototipo no es el MVP.

**Estimación vigente:** construcción 4–8 h; revisión y correcciones 2–3 h. No utilizar la estimación histórica de 29–45 h para este alcance reducido.
