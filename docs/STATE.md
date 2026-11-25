# Estado del proyecto

**Fase:** 0 — descubrimiento, sin código de producto.
**Criterio de reutilización:** solo fuentes con derechos de uso claros y compatibles; no se solicitarán permisos particulares.
**Actualizado:** 2026-11-25
**Rama de trabajo:** `research/source-automation-2026-11`
**Rama base:** `docs/phase-0-project-context`
**Pull request #1:** [abierto y en borrador](https://github.com/anonymit-project/album-numismatico/pull/1), sin fusionar ni modificar.\n**Pull request #2:** [abierto y en borrador](https://github.com/anonymit-project/album-numismatico/pull/2), dirigido a la rama de documentación de la PR #1.

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
6. Sigue pendiente probar automatización concreta del DOUE/Comisión y autoridades emisoras, más allá de la localización de páginas y documentos.
7. Continúan pendientes las validaciones de modelo, mapa, conservación, valoración histórica, backend/hosting, privacidad de identificación por foto, mockups y aprobación de cierre de Fase 0.

## Siguiente paso exacto

La siguiente iteración debe probar una consulta SPARQL/REST o alerta RSS personalizada de EUR-Lex con un filtro real para «New national side of euro coins intended for circulation», confirmar los campos CDM/Formex y diseñar el importador de staging. Para BEAC/BCEAO, preparar una extracción controlada de texto desde el manifiesto de páginas, con detección de cambios y revisión humana. Cuba permanece sin ingesta automatizada ni imágenes. No iniciar el MVP.

## Reglas para retomar

Leer, en este orden: `AGENTS.md`, este archivo, `docs/PRD.md`, `docs/DECISIONS.md`, `docs/DATA_MODEL.md`, `docs/BACKLOG.md` y `docs/CATALOG_SOURCES.md`. El repositorio es la fuente de verdad; si el chat contradice estos documentos, identificar la discrepancia y actualizar la documentación con el usuario.


## Iteración de automatización y fuentes estructuradas (25/11/2026)

**Rama:** `research/source-automation-2026-11`, creada desde `research/catalog-coverage-2026-11`.

### Hecho
- Releída la documentación de Fase 0 y comprobado el estado de PR #1 y PR #2 (abiertos, draft, sin fusionar). PR #3 también sigue abierto y draft, pero es una rama documental paralela basada en PR #2.
- Verificada la infraestructura de EUR-Lex/CELLAR: servicio SOAP/XML con registro, REST, SPARQL, RSS/Atom y documentos Formex. Identificados ejemplos 2026 de avisos del DOUE para conmemorativas de 2 € y cambio de caras nacionales regulares.
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
1. No se ha ejecutado una consulta SPARQL ni configurado una alerta RSS personalizada; la automatización de euro está verificada a nivel de interfaz, no de prueba de concepto.
2. No se ha probado un parser en BEAC/BCEAO ni se ha auditado exhaustivamente cada PDF; la extracción propuesta es documental, no código ejecutado.
3. La Resolución 357/1994 del CUC se ha localizado en una copia secundaria; falta una copia oficial accesible. No tratarla como fuente de importación.
4. No se ha encontrado licencia abierta general para imágenes de BEAC/BCEAO/Cuba.
5. No hay un dataset moderno maestro de monedas y billetes.

### Siguiente paso exacto
Probar en un entorno de investigación una consulta SPARQL/REST de CELLAR o una alerta RSS personalizada para recuperar un conjunto pequeño de avisos de monedas euro y validar los campos de Formex. En paralelo, definir el manifiesto versionado de páginas BEAC/BCEAO (sin descargar imágenes). Mantener Cuba en estado manual/documental. No iniciar el MVP.
