# Estado del proyecto

**Fase:** 0 — descubrimiento, sin código de producto.  
**Actualizado:** 2026-11-25  
**Rama de documentación:** `docs/phase-0-project-context`

## Objetivo de la iteración

Consolidar en el repositorio el contexto del proyecto y las decisiones confirmadas en conversaciones y feedback de mockups.

## Hecho

- PRD existente revisado íntegramente.
- Política de trabajo incorporada en `AGENTS.md`; no existía un `AGENTS.md` en la raíz de `main`.
- README inicial redactado.
- Decisiones, modelo conceptual, backlog y notas UX documentados.
- Feedback del álbum incorporado: selector visible de emisor/país; orden por denominación; filtros de monedas/billetes; filtros persistentes por usuario y sincronizados entre dispositivos.
- Confirmada la creación de rama de trabajo; `main` no se ha modificado.

## Estado del producto

No existe todavía una aplicación implementada. Los mockups son exploratorios y contienen datos ilustrativos, no un catálogo real. La vista de mapa demostrada con marcadores no define aún el diseño cartográfico final.

## Decisiones consolidadas

- Catálogo mundial progresivo; MVP acotado.
- Piezas que se identifican visualmente por anverso y reverso. Diferencias de diámetro o composición no crean otra pieza automáticamente; sí puede distinguirse una variante cuando el cambio es visualmente relevante o el usuario lo necesita.
- Separar diseño/pieza visual, emisión y ejemplar/posesión. El año es atributo de emisión/ejemplar, no una ficha visual distinta por defecto.
- Colecciones independientes y privadas por defecto. Compartir será voluntario y de solo lectura; nadie modifica inventario ajeno.
- Álbum tipo cromos: posesiones a color, faltantes atenuados; selector explícito «Lo tengo / Me falta».
- Álbum: país/emisor seleccionable, orden por denominación y filtro por monedas/billetes. Preferencias guardadas por usuario para persistir entre sesiones y dispositivos.
- Aceptar fichas sin imagen de catálogo; usar ilustración/silueta provisional cuando no haya imagen autorizada.

## Pendiente / bloqueos

1. Investigación comparativa de fuentes de catálogo, cobertura, licencias, límites y automatización.
2. Verificar cuotas y condiciones actuales de backend, hosting, almacenamiento, FX e identificación por foto.
3. Validar modelo con casos reales: Andorra, Cuba/CUP-CUC, Ecuador, euro, CFA, peseta y emisores históricos.
4. Cerrar propuesta de mapa para microestados, territorios y estados desaparecidos.
5. Resolver valoración de monedas sin cotización, escala de conservación, política de imágenes y moderación.
6. Validar stack y diseño con el usuario y su amigo.

## Siguiente paso exacto

Completar el informe de Fase 0 sobre fuentes y licencias del catálogo con documentación oficial y fecha de consulta. No iniciar implementación del MVP hasta la aprobación expresa del usuario.

## Reglas para retomar

Leer, en este orden: `AGENTS.md`, este archivo, `docs/PRD.md`, `docs/DECISIONS.md`, `docs/DATA_MODEL.md`, `docs/BACKLOG.md` y `docs/CATALOG_SOURCES.md`. El repositorio es la fuente de verdad; si el chat contradice estos documentos, identificar la discrepancia y actualizar la documentación con el usuario.
