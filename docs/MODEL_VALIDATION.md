# Validación estructural del modelo consolidado

**Fecha:** 2026-11-26  
**Rama:** `research/source-automation-2026-11`  
**Alcance:** Andorra, Cuba (CUP/CUC), Ecuador (sucre/USD), euro, XOF/XAF y peseta.  
**Naturaleza:** validación conceptual de Fase 0. No define SQL, no implementa código y no reabre D-012–D-017.

## 1. Resultado ejecutivo

El modelo consolidado **representa correctamente los seis casos en sus relaciones monetarias principales**: autoridad monetaria separada del emisor, roles temporales de uso/emisión, eventos de estado, transiciones dirigidas, caras reutilizables y valor facial racional exacto.

No se detecta contradicción que obligue a revocar o reabrir D-012–D-017. La validación identificó tres huecos de especificación, que el usuario aprobó como P7–P9 y que ahora están consolidados en D-018–D-020: atribución de autoridad por emisión, intención de circulación/unidades nominales de colección y distinción entre uso oficial y de facto.

La ausencia de una fuente completa —especialmente para Cuba— limita los datos que se podrán poblar, pero no invalida el modelo.

## 2. Matriz de los seis casos

| Caso | Hechos que el modelo debe representar | Cobertura actual | Resultado / observación |
|---|---|---|---|
| **Andorra** | Uso de peseta española y franco francés de facto antes del euro; euro como moneda oficial desde 2002; derecho andorrano a emitir monedas euro bajo el acuerdo monetario de 2011; monedas de colección denominadas en diners. | `issuer_currency` permite varios usos por periodo; `has_authorized_coinage` representa el derecho a emitir moneda euro; `design_side` permite compartir la cara común. | **Cubierto tras P8/P9 (D-019/D-020).** `use_basis` distingue uso de facto de adopción oficial; las piezas en diners conservan su unidad nominal sin crear una moneda oficial ficticia. |
| **Cuba (CUP/CUC)** | Dos monedas diferenciadas con coexistencia; proceso de unificación iniciado con efectos desde 1-1-2021; retirada del CUC dentro del plazo legal; CUP continúa. | Dos entidades `currency`, roles/periodos de uso y eventos de retirada/fin de curso legal/canje; transición dirigida opcional. | **Cubierto conceptualmente.** No imponer una equivalencia universal CUP/CUC ni una redenominación ficticia. Si se registra transición CUC→CUP, será `replacement` sin factor, salvo que una regla concreta y su ámbito estén acreditados. La complejidad de tasas y tratamientos contables debe conservarse como contexto, no reducirse a un único factor. |
| **Ecuador (sucre/USD)** | El USD sustituye al sucre; tipo oficial de 25.000 sucres por USD; el BCE acuña moneda fraccionaria nacional denominada en centavos de USD; existe una pieza de 1 sucre de 2000 que no entró en circulación. | `currency_transition` admite sustitución y factor exacto; `issuer_currency` distingue uso de USD y emisión nacional; D-017 representa centavos como fracción de USD. | **Cubierto tras P8 (D-019).** `circulation_intent` permite registrar la emisión de 1 sucre de 2000 como no destinada a circulación, sin confundir intención con estado jurídico. Para el factor, con orientación destino/origen: 1 sucre = 1/25.000 USD. |
| **Euro** | El BCE y los bancos centrales nacionales tienen derecho legal a emitir billetes; en la práctica los BCN los ponen físicamente en circulación. Los emisores legales de monedas son los Estados del área euro; la Comisión coordina los asuntos de moneda. Andorra tiene derecho limitado a emitir monedas, no billetes. | `monetary_authority` y `monetary_authority_currency` distinguen instituciones; `issuer_currency` distingue Estados usuarios y emisores de moneda; `design_side` resuelve la cara común. | **Cubierto tras P7 (D-018).** La relación opcional autoridad-emisión diferencia `legal_issuer` y `operational_issuer`; la ceca/imprenta sigue siendo productor físico, no autoridad. |
| **XOF / XAF** | XOF y XAF son monedas distintas. BCEAO emite para los ocho Estados UMOA; BEAC emite para los seis Estados CEMAC. Los signos monetarios tienen curso legal en los respectivos territorios; algunos billetes incorporan identificación del Estado miembro. | Dos monedas, dos autoridades y relaciones temporales; los Estados se representan como usuarios/jurisdicciones, no como autoridades emisoras. | **Cubierto tras P7 (D-018).** La autoridad responsable puede atribuirse a cada emisión mediante la relación opcional; los Estados siguen representándose como usuarios/jurisdicciones. Nunca fusionar XOF y XAF ni crear transición entre ambas. |
| **Peseta** | Sustitución por el euro; tipo irrevocable de 166,386 ESP por EUR; euro como moneda contable desde 1999, efectivo euro desde 2002, circulación dual hasta 28-2-2002 y canje de pesetas hasta 30-6-2021. | `currency_transition`, eventos tipados y valor racional exacto. | **Cubierto.** Con orientación destino/origen, 1 ESP = 500/83193 EUR. Deben registrarse por separado adopción, entrada de efectivo, fin de curso legal y fin del canje. |

## 3. Comprobación transversal de D-012–D-017

### D-012 — Autoridad monetaria independiente
Se confirma necesaria. BCEAO y BEAC son autoridades/institutos emisores comunes a varios Estados; el Eurosistema y los BCN desempeñan funciones diferenciadas; el BCE ecuatoriano conserva funciones sobre moneda fraccionaria nacional aunque Ecuador use USD. No confundir autoridad monetaria con Estado usuario, emisor político, ceca o imprenta.

### D-013 — Roles temporales emisor-moneda
Los roles `uses`, `legally_issues` y `has_authorized_coinage` son suficientes como conjunto inicial para los casos examinados. No añadir membresía en unión monetaria ni fabricación física a esta relación. La membresía y la producción son relaciones distintas. El significado de `uses` requiere una precisión opcional para distinguir adopción oficial de uso de facto (P9).

### D-014 — Cronología de estados
La cronología basada en eventos es adecuada. Los ejemplos demuestran que introducción/adopción, comienzo de circulación, fin de curso legal, retirada física y fin de canje no son sinónimos ni necesariamente simultáneos. El evento debe conservar objeto afectado, jurisdicción/ámbito, fecha o intervalo, precisión y procedencia. «Conmemorativa» o «no destinada a circulación» no debe convertirse en un estado legal de la moneda; falta, sin embargo, un atributo explícito de intención de circulación en la emisión (P8).

### D-015 — Caras compartidas
Adecuada para la cara común del euro y las monedas andorranas. La identidad coleccionable sigue siendo la pareja de caras. Una diferencia visible —por ejemplo, una marca territorial o letra de identificación— puede justificar un diseño/variante distinto; compartir una cara no fusiona piezas.

### D-016 — Transiciones
Adecuadas para peseta→euro y sucre→USD. El factor debe conservar la orientación ya aprobada: unidades de destino por unidad de origen. Ejemplos exactos:
- 1 ESP → 500/83193 EUR.
- 1 sucre ecuatoriano → 1/25.000 USD.

Para CUP/CUC no se debe inferir un factor único. La coexistencia se registra con los periodos y eventos de cada moneda; la retirada del CUC no obliga a afirmar que CUP sea una redenominación del CUC. XOF y XAF no tienen relación de transición entre sí.

### D-017 — Denominaciones
La representación racional evita coma flotante y no crea monedas independientes para céntimos/centavos. Es válida para EUR, USD, CUP/CUC, sucre, peseta y valores enteros XOF/XAF. Debe conservarse siempre el texto original. Queda el caso límite de denominaciones numismáticas en una unidad que no fue moneda oficial (Andorra, diners), tratado en P8.

## 4. Decisiones aprobadas P7–P9

El usuario aprobó expresamente las tres propuestas el 26-11-2026. Se incorporan de forma acotada, sin reabrir D-012–D-017.

### P7 — Atribución de autoridad a una emisión concreta (D-018)

Se aprueba una relación opcional y temporal entre `catalog_issue` y `monetary_authority`, con procedencia y roles iniciales `legal_issuer` y `operational_issuer`. El primero identifica la competencia/responsabilidad legal de emisión; el segundo, la ejecución o puesta en circulación. No se exige poblarla si no aporta precisión o falta evidencia. Cecas e imprentas siguen siendo productores físicos.

### P8 — Intención de circulación y unidad nominal de colección (D-019)

Se aprueba un atributo opcional `circulation_intent` en `catalog_issue`, con valores iniciales `intended_for_circulation` y `not_intended_for_circulation`. La ausencia significa desconocido. No equivale a un evento legal ni demuestra si una pieza llegó efectivamente a circular. Las categorías numismáticas de prueba/patrón quedan separadas.

Se aprueba conservar la denominación y unidad nominal originales aunque no correspondan a una moneda oficial independiente. No crear automáticamente una entidad `currency` para unidades como diners; normalizar solo con una unidad de referencia documentada.

### P9 — Naturaleza del uso de una moneda (D-020)

Se aprueba el calificador opcional `use_basis` en `issuer_currency`, con valores iniciales `official` y `de_facto`, independiente del rol `uses`. Solo se informa cuando existe evidencia. No se deduce curso legal, adopción oficial ni competencia de emisión a partir del uso de facto.

## 5. Particularidades históricas que no son errores del modelo

- La coexistencia CUP/CUC no implica que una moneda sea subunidad, variante o redenominación de la otra.
- La adopción del euro como unidad contable en 1999 y la llegada del efectivo en 2002 son eventos distintos.
- En Ecuador, el BCE dejó de emitir billetes/moneda nacional ordinaria tras la dolarización, pero siguió acuñando moneda fraccionaria nacional denominada en USD. No equivale a emitir una moneda ecuatoriana paralela.
- La moneda de 1 sucre de 2000 es una emisión numismática no circulante, no prueba de que el sucre siguiera vigente como moneda de curso legal.
- XOF y XAF comparten la denominación histórica «franco CFA» y una paridad con el euro, pero siguen siendo unidades monetarias y zonas de emisión distintas.
- En Andorra, el uso de monedas extranjeras antes de 2002 fue de facto; no debe registrarse como emisión andorrana de pesetas o francos.
- El fin del canje de pesetas (2021) no coincide con el fin de la circulación dual (2002).

## 6. Límites de fuentes y carga de datos

- **Andorra:** el acuerdo monetario y la AFA permiten verificar el uso del euro y el derecho de acuñación. Las monedas denominadas en diners requieren conservar su naturaleza de colección.
- **Cuba:** la legislación de unificación permite fijar el hito de 2021, pero la documentación de catálogo CUP/CUC sigue fragmentaria. La norma sobre CUC y la retirada deben conservar referencia y calidad de fuente; no declarar completas las series.
- **Ecuador:** el BCE aporta evidencia clara sobre dolarización, tipo de cambio, moneda fraccionaria y pieza de 1 sucre no circulante.
- **Euro:** el BCE distingue los derechos de emisión de billetes y monedas y las funciones de los BCN.
- **XOF/XAF:** BCEAO y BEAC documentan autoridad emisora y territorios; los catálogos históricos completos siguen requiriendo curación por familia/Estado.
- **Peseta:** Banco de España y Comisión Europea documentan tipo irrevocable, transición y fin de canje.

La disponibilidad de fuentes no modifica el modelo conceptual. D-008 sigue prohibiendo incorporar imágenes o materiales sin derechos compatibles; esta validación no aprueba ningún asset.

## 7. Conclusión y siguiente paso

**Resultado:** validación estructural satisfactoria. P7–P9 han sido aprobadas y consolidadas como D-018–D-020; no hay motivo para reabrir D-012–D-017. El siguiente trabajo es definir vocabularios controlados y reglas conceptuales de validación y recontrastar los seis casos con el modelo ampliado. No escribir SQL ni código de producto.

Fase 0 permanece abierta. CELLAR sigue aparcado. El MVP continúa bloqueado hasta aprobación expresa del cierre de Fase 0.

## Fuentes de contraste

- Andorra: [AFA — Euro y acuerdo monetario](https://www.afa.ad/en/eu); [Acuerdo monetario UE-Andorra](https://eur-lex.europa.eu/legal-content/EN/TXT/PDF/?uri=CELEX%3A02011A1217%2801%29-20260324).
- Ecuador: [BCE — Historia](https://www.bce.fin.ec/banco-central-del-ecuador/historia/); [BCE — Seguridad en billetes y monedas](https://www.bce.fin.ec/seguridades-en-billetes-y-monedas/); [Museo de la Moneda BCE — El último sucre](https://museodelamoneda.bce.fin.ec/index.php/museo/item/132-el-%C3%BAltimo-sucre.html).
- Cuba: [Decreto-Ley 17/2020, Gaceta Oficial (reproducción digital)](https://www.directoriocubano.com/servicios/gaceta-oficial/2020/extraordinaria/68/); [Gaceta Oficial, No. 82 extraordinaria de 2020](https://www.directoriocubano.com/servicios/gaceta-oficial/2020/extraordinaria/82/). Copias digitales no alojadas en el portal oficial; mantener procedencia y cautela.
- Euro: [BCE — Emisión y circulación](https://www.ecb.europa.eu/euro/cash_strategy/issuance/html/index.en.html); [Comisión Europea — Euro fuera del área euro](https://economy-finance.ec.europa.eu/euro/use-euro/euro-outside-euro-area_en).
- XOF: [BCEAO — Presentación](https://www.bceao.int/content/presentation-de-la-bceao); [BCEAO — Emisión de signos monetarios](https://www.bceao.int/fr/publications/ndeg1-emission-des-signes-monetaires-et-entretien-de-la-circulation-fiduciaire).
- XAF: [BEAC — Preguntas frecuentes](https://www.beac.int/en/faqs/); [BEAC — Historia de la emisión monetaria en África Central](https://www.beac.int/billets-pieces/histoire-franc-cfa/histoire-de-lemission-monetaire-afrique-centrale/).
- Peseta: [Banco de España — Tipos irrevocables](https://www.bde.es/wbe/es/sobre-banco/actividad-europea/eurosistema-sebc/historia-eurosistema/euro/tipos-irrevocables/); [Comisión Europea — España y el euro](https://economy-finance.ec.europa.eu/euro/eu-countries-and-euro/spain-and-euro_en).


## 8. Revalidación con vocabularios y reglas conceptuales — 26/11/2026

La especificación complementaria está en [VALIDATION_RULES.md](VALIDATION_RULES.md). Se contrastaron expresamente los seis casos con los vocabularios y reglas:

- **Andorra:** uso de peseta/franco como `uses` + `de_facto`; euro como uso oficial; autorización de acuñación separada; diners conservados como unidad nominal no monetaria.
- **Cuba:** CUP/CUC diferenciadas; coexistencia y retirada mediante hechos temporales; no imponer factor universal ni confundir retirada, curso legal y canje.
- **Ecuador:** sustitución sucre→USD con factor destino/origen 1/25.000; centavos como subunidad de USD; pieza de 1 sucre con intención no circulante sin inferir hechos jurídicos.
- **Euro:** responsabilidades legales y operativas por emisión; Estados usuarios y autoridades diferenciados; adopción contable, efectivo y estados de monedas anteriores separados.
- **XOF/XAF:** monedas y autoridades BCEAO/BEAC separadas; Estados miembros como usuarios/jurisdicciones; ninguna transición entre XOF y XAF.
- **Peseta:** sustitución ESP→EUR con factor 500/83193; adopción, efectivo, fin de curso legal y fin de canje como hitos distintos.

**Resultado:** no se identifica contradicción que requiera reabrir D-001–D-020 ni modificar la estructura aprobada. Las advertencias más relevantes son de evidencia y completitud, especialmente para Cuba, y de no inferir relaciones o hitos a partir de otros conceptos.

La validación es conceptual y documental. No se ha ejecutado un validador automatizado, ni se han auditado registros de catálogo individuales. No constituye cierre de Fase 0.
