# Estrategia operativa del catálogo numismático mundial

**Fecha:** 2026-11-27  
**Rama:** `research/source-automation-2026-11`  
**Estado:** estrategia conceptual aprobada; Fase 0 abierta.  
**Decisiones relacionadas:** D-008, D-021, D-023 y D-024.

## 1. Objetivo y límites

Definir cómo crecerá un catálogo propio de monedas y billetes con ambición mundial progresiva, sin prometer exhaustividad ni exigir completar el mundo antes del MVP.

Esta estrategia es operativa y conceptual. No define SQL, esquema físico, API, código, importadores, automatizaciones ni arquitectura de despliegue. Tampoco autoriza descargar o importar datasets ni iniciar el MVP.

Principios:
- El catálogo consolidado es propio; ninguna fuente externa tiene autoridad única.
- La calidad, identidad y procedencia prevalecen sobre el volumen bruto.
- Los metadatos pueden existir sin imágenes; D-008 gobierna íntegramente la reutilización visual.
- La cobertura y la verificación son dimensiones distintas.
- La ampliación es incremental y puede avanzar a distinta profundidad por emisor, moneda, familia o emisión.

## 2. Taxonomía y cobertura

### 2.1 Niveles del catálogo

La planificación de cobertura distingue siete niveles conceptuales:
1. **Emisores:** entidades actuales e históricas con atribución acreditada.
2. **Monedas:** unidades monetarias vigentes, históricas o compartidas.
3. **Familias y series:** conjuntos de piezas relacionados histórica o numismáticamente.
4. **Diseños:** identidad visual formada por la combinación de caras, conforme a D-002 y D-015.
5. **Emisiones:** emisiones concretas con sus atributos, fechas y responsabilidades cuando estén documentadas.
6. **Piezas:** denominaciones y tipos de moneda o billete del catálogo.
7. **Variantes:** diferencias identificables y relevantes para el coleccionista.

Estos niveles sirven para medir y planificar cobertura; no crean por sí mismos nuevas entidades ni alteran `DATA_MODEL.md`. Su correspondencia exacta con las entidades del modelo debe mantenerse explícita al desarrollar futuros trabajos.

### 2.2 Estados de cobertura

Cada ámbito evaluado puede describirse con uno de estos estados:
- `not_assessed`: no evaluado.
- `identified`: existencia identificada.
- `skeleton`: estructura básica registrada.
- `partial`: cobertura parcial conocida o con lagunas.
- `reviewed`: alcance conocido revisado con criterios documentados.
- `high_coverage`: cobertura amplia respecto de un alcance definido, sin afirmar exhaustividad.
- `blocked`: existen obstáculos relevantes documentales, técnicos o de derechos.

Los estados se aplican de forma independiente a cada nivel y ámbito; no se heredan automáticamente de un emisor a sus monedas o emisiones. Deben acompañarse de fecha de evaluación, alcance y explicación de lagunas cuando sea posible.

No equivalen a `verification_status` de las afirmaciones. Una familia puede tener cobertura parcial y contener algunas afirmaciones verificadas; una ficha identificada puede seguir sin verificación suficiente.

Los umbrales objetivos para `reviewed` y `high_coverage` quedan pendientes de definir con casos reales. No asignar porcentajes arbitrarios.

## 3. Arquitectura lógica de fuentes

Se distinguen cinco clases, sin jerarquía universal automática:

1. **Identificadores y vocabularios generales:** ISO 4217, ISO 3166, Wikidata y sistemas equivalentes. Ayudan a identificar y normalizar; no prueban por sí solos soberanía, uso, curso legal ni competencia emisora.
2. **Fuentes institucionales primarias:** legislación, boletines oficiales, bancos centrales, autoridades emisoras y organismos monetarios. Se priorizan para hechos jurídicos y responsabilidades institucionales.
3. **Datasets especializados:** conjuntos de datos numismáticos abiertos con licencia compatible, alcance conocido y contenido auditable. Son complementos, no autoridades únicas.
4. **Referencias auxiliares:** museos, bibliografía académica, catálogos especializados y comunidades. Sirven para descubrir, contrastar o documentar provisionalmente.
5. **Curación propia:** investigación, normalización, correspondencias y decisiones documentadas del catálogo.

La autoridad de una fuente depende del atributo y del hecho concreto. Una fuente normativa puede acreditar curso legal, pero no necesariamente peso o diámetro; un catálogo técnico puede ser mejor para dimensiones, pero no para la competencia legal de emisión.

La evaluación de cada candidato debe distinguir licencia del software, licencia de la base de datos, derechos de contribuciones y derechos de imágenes/diseños. La disponibilidad pública no equivale a permiso de reutilización.

## 4. Aceptación y auditoría

La aceptación se realiza en tres planos independientes:

### 4.1 Fuente
Registrar identidad del responsable, alcance, tipo, licencia y derechos conocidos, procedencia, localizadores, idioma, fecha de consulta, mantenimiento, disponibilidad y limitaciones. La evaluación de licencia debe cubrir el contenido que se pretende reutilizar, no solo el repositorio o su software.

### 4.2 Afirmación
Comprobar que la fuente respalda exactamente el atributo y el ámbito indicados; conservar literal original y normalización; registrar precisión temporal, localizador y estado de verificación. Aplicar las reglas de `VALIDATION_RULES.md`, incluidas V-01–V-09.

### 4.3 Registro consolidado
Comprobar identidad y tipo de entidades, relaciones, compatibilidad temporal, duplicados, conflictos y procedencia. La falta de evidencia suficiente suele mantener el registro provisional o generar advertencia; no debe convertirse en una afirmación inventada.

La auditoría periódica de fuentes debe observar disponibilidad, cambios de estructura, mantenimiento, alcance, licencias/condiciones y calidad. Una fuente inactiva no invalida automáticamente hechos históricos que documentó.

No se define una puntuación numérica universal de confianza ni una jerarquía automática de fuentes.

## 5. Flujo conceptual de ingesta y staging

Toda incorporación externa pasa conceptualmente por estas etapas:

1. **Captura:** identificar fuente, versión o estado observado, fecha, alcance y localizador.
2. **Staging:** conservar la representación original sin alterarla.
3. **Normalización:** producir una representación alineada con el modelo propio, conservando el vínculo al original y las reglas aplicadas.
4. **Correspondencia y deduplicación:** proponer entidades coincidentes sin fusionar automáticamente registros ambiguos.
5. **Validación:** aplicar vocabularios, reglas estructurales y temporales.
6. **Conflictos y revisión:** conservar evidencias incompatibles y resolverlas con intervención documentada.
7. **Aceptación:** incorporar al catálogo consolidado solo la información que supere los criterios correspondientes; lo provisional puede permanecer identificado como tal.

El staging conserva como mínimo dos perspectivas: dato original de la fuente y dato normalizado propuesto. Debe distinguir altas, actualizaciones, correcciones, posibles duplicados y conflictos. Una actualización de fuente genera una propuesta revisable; no sobrescribe automáticamente una afirmación verificada.

Este flujo es una especificación conceptual, no autorización para implementar importadores ni automatizaciones.

## 6. Procedencia y conflictos

La trazabilidad se asocia a la afirmación concreta, no solo a la ficha. Debe permitir reconstruir fuente, versión/consulta, localizador, valor original, normalización, actividad o método, revisión y cambios.

Reglas:
- No sobrescribir silenciosamente afirmaciones verificadas.
- Conservar evidencias incompatibles y marcar la afirmación como `disputed` cuando proceda.
- Distinguir error, dato antiguo, diferencia de alcance y dato incompleto.
- Resolver según la naturaleza del atributo, jurisdicción, periodo y alcance de la fuente.
- Registrar la justificación, responsable/actividad y fecha de resolución.
- Mantener historial y enlaces entre afirmaciones sustituidas y sucesoras.
- No deduplicar solo por similitud de nombre, denominación, año o imagen: dos registros pueden ser emisiones o variantes distintas.

La resolución puede concluir que dos fuentes describen hitos diferentes (por ejemplo, autorización y circulación), que una tiene alcance jurisdiccional distinto o que una contiene un error. La elección no se hace por precedencia automática de una clase de fuente.

## 7. Derechos de datos, textos e imágenes

Evaluar por separado:
- **Datos estructurados:** licencia de la base/contenido y derechos de terceros.
- **Textos y descripciones:** permiso de reutilización o redacción original propia.
- **Fotografías:** licencia individual, autoría, atribución y condiciones.
- **Diseño monetario representado:** derechos y restricciones aplicables al diseño, independientes de la licencia fotográfica.

Una licencia CC BY o MIT declarada para un repositorio no demuestra que cada dato, contribución o imagen esté cubierto. Tampoco una licencia de fotografía autoriza necesariamente la reproducción del diseño monetario.

Aplicación:
- D-008 prevalece sin excepciones.
- No contactar con titulares para solicitar permisos particulares.
- Ante ambigüedad, no incorporar el material; conservar, si resulta útil, una referencia bibliográfica/enlace.
- Priorizar metadatos; admitir fichas sin imagen y placeholders neutros.
- No descargar ni importar imágenes por defecto.

## 8. Métricas de cobertura y calidad

No se publicará un único porcentaje de «cobertura mundial»: no existe un denominador fiable que enumere todas las emisiones y variantes que han existido.

Medir por separado:
- **Geografía e identidad:** emisores identificados, evaluados y documentados.
- **Monedas:** monedas vigentes e históricas identificadas y documentadas.
- **Profundidad numismática:** familias, diseños, emisiones, piezas y variantes registradas por ámbito.
- **Calidad de evidencia:** afirmaciones verificadas, parcialmente verificadas, no verificadas y disputadas.
- **Procedencia:** afirmaciones con fuente y localizador identificables.
- **Derechos:** recursos con derechos evaluados y aptos para el uso previsto.
- **Salud operativa:** duplicados y conflictos pendientes, fuentes sin revisar, propuestas pendientes y antigüedad de revisiones.

Toda tasa o porcentaje debe declarar numerador, denominador, ámbito y fecha. Si el denominador es solo el conjunto de elementos identificados, debe decirlo expresamente; no presentarlo como porcentaje de todas las emisiones existentes.

La ausencia de imagen no es por sí sola un defecto de calidad ni reduce la cobertura de metadatos. Puede medirse como indicador descriptivo independiente.

## 9. Crecimiento progresivo

El catálogo crecerá por unidades de cobertura independientes, sin exigir que todos los emisores alcancen la misma profundidad. Una región puede tener emisiones ampliamente documentadas mientras otra conserva solo un esqueleto de emisores y monedas.

Etapas orientativas:
- **A — Esqueleto mundial:** identificar emisores, monedas y relaciones históricas.
- **B — Cobertura institucional:** incorporar familias, series y emisiones respaldadas por fuentes.
- **C — Enriquecimiento especializado:** añadir atributos técnicos, diseños, tiradas y complementos auditados.
- **D — Profundización histórica:** investigar periodos y entidades con documentación dispersa.
- **E — Mejora continua:** corregir, completar y ampliar según lagunas y necesidades.

Son etapas de trabajo, no puertas secuenciales globales: pueden coexistir en ámbitos diferentes. La prioridad considerará relevancia, disponibilidad/calidad de evidencia y coste de investigación/mantenimiento. Ninguna etapa exige completar el catálogo mundial antes del MVP.

## 10. Costes y mantenimiento

Se mantiene el presupuesto objetivo de 0 €. Priorizar fuentes públicas con condiciones compatibles, procesos por lotes y curación selectiva. No introducir servicios de pago para resolver problemas que puedan abordarse razonablemente con revisión y procesamiento controlado.

El coste económico cero no significa coste operativo cero: la investigación, revisión, auditoría, almacenamiento y mantenimiento consumen tiempo y pueden depender de cuotas gratuitas o condiciones cambiantes. Antes de cualquier implementación se deberán verificar límites, almacenamiento, frecuencia permitida, disponibilidad, cambios de licencia y posibles costes indirectos.

La revisión se priorizará por volatilidad y valor: fuentes con emisiones recientes o cambios frecuentes primero; fuentes históricas estables con menor frecuencia. No se establece una periodicidad universal hasta conocer el comportamiento de cada fuente.

## 11. Riesgos y mitigaciones

| Riesgo | Mitigación |
|---|---|
| Confundir cobertura con exhaustividad | Estados por ámbito y métricas con denominador explícito |
| Licencia del repositorio confundida con licencia de todo el contenido | Auditoría de datos, contribuciones, textos, fotografías y diseños por separado |
| Duplicación o fusión errónea | Correspondencias propuestas y revisión de identidad; no deduplicar solo por similitud |
| Conflictos históricos | Evidencia por afirmación, alcance temporal/jurisdiccional y resolución trazable |
| Dependencia de una fuente | Arquitectura multicapa y referencias independientes |
| Sobrecarga de mantenimiento | Actualización selectiva y priorizada |
| Cuotas gratuitas o condiciones cambiantes | Verificación antes de implementar y alternativa manual |
| Apariencia de catálogo completo con lagunas desconocidas | Declarar alcance conocido y limitaciones; evitar porcentajes mundiales engañosos |
| Ausencia de imágenes | Separar cobertura de metadatos e imágenes y usar placeholders |

## 12. Pendientes explícitos de Fase 0

Antes de diseñar una implementación física quedan por decidir o validar:
- Umbrales y evidencia mínima para declarar un ámbito `reviewed` o `high_coverage`.
- Cómo expresar el alcance conocido y las lagunas cuando no existe inventario externo fiable.
- Mapeo definitivo de los siete niveles de cobertura a las entidades del modelo.
- Criterios y frecuencia de auditoría por clase/fuente.
- Plantilla operativa de evaluación de licencia y derechos por contenido.
- Política de priorización y capacidad de revisión humana.
- Verificación de costes/cuotas de cualquier servicio concreto cuando se evalúe infraestructura.

Estos pendientes no invalidan la estrategia aprobada ni autorizan a saltar a implementación.

## 13. Resolución

El usuario aprobó P1–P9 íntegramente el 2026-11-27, sin modificaciones ni observaciones. Se consolidan como estrategia operativa conceptual del catálogo mundial progresivo. D-008, D-021 y D-023 permanecen vigentes; D-001–D-023 no se alteran. Fase 0 continúa abierta.
