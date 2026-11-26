# Modelo de datos conceptual

**Estado:** modelo conceptual actualizado y aprobado en Fase 0 (26/11/2026). No constituye todavía un esquema SQL ni autoriza el inicio del MVP.

## Principios
1. Separar emisor político/legal, autoridad monetaria, moneda, diseño visual, emisión y posesión.
2. Modelar relaciones y hechos con vigencia temporal cuando su significado pueda cambiar.
3. No confundir uso de moneda, competencia legal de emisión, autoridad monetaria ni fabricación física.
4. No duplicar fichas visuales por año o diferencias técnicas invisibles.
5. Conservar denominación original y valor facial exacto normalizado cuando exista evidencia suficiente.
6. Conservar procedencia, licencia y estado de verificación. D-008 prevalece: no incorporar materiales de reutilización dudosa.
7. Los cambios de catálogo no deben romper referencias de colecciones.
8. La colección y sus preferencias pertenecen a un usuario.

## Entidades y relaciones

### Emisor (`issuer`)
País, territorio, estado histórico, entidad no reconocida o unión monetaria que actúa como emisor de una pieza/emisión. Incluye nombre y alias, tipo, códigos, vigencia histórica, continente y coordenadas de referencia. No todos los emisores equivalen a países soberanos actuales. El emisor de una pieza identifica la entidad política/legal a la que se atribuye; no se sustituye por el banco central, autoridad monetaria, ceca o imprenta.

### Autoridad monetaria (`monetary_authority`)
Institución responsable de funciones monetarias: política monetaria, banco central o autoridad/emisor de billetes. Incluye nombre, tipo institucional, jurisdicción, fechas y referencias. Se relaciona temporalmente con monedas mediante `monetary_authority_currency`, con roles controlados como `monetary_policy`, `banknote_issuer` o `currency_authority`. Una moneda puede tener distintas autoridades o funciones compartidas a lo largo del tiempo. No inferir una autoridad única para todas las formas de emisión. Cecas e imprentas no son autoridades por fabricar piezas.

### Moneda (`currency`)
Unidad monetaria con nombre, código ISO 4217 si existe, símbolo, unidad principal y subunidad cuando estén documentadas. Los estados legales no se reducen a un único estado global: se registran como hechos temporales en `currency_status_event`. Conservar códigos históricos cuando proceda.

### Uso y roles de moneda por emisor (`issuer_currency`)
Relación temporal muchos-a-muchos entre emisor y moneda. Sustituye el booleano ambiguo `issues_own` por uno o varios roles tipados, cada uno con periodo y procedencia:
- `uses`: utiliza/adopta la moneda.
- `legally_issues`: tiene competencia legal para emitir moneda o piezas denominadas en ella.
- `has_authorized_coinage`: tiene autorización específica para emitir moneda propia dentro de una moneda compartida.

Los roles pueden coexistir si están documentados. No inferir `legally_issues` de `uses`. La relación incorpora el calificador opcional `use_basis`: `official` (uso oficialmente adoptado) o `de_facto` (uso de facto). Se registra solo cuando la fuente permita distinguirlo; su ausencia significa desconocido, no uso de facto. Este calificador no determina por sí solo curso legal ni competencia de emisión. Acuñación/impresión física (`mints`, `prints`) son relaciones de producción con emisión/pieza y ceca/imprenta, fuera de esta relación. La membresía en una unión monetaria es una relación institucional separada y no se deduce del uso de su moneda.

### Hechos de estado y cronología (`currency_status_event`)
Eventos legales/económicos fechados asociados al objeto afectado (moneda, relación emisor-moneda o emisión) y, cuando corresponda, jurisdicción. Tipos iniciales:
- `introduced`: introducción/adopción.
- `entered_circulation`: comienzo de circulación.
- `legal_tender_started`: inicio de curso legal.
- `legal_tender_ended`: fin de curso legal.
- `withdrawn_from_circulation`: retirada de circulación.
- `exchange_period_ended`: fin del canje.
- `demonetized`: desmonetización.

Cada evento incluye fecha/intervalo si la fuente lo permite, ámbito, procedencia y precisión conocida. No todos los eventos aplican a todos los objetos y no se inventan fechas. Un estado mostrado podrá derivarse de estos hechos o ser etiqueta descriptiva, pero no será la verdad primaria de un único `currency.status`. «Conmemorativa» y «no destinada a circulación» son características de emisión/pieza, no estados legales de moneda.

### Transiciones entre monedas (`currency_transition`)
Relación dirigida entre moneda origen y destino, con tipo controlado:
- `replacement`: sustitución de una unidad monetaria por otra.
- `redenomination`: cambio de escala/unidad definido legalmente.

Incluye fecha/periodo y factor exacto opcional (unidades destino por unidad origen), fuente y observaciones. No asumir que toda sustitución tiene factor. La coexistencia ordinaria se representa con periodos/eventos de uso y estado, no como transición. Registrar circulación paralela solo si existe régimen transitorio específico documentado.

### Cara/diseño lateral reutilizable (`design_side`)
Componente visual reutilizable de una cara: tipo (`obverse`, `reverse` u otra cara justificada), descripción, referencias de imagen y procedencia. Puede asociarse a varios diseños. Su reutilización conceptual no autoriza la reutilización de imágenes: aplicar D-008 y registrar licencia por imagen.

### Diseño de catálogo (`catalog_design`)
Unidad visual del álbum: tipo (moneda/billete), moneda, emisor principal y referencias a cara de anverso y reverso en `design_side`. La identidad visual base sigue siendo la combinación concreta de ambas caras, conforme a D-002. Compartir una cara no fusiona diseños ni crea una ficha coleccionable por cara. Puede existir sin imagen, con placeholder.

### Emisión (`catalog_issue`)
Concreta un diseño para un emisor y periodo/año, serie, tirada u otros datos necesarios. El año se registra aquí o en el ejemplar según granularidad de la fuente; no crea automáticamente un diseño distinto. Metal/diámetro y otras diferencias técnicas se almacenan como atributos de emisión cuando sean útiles. Solo se separan diseños cuando el cambio visual lo justifique o el usuario necesite distinguirlo. Puede ser ámbito de eventos de estado específicos.

### Atribución de autoridad a una emisión (`catalog_issue_monetary_authority`)

Relación opcional y temporal entre una emisión concreta (`catalog_issue`) y una autoridad monetaria (`monetary_authority`), con rol controlado y procedencia. Roles iniciales:
- `legal_issuer`: institución con competencia o responsabilidad legal de emisión para esa emisión.
- `operational_issuer`: institución que ejecuta la emisión o la puesta en circulación.

Puede haber varias autoridades/roles para una emisión. Fechas y procedencia deben respaldar cada atribución. No exigir esta relación cuando no aporte precisión o no exista evidencia. La ceca o imprenta se registra como productor físico, nunca como autoridad por el mero hecho de fabricar la pieza.

### Intención de circulación de la emisión

`catalog_issue` puede incluir el atributo opcional y controlado `circulation_intent`, con valores iniciales:
- `intended_for_circulation`.
- `not_intended_for_circulation`.

La ausencia del atributo representa desconocimiento. Expresa la intención/condición de la emisión, no un hecho legal de circulación: los eventos reales de curso legal, circulación, retirada y canje siguen en `currency_status_event`. La clasificación numismática de pruebas, patrones u otras clases debe mantenerse separada; no se deduce automáticamente de la intención.

La denominación y unidad nominal originales de una pieza se conservan aunque no correspondan a una moneda oficial independiente (por ejemplo, diners en piezas andorranas de colección). No crear una entidad `currency` por la mera aparición de esa unidad nominal. La normalización racional solo se realiza si existe una unidad de referencia y una equivalencia documentadas; de lo contrario, se conserva el texto original sin conversión.

### Denominación y valor facial
Conservar la denominación original. Cuando se pueda normalizar con evidencia suficiente, almacenar valor facial exacto como racional mediante numerador y denominador enteros (`face_value_numerator`, `face_value_denominator`) respecto de la unidad principal de la moneda. No usar coma flotante. Ejemplos: 1 USD = 1/1 USD; 50 centavos USD = 50/100 USD; 1 céntimo EUR = 1/100 EUR. Puede almacenarse etiqueta de unidad/subunidad para presentación. Las subunidades no son monedas independientes salvo que tengan existencia monetaria/legal propia. Para sistemas históricos no decimales se conserva el texto y solo se normaliza si la equivalencia está documentada.

### Imágenes (`catalog_image`)
Asociadas a `design_side` o, cuando corresponda, a emisión. Incluyen URL/almacenamiento, autor, fuente, licencia, atribución, restricciones de uso y fecha de verificación. No reutilizar imágenes sin permiso compatible. Eliminar EXIF/GPS de fotos de usuario. D-008 se mantiene íntegramente.

### Posesión (`user_collection_entry`)
Usuario, diseño/emisión, cantidad, año concreto si aplica, conservación, adquisición, notas, ubicación física, foto propia y valor estimado opcional. Duplicados pueden derivarse de cantidad > 1, con posibilidad de marcar unidades disponibles para intercambio más adelante.

### Wishlist (`wishlist_entry`)
Usuario, pieza, prioridad y nota.

### Perfil y preferencias (`user_profile` / `user_preferences`)
Idioma, tema y preferencias de interfaz. Incluir filtros del álbum: emisor/país, tipo, orden y filtros activos. Persistir en backend por usuario para sincronizar entre dispositivos; caché local como optimización, no como fuente única.

### Contribuciones e identificación (fases posteriores)
Propuestas de alta/corrección con estado y moderador; sesiones de identificación con candidatos y confirmación. No forman parte del MVP inicial.

## Reglas de integridad
- Cada emisión apunta a diseño, moneda y emisor válidos.
- Roles emisor-moneda, calificador opcional `use_basis`, relaciones autoridad-moneda y atribuciones autoridad-emisión tienen vigencia y procedencia; advertir si las fechas no encajan.
- `use_basis=de_facto` no implica curso legal, adopción oficial ni competencia de emisión.
- La atribución autoridad-emisión distingue `legal_issuer` de `operational_issuer`; no sustituye la relación de producción física.
- `circulation_intent` expresa intención de la emisión y no sustituye eventos jurídicos o hechos reales de circulación.
- Las unidades nominales no oficiales se conservan como denominación original y no generan automáticamente entidades `currency`; normalizar solo con referencia acreditada.
- `uses` no implica `legally_issues`; la autoridad monetaria no sustituye al emisor de la pieza.
- Eventos de estado indican objeto/ámbito; no extrapolar fechas a emisiones o jurisdicciones sin evidencia.
- Una transición es dirigida y tipada; el factor, si existe, es exacto y su orientación está documentada.
- Valor facial normalizado usa racionales exactos; conservar siempre el texto original.
- La identidad visual no deriva solo de denominación/año ni de compartir una cara.
- Fusiones/reemplazos conservan alias o redirecciones para no invalidar posesiones.
- RLS/controles: cada usuario solo lee y modifica su inventario y preferencias privadas; el catálogo es de lectura general.
- Compartición futura explícita y de solo lectura.

## Vocabularios y reglas conceptuales de validación

La especificación inicial de valores controlados, precisión temporal, procedencia/evidencia, coherencia entre entidades y severidades de validación se encuentra en [VALIDATION_RULES.md](VALIDATION_RULES.md). Debe leerse junto con este modelo. No introduce SQL ni altera las decisiones D-001–D-020.

## Pendiente para diseño físico y validación de Fase 0
- Definir esquema SQL y constraints solo tras cerrar el resto de Fase 0; este documento es conceptual.
- Determinar granularidad de emisión/año en series con múltiples años y diseños idénticos.
- Representar variantes que el usuario quiera separar aunque sean visualmente casi iguales.
- Traducir los vocabularios y reglas conceptuales de VALIDATION_RULES.md a constraints/tests únicamente tras aprobar el cierre de Fase 0 y autorizar esa implementación.
- Ordenar denominaciones históricas no decimales o no normalizadas.
- Escala de conservación y tratamiento de monedas sin cotización.
- Modelo de almacenamiento/licencia de imágenes.
- Revisar constraints tras contrastar fuentes y preparar casos de prueba.
