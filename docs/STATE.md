# Estado del proyecto

**Fase:** 0 — descubrimiento, sin código de producto.
**Criterio de reutilización:** solo fuentes con derechos de uso claros y compatibles; no se solicitarán permisos particulares.
**Actualizado:** 2026-11-25
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
