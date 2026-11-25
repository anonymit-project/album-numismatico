# Prueba de concepto CELLAR / Formex — C/2026/406

**Fecha de validación:** 2026-11-25  
**Fase:** 0 — investigación, sin código de producto.  
**Rama:** `research/source-automation-2026-11`  
**Aviso:** [EUR-Lex C/2026/406 — Lituania](https://eur-lex.europa.eu/eli/C/2026/406/oj/spa)

## Resultado

**Prueba positiva de recuperación y lectura de recursos CELLAR para un aviso numismático real, en español y lituano.** Se ha validado manualmente el recorrido SPARQL → Expression → Manifestation → Item → documento XHTML/Formex.

Esto demuestra la viabilidad técnica para este aviso concreto. No demuestra todavía un importador automático generalizable, una ingesta programada ni cobertura exhaustiva de avisos.

## 1. Consulta SPARQL ejecutada

Ejecutada por el usuario en el [editor SPARQL oficial de CELLAR](https://op.europa.eu/en/advanced-sparql-query-editor). Se usaron las expresiones española y lituana conocidas:

```sparql
PREFIX cdm: <http://publications.europa.eu/ontology/cdm#>
PREFIX purl: <http://purl.org/dc/elements/1.1/>

SELECT DISTINCT
    ?expr
    ?langCode
    ?manifestation
    ?format
    ?item
WHERE {
    VALUES ?expr {
        <http://publications.europa.eu/resource/cellar/d96c2765-f66c-11f0-b9bc-01aa75ed71a1.0007>
        <http://publications.europa.eu/resource/cellar/d96c2765-f66c-11f0-b9bc-01aa75ed71a1.0015>
    }

    ?expr cdm:expression_uses_language ?lang .
    ?lang purl:identifier ?langCode .

    ?manifestation
        cdm:manifestation_manifests_expression ?expr ;
        cdm:manifestation_type ?format .

    ?item cdm:item_belongs_to_manifestation ?manifestation .
}
LIMIT 100
```

La consulta devolvió **seis bindings**: tres manifestaciones para cada expresión, con formatos `pdfa2a`, `fmx4` y `xhtml`.

| Idioma | Expression | Formato | Manifestation | Item |
|---|---|---|---|---|
| SPA | `.0007` | `pdfa2a` | `.0007.01` | `.0007.01/DOC_1` |
| SPA | `.0007` | `fmx4` | `.0007.02` | `.0007.02/DOC_1` |
| SPA | `.0007` | `xhtml` | `.0007.03` | `.0007.03/DOC_1` |
| LIT | `.0015` | `pdfa2a` | `.0015.01` | `.0015.01/DOC_1` |
| LIT | `.0015` | `fmx4` | `.0015.02` | `.0015.02/DOC_1` |
| LIT | `.0015` | `xhtml` | `.0015.03` | `.0015.03/DOC_1` |

Los URIs completos se forman anteponiendo:

`http://publications.europa.eu/resource/cellar/d96c2765-f66c-11f0-b9bc-01aa75ed71a1`

a cada sufijo de Expression, Manifestation o Item de la tabla (para Item, añadir `/DOC_1` tras el sufijo de Manifestation).

## 2. Recuperación de recursos

### XHTML español

El recurso [Expression española XHTML — DOC_1](http://publications.europa.eu/resource/cellar/d96c2765-f66c-11f0-b9bc-01aa75ed71a1.0007.03/DOC_1) se abrió en navegador y mostró el aviso completo, incluida la ilustración de la moneda y los datos numismáticos.

### Formex español

El recurso [Expression española Formex — DOC_1](http://publications.europa.eu/resource/cellar/d96c2765-f66c-11f0-b9bc-01aa75ed71a1.0007.02/DOC_1) se descargó como ZIP. El paquete contenía tres XML y una imagen TIFF. Se identificaron:

- `C_202600406ES.000101.fmx.xml`: contenido principal.
- `C_202600406ES.doc.fmx.xml`: metadatos/referencia del documento.
- `C_202600406ES.toc.fmx.xml`: tabla de contenido.
- `C_202600406ES.000102.fmx.tif`: imagen incluida.

El XML principal contiene el texto del aviso y la referencia estructurada a la imagen. La imagen se conserva únicamente como evidencia de que el paquete la referencia; **no se incorpora al catálogo ni al repositorio**.

### Formex lituano

El recurso [Expression lituana Formex — DOC_1](http://publications.europa.eu/resource/cellar/d96c2765-f66c-11f0-b9bc-01aa75ed71a1.0015.02/DOC_1) se validó mediante el contenido XML principal proporcionado por el usuario.

El XML lituano presenta una estructura Formex equivalente: `GENERAL`, `BIB.INSTANCE`, `TITLE`, `CONTENTS`, párrafos `P`, marcas tipográficas `HT`, cifra `FT TYPE="NUMBER"` y referencia de imagen `INCL.ELEMENT`. Incluye la referencia al TIFF `C_202600406LT.000102.fmx.tif`.

## 3. Campos numismáticos comprobados

| Campo | Español | Lituano |
|---|---|---|
| País emisor | Lituania | Lietuva |
| Tema | Regiones etnográficas lituanas, Lituania Menor | Lietuvos etnografiniai regionai, Mažoji Lietuva |
| Diseñador de la cara nacional | Rolandas Rimkūnas | Rolandas Rimkūnas |
| Autor del escudo regional | Arvydas Každailis | Arvydas Každailis |
| Tirada estimada | 500.000 | 500000 |
| Fecha de emisión | Cuarto trimestre de 2025 | 2025 m. ketvirtasis ketvirtis |
| Descripción del diseño | Presente | Presente |
| Referencia a imagen | Presente | Presente |

En el XML lituano se observaron además estas construcciones útiles para extracción:

- `<DATE ISO="20260121">`: fecha de publicación.
- `<FT TYPE="NUMBER">500000</FT>`: cifra de tirada.
- `<HT TYPE="BOLD">`: rótulos de los campos.
- `<INCL.ELEMENT ... TYPE="TIFF"/>`: referencia al recurso gráfico.
- `<P>`: párrafos del contenido.
- El texto del valor sigue siendo lingüístico; el parser debe asociar rótulos y párrafos, no asumir que todos los campos están en etiquetas semánticas específicas.

## 4. Conclusión técnica y límites

### Verificado

1. El endpoint SPARQL devuelve las expresiones, idiomas, manifestaciones, formatos e Items de este aviso.
2. La jerarquía WEMI permite localizar recursos `pdfa2a`, `fmx4` y `xhtml` en ambos idiomas.
3. El Item Formex español se descarga como paquete ZIP con XML y TIFF.
4. El XHTML español se puede abrir directamente en navegador.
5. El XML Formex español y el XML principal lituano contienen los campos numismáticos necesarios para una ficha de staging.
6. La estructura XML se conserva entre los dos idiomas probados, aunque los valores textuales estén traducidos.

### No verificado todavía

- Automatización desatendida desde un script propio, incluyendo tratamiento de errores, reintentos, paginación y cambios.
- Generalización a otros avisos, tipos de publicación, emisores y estructuras Formex.
- Extracción robusta de campos mediante un parser ejecutable y tests.
- Cobertura y estabilidad de una búsqueda de avisos numismáticos a escala.
- Política de reutilización aplicable a cada texto, documento e imagen concretos. La disponibilidad técnica no concede por sí misma derechos sobre imágenes de diseños monetarios.

**No se ha escrito código de producto ni un importador. No se ha incorporado ninguna imagen.** Se mantiene D-008 y la revisión humana antes de aceptar datos en el catálogo.

## 5. Próximo paso recomendado

Hacer una segunda prueba con otro aviso de moneda euro, preferiblemente de otra clase (por ejemplo, una nueva cara nacional regular en vez de una conmemorativa de 2 €). Después, definir un pequeño mapeo Formex → staging con ejemplos y tests, sin conectarlo aún al catálogo de producto.


## 6. Segunda prueba: Mónaco — C/2026/419

**Fecha de validación:** 2026-11-25  
**Aviso:** [EUR-Lex C/2026/419 — Mónaco](https://eur-lex.europa.eu/eli/C/2026/419/oj/eng)

### Resultado observado

- La consulta SPARQL permitió localizar el Work, sus Expressions, Manifestations e Items.
- La Expression inglesa (ENG) ofrece tres formatos: `pdfa2a`, `fmx4` y `xhtml`.
- El Item Formex se descargó manualmente como ZIP con **3 XML y 8 TIFF**.
- XML principal: `C_202600419EN.000101.fmx.xml`.
- El XML principal contiene información estructurada de las **ocho denominaciones**, el país emisor, la fecha de emisión y las descripciones de diseño. También recoge datos específicos de la moneda de 2 €, incluida la ceca y la inscripción del canto.

### Interpretación y límites

La segunda prueba confirma que CELLAR permite recuperar y leer un paquete Formex de otro aviso numismático y de otro emisor (Mónaco), y que el XML puede contener datos estructurados para varias denominaciones y detalles técnicos adicionales. Amplía la evidencia más allá del aviso lituano C/2026/406.

La ejecución sigue siendo **manual**. No demuestra automatización general, robustez frente a otros formatos/avisos ni un parser probado. La descarga de TIFF tampoco concede derechos para reutilizar las imágenes; no se incorpora ningún TIFF al catálogo ni al repositorio y se mantiene D-008.

### Conclusión actualizada

Hay dos pruebas manuales positivas con avisos distintos: C/2026/406 (Lituania, dos expresiones lingüísticas) y C/2026/419 (Mónaco, ocho denominaciones). La evidencia respalda la viabilidad de CELLAR/Formex como fuente de investigación para metadatos numismáticos, pero no justifica todavía implementar una ingesta automática ni reutilizar imágenes.

### Pendiente

1. Probar la descarga y el tratamiento mediante un script controlado, incluyendo errores, reintentos y trazabilidad, antes de hablar de automatización.
2. Diseñar un mapeo mínimo Formex/XML → staging con tests y revisión humana; todavía no desarrollar el parser.
3. Verificar por separado cualquier derecho de reutilización antes de incorporar imágenes; por defecto, excluir los TIFF.


## 7. Detección de nuevos avisos: CELLAR RSS/Atom y alertas EUR-Lex

**Fecha de investigación:** 2026-11-25  
**Estado:** documentación oficial revisada; no se ha ejecutado el feed ni creado una alerta en una cuenta.

### CELLAR RSS/Atom

La documentación oficial de CELLAR describe un feed de notificaciones de ingestión que cubre EUR-Lex y otras publicaciones de la Oficina de Publicaciones. El canal relevante es ingestion. Admite los tipos CREATE, UPDATE y DELETE, y filtros por fechas y clases WEMI (work, expression, manifestation, item, entre otras). La documentación indica que los resultados pueden paginarse cuando superan 1.000 entradas.

Las entradas incluyen identificador del evento, cellarId, rootCellarId, tipo, clases, identificadores asociados (por ejemplo CELEX) y fecha de ingestión. No se documenta un filtro temático específico para monedas: el feed es general y los candidatos numismáticos tendrían que filtrarse después mediante metadatos/título y, cuando proceda, SPARQL.

Ejemplo oficial de endpoint documentado:

    http://publications.europa.eu/webapi/notification/ingestion?startDate=2016-07-01&endDate=2016-07-31&type=UPDATE&wemiClasses=work,event&page=3

La documentación admite negociación de contenido RSS o Atom mediante Accept: application/rss+xml o Accept: application/atom+xml. No se ha probado aquí una consulta real al endpoint, su paginación ni su comportamiento operativo.

### Alertas RSS de EUR-Lex

EUR-Lex permite generar RSS a partir de búsquedas guardadas y recibir nuevos documentos que coincidan con los criterios. También ofrece alertas asociadas a documentos y procedimientos. La configuración de búsquedas guardadas requiere cuenta e inicio de sesión EU Login; el límite documentado es de 50 búsquedas guardadas, compartido con las alertas por correo.

Para avisos numismáticos de monedas euro, los títulos observados incluyen al menos las variantes “New national side of euro coins intended for circulation” y “New national sides of euro circulation coins”. Una búsqueda temática debería contemplar ambas variantes y comprobarse con ejemplos históricos antes de considerarse suficientemente exhaustiva. No se ha creado ni probado una alerta en una cuenta del usuario.

### Comparación y recomendación

- **CELLAR RSS/Atom:** mejor candidato como mecanismo técnico principal de seguimiento, por ofrecer eventos de ingestión y cambios con identificadores CELLAR/WEMI trazables. Requiere recuperar y filtrar el flujo general; no es una alerta numismática ya configurada.
- **EUR-Lex RSS:** útil como detector temático secundario y contraste, mediante una o varias búsquedas guardadas. Depende de la configuración de una cuenta EUR-Lex y no sustituye la trazabilidad de eventos de CELLAR.
- **Estrategia recomendada para una futura prueba:** consultar periódicamente CELLAR ingestion, filtrar candidatos por metadatos/títulos y contrastarlos con una búsqueda guardada RSS de EUR-Lex. Deduplicar por identificador del documento lógico (rootCellarId y/o ELI/CELEX cuando estén disponibles), conservando cellarId e identificador de evento para rastrear versiones y modificaciones. Agrupar expresiones lingüísticas en una sola ficha lógica.
- Todo candidato debe entrar en staging y pasar revisión humana; nunca incorporarse directamente al catálogo.

### Límites

La investigación no acredita cobertura exhaustiva de publicaciones, cuotas, SLA, frecuencia de consulta permitida ni estabilidad operativa. Tampoco demuestra que una alerta personal EUR-Lex pueda integrarse como backend sin depender de la cuenta. Ambos mecanismos se refieren a publicaciones de la UE y no resuelven la cobertura mundial del catálogo. No se ha implementado código ni configurado ninguna alerta.


## 8. Prueba operativa del feed CELLAR RSS/Atom — 25/11/2026

**Rama:** `research/source-automation-2026-11`  
**Fase:** 0 — investigación, sin código de producto.  
**Estado:** bloqueada por conectividad DNS del entorno de ejecución; no se demuestra un fallo de CELLAR.

### Alcance intentado

Se intentó acceder al endpoint oficial de notificaciones de ingestión mediante HTTPS y realizar una petición filtrada para inspeccionar eventos. También se comprobó la resolución DNS de dominios externos de control y de EUR-Lex.

### Resultado y diagnóstico

Las peticiones desde el entorno de ejecución no pudieron llegar al servicio: la resolución DNS devolvió `Temporary failure in name resolution`, también para dominios de control ajenos a CELLAR. Por tanto, el fallo observado pertenece a la conectividad/DNS del entorno de esta sesión. **No es evidencia de indisponibilidad ni de un defecto del servicio CELLAR.**

No se obtuvieron respuestas HTTP del endpoint. En consecuencia, esta sesión no ha verificado operativamente:
- estructura real de una entrada RSS/Atom ni sus namespaces;
- valores efectivos y formato de los identificadores `id`, `cellarId`, `rootCellarId`, tipo, clases, identificadores asociados y fecha;
- semántica y límites de los filtros `startDate`, `endDate`, `type` y `wemiClasses`;
- paginación, número de elementos por página ni estabilidad del recorrido;
- recuperación de metadatos de un recurso notificado mediante CELLAR/SPARQL o negociación HTTP.

La estructura y los parámetros descritos en la sección anterior siguen siendo **documentación esperada**, no observaciones de una respuesta real obtenida en esta prueba.

### Identidad y deduplicación: hipótesis de trabajo

Mantener separados tres niveles:
1. **Evento:** identificador de evento `id`; permite distinguir CREATE/UPDATE/DELETE y conservar el historial.
2. **Recurso WEMI:** `cellarId`; identifica el recurso concreto afectado, por ejemplo una expresión o manifestación.
3. **Documento lógico:** `rootCellarId` y, cuando esté disponible, ELI/CELEX; sirven para agrupar recursos y versiones lingüísticas del mismo aviso.

No deduplicar exclusivamente por `cellarId` ni descartar eventos UPDATE/DELETE. Agrupar idiomas bajo el documento lógico, conservando cada expresión y recurso como evidencia. Esta es una estrategia propuesta a partir del modelo documentado; debe contrastarse con eventos reales antes de implementarla.

### Contraste de avisos conocidos

Se confirma documentalmente que C/2026/406 (Lituania) y C/2026/419 (Mónaco) son avisos numismáticos y que sus títulos presentan variantes textuales. No se pudo comprobar que el feed devuelva eventos correspondientes a esos avisos, ni su distribución por idioma o clase WEMI. La consulta de publicaciones conocidas no equivale a verificar presencia en el feed.

### Próxima prueba necesaria

Repetir la prueba desde un entorno con salida DNS/HTTPS funcional, usando ventanas temporales pequeñas y filtros controlados. Guardar respuestas RSS y Atom originales, registrar cabeceras y URLs solicitadas, probar cada filtro por separado, comprobar paginación con un conjunto que supere el límite documentado y seguir al menos un evento hasta sus metadatos WEMI. Contrastar después los identificadores con C/2026/406 y C/2026/419. No configurar alertas personales ni desarrollar parser o automatización permanente.

**Conclusión:** prueba operativa inconclusa por limitación del entorno. CELLAR no queda validado ni refutado en esta sesión. Se mantienen D-008, staging y revisión humana; no se incorpora ningún dato o imagen al catálogo.


## 9. Prueba operativa de filtros CELLAR RSS/Atom — 25/11/2026

**Estado:** prueba manual positiva de los filtros básicos desde PowerShell del usuario. Esta sección actualiza y complementa la sección 8: el bloqueo DNS correspondía al entorno de ejecución del agente, no al equipo/red desde el que el usuario ejecutó las peticiones.

### Entorno y petición

Endpoint:

    https://publications.europa.eu/webapi/notification/ingestion

Cabecera:

    Accept: application/atom+xml

Ventana temporal utilizada en las pruebas:

    startDate=2026-11-19&endDate=2026-11-25

El usuario ejecutó las peticiones desde PowerShell. Para la consulta sin filtros se obtuvo HTTP 200, Content-Type `text/xml;charset=UTF-8`, XML Atom válido, página 1, 1.000 entradas y `moreEntries=true`.

### Resultados observados

| Prueba | Resultado comunicado | Evaluación |
|---|---|---|
| Sin filtros | HTTP 200; 1.000 entradas; `moreEntries=true`. Las dos primeras entradas inspeccionadas eran eventos `update`, de clases `EVENT` y `DOSSIER`. | Feed accesible y respuesta Atom válida. La página no representa necesariamente toda la ventana temporal. |
| `type=create` | Las primeras tres entradas inspeccionadas eran `create`, con clases `MANIFESTATION`, `ITEM` y `MANIFESTATION`. | Resultados observados coherentes con el filtro de tipo. |
| `type=update` | Las primeras cinco entradas inspeccionadas eran `update`, de clases `EVENT`, `DOSSIER`, `WORK`, `MANIFESTATION` y `EXPRESSION`. | Resultados observados coherentes con el filtro de tipo. |
| `wemiClasses=DOSSIER` | Las diez primeras entradas inspeccionadas eran `update DOSSIER`. | Resultados observados coherentes con el filtro de clase WEMI. |
| `type=create&wemiClasses=ITEM` | HTTP 200; 1.000 entradas; `moreEntries=true`. Las diez primeras entradas inspeccionadas eran `create ITEM`. | Combinación de filtros aceptada; los resultados inspeccionados cumplen ambos criterios. |

No se comunicaron los códigos HTTP ni los recuentos de las pruebas individuales `type=create`, `type=update` y `wemiClasses=DOSSIER`; no se atribuyen aquí valores no observados.

### Conclusiones verificadas

1. El endpoint de ingestion responde desde el entorno del usuario y entrega XML Atom.
2. Los filtros `type` y `wemiClasses` aceptan los valores probados y devuelven primeras entradas coherentes con ellos.
3. La combinación `type=create` + `wemiClasses=ITEM` también devuelve resultados coherentes con ambos filtros.
4. La respuesta puede alcanzar 1.000 entradas y señalar que hay más resultados mediante `moreEntries=true`.

La evidencia confirma operativamente el acceso y el comportamiento básico de los filtros en las entradas inspeccionadas. No demuestra que se haya inspeccionado exhaustivamente todo el conjunto devuelto ni que todos los registros de la ventana cumplan el filtro.

### Límites que siguen abiertos

- **Paginación:** no probada. No se ha recuperado la ventana completa ni determinado el total de eventos.
- **Valores múltiples de `wemiClasses`:** no probados.
- **Eventos DELETE:** no probados.
- **Cobertura numismática:** no se ha demostrado que los avisos C/2026/406 o C/2026/419 aparezcan en el feed ni se ha validado un método exhaustivo para detectar avisos de monedas.
- **Campos de las entradas:** en la salida de PowerShell de las dos primeras entradas sin filtros, `title`, `summary`, `id` y `link href` aparecieron como cadenas plantilla `$item.*`. No se ha determinado si se trata de un problema de representación/consulta o del contenido recibido; no deben tratarse todavía como campos utilizables sin una inspección específica.
- **Automatización:** todas las pruebas fueron manuales. No existe un cliente, parser, sincronizador ni proceso programado.
- **Identidad y deduplicación:** la hipótesis de la sección 8 basada en `id`, `cellarId` y `rootCellarId` sigue pendiente de validación con eventos inspeccionados en profundidad.

### Próximo paso recomendado

En una tarea separada, comprobar la paginación con una ventana que devuelva más de 1.000 entradas: conservar la primera respuesta y seguir el mecanismo de continuación que indique el propio feed, verificando ausencia de huecos y duplicados. No abordar todavía automatización permanente ni parser. Después podrán probarse valores múltiples de `wemiClasses`, eventos DELETE y la resolución de metadatos de un evento concreto.

**Conclusión:** CELLAR ingestion y los filtros básicos quedan validados manualmente en el entorno del usuario. La paginación y la detección numismática fiable siguen pendientes. Se mantienen Fase 0, D-008, staging y revisión humana; no se incorpora ningún dato ni imagen al catálogo.
