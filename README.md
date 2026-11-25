# Álbum numismático

Aplicación web progresiva (PWA) para catalogar monedas y billetes actuales e históricos y gestionar colecciones privadas con una experiencia visual de álbum de cromos.

> **Estado:** Fase 0 — descubrimiento y definición. No comenzar el desarrollo del producto hasta cerrar y aprobar esta fase.

## Objetivos

- Consultar un catálogo fiable de piezas, organizado por emisor, moneda y emisiones.
- Registrar posesiones, cantidades, años, duplicados y piezas buscadas.
- Ver lo que se tiene a color y lo que falta atenuado.
- Consultar progreso y estadísticas; más adelante, explorar colecciones en mapa.
- Importar y exportar inventarios.
- Sincronizar colecciones privadas entre dispositivos.

El catálogo crecerá progresivamente: no se promete exhaustividad mundial desde el MVP. La fiabilidad, trazabilidad y licencia de los datos e imágenes prevalecen sobre la amplitud.

## Alcance inicial acordado

MVP previsto para 2 usuarios: España (pesetas y euros, incluidas conmemorativas) y un conjunto pequeño de emisores adicionales; álbum visual, marcado de posesión/cantidad, importación Excel/CSV y estadísticas básicas. La app será PWA, móvil primero, con escritorio útil para importaciones. Presupuesto objetivo: 0 €.

## Estado actual

- Fase 0; aún no hay implementación funcional del producto.
- Mockups conceptuales revisados: Álbum, Mapa y Resumen.
- Requisitos y decisiones de producto se documentan en `docs/`.
- Fuentes, licencias, servicios gratuitos y modelo de datos siguen en investigación/validación.

## Cómo trabajar

1. Leer `AGENTS.md` y `docs/STATE.md` antes de cada tarea.
2. Tratar `docs/PRD.md` y `docs/DECISIONS.md` como requisitos y decisiones vigentes.
3. Trabajar incrementalmente en ramas; no modificar `main` directamente.
4. No introducir código de producto hasta que el usuario apruebe el cierre de Fase 0.
5. Verificar documentación oficial para precios, cuotas, APIs, versiones y licencias.
6. Al cerrar cada iteración, actualizar STATE, DECISIONS y BACKLOG.
7. **No dejar ningún chat sin un cierre accionable:** terminar siempre con una pregunta concreta para el usuario o con un prompt de relevo autosuficiente listo para el siguiente chat. Aplicar el detalle de `AGENTS.md`.

## Documentación

- [Política de trabajo](AGENTS.md)
- [Requisitos del producto (PRD)](docs/PRD.md)
- [Estado actual](docs/STATE.md)
- [Registro de decisiones](docs/DECISIONS.md)
- [Modelo de datos](docs/DATA_MODEL.md)
- [Fuentes y licencias del catálogo](docs/CATALOG_SOURCES.md)
- [Backlog](docs/BACKLOG.md)
- [Mockups y comportamiento UX](docs/MOCKUPS.md)
- [Privacidad y RGPD](docs/PRIVACY.md)
- [Historial de cambios](docs/CHANGELOG.md)

## Desarrollo

Todavía no hay stack ni comandos de desarrollo aprobados. Se decidirán tras la investigación de Fase 0 y quedarán reflejados aquí antes de implementar el MVP.
