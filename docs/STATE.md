# Estado del proyecto

**Fase:** 0 — descubrimiento, sin código de producto.
**Criterio de reutilización:** solo fuentes con derechos de uso claros y compatibles; no se solicitarán permisos particulares.
**Actualizado:** 2026-11-26
**Rama de trabajo:** `research/source-automation-2026-11`
**Rama base:** `research/catalog-coverage-2026-11`
**Pull request #1:** [abierto y en borrador](https://github.com/anonymit-project/album-numismatico/pull/1), sin fusionar ni modificar.
**Pull request #2:** [abierto y en borrador](https://github.com/anonymit-project/album-numismatico/pull/2), dirigido a la rama de documentación de la PR #1.

## Objetivo de la iteración

Completar la prueba de cobertura numismática para España, Andorra, Cuba, Ecuador y monedas XOF/XAF; evaluar imágenes y datasets bajo D-008; documentar sin iniciar el MVP.

## Hecho

- Leídos `AGENTS.md`, `docs/STATE.md`, `docs/PRD.md`, `docs/DECISIONS.md`, `docs/DATA_MODEL.md`, `docs/BACKLOG.md`, `docs/MOCKUPS.md` y `docs/CATALOG_SOURCES.md`.
- Verificado el repositorio: `main` y `docs/phase-0-project-context` existen. La rama documental está 22 commits por delante de `main` y 0 por detrás (la cifra de 16 commits del STATE anterior estaba desactualizada). `main` no se ha modificado.
- Localizada la PR #1 sobre la rama documental; permanece abierta y en borrador según el estado documentado y la búsqueda de PR.
- Creada la rama `research/catalog-coverage-2026-11` desde `docs/phase-0-project-context`.
- Probados ejemplos concretos de pesetas, euros regulares y conmemorativos, billetes españoles, Andorra, Cuba CUP/CUC, Ecuador sucre/USD y emisiones CFA XOF/XAF.
- Identificadas como fuentes institucionales útiles BCE/Comisión/DOUE, AFA, Banco de España, Museo Numismático/BCE Ecuador, BCEAO y BEAC.
- Verificados ejemplos de imágenes Commons con declaraciones CC0, CC BY-SA y dominio público, pero no aprobada ninguna incorporación: la licencia fotográfica no elimina las reglas de reproducción del diseño monetario.
- Precisadas las restricciones de reproducción de billetes euro, pesetas, monedas euro y las disposiciones cubanas sobre usos publicitarios.
- Identificados Nomisma, Syllogeum y CANOA como corpus reales de moneda principalmente antigua, sin cobertura suficiente del catálogo moderno. NumisLib anuncia una base de países/monedas, pero su licencia de base no quedó verificada.
- Actualizado `docs/CATALOG_SOURCES.md` con matriz de cobertura, ejemplos, resultados de derechos, datasets y enlaces.

## Resultado de la prueba

- **Cobertura de metadatos:** razonable para euro y CFA a través de autoridades emisoras; dispersa pero útil para peseta y sucre ecuatoriano; débil para Cuba CUP/CUC.
- **Imágenes reutilizables:** no se ha aprobado ninguna imagen de terceros para el catálogo. Las páginas institucionales son referencias; Commons exige análisis doble de licencia de fotografía y derechos/reglas del diseño monetario.
- **Dataset maestro:** no localizado. Los corpus abiertos encontrados se centran en moneda antigua. Numista continúa excluida.
- **Modelo:** XOF y XAF deben seguir siendo monedas diferentes, asociadas a sus autoridades monetarias supranacionales y a sus respectivos estados usuarios. Ecuador requiere distinguir USD usado de la moneda fraccionaria nacional acuñada por el BCE.

## Decisiones consolidadas

No se ha añadido ninguna decisión de producto. D-001 a D-008 siguen vigentes. Se aplica D-008 sin excepciones: no contactar con titulares, no reutilizar imágenes con licencia o derechos ambiguos y usar placeholders cuando no haya un recurso claramente compatible.

## Bloqueos y pendientes

1. No hay dataset abierto verificado que cubra de forma suficiente monedas y billetes modernos del alcance.
2. Cuba necesita una fuente primaria/estructurada mejor para el catálogo CUP/CUC; las referencias secundarias no son base de ingesta.
3. Las imágenes oficiales de Andorra, Ecuador, BEAC y BCEAO no muestran una licencia abierta general en los recursos revisados.
4. Las imágenes de pesetas y monedas euro encontradas en Commons no se aprueban automáticamente; la compatibilidad de la reproducción concreta debe quedar acreditada antes de incorporarlas.
5. Las imágenes oficiales de billetes euro solo son candidatas si se usan tal como permite el BCE, con «SPECIMEN» y los límites técnicos.
6. Continúan pendientes las validaciones de modelo, mapa, conservación, valoración histórica, backend/hosting, privacidad de identificación por foto, mockups y aprobación de cierre de Fase 0.

## Siguiente paso exacto

Probar CELLAR con un segundo aviso de moneda euro de otra clase (preferiblemente una nueva cara nacional regular, además de la conmemorativa de 2 € ya validada). Después, definir y probar un mapeo pequeño Formex/XML → staging con tests, sin conectarlo todavía al catálogo de producto. Para BEAC/BCEAO, preparar una extracción controlada de texto desde el manifiesto de páginas, con detección de cambios y revisión humana. Cuba permanece sin ingesta automatizada ni imágenes. No iniciar el MVP.

## Reglas para retomar

Leer, en este orden: `AGENTS.md`, este archivo, `docs/PRD.md`, `docs/DECISIONS.md`, `docs/DATA_MODEL.md`, `docs/BACKLOG.md` y `docs/CATALOG_SOURCES.md`. El repositorio es la fuente de verdad; si el chat contradice estos documentos, identificar la discrepancia y actualizar la documentación con el usuario.


## Iteración de automatización y fuentes estructuradas (25/11/2026)

**Rama:** `research/source-automation-2026-11`, creada desde `research/catalog-coverage-2026-11`.

### Hecho
- Releída la documentación de Fase 0 y comprobado el estado de PR #1 y PR #2 (abiertos, draft, sin fusionar). PR #3 también sigue abierto y draft, pero es una rama documental paralela basada en PR #2.
- Verificada la infraestructura de EUR-Lex/CELLAR: servicio SOAP/XML con registro, REST, SPARQL, RSS/Atom y documentos Formex. Revisada la guía oficial de desarrolladores que explica la jerarquía WEMI, el endpoint SPARQL, la obtención del identificador de fichero en Item y la descarga mediante negociación HTTP. Identificados ejemplos 2026 de avisos del DOUE para conmemorativas de 2 € y cambio de caras nacionales regulares.
- Documentados campos observables en los avisos: país emisor, tema, descripción, diseñador cuando consta, tirada estimada y fecha de emisión.
- Verificada la estructura HTML de BEAC: familias actuales e históricas, enlaces a PDF y tabla documental de piezas demonetizadas; detectada prohibición expresa de reproducción en una brochure oficial.
- Verificada la estructura HTML de BCEAO: billetes vigentes, retirados, anteriores a BCEAO y monedas; las páginas históricas están organizadas por los ocho estados miembros. La página de monedas ofrece datos técnicos de al menos las piezas de 200 y 500 FCFA.
- Localizados textos normativos primarios cubanos sobre emisión y reproducción de dinero; la Resolución 357/1994 describe la emisión inicial de CUC, pero la copia localizada está alojada fuera de un dominio institucional. No se encontró catálogo abierto ni API.
- Actualizado `docs/CATALOG_SOURCES.md` con métodos de extracción, límites, URLs y condiciones de reutilización.

### Resultado
- **Euro:** automatización viable a nivel de detección y recuperación de metadatos/documentos mediante CELLAR/EUR-Lex; aún falta probar la consulta filtrada exacta.
- **BEAC/BCEAO:** extracción de metadatos por lotes factible desde páginas concretas; no hay API/feed de emisiones identificado. Revisión humana obligatoria.
- **Cuba:** sigue siendo la mayor laguna; solo se puede avanzar con documentación jurídica y curación manual limitada.
- **Imágenes:** no se aprueba ninguna imagen nueva. Las imágenes monetarias quedan fuera de la ingesta por defecto.

### Pendiente y bloqueos
1. Se ha preparado una consulta SPARQL con un ELI real y confirmado el contenido del aviso desde el índice web, pero no se ha podido ejecutar el endpoint ni descargar Formex desde este entorno; no considerar validada la automatización de extremo a extremo.
2. No se ha probado un parser en BEAC/BCEAO ni se ha auditado exhaustivamente cada PDF; la extracción propuesta es documental, no código ejecutado.
3. La Resolución 357/1994 del CUC se ha localizado en una copia secundaria; falta una copia oficial accesible. No tratarla como fuente de importación.
4. No se ha encontrado licencia abierta general para imágenes de BEAC/BCEAO/Cuba.
5. No hay un dataset moderno maestro de monedas y billetes.

### Siguiente paso exacto
Ejecutar una prueba de concepto de CELLAR: consulta SPARQL de avisos de monedas euro, recuperación del recurso Item y descarga Formex/XML por negociación HTTP; contrastar el resultado con una alerta RSS personalizada. Validar el mapeo de campos antes de plantear un importador. En paralelo, definir el manifiesto versionado de páginas BEAC/BCEAO (sin descargar imágenes). Mantener Cuba en estado manual/documental. No iniciar el MVP.


## Prueba de concepto CELLAR (25/11/2026)

- Recuperado desde el índice web oficial el texto de C/2026/406 (Lituania), confirmando los campos numismáticos del aviso: país emisor, tema, descripción, diseñador, tirada estimada y fecha de emisión.
- Revisada la documentación oficial de CELLAR Knowledge Graph y RSS/Atom; se preparó una consulta SPARQL concreta contra el ELI de C/2026/406 para extraer Work/Expression/Manifestation/Item.
- **No se pudo ejecutar la consulta ni descargar el Formex desde el entorno del agente.** Las pruebas directas fallaron por restricciones de red/DNS de esta sesión, no por un fallo demostrado de CELLAR.
- No se había configurado una alerta EUR-Lex ni ejecutado un parser. La prueba documental inicial no validaba todavía la cadena técnica.

### Resultado actualizado tras la ejecución manual del usuario
- El usuario ejecutó la consulta SPARQL en el editor oficial de CELLAR y obtuvo **seis resultados**: tres manifestaciones para español (`SPA`) y tres para lituano (`LIT`), en formatos `pdfa2a`, `fmx4` y `xhtml`.
- Se recuperó en navegador el Item XHTML español y se visualizó el aviso completo.
- Se descargó el Item Formex español como ZIP, con tres XML y un TIFF. Se examinó el XML principal español y se confirmó que contiene el texto del aviso, la referencia a la imagen y los campos numismáticos.
- Se examinó el XML principal lituano proporcionado por el usuario. Conserva una estructura Formex equivalente y permite identificar los mismos datos numismáticos en lituano.
- Campos contrastados en ambas expresiones: emisor (Lituania), tema (Lituania Menor), diseñador (Rolandas Rimkūnas), autor del escudo (Arvydas Každailis), tirada estimada (500.000) y fecha de emisión (cuarto trimestre de 2025).
- La consulta, los URIs, los recursos recuperados, el contenido XML y los límites están documentados en [`docs/CELLAR_POC.md`](CELLAR_POC.md).

### Conclusión
**Prueba manual positiva de extremo a extremo para un aviso concreto y dos idiomas.** Queda demostrado el acceso SPARQL, la localización WEMI, la recuperación de XHTML/Formex y la lectura de los campos numismáticos. No equivale a automatización desatendida, parser probado, cobertura general ni autorización para reutilizar las imágenes.

### Pendiente
1. Validar un segundo aviso de otra clase (preferiblemente una nueva cara nacional regular) para comprobar variación documental.
2. Implementar y probar, solo como herramienta de investigación y no como código de producto, un mapeo Formex/XML a un esquema de staging con tests.
3. Mantener sin cambios la política de imágenes: no incorporar el TIFF ni otros diseños monetarios sin derechos verificados.
4. Continuar las tareas de Fase 0 de modelo, fuentes, licencias, mapa, valoración, mockups y costes.

## Estado de PR #4

PR #4 permanece abierta, en borrador y sin fusionar. Los cambios de esta iteración se registran en la misma rama de investigación; no se modifica `main` ni se inicia el MVP.


## Segunda prueba CELLAR — Mónaco C/2026/419 (25/11/2026)

### Hecho
- Ejecutada manualmente la consulta SPARQL y localizados Work, Expressions, Manifestations e Items.
- La Expression inglesa (ENG) ofrece `pdfa2a`, `fmx4` y `xhtml`.
- Descargado el Item Formex como ZIP con 3 XML y 8 TIFF.
- Identificado el XML principal: `C_202600419EN.000101.fmx.xml`.
- Confirmado que el XML contiene datos estructurados de ocho denominaciones, emisor, fecha de emisión y diseños; para la moneda de 2 € incluye además ceca e inscripción del canto.
- Documentada la prueba y sus límites en `docs/CELLAR_POC.md`.

### Resultado
**Segunda prueba manual positiva** de recuperación y lectura de Formex para otro aviso y emisor. Junto con C/2026/406, refuerza la viabilidad de CELLAR como fuente de metadatos numismáticos. No acredita automatización general ni un parser probado.

### Límites y pendientes
- La prueba fue manual; no se ha implementado ni ejecutado automatización desatendida.
- Los 8 TIFF no se incorporan. La disponibilidad/descarga de imágenes no resuelve sus derechos de reutilización; se mantiene D-008.
- Siguiente paso técnico, cuando se autorice: diseñar una muestra de mapeo Formex → staging y sus tests. No desarrollar todavía el parser ni iniciar el MVP.


## Investigación de detección de avisos oficiales (25/11/2026)

### Hecho
- Revisada la documentación oficial de CELLAR RSS/Atom. El canal ingestion notifica eventos CREATE, UPDATE y DELETE, con filtros por fechas y clases WEMI. Las entradas aportan identificadores de evento, recurso (cellarId), raíz lógica (rootCellarId), clases, identificadores asociados y fecha.
- Confirmado que CELLAR no documenta un filtro temático numismático en ese feed; la detección requiere filtrar posteriormente los eventos mediante metadatos/títulos y, cuando proceda, SPARQL.
- Revisada la documentación oficial de RSS de EUR-Lex: permite generar feeds a partir de búsquedas guardadas. Requiere cuenta/EU Login y el límite documentado es de 50 búsquedas guardadas compartidas con alertas por correo.
- Identificadas dos variantes recurrentes de títulos de avisos de caras nacionales de monedas euro; una búsqueda temática tendría que contemplar ambas y validarse con ejemplos anteriores.
- Comparativa y recomendación documentadas en docs/CELLAR_POC.md.

### Resultado y recomendación
CELLAR RSS/Atom es el candidato principal para una futura detección técnica por su trazabilidad de eventos y recursos WEMI. EUR-Lex RSS es un contraste temático complementario, pero depende de búsquedas guardadas en una cuenta. Se recomienda un flujo híbrido, deduplicación por identificador lógico y staging con revisión humana.

### No verificado
No se ha ejecutado el endpoint RSS/Atom, comprobado su paginación en operación, creado una alerta EUR-Lex ni medido cobertura, frecuencia, cuotas o SLA. La investigación documental no equivale a una prueba operativa ni a una automatización implementada.


## Prueba operativa CELLAR RSS/Atom — 25/11/2026

- Confirmada la rama `research/source-automation-2026-11`; revisados AGENTS.md, STATE.md, DECISIONS.md, BACKLOG.md y CELLAR_POC.md.
- Intentado el acceso HTTPS al endpoint oficial de ingestion y una petición filtrada. El entorno devolvió `Temporary failure in name resolution`; también falló la resolución DNS de dominios externos de control.
- Diagnóstico: bloqueo de conectividad/DNS del entorno de ejecución, no fallo demostrado de CELLAR. No se recibieron respuestas HTTP.
- No se han verificado en operación las entradas, identificadores, filtros, paginación ni recuperación de metadatos. La estructura descrita sigue siendo documental.
- C/2026/406 (Lituania) y C/2026/419 (Mónaco) siguen confirmados como avisos numismáticos por la documentación y pruebas manuales previas; no se ha confirmado su presencia en el feed.
- Añadida a `docs/CELLAR_POC.md` la hipótesis de deduplicación por evento (`id`), recurso (`cellarId`) y documento lógico (`rootCellarId` + ELI/CELEX cuando exista), pendiente de contraste con respuestas reales.
- No se ha escrito código, configurado alertas ni incorporado datos o imágenes. D-008 y revisión humana permanecen vigentes.

### Siguiente paso exacto

Repetir la prueba operativa desde un entorno con DNS/HTTPS funcional, conservar respuestas RSS/Atom originales, validar filtros por separado, comprobar paginación y seguir eventos hasta sus metadatos WEMI. La tarea permanece abierta; no marcarla como completada.


## Preferencia de organización del trabajo (25/11/2026)

El usuario prefiere trabajar mediante muchos chats breves, cada uno centrado en una tarea sencilla y acotada, en lugar de conversaciones largas con varias tareas acumuladas. Al cerrar cada tarea, preparar un prompt de relevo autosuficiente para un chat nuevo. Mantener además el aviso proactivo cuando el contexto se aproxime a su límite. Norma detallada en `AGENTS.md`.


## Actualización de prueba operativa CELLAR RSS/Atom — 25/11/2026

Esta actualización complementa el resultado anterior de bloqueo DNS: el intento desde el entorno del agente falló por DNS, pero el usuario pudo ejecutar las peticiones desde PowerShell y validar el endpoint.

### Hecho
- Endpoint `https://publications.europa.eu/webapi/notification/ingestion`, con `Accept: application/atom+xml`, accesible desde el entorno del usuario.
- Consulta sin filtros para 19–25/11/2026: HTTP 200, XML Atom válido, página 1, 1.000 entradas y `moreEntries=true`.
- Probados `type=create`, `type=update`, `wemiClasses=DOSSIER` y la combinación `type=create&wemiClasses=ITEM`. Las primeras entradas inspeccionadas en cada caso cumplen los filtros solicitados.
- La combinación create + ITEM devolvió HTTP 200, 1.000 entradas y `moreEntries=true`.
- Los detalles, muestras y límites están documentados en `docs/CELLAR_POC.md`, sección 9.

### Conclusión
**Acceso al feed y filtros básicos validados manualmente.** Esto corrige el estado anterior de “sin respuesta HTTP” para las pruebas realizadas por el agente: el servicio sí respondió desde el entorno del usuario. No se ha validado aún la paginación, la ventana completa, valores múltiples de clases WEMI, eventos DELETE ni la detección fiable de avisos numismáticos.

### Pendiente
1. Probar paginación y comprobar continuidad, huecos y duplicados al superar 1.000 entradas.
2. Investigar la representación de `title`, `summary`, `id` y `link href`, que aparecieron como cadenas plantilla `$item.*` en la salida de PowerShell.
3. Probar valores múltiples de `wemiClasses` y eventos DELETE.
4. Seguir un evento real hasta sus metadatos WEMI y comprobar si puede relacionarse con un aviso numismático conocido.
5. Solo después, valorar un cliente de investigación con persistencia y trazabilidad; no iniciar automatización de producto.

Se mantiene Fase 0, D-008 y revisión humana. No se ha escrito código ni incorporado datos o imágenes al catálogo.


## Actualización de paginación CELLAR RSS/Atom (25/11/2026)

- Página 1 del feed ingestion, para la ventana 19–25/11/2026, descargada desde PowerShell: HTTP 200 y 1.000 entradas.
- En una prueba previa comunicada, página 2 también devolvió HTTP 200 y 1.000 entradas.
- Las tres primeras entradas de página 2 comparten timestamp con la última observada de página 1 (`2026-11-19T00:49:36.274+01:00`). Esto no prueba duplicidad; falta comparar identificadores y contenido.
- La descarga de página 1 se hizo con URL literal completa. Para PowerShell se recomienda `Invoke-WebRequest -UseBasicParsing`; no depender de variables creadas en ejecuciones anteriores.
- **Estado:** acceso a ambas páginas observado, pero continuidad, huecos y duplicados siguen sin validar. No deduplicar por timestamp.
- Evidencia y siguiente prueba en la sección 10 de `docs/CELLAR_POC.md`.

### Siguiente paso exacto

Descargar página 1 y página 2 en una sola ejecución de PowerShell, conservar las respuestas y comparar sus elementos de frontera usando los campos XML reales. Inspeccionar XML crudo si los campos de identidad aparecen como plantillas. No abordar todavía otros filtros ni automatización.


## Actualización: paginación operativa CELLAR — 25/11/2026

- P1–P5 de la ventana 19–25/11/2026 descargadas desde PowerShell: HTTP 200 y 1.000 entradas por página; al menos 5.000 entradas recuperadas.
- notifReq:moreEntries=true observado en P3, P4 y P5; no se ha localizado la página final.
- Fronteras P1/P2, P2/P3 y P3/P4: timestamp compartido, pero cero claves cellarId|updated repetidas. Recuentos de entradas con el timestamp frontera: 38/11, 4/4 y 68/5.
- P1–P3 conservaron hashes idénticos de claves ordenadas en consultas repetidas, incluida una tras unos 15 minutos. Esto no demuestra estabilidad ante inserciones ni estabilidad de P4/P5.
- cellarId|updated es una clave candidata de deduplicación, no una garantía global. No usar updated solo como cursor.
- Evidencia detallada en docs/CELLAR_POC.md, sección 11.

### Siguiente paso exacto

Continuar desde page=6 hasta la condición terminal notifReq:moreEntries. Registrar por página el número de entradas, moreEntries y límites temporales. No diseñar aún el cursor incremental ni implementar sincronizador. Después probar estabilidad de las páginas más recientes y cambios por inserciones tardías. Mantener Fase 0 y no iniciar el MVP.

## Actualización CELLAR — límite de paginación localizado provisionalmente (25/11/2026)

- El usuario inspeccionó los metadatos de la respuesta Atom de P9: el feed incluye `startDate`, `endDate`, `page` y `moreEntries`, pero no se observó un total de resultados ni enlace a última página.
- Para evitar recorrer secuencialmente todas las páginas, ejecutó una búsqueda exponencial y binaria desde PowerShell.
- El script comunicó P330 con `moreEntries=true` y P331 con `moreEntries=false`; resultado final: límite localizado provisionalmente en P331.
- No se conoce todavía el recuento de entradas de P331 ni si está vacía/parcial/completa. Tampoco se ha comparado la frontera P330→P331 ni comprobado P332.
- La búsqueda binaria presupone monotonía de `moreEntries` respecto al número de página; la salida aportada no incluye la traza de páginas intermedias. Confirmar directamente P330 y P331 antes de dar por validada la condición terminal.

### Siguiente paso exacto

En un chat nuevo, leer los documentos obligatorios y realizar una única comprobación PowerShell de P330 y P331, registrando HTTP, recuento, `page`, `moreEntries` y primer/último `updated`. Comparar la frontera si se dispone de las claves. No recorrer páginas intermedias ni implementar sincronizador/parser. Tras confirmar P331, decidir si una consulta única a P332 aporta valor para caracterizar el comportamiento posterior al final. Evidencia detallada en `docs/CELLAR_POC.md`, sección 12.


## Cierre de validación de paginación CELLAR — 26/11/2026

**Rama:** `research/source-automation-2026-11`  
**Fase:** 0 — investigación; sin código de producto.

### Objetivo de la iteración
Cerrar la comprobación directa del límite de paginación del feed CELLAR ingestion para `startDate=2026-11-19&endDate=2026-11-25`.

### Resultado confirmado por el usuario desde PowerShell

- P330: HTTP 200, página XML 330, 1.000 entradas, `moreEntries=true`; primer/último `updated`: 2026-11-24T23:28:33.843+01:00 / 2026-11-24T23:43:56.595+01:00.
- P331: HTTP 200, página XML 331, 959 entradas, `moreEntries=false`; primer/último `updated`: 2026-11-24T23:43:56.595+01:00 / 2026-11-24T23:58:29.346+01:00.
- P330→P331: cero claves repetidas en la comparación de las últimas 10 y primeras 10 claves `cellarId|updated`. El timestamp de frontera coincide, pero no las claves de esas ventanas.
- P332: HTTP 200, página XML 332, cero entradas, `moreEntries=false`.

### Conclusión
La paginación y la condición terminal quedan **validadas manualmente para esta consulta/captura**. P331 es la última página no vacía observada; P332 confirma el comportamiento posterior al final. No se afirma el total exacto de entradas porque no se registraron recuentos de todas las páginas P1–P329. La comparación de frontera es limitada a ventanas de 10; no demuestra unicidad global ni ausencia de huecos en todo el conjunto.

### No demostrado / no realizado
- Estabilidad entre capturas e inserciones tardías; comportamiento de las páginas recientes bajo nuevas notificaciones.
- Unicidad global de `cellarId|updated` o idoneidad como clave de deduplicación/cursor.
- Extracción y semántica del identificador de evento `id`, `rootCellarId`, eventos DELETE y valores múltiples de `wemiClasses`.
- Cobertura exhaustiva de avisos numismáticos.
- Cliente automatizado, parser, sincronizador o código de producto.
- No se han incorporado datos ni imágenes. D-008 permanece vigente.

### Siguiente paso exacto
Inspeccionar una entrada Atom real en bruto para identificar los campos de evento/recurso (`id`, `cellarId`, `rootCellarId`) y determinar qué representa cada uno. Mantenerlo como una prueba de observación, sin diseñar cursor incremental ni implementar código de sincronización. Antes de actuar en una nueva sesión, releer `AGENTS.md`, `docs/STATE.md`, `docs/DECISIONS.md`, `docs/BACKLOG.md`, `docs/CELLAR_POC.md` y `docs/PRD.md`.


## Inspección de identidad Atom CELLAR — 26/11/2026

### Hecho
- Desde PowerShell, el usuario recuperó la primera entrada de P331 para la ventana 19–25/11/2026 y mostró el XML Atom original (`OuterXml`). HTTP 200; `Content-Type: text/xml;charset=UTF-8`.
- La entrada es `update` y `wemiClass=EXPRESSION`; `classes/class` apunta a `cdm#expression`.
- `cellarId=cellar:36f412cf-e80d-11f1-b745-01aa75ed71a1.0004`; `rootCellarId=cellar:36f412cf-e80d-11f1-b745-01aa75ed71a1`.
- `identifiers` contiene CELEX y consolidation con sufijo `.CES`; `rootIdentifiers` contiene CELEX, consolidation y ELI sin ese sufijo.
- `atom:id` contiene literalmente `${item.cellarUri}_2026-11-24T23:43:56.595+01:00`; `title`, `summary` y `link href` también contienen plantillas `$item.*` sin resolver.

### Interpretación y límites
La muestra apoya que `cellarId` es el recurso concreto (Expression) y `rootCellarId` su raíz documental, y que `identifiers`/`rootIdentifiers` relacionan expresión y documento lógico con CELEX/consolidation/ELI. No valida la semántica completa ni la unicidad de estos campos. El identificador Atom de evento no es utilizable en esta respuesta porque conserva una plantilla literal; no adoptar `cellarId|updated` como sustituto probado. Tampoco se ha seguido aún el recurso hasta metadatos WEMI independientes.

### Siguiente paso exacto
Inspeccionar una segunda entrada de otra clase WEMI (preferiblemente ITEM o WORK) para comprobar si las plantillas sin resolver afectan también a sus campos `id`, `title`, `summary` y `link`. Mantener la prueba manual, sin parser, cliente, sincronizador ni código de producto.

La evidencia detallada queda en `docs/CELLAR_POC.md`, sección 14. Fase 0 y D-008 continúan vigentes; no se incorporan datos ni imágenes al catálogo.


## Segunda inspección de identidad Atom CELLAR — 26/11/2026

### Hecho
- Reutilizada la respuesta P331 ya descargada (ventana 19–25/11/2026; HTTP 200; 959 entradas), sin repetir la petición.
- Inspeccionada la primera entrada `ITEM` encontrada, índice 7 del array XML (base cero).
- La entrada es `type=create`, `wemiClass=ITEM`; `cellarId=cellar:ed772589-e81d-11f1-b745-01aa75ed71a1.0024.02/DOC_1` y `rootCellarId=cellar:ed772589-e81d-11f1-b745-01aa75ed71a1`.
- `atom:id`, `title`, `summary` y `link href` vuelven a contener las plantillas literales `${item.cellarUri}`, `$item.title`, `$item.entrySummary` y `$item.cellarUri`.
- La comparación con la entrada EXPRESSION de la sección 14 muestra las mismas cuatro plantillas en dos clases WEMI y dos tipos de evento distintos. Evidencia completa en la sección 15 de `docs/CELLAR_POC.md`.

### Conclusión y límites
La repetición en dos muestras refuerza que las plantillas no resueltas no son exclusivas de la entrada EXPRESSION observada. No permite generalizar a todo el feed ni establece la semántica/unicidad de los identificadores. `cellarId` y `rootCellarId` sí aparecen materializados en ambas entradas. No usar `atom:id` como ID de evento válido ni adoptar `cellarId|updated` como sustituto global probado.

### Siguiente paso exacto
Seguir uno de los `cellarId` observados hasta sus metadatos WEMI mediante CELLAR/SPARQL, en una tarea separada. No investigar todavía DELETE ni múltiples `wemiClasses`; no implementar parser, cliente, cursor ni sincronizador. Fase 0 y D-008 continúan vigentes; sin datos ni imágenes incorporados al catálogo.


## Cierre de prueba de seguimiento WEMI y planificación — 26/11/2026

### Prueba CELLAR
- Se intentó consultar las propiedades salientes del ITEM `cellar:ed772589-e81d-11f1-b745-01aa75ed71a1.0024.02/DOC_1` en el editor SPARQL oficial.
- La consulta simplificada devolvió `bindings: []`. Una consulta previa con UNION/BIND falló al compilar (Virtuoso SP031).
- Resultado: prueba **inconclusa**. No demuestra que el recurso sea inválido ni que no exista; no se obtuvieron triples con esa URI y consulta. Detalle en la sección 16 de `docs/CELLAR_POC.md`.
- No continuar investigando CELLAR en esta iteración. No implementar parser, cliente ni sincronizador.

### Previsión de producto (estimación orientativa, no compromiso)

Supuesto de planificación: una persona desarrollando con ayuda de herramientas, unas 8–10 horas efectivas por semana, decisiones del usuario en plazos cortos y sin bloqueos extraordinarios de servicios gratuitos. Las estimaciones se recalibrarán tras cerrar Fase 0 y probar el primer esqueleto técnico.

- **Mock-up navegable para revisión:** objetivo de 2–4 semanas desde ahora. Incluye flujos principales y pantallas clave, no backend ni datos reales completos.
- **V1 mínimamente funcional:** objetivo de 3–5 meses desde ahora, condicionado al cierre/aprobación de Fase 0 y a limitar el alcance al MVP descrito abajo.
- Si la dedicación semanal es menor, hay decisiones pendientes o el alcance crece hacia mapa, escáner, catálogo mundial o automatización completa, la fecha se desplaza. No presentar estas fechas como garantía.

### Alcance propuesto para V1

PWA móvil instalable; autenticación; colección privada; catálogo semilla limitado y trazable; álbum con tengo/falta y cantidades; alta/edición manual; importación CSV básica; KPIs sencillos; exportación de datos; diseño adaptable, modo oscuro, CI y pruebas esenciales. Quedan fuera de V1 el globo/mapa avanzado, escáner por foto, importación XLSX avanzada/asistente por lotes, catálogo mundial completo, contribuciones públicas, gamificación y funciones sociales.

### Siguiente paso exacto

Continuar Fase 0 por la tarea de mayor desbloqueo: cerrar el modelo de datos con los casos límite ya definidos y resolver decisiones mínimas de UX/alcance del MVP. Preparar mock-up navegable tras acordar esos flujos. No iniciar código de producto hasta aprobación expresa del cierre de Fase 0.


## 17. Decisión de prototipado y siguiente iteración — 26/11/2026

- El usuario ha aprobado que la siguiente tarea sea construir un **prototipo interactivo responsive**, móvil primero y también usable en ordenador, para validar la viabilidad de la experiencia de la app.
- D-009 autoriza expresamente este prototipo antes del cierre de Fase 0, con límites estrictos: datos ficticios, sin backend, autenticación, sincronización, persistencia real, catálogo ni servicios externos. No es el MVP ni código de producto.
- El objetivo de la siguiente iteración es implementar el prototipo y dejarlo listo para revisión del usuario y su amigo en navegador Android y escritorio.
- La planificación detallada y las estimaciones de dedicación están en docs/BACKLOG.md, sección «Planificación de entregables y estimación».
- **Estimación inicial:** 29–45 horas para construir el prototipo (aprox. 4–6 jornadas de 7–8 h), más 6–10 horas para revisión y ajustes. Son rangos orientativos, sujetos a la estructura existente del repositorio y al feedback.
- La investigación CELLAR queda cerrada como inconclusa en su última prueba (sección 16 de docs/CELLAR_POC.md); no es el siguiente paso.
- Fase 0 continúa abierta. No se ha aprobado el MVP ni se ha modificado main.


## Cambio de alcance del prototipo UX — 26/11/2026

**Decisión vigente:** D-010 aclara D-009. El prototipo será una maqueta visual interactiva para validar diseño, navegación y usabilidad, no una simulación funcional extensa.

### Alcance mínimo
- Recorrido navegable: inicio → emisor → moneda → serie → álbum → ficha.
- Interacciones visibles: tengo/me falta, cantidad sencilla y progreso.
- Búsqueda, filtros y orden básicos que actualicen la vista.
- Diseño móvil primero y responsive para Android y escritorio.
- Datos ficticios, placeholders neutros y sin persistencia.

### Fuera de alcance
No construir flujos de alta/edición, importación/carga simulada, formularios administrativos completos, validación de ficheros, lógica de negocio exhaustiva, backend ni arquitectura de producción. Esos elementos solo se añadirán si una necesidad concreta de validación UX lo justifica.

### Enfoque y estimación revisados
Se prioriza el camino más rápido para obtener una demo navegable, sin imponer framework ni estructura de producción. Estimación preliminar revisada: **4–8 horas de construcción** y **2–3 horas de revisión/correcciones**, pendiente de confirmar al implementar el primer corte visual. La estimación anterior de 29–45 h queda sustituida para este alcance reducido; no se ha cambiado la estimación de un MVP futuro.

### Siguiente paso exacto
Crear el primer corte navegable con diseño responsive y datos ficticios, limitado al recorrido principal y las interacciones descritas. Probarlo realmente en navegador Android y escritorio; si el entorno no permite alguna prueba, documentar la limitación y solicitar la comprobación al usuario. No continuar CELLAR ni ampliar funcionalidades sin autorización.


## Prototipo visual responsive — 26/11/2026

### Alcance y decisiones aplicadas
- Se inicia el prototipo visual interactivo conforme a D-009 y D-010; la Fase 0 permanece abierta y esto no autoriza el MVP.
- Inspección de la rama: existe README y documentación de proyecto, pero no se encontraron `package.json`, `index.html` ni estructura frontend en las rutas habituales. Se elige un único `index.html` autocontenido, sin framework, dependencias ni compilación.
- Se crea `index.html` con navegación Inicio → Emisores → Moneda → Serie → Álbum → Ficha; pantallas de progreso; datos de demostración; placeholders geométricos neutros; posesión/cantidad; búsqueda, filtros y ordenación.
- Diseño responsive con navegación lateral en escritorio y barra inferior en pantallas estrechas. Los cambios son solo memoria de la pestaña/sesión; no hay backend ni persistencia.
- No se modifica el modelo de datos ni se incorporan imágenes, textos o datos numismáticos de terceros. No se añade una decisión de producto nueva; D-010 es suficiente.

### Verificación
- Confirmada por GitHub la creación y posterior ajuste de `index.html` en `research/source-automation-2026-11`.
- No se ha ejecutado el prototipo en un navegador real ni probado Android/escritorio desde este entorno. Tampoco se ha configurado hosting público. La revisión visual/táctil queda pendiente del usuario.
- La muestra contiene ocho piezas ficticias; cantidades y progreso se recalculan al interactuar. No representa catálogo ni reglas numismáticas reales.

### Próximo paso exacto
- Abrir la maqueta en escritorio y Android mediante un servidor estático o una vista previa publicada; revisar navegación, legibilidad, filtros y cambios de posesión/cantidad. Registrar feedback antes de modificar el diseño.
- Para facilitar una URL pública estable, decidir/configurar el hosting estático (por ejemplo, GitHub Pages) en una tarea posterior; no asumir que está habilitado.

### Límites
- El fichero es un prototipo desechable, no arquitectura ni código base del MVP.
- CELLAR continúa aparcado. No reanudar parser, sincronizador ni pruebas de feed en esta iteración.


## Ampliación del prototipo: mapamundi y billetes — 26/11/2026

- Solicitud del usuario: añadir una vista de mapamundi con los países seleccionados y ampliar la muestra para incluir billetes.
- Se amplía el prototipo con una vista de mapa esquemática que destaca España, Francia, Italia y Madagascar. Madagascar se incorpora como emisor de demostración para separar visualmente los marcadores europeos; sus datos son ficticios.
- Se añade un recorrido de serie «Billetes», con placeholders rectangulares y ejemplos de denominaciones en euros; para Madagascar, ejemplos de ariary. Se mantiene la interacción de posesión y cantidad.
- El mapa es una ilustración esquemática, no un mapa geográfico preciso ni un globo 3D; no calcula aún progreso por país. No usa teselas ni recursos cartográficos externos.
- La ampliación sigue siendo UX desechable: sin persistencia, backend ni imágenes monetarias reales.

### Verificación y límites
- Cambios registrados en la rama de investigación y revisados por contenido/estructura del HTML.
- No se ha ejecutado en navegador ni validado visualmente en Android/escritorio. La forma, precisión geográfica y usabilidad del mapa deben revisarse en la siguiente prueba manual.
- El mapa no sustituye la futura decisión de cartografía D3-geo/Natural Earth ni resuelve estados históricos, territorios o uniones monetarias.

### Siguiente paso exacto
- Abrir la vista previa y probar en escritorio y Android la navegación Mapamundi ↔ emisor y Álbum → Billetes → Ficha. Recoger feedback antes de otra ronda.


## Estado de publicación y revisión externa — 26/11/2026

Esta sección actualiza la situación de entrega descrita en los apartados anteriores, que reflejaban el estado previo a la publicación.

- El usuario confirma que ha publicado el prototipo mediante GitHub Pages, ha conseguido abrir la página renderizada (no solo el código fuente HTML) y ha compartido la URL con un amigo para recoger feedback.
- La publicación y la revisión por el amigo se registran como **confirmación comunicada por el usuario**; no se han verificado independientemente desde esta sesión ni se ha inspeccionado la URL publicada.
- El amigo todavía no ha enviado feedback. No hay observaciones recibidas ni cambios de UX aprobados.
- Sigue pendiente una revisión propia en navegador real, tanto en Android como en escritorio. No se debe marcar como validada la experiencia responsive hasta realizarla.
- El prototipo sigue siendo desechable, con datos ficticios y sin backend, persistencia, autenticación o sincronización. La Fase 0 permanece abierta.

### Próximo paso exacto
Esperar el feedback del amigo. Cuando llegue, clasificar cada observación como usabilidad, diseño, funcionalidad o preferencia personal; evaluar impacto/esfuerzo y proponer una ronda acotada de correcciones. En paralelo o después, realizar la revisión propia en Android y escritorio. No ampliar el prototipo mientras no haya evidencia concreta que lo justifique.


## Reorientación del trabajo tras publicar el prototipo — 26/11/2026

### Decisión operativa vigente
No se esperará el feedback del prototipo para continuar con las tareas de descubrimiento. La validación UX queda **diferida, pero no cancelada**: el usuario ya ha publicado la demo en GitHub Pages y la ha compartido con un amigo; se recogerá y aplicará el feedback cuando esté disponible. La revisión propia en Android y escritorio también queda pendiente, pero ninguna de estas actividades bloquea el trabajo actual de Fase 0.

### Trabajo activo
Retomar la validación del modelo conceptual y su encaje con el catálogo, usando casos representativos: Andorra, Cuba (CUP/CUC), Ecuador (sucre/USD y moneda fraccionaria nacional), euro, XOF/XAF y peseta, además de emisores/monedas históricos cuando afecten a las relaciones temporales. Partir de `docs/DATA_MODEL.md` y contrastar con la evidencia y limitaciones de `docs/CATALOG_SOURCES.md`. El objetivo inmediato es detectar huecos estructurales y precisar qué entidades, relaciones, vigencias y procedencia requiere el modelo; no crear todavía un catálogo exhaustivo ni importar datos.

### Límites que no cambian
- Fase 0 sigue abierta. No se ha aprobado su cierre ni el inicio del MVP.
- No escribir código de producto ni convertir el prototipo en base de producción.
- Mantener D-008: no incorporar datos o imágenes sin derechos compatibles verificados.
- La investigación CELLAR queda aparcada; no reanudar parser, feed, cursor o sincronizador salvo petición expresa.
- La validación de backend/hosting, privacidad, conservación, valoración, mapa y catálogo semilla sigue pendiente.

### Siguiente paso exacto
Realizar una revisión estructural de `docs/DATA_MODEL.md` contra los casos enumerados y la evidencia de `docs/CATALOG_SOURCES.md`. Entregar una matriz caso → entidades/relaciones necesarias → cobertura actual → hueco o ambigüedad → propuesta mínima. No modificar el modelo como decisión aprobada sin explicar el impacto y distinguir propuesta de decisión consolidada.


## Validación estructural del modelo numismático — 26/11/2026

**Resultado:** revisión conceptual de `docs/DATA_MODEL.md` frente a Andorra, Cuba CUP/CUC, Ecuador (sucre, USD y moneda fraccionaria nacional), euro, XOF/XAF, peseta y monedas históricas, contrastada con `docs/CATALOG_SOURCES.md`.

### Conclusiones
- La separación actual entre emisor, moneda, relación temporal, diseño, emisión y posesión es una base válida; no basta aún para expresar con precisión todas las relaciones de autoridad y estatus monetario.
- Huecos principales detectados: distinguir entidad política de autoridad monetaria; roles explícitos en la relación emisor-moneda; estados y fechas independientes de circulación/retirada/canje; transición monetaria con coexistencia y conversión; identidad por caras compartibles; denominaciones estructuradas.
- Casos críticos: Ecuador (USD utilizado y fraccionaria nacional), euro (múltiples emisores y cara común), XOF/XAF (autoridad supranacional distinta de estados usuarios), Cuba (coexistencia CUP/CUC y retirada), monedas históricas (emisores/autoridades extinguidos y sucesión monetaria).
- Se prepararon seis propuestas no aprobadas: P1 autoridad emisora; P2 roles de relación emisor-moneda; P3 estado monetario de emisión; P4 modelado de caras; P5 transiciones monetarias; P6 denominaciones estructuradas.

### Fuentes y límites de poblamiento
- Euro: BCE/Comisión/DOUE y CELLAR ofrecen buen soporte para metadatos de emisiones y avisos; los derechos de las imágenes de caras nacionales y comunes siguen sujetos a verificación separada.
- Andorra: BCE y AFA ofrecen metadatos de euro y acuerdo monetario; no hay licencia abierta general verificada para imágenes institucionales.
- XOF/XAF: BCEAO y BEAC publican familias y datos técnicos en HTML/PDF; no se identificó API/dataset común ni licencia abierta general para imágenes. Extracción controlada con revisión humana.
- Ecuador: BCE/Museo Numismático permiten contrastar sucre y fraccionarias USD; no se identificó licencia abierta general para imágenes.
- Peseta: Banco de España y Commons ayudan a localizar/contrastar piezas, pero las reglas de reproducción de moneda/billete se deben verificar por separado de la licencia fotográfica.
- Cuba: fuentes normativas y referencias secundarias permiten un esqueleto histórico, pero no existe en lo revisado un catálogo oficial estructurado y reutilizable; no automatizar ni importar imágenes.
- Wikidata CC0 puede enriquecer entidades, códigos y relaciones, pero no es autoridad numismática única. ISO 4217/3166 aportan identificadores, no un catálogo de emisiones. Natural Earth es cartografía, no fuente de soberanía monetaria.

### Estado y límites
- No se modifica `docs/DATA_MODEL.md` ni `docs/DECISIONS.md`: las propuestas requieren revisión y aprobación expresa.
- D-008 permanece vigente. Acceso institucional o licencia de fotografía no implica permiso para reproducir el diseño monetario.
- Fase 0 sigue abierta; no se autoriza MVP ni código de producto.
- D-011 sigue vigente: feedback UX diferido, no cancelado; revisión Android/escritorio pendiente.
- CELLAR permanece aparcado salvo petición expresa.

### Siguiente paso exacto
Revisar y decidir P1–P6. Antes de rediseñar el modelo completo, acordar si se acepta la separación de autoridad monetaria y los roles explícitos de las relaciones. Después concretar el mínimo esquema conceptual revisado y volver a probarlo con los mismos casos. No iniciar implementación.


## Revisión de propuestas del modelo P1–P6 — 26/11/2026

- Revisadas individualmente las seis propuestas frente a Andorra, Cuba CUP/CUC, Ecuador, euro, XOF/XAF y peseta.
- Elaborado `docs/MODEL_REVIEW.md` con problema, alternativas, recomendación mínima, complejidad, consecuencias y matriz de cobertura.
- Recomendaciones técnicas: P1 autoridad monetaria separada (acotada); P2 roles temporales tipados; P3 cronología legal basada en hechos/fechas; P4 caras reutilizables manteniendo identidad por pareja; P5 transiciones tipadas sin confundir coexistencia; P6 valor facial racional exacto más etiqueta original.
- **Estado de aprobación:** ninguna propuesta aprobada. No se modifican `DATA_MODEL.md` ni `DECISIONS.md`; D-008 y D-011 siguen vigentes.
- **Fase 0:** abierta. CELLAR sigue aparcado. No se inicia MVP ni código de producto.
- **Siguiente paso:** el usuario debe aprobar o rechazar P1–P6 individualmente; solo entonces se consolidarán los cambios autorizados.


## Aprobación y consolidación de P1–P6 — 26/11/2026

El usuario ha aprobado expresamente las seis propuestas P1–P6 según las recomendaciones de `docs/MODEL_REVIEW.md`.

- Actualizado `docs/DATA_MODEL.md` con autoridad monetaria independiente, roles temporales emisor-moneda, eventos de estado monetario, caras reutilizables, transiciones tipadas y denominaciones racionales exactas.
- Registradas D-012 a D-017 en `docs/DECISIONS.md`.
- D-001 a D-011 se mantienen, incluida D-008 sin cambios. D-002 conserva la identidad de pieza como pareja de caras.
- La aprobación consolida el modelo conceptual, no un esquema SQL ni autoriza el MVP o código de producto.
- **Fase 0 sigue abierta.** CELLAR continúa aparcado. No se modifica `main`, no se fusionan ramas ni se abre PR.
- Pendiente: validar el modelo actualizado con casos representativos y concretar vocabularios/reglas conceptuales antes de proponer el cierre de Fase 0.


## Validación del modelo consolidado — 26/11/2026

- Validado conceptualmente el modelo consolidado con Andorra, Cuba CUP/CUC, Ecuador sucre/USD, euro, XOF/XAF y peseta; matriz y razonamiento en `docs/MODEL_VALIDATION.md`.
- **Resultado:** cobertura satisfactoria de las relaciones principales. No se detectan contradicciones que justifiquen reabrir D-012–D-017.
- Casos confirmados: coexistencia CUP/CUC sin factor universal; sucre→USD con factor exacto; fraccionaria ecuatoriana denominada en USD; euro con responsabilidades diferentes para billetes/monedas; XOF y XAF separados; peseta→EUR con transición y eventos cronológicos diferenciados.
- Identificados tres huecos de especificación pendientes de decisión: P7 atribución de autoridad por emisión; P8 intención de circulación y unidad nominal de colección; P9 distinción entre uso oficial y uso de facto.
- No se modifican `DATA_MODEL.md` ni `DECISIONS.md` en esta iteración: P7–P9 son propuestas, no decisiones aprobadas. D-008 y D-012–D-017 permanecen intactas.
- Fase 0 continúa abierta; CELLAR aparcado; sin SQL, código de producto, cambios en `main`, merges ni PR.

**Siguiente paso exacto:** revisar y decidir P7–P9. Después, si se aprueban, incorporar solo los ajustes mínimos al modelo y definir vocabularios/reglas conceptuales. No iniciar el MVP.


## Aprobación y consolidación de P7–P9 — 26/11/2026

El usuario ha aprobado expresamente P7, P8 y P9, sin solicitar modificaciones. Se consolidan únicamente sus alcances aprobados:

- **D-018 / P7:** relación opcional y temporal entre emisión y autoridad monetaria, con roles `legal_issuer` y `operational_issuer`, procedencia y sin confundir autoridad con ceca/imprenta.
- **D-019 / P8:** `circulation_intent` opcional en emisión (`intended_for_circulation` / `not_intended_for_circulation`); ausencia significa desconocido. Se conservan unidades nominales originales no oficiales sin crear automáticamente monedas independientes; normalización solo con referencia documentada. Pruebas y patrones quedan como clasificación separada.
- **D-020 / P9:** calificador opcional `use_basis` en `issuer_currency` (`official` / `de_facto`), sin inferir curso legal ni competencia de emisión.

### Documentación consolidada
- Actualizados `docs/DATA_MODEL.md`, `docs/DECISIONS.md`, `docs/MODEL_VALIDATION.md`, `docs/BACKLOG.md` y este `docs/STATE.md`.
- D-008 y D-012–D-017 permanecen intactas; no se reabren.
- No se ha escrito SQL ni código de producto, no se ha modificado `main`, ni se ha fusionado o abierto una PR.
- Fase 0 permanece abierta; CELLAR sigue aparcado; el MVP continúa bloqueado.

### Siguiente paso exacto
Definir vocabularios controlados y reglas conceptuales de validación del modelo ampliado, y volver a contrastar los seis casos con foco en P7–P9. Después continuar las tareas restantes de Fase 0. No iniciar SQL, código de producto ni MVP.
