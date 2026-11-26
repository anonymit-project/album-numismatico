# Mockups y comportamiento UX

## Estado

Se han revisado dos iteraciones conceptuales de la interfaz. Son prototipos de interacción, no una implementación ni un catálogo real. Las piezas, cifras y marcadores mostrados son datos ficticios.

## Navegación prevista

Pestañas principales exploratorias: Álbum, Mapa y Resumen. El producto completo podrá incorporar Buscar, Escáner, Importar/Exportar y Perfil/Ajustes.

## Álbum — requisitos confirmados

- Selector de país/emisor visible y fácil de localizar en la cabecera del álbum. La selección determina las piezas mostradas.
- Navegación conceptual: emisor → moneda → serie → piezas.
- Orden predeterminado por denominación (orden numérico/natural, no alfabético simple).
- Filtro de tipo: todas, monedas o billetes.
- Filtros de posesión: todas, las tengo, me faltan; posteriormente duplicados y wishlist.
- Los filtros y preferencias deben persistir por usuario y sincronizarse entre dispositivos; no pedir que se vuelvan a aplicar en cada visita.
- Piezas poseídas a color; piezas faltantes desaturadas/atenuadas.
- Control explícito «Lo tengo / Me falta» y cantidad visible cuando se posee más de una.
- Una pieza puede mostrarse con ilustración neutra si aún no hay imagen autorizada.

## Mapa

El prototipo con marcadores es únicamente demostrativo. La solución final debe estudiar países actuales, microestados, territorios dependientes, emisores históricos y uniones monetarias. No se ha decidido aún cómo representar estados desaparecidos ni cómo colorear progreso.

## Resumen

KPIs ilustrativos; las métricas definitivas dependerán del catálogo validado y de las reglas de completitud.

## Pendiente de validación

- Jerarquía visual y densidad de la página de álbum.
- Cómo presentar monedas comunes y monedas supranacionales.
- Selector de emisor cuando existan emisores históricos o territorios.
- Comportamiento en móvil y escritorio.
- Mapa final y leyenda.


## Prototipo visual interactivo reducido — 26/11/2026

Conforme a D-010, la siguiente entrega no es una simulación completa de la aplicación. Es una maqueta visual navegable para validar jerarquía, diseño, navegación y usabilidad.

### Recorrido que debe cubrir
Inicio/resumen → selector de emisor → moneda → serie → álbum → ficha de pieza.

### Interacciones que sí aportan valor
- Seleccionar emisor, moneda y serie.
- Cambiar entre «Lo tengo» y «Me falta».
- Ajustar una cantidad simple.
- Ver el progreso del álbum actualizarse.
- Buscar, filtrar y ordenar el conjunto de demostración.

### Elementos que no es necesario implementar
Alta y edición completas, importación/carga de ficheros, validaciones, procesos administrativos y simulación detallada de operaciones. No añadirlos por parecer funcionalidades del PRD: solo se incluirán si una prueba UX concreta los necesita.

### Criterios de diseño
- Móvil primero, cómodo con interacción táctil; escritorio también debe ser útil.
- Datos ficticios claramente reconocibles y placeholders neutros.
- La posesión se distingue visualmente; las piezas faltantes aparecen atenuadas.
- No usar imágenes monetarias de terceros sin derechos verificados (D-008).
- Sin persistencia: los cambios viven solo mientras la demo está abierta.


## Ampliación solicitada — mapamundi y billetes (26/11/2026)

- La navegación incluye una pestaña «Mapamundi» accesible en móvil y escritorio.
- El mapa de la demo destaca los emisores incluidos en los datos de muestra. Se usa Madagascar como ejemplo distante para que el usuario pueda valorar marcadores separados; no implica prioridad de catálogo ni una decisión sobre el alcance geográfico.
- Los billetes aparecen como una serie diferenciada dentro del flujo emisor → moneda → serie → álbum → ficha. Se emplean rectángulos neutros, no reproducciones monetarias.
- En esta iteración el mapa es esquemático, plano y no interactivo por país; el usuario debe validar si la representación es suficiente para la revisión UX.
