# Estado del proyecto

**Fase:** 0 — descubrimiento, sin código de producto.  
**Actualizado:** 2026-11-25  
**Rama de documentación:** `docs/phase-0-project-context`  
**Pull request:** [#1 — documentación inicial de Fase 0](https://github.com/anonymit-project/album-numismatico/pull/1) (abierto, borrador; no fusionado)

## Objetivo de la iteración

Investigar fuentes de catálogo e imágenes, licencias, APIs, cuotas y automatización con documentación oficial; actualizar la documentación sin iniciar el MVP.

## Hecho

- Revisados `AGENTS.md`, `STATE.md`, `PRD.md`, `DECISIONS.md`, `DATA_MODEL.md`, `BACKLOG.md`, `MOCKUPS.md` y `CATALOG_SOURCES.md`.
- Verificado GitHub: PR #1 sigue abierto y en borrador; rama de trabajo 12 commits por delante de `main`, 0 por detrás. `main` no se ha modificado.
- Comparadas Numista, Wikidata, Wikimedia Commons, BCE/Comisión Europea, Banco de España, ISO 4217/3166 y Natural Earth.
- Actualizado `docs/CATALOG_SOURCES.md` con matriz comparativa, enlaces oficiales, derechos, cuotas, riesgos, estrategia de ingesta y pendientes.
- Confirmado que Wikidata publica datos estructurados bajo CC0 y ofrece dumps semanales e incrementales; su SPARQL público tiene límites operativos sujetos a cambios.
- Confirmado que Commons requiere revisar licencia y autoría archivo por archivo y que Wikimedia introdujo límites de API en 2026.
- Confirmadas restricciones de reproducción de imágenes de billetes euro y pesetas en España; las caras nacionales de monedas euro tienen derechos del emisor y la cara común pertenece a la UE.
- Confirmado que ISO permite uso gratuito de los códigos, pero el servicio de listas preparadas y actualizadas automáticamente puede ser de pago.
- Identificado Natural Earth como fuente cartográfica en dominio público.

## Hallazgo crítico: Numista

La cuota gratuita actual es de 2.000 peticiones/mes y excluye búsqueda por imagen. Los términos oficiales prohíben la extracción sistemática para reproducir el catálogo, la redistribución masiva y el uso de datos almacenados para operar un servicio público. La excepción de almacenamiento para «Personal Project» se define como privado, no comercial y no disponible al público general; no está claro que cubra una PWA alojada en internet para 2–3 usuarios aunque requiera autenticación. Los metadatos de endpoints específicos pueden cachearse hasta 7 días; el resto de datos no se puede persistir salvo que aplique la excepción estricta. El plan de pago no encaja con el objetivo de 0 € (100 € de activación y mínimo 100 €/mes, sin IVA).

**Resultado provisional:** no usar Numista como semilla ni catálogo maestro. Solicitar confirmación escrita antes de integrar datos persistentes o mostrar resultados a los otros usuarios.

## Estado del producto

No existe todavía una aplicación implementada. Los mockups son exploratorios y contienen datos ilustrativos, no un catálogo real. La investigación no autoriza a importar ni redistribuir imágenes.

## Decisiones consolidadas

Se mantienen D-001 a D-007. Esta iteración no introduce decisiones de producto nuevas: las fuentes recomendadas son propuestas sujetas a validación y a pruebas de cobertura.

## Pendiente / bloqueos

1. Obtener respuesta escrita de Numista sobre el uso exacto previsto.
2. Probar cobertura y calidad con muestras reales de España (pesetas y euros, incluidas conmemorativas), Andorra, Cuba CUP/CUC, Ecuador, XOF/XAF y emisores históricos.
3. Identificar datasets numismáticos especializados con licencia explícita compatible; aún no se ha confirmado uno que cubra el alcance.
4. Comprobar opciones oficiales de automatización del Diario Oficial de la UE y autoridades emisoras.
5. Verificar imágenes concretas y documentar derechos de reproducción, especialmente billetes euro y pesetas.
6. Completar validación del modelo con casos históricos y supranacionales.
7. Verificar cuotas y condiciones actuales de backend, hosting, almacenamiento, FX e identificación por foto.
8. Resolver mapa de microestados, territorios y estados desaparecidos, valoración sin cotización, conservación y moderación.
9. Validar mockups, stack y diseño con el usuario y su amigo.
10. Obtener aprobación expresa para cerrar Fase 0.

## Siguiente paso exacto

Continuar la investigación con una prueba de cobertura basada en un conjunto de piezas reales y localizar datasets especializados abiertos con licencia compatible. En paralelo, solicitar aclaración escrita a Numista. No iniciar implementación del MVP hasta la aprobación expresa del usuario.

## Reglas para retomar

Leer, en este orden: `AGENTS.md`, este archivo, `docs/PRD.md`, `docs/DECISIONS.md`, `docs/DATA_MODEL.md`, `docs/BACKLOG.md` y `docs/CATALOG_SOURCES.md`. El repositorio es la fuente de verdad; si el chat contradice estos documentos, identificar la discrepancia y actualizar la documentación con el usuario.
