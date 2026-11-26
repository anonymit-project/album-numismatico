# Vocabularios controlados y reglas conceptuales de validación

**Fecha:** 2026-11-26  
**Rama:** `research/source-automation-2026-11`  
**Estado:** especificación conceptual propuesta para Fase 0; no modifica D-001–D-020 ni define SQL, código o restricciones físicas.

## 1. Objetivo y principios

Este documento concreta los vocabularios iniciales y las reglas de coherencia del modelo descrito en `DATA_MODEL.md`. Los vocabularios son cerrados para los campos tipados indicados, pero ampliables mediante revisión documental: no se deben introducir valores libres que parezcan equivalentes a valores controlados.

Principios:

1. **Desconocido no significa falso.** La ausencia de un atributo opcional significa desconocimiento/no documentado, no el valor contrario.
2. **Validez, evidencia y completitud son dimensiones distintas.** Un dato puede ser válido pero estar insuficientemente documentado; la falta de evidencia suele producir advertencia, no error estructural.
3. **Los hechos son temporales y contextualizados.** Toda afirmación histórica debe identificar qué entidad/relación afecta, en qué ámbito y durante qué periodo, cuando esos datos sean conocidos.
4. **No inferir competencias.** Uso, curso legal, emisión legal, autoridad monetaria y fabricación física son conceptos independientes.
5. **Conservar el original.** Los nombres, denominaciones, unidades nominales, textos y fechas de fuente se conservan aunque exista una normalización.
6. **No forzar exhaustividad.** No se exige completar todos los campos ni poblar relaciones opcionales sin evidencia.
7. **No destruir contradicciones.** Evidencias incompatibles se conservan y se escalan para revisión; no se resuelven sobrescribiendo silenciosamente una fuente.
8. **Los códigos externos identifican, no definen por sí solos la entidad.** Un código ausente o retirado no invalida una moneda, emisor o territorio histórico.

## 2. Convenciones de validación

Cada regla se clasifica como:

- **ERROR:** contradicción lógica, referencia inexistente, valor fuera de un vocabulario cerrado o dato matemáticamente imposible.
- **ADVERTENCIA:** incoherencia temporal/contextual probable, atribución insuficientemente respaldada o ambigüedad que requiere revisión humana.
- **INFORMACIÓN:** dato opcional ausente, precisión limitada o circunstancia histórica que conviene mostrar sin bloquear el registro.

La severidad se refiere a la calidad/integridad del catálogo, no a la importancia histórica del objeto. Una advertencia no debe impedir conservar un registro provisional. Una corrección manual debe dejar trazabilidad.

## 3. Vocabularios controlados

Los siguientes son los vocabularios iniciales recomendados. Los campos que el modelo actual describe como texto libre (nombres, descripciones, denominaciones, notas, jurisdicción textual, título de fuente) no se convierten automáticamente en enumeraciones.

### 3.1 Emisor: `issuer.type`

Valores iniciales:

- `sovereign_state`: Estado soberano actual o histórico.
- `subnational_entity`: entidad territorial subestatal con atribución emisora acreditada.
- `dependent_territory`: territorio dependiente o autónomo con atribución emisora acreditada.
- `monetary_union`: unión o entidad política supranacional que actúa como emisor.
- `historical_polity`: entidad política histórica que no encaja adecuadamente en las anteriores.
- `other`: entidad emisora acreditada de otra naturaleza, acompañada de descripción.

No clasificar automáticamente todo territorio que utiliza una moneda como emisor. Los códigos ISO 3166 son identificadores geográficos auxiliares, no el vocabulario de tipos de emisor.

### 3.2 Autoridad monetaria: tipo institucional

Valores iniciales recomendados para `monetary_authority.type`:

- `central_bank`: banco central nacional o supranacional.
- `currency_board`: caja de conversión u organismo equivalente.
- `treasury`: tesoro o departamento estatal con función monetaria acreditada.
- `supranational_authority`: institución supranacional con competencia monetaria.
- `other_monetary_authority`: otra institución, descrita explícitamente.

No incluir cecas, imprentas ni empresas contratistas por el mero hecho de fabricar billetes o monedas.

### 3.3 Roles emisor-moneda: `issuer_currency.role`

Valores aprobados por D-013:

- `uses`: utiliza/adopta la moneda.
- `legally_issues`: tiene competencia legal para emitir moneda o piezas denominadas en ella.
- `has_authorized_coinage`: dispone de autorización específica para emitir moneda propia dentro de una moneda compartida.

Calificador opcional `use_basis`, aprobado por D-020:

- `official`: uso oficialmente adoptado.
- `de_facto`: uso de facto sin que ese hecho demuestre adopción oficial o competencia emisora.

No crear valores `mints`, `prints` o `member_of_union` en este vocabulario: producción física y membresía institucional son relaciones diferentes. No inferir `use_basis` por ausencia de evidencia.

### 3.4 Relación emisión-autoridad: `catalog_issue_monetary_authority.role`

Valores aprobados por D-018:

- `legal_issuer`: institución con competencia/responsabilidad legal sobre la emisión concreta.
- `operational_issuer`: institución que ejecuta la emisión o la puesta en circulación.

Ambos roles pueden recaer en la misma institución o en instituciones distintas. Son opcionales y pueden coexistir. No equivalen a ceca/imprenta.

### 3.5 Intención de circulación: `catalog_issue.circulation_intent`

Valores aprobados por D-019:

- `intended_for_circulation`: emisión concebida para circulación.
- `not_intended_for_circulation`: emisión no concebida para circulación ordinaria.

Ausencia = desconocido/no documentado. No añadir `circulated` o `never_circulated`: describirían hechos efectivos, no intención. La clase numismática (prueba, patrón, ensayo, bullion, conmemorativa, colección, etc.) es otro atributo/vocabulario futuro y no debe inferirse de este campo.

### 3.6 Eventos monetarios: `currency_status_event.event_type`

Valores aprobados por D-014:

- `introduced`: introducción/adopción de la moneda o del régimen indicado.
- `entered_circulation`: comienzo de circulación efectiva del objeto/moneda en el ámbito.
- `legal_tender_started`: comienzo de curso legal.
- `legal_tender_ended`: fin de curso legal.
- `withdrawn_from_circulation`: retirada de circulación; no implica por sí sola fin de canje.
- `exchange_period_ended`: fin del periodo de canje.
- `demonetized`: desmonetización jurídica del objeto/moneda en el ámbito indicado.

El evento debe referirse explícitamente a su objeto: moneda, relación emisor-moneda o emisión, según corresponda. La jurisdicción/ámbito debe expresarse cuando el hecho no sea universal. No añadir `commemorative`, `not_circulating` o `replacement` como eventos: son clasificación de emisión o tipo de transición.

### 3.7 Transiciones: `currency_transition.type`

Valores aprobados por D-016:

- `replacement`: sustitución de una moneda por otra.
- `redenomination`: cambio legal de escala/unidad de una misma continuidad monetaria.

La relación es dirigida: moneda origen → moneda destino. El factor opcional expresa unidades de destino por una unidad de origen. No crear `coexistence` como transición ordinaria; la coexistencia se expresa con periodos/eventos. Una sustitución puede carecer de factor.

### 3.8 Caras: `design_side.side_type`

Valores iniciales:

- `obverse`: anverso.
- `reverse`: reverso.
- `other`: otra cara o componente visual, con descripción obligatoria que justifique su uso.

No convertir una cara en ficha coleccionable autónoma. La identidad visual del diseño sigue siendo la combinación de caras según D-002 y D-015.

### 3.9 Valor facial y unidades nominales

- La denominación original es texto obligatorio para conservar la forma documentada de la pieza.
- El valor normalizado es opcional y se expresa como racional exacto: numerador entero y denominador entero positivo, respecto de la unidad principal de una moneda identificada.
- Etiquetas como céntimo, centavo o diner no crean por sí mismas entidades `currency`.
- Una unidad nominal sin moneda oficial de referencia se conserva como texto y no se normaliza hasta disponer de equivalencia documentada.
- No usar coma flotante, redondeos implícitos ni equivalencias asumidas.

### 3.10 Códigos externos

- `currency.iso4217_code`: código vigente o histórico de ISO 4217 cuando exista y sea aplicable. Guardar su periodo/estado y no reutilizar códigos retirados para otra moneda.
- `issuer`/territorio: ISO 3166-1 alpha-2/alpha-3/numeric cuando proceda; ISO 3166-3 para códigos históricos retirados, si existe correspondencia.
- Los códigos son atributos identificativos auxiliares; no determinan soberanía, legitimidad, reconocimiento, uso monetario ni autoridad emisora.
- Para entidades sin código adecuado, usar identificador interno estable y alias; no inventar códigos que parezcan ISO.
- Los códigos ISO 4217 de fondos o metales preciosos no deben aceptarse como monedas de circulación sin clasificación explícita.

### 3.11 Procedencia: vocabulario de fuente y estado de evidencia

Tipo de fuente (`source_type`) inicial:

- `official_primary`: norma, boletín oficial, acto jurídico o publicación primaria del organismo competente.
- `official_institutional`: catálogo, ficha o publicación institucional no normativa.
- `academic_or_museum`: publicación académica, museo o catálogo especializado con autoría identificable.
- `reputable_secondary`: obra secundaria o medio de referencia con autoría/procedencia identificable.
- `community_reference`: base colaborativa o aportación comunitaria.
- `user_supplied`: documento o información aportada por el usuario.
- `derived`: dato calculado o inferido a partir de otras evidencias; debe identificar sus entradas y método.

Estado de verificación (`verification_status`):

- `verified`: la afirmación concreta está respaldada por evidencia adecuada y revisada.
- `partially_verified`: solo una parte del dato o del intervalo está confirmada.
- `unverified`: pendiente de revisión.
- `disputed`: existen evidencias incompatibles relevantes.
- `superseded`: la fuente o afirmación fue sustituida por evidencia posterior, conservando historial.

No confundir el tipo de fuente con su estado: una fuente oficial puede no probar el campo concreto, y una fuente secundaria puede ser la única evidencia disponible. No establecer una puntuación numérica universal de confianza.

## 4. Reglas temporales

### 4.1 Representación de fechas y precisión

Conservar la fecha literal de la fuente y normalizar solo hasta la precisión realmente disponible. Precisiones conceptuales:

- `day`: día exacto.
- `month`: mes conocido, día desconocido.
- `year`: año conocido, día y mes desconocidos.
- `period`: intervalo explícito.
- `approximate`: fecha aproximada, con explicación/fuente.
- `unknown`: fecha desconocida.

No convertir un año en 1 de enero ni un mes en su primer día como si fueran hechos. Una fecha aproximada no debe tratarse como exacta en comparaciones. Para cronologías antiguas, registrar el sistema/calendario original si afecta a la interpretación y documentar cualquier conversión.

### 4.2 Intervalos de vigencia

- Interpretar los periodos de vigencia como intervalos semiabiertos conceptuales `[inicio, fin)`: inicio incluido, fin excluido. Si la fuente expresa otra convención, conservarla en la nota/evidencia.
- Un extremo nulo significa límite desconocido o abierto según el contexto; debe distinguirse conceptualmente de «no existía».
- Una relación temporal solo es válida durante el intervalo acreditado.
- No exigir que relaciones distintas sean contiguas: puede haber huecos reales o falta de documentación.
- No permitir solapamientos contradictorios para la misma entidad, rol, ámbito y afirmación, salvo que la fuente describa expresamente coexistencia, competencias compartidas o jurisdicciones diferentes.

### 4.3 Fecha del hecho frente a fecha de la fuente

Distinguir:
- fecha de validez histórica del hecho;
- fecha de publicación/entrada en vigor de la norma o documento;
- fecha de consulta/recuperación de la fuente;
- fecha de incorporación o revisión del dato en el catálogo.

No usar la fecha de publicación como fecha efectiva del hecho salvo que la fuente lo establezca.

### 4.4 Coherencia de eventos

- `introduced`, `entered_circulation` y `legal_tender_started` son hitos distintos; pueden coincidir, pero no se presumen simultáneos.
- `withdrawn_from_circulation` no implica `legal_tender_ended` ni `exchange_period_ended`.
- `legal_tender_ended` no implica que el canje haya terminado.
- `demonetized` exige evidencia de desmonetización jurídica en el ámbito afectado; no se deduce de que una moneda deje de circular.
- Una emisión puede ser `not_intended_for_circulation` y no tener eventos de circulación; no registrar automáticamente un evento de retirada o desmonetización.
- La cronología de una moneda no se extrapola a todas las emisiones, territorios o relaciones emisor-moneda sin evidencia.
- Un evento sin fecha exacta puede conservarse con precisión parcial; no inventar el día.

### 4.5 Roles y autoridades a lo largo del tiempo

- Las vigencias de `issuer_currency` y `catalog_issue_monetary_authority` deben encajar con el periodo de existencia/atribución de las entidades relacionadas.
- Si una autoridad empieza a existir después de una emisión histórica, no atribuirle esa emisión retroactivamente sin norma o sucesión institucional explícita.
- Los roles `legal_issuer` y `operational_issuer` pueden tener periodos distintos y no tienen que ser simultáneos.
- El rol `has_authorized_coinage` requiere autorización aplicable al emisor y al periodo; no se infiere de que existan monedas acuñadas.
- `use_basis` califica el rol `uses`; no debe interpretarse como una afirmación independiente de curso legal.

## 5. Procedencia y evidencia

Cada afirmación histórica relevante debe poder rastrearse a una o más fuentes concretas. La procedencia se asocia al hecho/relación/campo, no únicamente a la ficha global.

Registro conceptual mínimo de una fuente:

- identificador estable interno;
- título y organismo/editor o autor;
- URL/URI o referencia bibliográfica/archivo;
- tipo de fuente;
- fecha de publicación y fecha de consulta, si se conocen;
- idioma;
- localizador concreto (artículo, página, tabla, sección, identificador ELI, número de catálogo);
- fragmento/notas que expliquen qué afirmación respalda;
- versión, copia o huella de captura cuando sea necesario para reproducibilidad;
- restricciones/licencia conocidas para el material que se pretenda reutilizar.

Reglas:

1. Una fuente respalda solo los campos que efectivamente contiene. Una página institucional sobre una moneda no prueba automáticamente cada emisión, fecha o tirada.
2. Para hechos legales, priorizar norma/boletín oficial y documentar jurisdicción, vigencia y disposiciones transitorias.
3. Para características de una pieza, priorizar catálogo institucional, aviso de emisión o ficha de autoridad emisora; la fuente legal puede no contener datos numismáticos.
4. Una fuente secundaria o comunitaria puede orientar una investigación o respaldar provisionalmente un dato, pero no se etiqueta como fuente primaria.
5. Para datos derivados (por ejemplo, factor racional), conservar las fuentes de entrada, fórmula, orientación y resultado exacto.
6. Ante conflicto, conservar ambas evidencias, marcar `disputed` y abrir revisión; no elegir por jerarquía automática sin analizar qué autoridad y campo cubre cada fuente.
7. La fecha de consulta no sustituye a la fecha de publicación ni acredita que la página siga disponible.
8. Una URL o una licencia de fotografía no demuestra derechos de reproducción del diseño monetario. D-008 prevalece: sin permiso/licencia compatible verificada, no incorporar la imagen.
9. Las fuentes de usuario pueden ser útiles para iniciar una revisión, pero no se consideran verificadas por el mero hecho de haber sido aportadas.

El enfoque es compatible conceptualmente con W3C PROV (entidades, actividades y agentes responsables), sin exigir adoptar PROV-O ni RDF en la implementación.

## 6. Reglas entre entidades y relaciones

### 6.1 Identidad y referencias

- Toda referencia debe apuntar a una entidad existente del tipo esperado.
- Una emisión debe referenciar diseño, moneda y emisor válidos.
- Un diseño debe referenciar las caras requeridas según su tipo; cada cara debe tener tipo coherente.
- Una relación autoridad-moneda debe enlazar una autoridad y una moneda existentes.
- Una transición debe enlazar dos monedas distintas y tener dirección inequívoca.
- Las fusiones, alias y sustituciones de registros deben conservar redirecciones/historial para no romper posesiones ni procedencia.

### 6.2 Emisor, moneda y autoridad

- `uses` no implica `legally_issues`.
- `use_basis=de_facto` no implica adopción oficial, curso legal ni competencia emisora.
- `has_authorized_coinage` no convierte automáticamente al Estado en emisor de billetes.
- Una autoridad monetaria no sustituye al emisor político/legal de la pieza.
- `legal_issuer` y `operational_issuer` identifican responsabilidades institucionales; no describen fabricación física.
- La ceca/imprenta se modela como productor físico y requiere relación propia; no se almacena como autoridad por defecto.
- La ausencia de relación autoridad-emisión no es error: D-018 la hace opcional.

### 6.3 Eventos y ámbitos

- El objeto afectado por un evento debe ser compatible con el tipo de evento y estar identificado sin ambigüedad.
- Los eventos de curso legal deben indicar el ámbito/jurisdicción cuando la condición no sea universal.
- No duplicar un mismo hecho como si fueran varios hitos distintos sin motivo documental.
- Si dos fechas de eventos parecen invertidas (por ejemplo, fin de canje anterior a su inicio), error solo cuando se refieran al mismo régimen, objeto y ámbito y la evidencia sea inequívoca; en otro caso, advertencia.
- Eventos en monedas y emisiones distintas no se ordenan ni comparan como una única cronología global.

### 6.4 Transiciones y factores

- `replacement` no exige factor de conversión.
- `redenomination` normalmente requiere factor y base legal; si falta, advertencia, no error automático mientras el dato esté incompleto.
- Si existe factor, numerador y denominador deben ser enteros, denominador positivo y valor positivo; cero o negativo es error para conversiones monetarias ordinarias.
- La orientación debe expresarse siempre como unidades de destino por unidad de origen.
- No registrar coexistencia ordinaria como transición.
- No crear transición entre XOF y XAF por compartir nombre histórico o paridad con el euro.
- No asignar un factor universal CUP/CUC sin norma que lo establezca para el ámbito y periodo concretos.

### 6.5 Emisiones, denominaciones y caras

- `circulation_intent` no determina clase numismática, curso legal ni circulación efectiva.
- La ausencia de `circulation_intent` es desconocimiento, no error.
- Una unidad nominal no oficial (por ejemplo, diners en una pieza de colección) se conserva sin crear moneda ficticia.
- Un valor facial normalizado debe corresponder a la moneda/unidad de referencia declarada y a la denominación original.
- Numerador debe ser entero; denominador entero estrictamente positivo; conservar racional exacto sin redondeo.
- Un diseño visual no se identifica solo por denominación/año. La combinación de caras determina identidad visual conforme a D-002.
- Una cara compartida no fusiona diseños; diferencias visibles relevantes pueden justificar diseño/variante separado.

### 6.6 Códigos e identificadores

- No exigir ISO 4217 para monedas históricas o unidades no codificadas.
- No exigir ISO 3166 para entidades históricas, territorios o emisores sin código adecuado.
- No asignar un código actual a una entidad histórica por simple continuidad territorial.
- El código debe ser compatible con la moneda/entidad y el periodo de validez; cambios y retiros se conservan históricamente.
- Código duplicado para dos monedas distintas en el mismo ámbito temporal es error, salvo que la especificación externa indique expresamente reutilización temporal y el periodo esté modelado.

## 7. Casos de error, advertencia e información

| Caso | Severidad | Tratamiento |
|---|---|---|
| Valor de enumeración fuera del vocabulario cerrado | ERROR | Corregir o proponer ampliación controlada |
| Referencia a entidad inexistente o de tipo incorrecto | ERROR | Resolver referencia |
| Denominador racional cero/negativo o factor no positivo | ERROR | Corregir valor |
| Emisión sin diseño, moneda o emisor | ERROR | Completar referencia |
| Transición sin origen/destino distintos | ERROR | Corregir dirección |
| Fechas exactas incompatibles en el mismo ámbito (fin anterior a inicio) | ERROR | Revisar cronología |
| `uses` usado como prueba de `legally_issues` | ERROR | Separar roles |
| `de_facto` interpretado como curso legal o emisión | ERROR | Corregir inferencia |
| Autoridad monetaria tratada como emisor político sin atribución | ADVERTENCIA | Revisar responsabilidades |
| Ceca/imprenta registrada como autoridad por fabricar | ADVERTENCIA | Reclasificar como productor |
| Evento sin ámbito claro cuando puede variar por territorio | ADVERTENCIA | Precisar jurisdicción |
| Fecha de año/mes convertida en día exacto | ERROR si se afirma como exacta; ADVERTENCIA si la conversión es solo técnica y visible | Recuperar precisión original |
| Solapamiento de roles con alcance aparentemente contradictorio | ADVERTENCIA | Revisar evidencia y jurisdicción |
| `redenomination` sin factor o base legal disponible | ADVERTENCIA | Mantener provisional y documentar ausencia |
| Factor derivado sin fórmula o fuentes | ADVERTENCIA | Añadir procedencia reproducible |
| Fuente secundaria para hecho legal sin fuente primaria accesible | ADVERTENCIA | Registrar limitación |
| Fuentes contradictorias | ADVERTENCIA | Marcar disputed y conservar ambas |
| Código ISO ausente para moneda histórica | INFORMACIÓN | Aceptar registro |
| Autoridad-emisión opcional ausente | INFORMACIÓN | No bloquear |
| Intención de circulación desconocida | INFORMACIÓN | Mantener null/desconocido |
| Fecha histórica solo conocida por año | INFORMACIÓN | Conservar precisión anual |
| Pieza sin imagen por D-008 | INFORMACIÓN | Usar placeholder |
| Denominación no normalizable con seguridad | INFORMACIÓN | Conservar texto original |

## 8. Contraste con los seis casos de MODEL_VALIDATION.md

### Andorra

- Registrar peseta y franco francés como `uses` con `use_basis=de_facto` en los periodos acreditados; no inferir `legally_issues`.
- Registrar el euro como uso oficial desde el hito documentado.
- La autorización andorrana de moneda euro se representa con `has_authorized_coinage` y/o atribución legal por emisión cuando la fuente lo concrete; no implica billetes.
- Piezas en diners: conservar denominación/unidad nominal; no crear `currency` para diners sin existencia monetaria propia acreditada.
- Advertir si se atribuye a Andorra la emisión de pesetas/francos usados de facto o se normalizan diners sin equivalencia.

### Cuba (CUP/CUC)

- CUP y CUC son dos entidades moneda distintas; la coexistencia se representa con periodos y eventos, no con una relación de subunidad.
- El proceso de unificación y retirada del CUC requiere eventos separados y ámbito/fuente por afirmación.
- No inferir que fin de curso legal, retirada física y fin de canje coinciden.
- No añadir factor CUP/CUC universal ni `redenomination` si la fuente no establece esa equivalencia para el contexto.
- La falta de catálogo estructurado o fuente primaria accesible produce advertencias/completitud baja, no invalida la estructura del modelo.

### Ecuador (sucre/USD)

- Sucre y USD son monedas distintas; la sustitución es `replacement` con factor destino/origen exacto solo para el régimen acreditado: 1 sucre = 1/25.000 USD.
- La moneda fraccionaria ecuatoriana conserva USD como moneda y centavos como unidad/subunidad; no crear moneda separada.
- La pieza de 1 sucre de 2000 puede llevar `not_intended_for_circulation`; esto no afirma por sí solo que nunca circuló ni altera los eventos jurídicos del sucre.
- BCE como autoridad/productor/emisor se atribuye por función y emisión concretas; no generalizar su competencia a todos los billetes USD.

### Euro

- Mantener moneda EUR única, y separar Estados usuarios/emisores, autoridades monetarias y responsabilidades por emisión.
- Los roles `legal_issuer` y `operational_issuer` pueden recaer en instituciones distintas; no inferir que el organismo coordinador o la ceca sea el emisor legal.
- Distinguir inicio de adopción/unidad contable, inicio de efectivo, fin de curso legal de moneda anterior y fin de canje.
- La cara común reutilizable no fusiona diseños nacionales.
- No exigir que cada emisión tenga atribución autoridad-emisión si no añade precisión o no hay evidencia.

### XOF / XAF

- XOF y XAF deben ser monedas diferentes con autoridades distintas (BCEAO y BEAC).
- Los Estados miembros se representan como usuarios/jurisdicciones, no como autoridades emisoras por defecto.
- La atribución de autoridad por emisión puede indicar BCEAO/BEAC y roles pertinentes; los Estados identificados en un billete no se convierten automáticamente en emisores legales.
- No crear transición entre XOF y XAF ni fusionarlas por paridad/nombre compartido.
- La falta de código/atribución adicional para emisiones antiguas genera advertencia o información según el impacto, no una fusión.

### Peseta

- ESP y EUR son monedas distintas relacionadas mediante `replacement`; conservar factor exacto 1 ESP = 500/83193 EUR (equivalente a 1/166,386) con orientación destino/origen.
- Registrar adopción/unidad contable, introducción de efectivo, circulación dual, fin de curso legal y fin de canje como hitos diferenciados.
- No inferir que fin de circulación dual coincide con fin de canje.
- El código histórico ESP puede conservarse aunque ya no sea vigente.
- Los años/fechas solo se precisan hasta lo que demuestre la fuente.

## 9. Resultado de contraste

Los seis casos encajan con los vocabularios y reglas propuestos. No aparece una contradicción que exija modificar D-001–D-020 ni alterar las entidades/relaciones aprobadas. Los principales riesgos son de calidad de evidencia y precisión histórica, no de estructura:

- Cuba: cobertura documental y cronología legal con fuentes primarias accesibles.
- Andorra: no confundir uso de facto, autorización de acuñación y unidades nominales de colección.
- Ecuador: no confundir intención de circulación, circulación efectiva y moneda de denominación USD.
- Euro y XOF/XAF: atribuir autoridad a cada emisión sin convertir territorios usuarios en autoridades.
- Peseta: conservar por separado los hitos de adopción, efectivo, curso legal y canje.

## 10. Límites y siguientes pasos

- Los vocabularios son iniciales y pueden ampliarse mediante revisión explícita y documentada; no se ha creado un procedimiento automático de gobernanza.
- No se ha definido SQL, JSON Schema, constraints físicos, API ni código.
- No se ha auditado cada registro histórico ni se ha ejecutado una validación automatizada.
- La especificación no aprueba fuentes ni imágenes: D-008 permanece intacta.
- Las reglas de conservación, valoración, mapa, privacidad/moderación, infraestructura y catálogo semilla siguen pendientes de Fase 0.
- No cierra Fase 0 ni autoriza el MVP.

## Referencias normativas/metodológicas

- ISO 4217: códigos de moneda; Maintenance Agency SIX.
- ISO 3166-1/3: códigos geográficos actuales e históricamente retirados; ISO 3166 Maintenance Agency.
- W3C PROV-DM / PROV-O: modelo conceptual de procedencia basado en entidades, actividades y agentes.

Estas referencias orientan la identificación y procedencia; no sustituyen la evidencia primaria de cada hecho numismático ni amplían automáticamente los campos aprobados.
