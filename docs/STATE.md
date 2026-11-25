# Estado del proyecto

**Fase:** 0 — descubrimiento, sin código de producto.
**Criterio de reutilización:** solo fuentes con derechos de uso claros y compatibles; no se solicitarán permisos particulares.
**Actualizado:** 2026-11-25
**Rama de trabajo:** `research/catalog-coverage-2026-11`
**Rama base:** `docs/phase-0-project-context`
**Pull request #1:** abierto y en borrador; no fusionado. Esta iteración aún no modifica el PR #1.

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

Completar una pasada acotada de fuentes estructuradas y automatización: comprobar los feeds/consultas del DOUE para monedas euro, documentar la estructura de las páginas BEAC/BCEAO y localizar una fuente primaria verificable para CUP/CUC. Mantener las imágenes en placeholder salvo licencia y reglas de reproducción inequívocas. No iniciar el MVP.

## Reglas para retomar

Leer, en este orden: `AGENTS.md`, este archivo, `docs/PRD.md`, `docs/DECISIONS.md`, `docs/DATA_MODEL.md`, `docs/BACKLOG.md` y `docs/CATALOG_SOURCES.md`. El repositorio es la fuente de verdad; si el chat contradice estos documentos, identificar la discrepancia y actualizar la documentación con el usuario.
