# Revisión de propuestas del modelo conceptual P1–P6

**Fecha:** 2026-11-26  
**Rama:** `research/source-automation-2026-11`  
**Estado:** análisis y recomendaciones; ninguna propuesta aprobada.  
**Alcance:** validación conceptual con Andorra, Cuba CUP/CUC, Ecuador, euro, XOF/XAF, peseta y emisores/monedas históricos. No define SQL ni autoriza implementación.

## Criterio

Se distingue entre: (1) hechos que el modelo debe poder representar; (2) datos que las fuentes disponibles permiten poblar; y (3) decisiones de diseño pendientes. Que una fuente no aporte datos completos no justifica simplificar incorrectamente el dominio. A la inversa, no se debe crear una abstracción genérica para cada excepción imaginable.

## Resumen ejecutivo

| Propuesta | Recomendación | Prioridad | Complejidad |
|---|---|---:|---:|
| P1 Autoridad monetaria independiente | Aprobar con alcance acotado | Alta | Media |
| P2 Roles emisor–moneda | Aprobar, sustituyendo el booleano actual por roles tipados | Alta | Media |
| P3 Estados y fechas monetarias | Aprobar el modelo basado en eventos/fechas; evitar un estado único | Alta | Media-alta |
| P4 Caras compartidas | Aprobar normalización mínima de caras, preservando identidad del diseño completo | Media | Media |
| P5 Transiciones monetarias | Aprobar relaciones tipadas; coexistencia no debe confundirse con sustitución | Alta | Media |
| P6 Denominaciones estructuradas | Aprobar estructura numérica exacta más texto original | Alta | Baja-media |

Estas son recomendaciones técnicas, no decisiones del proyecto. Requieren aprobación individual del usuario.

## P1 — Autoridad monetaria independiente

**Problema.** El modelo actual usa `issuer` para países, territorios, estados históricos y uniones monetarias, y deja en `issuer_currency` un booleano `issues_own`. Esto mezcla quién utiliza una moneda, quién tiene competencia legal para emitirla y qué institución administra la política monetaria. En XOF/XAF la autoridad supranacional no es equivalente a cada estado usuario; en el euro, además, la emisión de billetes y la emisión de monedas tienen marcos institucionales distintos. Andorra añade el caso de un emisor político que utiliza el euro y tiene derecho a emitir moneda euro bajo acuerdo.

**Alternativas.**
1. Añadir bancos centrales y autoridades como tipos adicionales de `issuer`. Es el cambio de menor tamaño, pero convierte una entidad llamada emisor en una taxonomía heterogénea y no resuelve por sí solo sus competencias.
2. Crear `monetary_authority` como entidad independiente y relaciones explícitas con moneda y/o territorio. Es más claro, pero no debe asumir que una autoridad única controla todas las formas de emisión.
3. Mantener solo texto libre en moneda/emisión. Es sencillo, pero no permite consultar ni validar autoridades y confunde institución con país.

**Recomendación mínima.** Separar la autoridad monetaria como entidad institucional independiente, relacionada con la moneda mediante una relación temporal y tipada (por ejemplo, autoridad responsable, banco emisor o autoridad de política monetaria). No convertirla en sustituto de `issuer`: el emisor de una pieza concreta debe seguir identificando al estado/entidad que la pone en circulación o figura como emisor legal. La ceca y la imprenta son productores físicos, no autoridades monetarias, y quedan fuera de esta propuesta salvo que el catálogo necesite atribuirlos.

**Cobertura.** XOF y XAF quedan diferenciados con BCEAO y BEAC respectivamente; los ocho estados UMOA y seis estados CEMAC siguen siendo usuarios/miembros, no autoridades. Euro permite distinguir Estados emisores de monedas, Eurosistema/BCE y bancos centrales nacionales sin atribuir erróneamente toda emisión de moneda a la BCE. Andorra se representa como emisor de sus euros y usuario del euro; Ecuador como usuario de USD y autoridad nacional para su moneda fraccionaria histórica/nacional si se documenta así. Cuba y peseta no requieren autoridad supranacional, aunque pueden vincularse sus bancos centrales nacionales cuando haya evidencia.

**Consecuencias y complejidad.** Añade una entidad y una relación consultable; exige fechas y procedencia. Complejidad media. No implica poblar de inmediato todas las autoridades históricas. Fuentes institucionales actuales ofrecen soporte razonable para euro y CFA; para periodos históricos y Cuba la cobertura es desigual y debe quedar explícitamente incompleta.

## P2 — Roles de las relaciones emisor–moneda

**Problema.** `issuer_currency.issues_own` es un booleano insuficiente. No expresa si el emisor usa una moneda extranjera, tiene competencia legal para emitirla, es miembro de una unión monetaria o acuña/fabrica físicamente las piezas. Además, acuñación/impresión no equivale necesariamente a emisión legal.

**Alternativas.**
1. Mantener `issues_own`: simple, pero insuficiente para Andorra, Ecuador, euro y CFA.
2. Añadir varios booleanos: fácil al principio, pero proliferan combinaciones contradictorias y semántica ambigua.
3. Relación temporal con uno o varios roles tipados: algo más compleja, pero extensible y consultable.

**Recomendación mínima.** Sustituir `issues_own` por roles explícitos en una relación temporal emisor–moneda, permitiendo más de uno cuando corresponda. Conjunto inicial sugerido: `uses` (utiliza/acepta como moneda), `legally_issues` (emite legalmente), `has_authorized_coinage` (tiene derecho o autorización para emitir moneda propia de esa moneda compartida). No incluir `mints` ni `prints` como rol emisor–moneda: son relaciones de producción entre emisión/pieza y ceca/imprenta. La pertenencia a una unión monetaria debe modelarse respecto de la unión/organización, no inferirse automáticamente de usar una moneda; si se necesita, será una relación de membresía separada.

**Cobertura.**
- Andorra: `uses` peseta/franco históricamente y euro actualmente; `has_authorized_coinage` para su acuerdo de acuñación de euros; no confundirlo con fabricar físicamente cada pieza.
- Ecuador: `uses` sucre y posteriormente USD; el centavo ecuatoriano no crea por ello una moneda independiente del USD. La atribución de emisión/acuñación debe registrarse con precisión y fuente.
- Euro: los estados miembros usan euro; los estados habilitados emiten monedas euro nacionales. No atribuir a cada estado la emisión de billetes euro.
- XOF/XAF: los estados utilizan la moneda regional; BCEAO/BEAC se representan como autoridades/emisores legales mediante P1, no como estados usuarios.
- Cuba y peseta: roles de uso y emisión nacional cubren el caso, con fechas históricas.

**Consecuencias y complejidad.** Mejora la integridad y evita booleanos ambiguos. Complejidad media: se necesitan vocabulario controlado, fechas y reglas de validación. La fuente disponible permite poblar algunos roles, no necesariamente todos los periodos.

## P3 — Estados monetarios y fechas

**Problema.** `currency.status` y fechas genéricas de vigencia no bastan. «Emitida», «puesta en circulación», «curso legal», «retirada», «canjeable» y «desmonetizada» son hechos diferentes. Además, una moneda puede coexistir con otra, seguir siendo canjeable tras perder curso legal o tener emisiones conmemorativas no destinadas a circulación. El estado puede variar por territorio y por denominación/emisión.

**Alternativas.**
1. Un único estado y dos fechas en `currency`: simple, pero pierde cronología y matices.
2. Añadir fechas independientes a moneda, emisor-moneda y emisión: mejor, aunque puede generar campos nulos y ambigüedad sobre el ámbito de cada fecha.
3. Registrar eventos/intervalos tipados y derivar el estado actual o histórico: más robusto, algo más complejo.

**Recomendación mínima.** Separar el ciclo de vida de la moneda del ciclo de vida de cada emisión/denominación. Registrar, cuando la fuente lo indique, fechas tipadas de introducción, inicio de circulación, retirada de curso legal, fin de canje y desmonetización, indicando el ámbito territorial y el objeto afectado. No guardar un `status` universal como verdad primaria: puede mantenerse un estado descriptivo derivado o una etiqueta editorial, pero los hechos fechados son la fuente de verdad. Distinguir también la condición «conmemorativa» y «no destinada a circulación» del estado legal de la moneda.

**Cobertura.** CUC/CUP exige coexistencia y retirada/canje; las pesetas y el sucre requieren distinguir sustitución, retirada y posible canje; CFA ofrece familias vigentes y demonetizadas con fechas diferentes; euro necesita distinguir monedas regulares y conmemorativas, y emisión de puesta en circulación. Andorra comparte el ciclo del euro pero no necesariamente las mismas competencias de emisión. Las fuentes BEAC/BCEAO muestran que fechas de demonetización y fin de canje no coinciden.

**Consecuencias y complejidad.** Es la propuesta con mayor impacto transversal. Complejidad media-alta por ámbito, cronología y evidencia incompleta. La recomendación no exige inventar fechas ausentes: se permiten hechos desconocidos y fuentes por dato. Evitar modelar cada estado legal como una moneda diferente.

## P4 — Caras compartidas

**Problema.** El diseño actual identifica una pieza por el conjunto visual anverso/reverso. En el euro, una cara común se repite en monedas de distintos países y años; duplicar esa cara en cada diseño genera redundancia y dificulta corregir o actualizar un elemento común.

**Alternativas.**
1. Duplicar el anverso/reverso en cada `catalog_design`: modelo simple, redundancia tolerable para catálogo pequeño.
2. Crear `design_side` reutilizable y asociar dos caras a cada diseño: normaliza componentes compartidos sin cambiar la identidad de la pieza.
3. Modelar un sistema genérico de componentes, capas, variantes y composición gráfica: excesivo para el alcance actual.

**Recomendación mínima.** Introducir una entidad reutilizable de cara/diseño lateral (`design_side`) con tipo de cara, descripción, referencias de imagen y procedencia; `catalog_design` sigue siendo la combinación concreta de anverso y reverso. Una cara puede compartirse entre varios diseños, pero la identidad de álbum continúa siendo el par de caras, conforme a D-002. No dividir una pieza en dos fichas coleccionables ni inferir que dos piezas son idénticas por compartir una cara.

**Cobertura.** Resuelve la cara común del euro por denominación/periodo y conserva las caras nacionales diferentes; funciona también para diseños de billetes con elementos comunes si aparece un caso real. Peseta, Cuba, Ecuador y CFA pueden usar caras independientes sin coste conceptual adicional. Andorra puede reutilizar la cara común del euro. No depende de que las imágenes se puedan reutilizar: la entidad puede existir con placeholder y metadatos.

**Consecuencias y complejidad.** Añade una entidad y asociaciones, complejidad media. Beneficio real en euro; valor menor en otros casos. No debe expandirse a un editor de composición visual.

## P5 — Transiciones monetarias

**Problema.** El modelo menciona sustitución/redenominación, pero no distingue relaciones diferentes. Peseta→euro y sucre→USD son sustituciones; CUP/CUC coexistieron y tuvieron cronologías distintas; una redenominación implica una relación cuantitativa que no siempre existe en una sustitución. Una relación genérica `replaced_by` pierde coexistencia y conversión.

**Alternativas.**
1. Campo `replaced_by` en `currency`: simple, pero solo permite una sustitución lineal.
2. Tabla de transición tipada entre monedas, con fechas y factor opcional: representa casos diversos sin convertir la coexistencia en una transición artificial.
3. Grafo general de equivalencias y operaciones monetarias: demasiado abstracto para el catálogo.

**Recomendación mínima.** Añadir una relación `currency_transition` entre moneda origen y destino, con tipo controlado (`replacement`, `redenomination`, eventualmente `parallel_circulation` solo si se decide registrar explícitamente coexistencia), fecha/periodo y factor exacto opcional con orientación inequívoca. La coexistencia ordinaria debe derivarse principalmente de los intervalos de uso de P2/P3; no duplicarla como transición salvo que una norma establezca un régimen transitorio relevante. No asumir que una sustitución tiene factor de conversión.

**Cobertura.** Peseta→euro: sustitución con factor fijo documentado. Sucre→USD: sustitución, con factor oficial si se incorpora y verifica. CUP/CUC: no forzar una relación de conversión o sustitución simple; registrar su coexistencia y los respectivos eventos de retirada. XOF/XAF no son transiciones entre sí: son monedas distintas. Andorra refleja cambios de moneda utilizada sin afirmar que acuñara pesetas/francos propios. Ecuador fraccionario se resuelve con P6, no creando una moneda paralela.

**Consecuencias y complejidad.** Añade relación y validaciones temporales; complejidad media. Factores y fechas siempre opcionales y trazados a fuente. Evita automatizar conversiones cuando la fuente no las documente.

## P6 — Denominaciones estructuradas

**Problema.** Guardar denominación como texto o número decimal ambiguo no permite ordenar y comparar con fiabilidad, y puede confundir la unidad monetaria con la subunidad o con una denominación histórica. El caso crítico es el centavo ecuatoriano: es una fracción del USD, no una moneda independiente. También existen fracciones no decimales y denominaciones cuya escritura original debe conservarse.

**Alternativas.**
1. Texto libre (`"50 centavos"`): fiel a la fuente, pero no ordenable ni calculable con seguridad.
2. Número decimal más etiqueta: suficiente para muchos casos modernos, pero ambiguo en monedas históricas/no decimales y sujeto a redondeos.
3. Valor racional exacto (numerador/denominador) expresado en la unidad de cuenta de la moneda, más etiqueta original y, cuando proceda, unidad/subunidad: algo más estructurado, sin inventar monedas adicionales.

**Recomendación mínima.** Mantener el texto original de denominación y añadir un valor facial exacto normalizado como racional (numerador y denominador) respecto de la unidad principal de la moneda. Añadir etiqueta de unidad/subunidad cuando ayude a presentar el valor; no convertir cada subunidad en una entidad `currency`. Evitar coma flotante. Para casos modernos decimales puede usarse denominador 1 en unidad menor normalizada o una representación decimal exacta, pero la convención debe ser única y documentada. La unidad de cuenta y sus fracciones deben ser atributos de la moneda, no monedas separadas salvo que tengan existencia monetaria/legal independiente.

**Cobertura.** USD: 1 centavo = 1/100 USD, incluido el centavo ecuatoriano; no se crea una moneda «centavo». Euro: 1 céntimo = 1/100 EUR. XOF/XAF: denominaciones enteras de francos CFA. Peseta, CUP/CUC y sucre: denominaciones nominales y fracciones documentadas; si una fuente solo aporta texto, se conserva sin inventar normalización. Billetes y monedas comparten el mismo valor facial estructurado.

**Consecuencias y complejidad.** Mejora ordenación, filtros y futuras sumas; complejidad baja-media. Requiere definir cómo ordenar denominaciones históricas sin conversión entre monedas y cómo tratar valores desconocidos. No implica valoración de mercado.

## Cobertura cruzada y dependencias

| Caso | P1 autoridad | P2 roles | P3 ciclo legal | P4 caras | P5 transición | P6 valor facial |
|---|---|---|---|---|---|---|
| Andorra | autoridad euro separada del emisor estatal | uso + derecho de acuñación | ciclo del euro y emisiones propias | cara común euro | cambios de moneda usada | EUR y céntimos |
| Cuba CUP/CUC | bancos centrales según periodo/fuente | uso/emisión diferenciados | coexistencia, retirada y canje | no imprescindible | no forzar conversión simple | denominaciones CUP/CUC |
| Ecuador sucre/USD | autoridad nacional vs USD | uso USD y emisión nacional diferenciados | sustitución y retirada | no imprescindible | sucre→USD | centavo como 1/100 USD |
| Euro | BCE/Eurosistema vs estados emisores de monedas | uso y emisión de monedas no equivalen a billetes | circulación y emisiones conmemorativas | cara común reutilizable | no aplica entre estados | EUR/céntimos |
| XOF/XAF | BCEAO y BEAC separados | autoridad emisora vs estados usuarios | gamas vigentes/demonetizadas/canje | opcional | nunca fusionar XOF/XAF | valores CFA |
| Peseta | autoridad nacional histórica | uso/emisión | retirada y canje | opcional | peseta→euro | pesetas y fracciones documentadas |

## Orden de implementación conceptual recomendado

Si se aprueban, definir primero P1 y P2 conjuntamente (separar actores y responsabilidades); después P3 y P5 (cronología y transiciones); P6 puede definirse en paralelo y es de bajo coste; P4 puede aprobarse como normalización limitada por el caso euro. No hay dependencia de CELLAR ni necesidad de escribir código.

## Decisiones que debe tomar el usuario

Aprobar o rechazar individualmente P1–P6. En particular:
- P1: entidad independiente `monetary_authority` o extensión tipada de `issuer`.
- P2: aceptar los tres roles mínimos propuestos y dejar membresía/producción fuera de `issuer_currency`.
- P3: aceptar fechas/eventos tipados como fuente de verdad en lugar de un estado único.
- P4: aceptar reutilización de caras manteniendo la identidad por pareja.
- P5: aceptar transiciones tipadas y tratar coexistencia mediante intervalos salvo excepción documentada.
- P6: aceptar racional exacto más etiqueta original como representación mínima.

Hasta recibir aprobación expresa, las seis propuestas permanecen pendientes y no modifican D-001–D-011, D-008 ni el modelo vigente.
