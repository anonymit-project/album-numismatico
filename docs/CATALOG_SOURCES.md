# Fuentes del catálogo y licencias

**Estado:** investigación documental inicial completada; selección de fuentes aún provisional.  
**Verificación:** 2026-11-25.  
**Regla:** no importar ni redistribuir datos o imágenes hasta validar las condiciones aplicables al recurso concreto y registrar su procedencia.

## Conclusión ejecutiva

**Política aprobada:** no se contactará con proveedores para pedir excepciones. Solo se reutilizarán datos o imágenes con una licencia pública explícita, dominio público verificable o permiso ya existente y aplicable. Si hay dudas, se excluye el recurso o se conserva únicamente el enlace de referencia.

No existe una única fuente que resuelva el catálogo mundial con cobertura, fiabilidad, licencia y automatización adecuadas. La estrategia recomendada es un **catálogo propio, pequeño, curado y versionado**, construido mediante fuentes complementarias:

1. **Fuentes oficiales de emisores y autoridades monetarias** para validar diseños, fechas y emisiones.
2. **Wikidata (CC0)** para entidades, monedas, identificadores y relaciones históricas; nunca como autoridad numismática única.
3. **Wikimedia Commons** como posible fuente de imágenes, siempre con revisión de licencia y derechos por archivo.
4. **Numista** queda excluida de la ingesta y de la aplicación: sus condiciones no garantizan el uso previsto.
5. **ISO 4217 / ISO 3166** como sistemas de códigos; no como catálogo numismático.
6. **Natural Earth** para geometrías cartográficas, no para definir emisores monetarios.

La automatización debe limitarse a importar cambios desde fuentes con derechos compatibles, generar propuestas y registrar diferencias. La aprobación de piezas numismáticas seguirá siendo curada.

## Matriz comparativa

| Fuente | Cobertura y utilidad | Derechos / licencia | Cuotas y automatización | Evaluación |
|---|---|---|---|---|
| [Numista API](https://en.numista.com/api/doc/) | Catálogo especializado de monedas y billetes; búsqueda, detalle e identificadores N#. Cobertura y calidad colaborativas, no garantizadas. | Licencia API no transfiere propiedad. Atribución Numista y N# obligatorios. Prohíbe distribución masiva, feeds y reconstrucción sistemática. Excepción de almacenamiento para proyecto personal privado, no público. Imágenes sujetas además a derechos/licencia indicados por recurso. | Plan gratuito: 2.000 peticiones/mes, sin búsqueda por imagen. Metadatos de endpoints concretos: caché hasta 7 días; otros datos no persistentes salvo excepción estricta de proyecto personal. Máximo 10 peticiones concurrentes. Plan de pago: 100 € de activación + mínimo 100 €/mes (sin IVA, con excepción del primer mes). | **Excluir.** No usar API, datos ni imágenes de Numista. No se solicitará aclaración ni excepción. |
| [Wikidata](https://www.wikidata.org/wiki/Wikidata:Licensing) | Emisores, estados históricos, monedas, fechas, códigos, relaciones y enlaces externos. Calidad desigual y cobertura numismática incompleta; los statements pueden carecer de referencias. | Datos estructurados bajo CC0. Imágenes y otros medios enlazados no heredan CC0: revisar su licencia individual. | SPARQL público: límites publicados sujetos a cambios; documentación actual indica aproximadamente 4 consultas/s y 240/min para clientes anónimos, con concurrencia limitada. Dumps JSON semanales e incrementales diarios disponibles; demasiado grandes para el uso inicial. | **Muy recomendable como enriquecimiento**, importación selectiva y reconciliación de entidades; no como fuente única ni como verdad automática. |
| [Wikimedia Commons](https://commons.wikimedia.org/wiki/Commons:Reusing_content_outside_Wikimedia/en) | Fotografías de monedas y billetes, a veces con anverso/reverso y buena documentación. Cobertura irregular. | Licencia por archivo: dominio público, CC BY, CC BY-SA u otras. Comprobar autor, licencia, atribución, modificaciones y restricciones ajenas al copyright. Commons no garantiza que la información de derechos sea correcta. | MediaWiki API con límites de velocidad introducidos en 2026 y sujetos a cambios. Recomienda User-Agent identificable, concurrencia ≤3 y respetar Retry-After. Metadatos de licencia pueden consultarse mediante imageinfo/extmetadata. | **Candidato preferente para imágenes**, con validación individual y registro de atribución/licencia. No descargar en lote indiscriminadamente. |
| [BCE — monedas euro](https://www.ecb.europa.eu/euro/coins/html/index.en.html) y [Diario Oficial UE](https://eur-lex.europa.eu/) | Denominaciones, caras comunes/nacionales y conmemorativas de 2 €. El Diario Oficial de la UE es la fuente multilingüe autoritativa de publicación de nuevos diseños; la web del BCE puede ir retrasada. | Copyright de cara común: UE/Comisión; caras nacionales: legislación del emisor. La reproducción de monedas euro tiene restricciones específicas; consultar Comisión y autoridad emisora. | Información pública y páginas descargables; no se ha verificado una API de catálogo ni una cuota automatizada estable. Automatizar consulta de publicaciones oficiales, no scraping agresivo. | **Fuente primaria de validación** para euro; imágenes sujetas a análisis jurídico aparte. |
| [BCE — billetes euro](https://www.ecb.europa.eu/euro/banknotes/images/html/index.en.html) | Series, denominaciones, elementos visuales y descargas oficiales de billetes euro. | Reproducciones digitales de billetes completos deben cumplir reglas ECB/2013/10: «specimen» diagonal, límites de tamaño de texto y máximo 72 dpi al 100 %. Las imágenes descargables de baja resolución ya incluyen «specimen». | Descarga manual disponible; imágenes HD solo para usos profesionales y bajo solicitud. No se ha identificado API de catálogo. | **Fuente oficial para metadatos e imágenes de referencia**, pero las imágenes con «specimen» pueden no ser adecuadas para la experiencia visual del álbum. |
| [Banco de España — Gabinete Numismático](https://www.bde.es/wbe/es/punto-informacion/contenidos/servicios/archivo-historico/colecciones-numismaticas/) | Colección institucional de moneda y billete español; fondos de billetes desde Banco de San Carlos (1783) y colecciones históricas. Recurso de consulta y bibliografía, no catálogo exhaustivo descargable. | No se ha localizado una licencia abierta general de imágenes/datos. La reproducción de imágenes de billetes euro y de billetes o monedas en pesetas requiere autorización del Banco de España según su trámite oficial. | No se ha verificado API pública ni cuota de automatización. | **Fuente de contraste histórico**, no asumir reutilización de sus imágenes. |
| [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) / [ISO 3166](https://www.iso.org/iso-3166-country-codes.html) | Códigos normalizados de monedas y países/subdivisiones, incluidos códigos históricos en las listas pertinentes. No describen diseños, emisiones ni todos los emisores numismáticos. | ISO permite uso gratuito de los códigos. La descarga de listas oficiales preparadas y actualizadas automáticamente puede depender de un servicio de pago. No copiar el texto íntegro de las normas ISO. | No se ha confirmado una API gratuita oficial para sincronización. Mantener un subconjunto versionado y revisar cambios publicados por ISO/maintenance agencies. | **Útiles como identificadores**, no como catálogo. Guardar código, fuente y fecha de revisión; permitir emisores sin código ISO. |
| [Natural Earth](https://www.naturalearthdata.com/about/terms-of-use/) | Geometrías geográficas y límites para mapa. No modela soberanía monetaria, reconocimiento ni emisores históricos con precisión numismática. | Datos en dominio público; uso y modificación permitidos sin atribución obligatoria. | Descargas de ficheros; no requiere API. Automatización por versión publicada. | **Recomendado para cartografía**, separado del modelo de emisores. |

## Condiciones y riesgos determinantes

### Numista: limitación contractual más importante

Los términos oficiales definen «Personal Project» como proyecto privado, no comercial, de una persona y no disponible al público general, clientes ni miembros de una organización. Permiten almacenar datos en ese supuesto, pero excluyen la publicación/redistribución, el acceso de terceros y el uso para operar un servicio comercial o públicamente disponible. También prohíben la recuperación sistemática para reproducir o sustituir el catálogo.

El proyecto prevé dos o tres usuarios y una PWA con cuentas. **No está claro que una aplicación alojada en internet, aunque esté protegida por login y limitada a amigos, entre en la excepción.** No intentaremos obtener una excepción: la fuente queda fuera del proyecto. La cuota gratuita de 2.000 peticiones no elimina estas restricciones. La API no debe ser una dependencia estructural.

La licencia API tampoco equivale a una licencia general de las fotografías. Dado que no vamos a integrar Numista, no utilizaremos sus imágenes.

### Imágenes de billetes y monedas: no confundir acceso con permiso

- Que una imagen sea descargable o aparezca en una API no implica permiso para redistribuirla.
- En Commons, la licencia se decide por archivo. Registrar URL de la página del archivo, autor, licencia/version, atribución, fuente original, fecha de comprobación y modificaciones.
- Para billetes euro, una reproducción digital completa está sometida a reglas anti-falsificación (incluido «specimen» y 72 dpi); las imágenes oficiales disponibles ya llevan esa marca.
- Para monedas euro, los derechos de las caras nacionales corresponden a los emisores; la cara común está protegida por la UE. La Comisión indica que la autorización de caras nacionales conmemorativas debe solicitarse a la autoridad competente.
- En España, el Banco de España exige autorización para reproducir imágenes de billetes euro y de billetes o monedas en pesetas, conforme a los requisitos publicados.
- Recomendación provisional: no mostrar reproducciones oficiales de billetes/monedas sin comprobar primero que el uso concreto cumple la normativa. Priorizar imágenes propias del usuario y archivos de Commons con licencia individual inequívoca y compatible. En cualquier otro caso, placeholder neutro.

## Arquitectura de ingesta recomendada

1. **Catálogo propio como fuente de verdad:** IDs internos estables y datos versionados en el repositorio.
2. **Procedencia por campo o afirmación:** fuente, URL, identificador externo, fecha de consulta, referencia documental y nivel de confianza. No basta con una fuente general por ficha si cada atributo procede de sitios distintos.
3. **Importadores pequeños y reproducibles:** Wikidata selectivo, publicaciones oficiales y datasets abiertos. Guardar respuestas originales solo si su licencia/condiciones lo permiten.
4. **Revisión humana:** los cambios externos generan propuestas/diffs; no sobreescriben automáticamente datos verificados.
5. **Identificadores externos desacoplados:** tabla external_reference(source, external_id, url, checked_at); permitir varias referencias por entidad.
6. **Derechos separados de los metadatos:** catalog_image debe almacenar titular/autor, licencia, versión, atribución, URL de página del archivo, URL del recurso, restricciones, fecha de verificación y estado de revisión.
7. **Sin imagen válida, hay ficha:** placeholder neutro. Nunca bloquear una pieza por falta de imagen.
8. **Sin API pública estable, no hay dependencia de runtime:** preferir ingesta por lotes y revisión, evitando que la aplicación falle cuando una fuente externa no responda.

## Evaluación de automatización y coste

| Fuente | Automatización inicial viable | Coste publicado / riesgo |
|---|---|---|
| Wikidata | Consultas SPARQL pequeñas o dumps incrementales; guardar IDs Q y referencias. | Sin tarifa por consulta publicada; límites y disponibilidad compartida, sujetos a cambios. |
| Commons | Búsqueda por API y extracción de metadatos por archivo; cola de revisión. | Sin tarifa API publicada; límites de velocidad nuevos en 2026. El coste real es la revisión de derechos. |
| BCE / Comisión / Diario Oficial | Revisar nuevas publicaciones de euro y cambios de páginas oficiales. | Sin precio de acceso identificado; automatización/API concreta pendiente de validar. |
| Banco de España | Consulta documental/manual y bibliografía. | Sin API abierta localizada; derechos de reproducción requieren atención específica. |
| ISO | Revisión periódica de códigos y cambios publicados. | Uso de códigos gratuito; servicio automatizado de listas puede ser de pago. |
| Numista | No se utilizará. | Plan gratuito limitado a 2.000 peticiones/mes; riesgo contractual incompatible con el criterio conservador adoptado. |
| Natural Earth | Descargar versión publicada y actualizar por lotes. | Dominio público. |

## Pendientes de verificación antes de aprobar fuentes

- Obtener respuesta escrita de Numista sobre el caso de uso exacto (PWA autenticada para 2–3 personas, alojamiento en internet, almacenamiento persistente de fichas y visualización a esos usuarios).
- Probar cobertura real con una muestra representativa: pesetas, euros regulares y conmemorativos, billetes españoles, Andorra, Cuba CUP/CUC, Ecuador, XOF/XAF y emisores históricos.
- Revisar individualmente los derechos de las imágenes concretas que se quieran incorporar, especialmente diseños protegidos de billetes y monedas.
- Comprobar si hay feeds, APIs o ficheros oficiales de la Comisión/diarios oficiales que permitan automatización fiable para monedas euro.
- Identificar datasets especializados abiertos y con licencia explícita para billetes/monedas históricas; no se ha confirmado todavía uno que cubra de forma suficientemente fiable el alcance del proyecto.
- Definir política de atribución y retirada de imágenes si cambia una licencia o aparece una reclamación.

## Fuentes oficiales consultadas (25/11/2026)

- [Numista API documentation](https://en.numista.com/api/doc/)
- [Numista API pricing](https://en.numista.com/api/pricing.php)
- [Numista API Terms of Use and License Agreement](https://en.numista.com/api/license.php)
- [Wikidata licensing](https://www.wikidata.org/wiki/Wikidata:Licensing)
- [Wikidata database downloads](https://www.wikidata.org/wiki/Wikidata:Database_download)
- [Wikidata Query Service access policy](https://www.wikidata.org/wiki/Wikidata:SPARQL_query_service/API)
- [Wikimedia Commons reuse policy](https://commons.wikimedia.org/wiki/Commons:Reusing_content_outside_Wikimedia/en)
- [Wikimedia API rate limits](https://www.mediawiki.org/wiki/Wikimedia_APIs/Rate_limits)
- [ECB — euro coins](https://www.ecb.europa.eu/euro/coins/html/index.en.html)
- [ECB — €2 commemorative coins](https://www.ecb.europa.eu/euro/coins/comm/html/index.en.html)
- [European Commission — copyright and reproduction of euro coins and notes](https://economy-finance.ec.europa.eu/euro/euro-coins-and-notes/copyright-and-reproduction-rules-euro-coins-and-notes_en)
- [ECB — banknote images and reproduction rules](https://www.ecb.europa.eu/euro/banknotes/images/html/index.en.html)
- [Banco de España — Gabinete Numismático](https://www.bde.es/wbe/es/punto-informacion/contenidos/servicios/archivo-historico/colecciones-numismaticas/)
- [Banco de España — autorización de reproducción](https://sedeelectronica.bde.es/sede/es/tramites/autorizacion-reproduccion-billetes-p55.html)
- [ISO 4217 currency codes](https://www.iso.org/iso-4217-currency-codes.html)
- [ISO 3166 country codes](https://www.iso.org/iso-3166-country-codes.html)
- [Natural Earth terms of use](https://www.naturalearthdata.com/about/terms-of-use/)
- [ECB SDMX web services](https://data.ecb.europa.eu/help/getting-data-web-services-sdmx-0)
- [ECB euro reference exchange rates](https://www.ecb.europa.eu/stats/policy_and_exchange_rates/euro_reference_exchange_rates/html/index.en.html)

**Nota de alcance:** esta investigación documental no sustituye asesoramiento jurídico ni constituye una auditoría de cada imagen o dataset. Las cuotas y políticas de servicios externos deben revalidarse antes de desplegar una integración.


## Fuentes oficiales de tipos de cambio (complementario)

El [BCE publica tipos de cambio de referencia frente al euro](https://www.ecb.europa.eu/stats/policy_and_exchange_rates/euro_reference_exchange_rates/html/index.en.html) para una selección de divisas, normalmente cada día hábil alrededor de las 16:00 CET (salvo cierres TARGET). Ofrece descargas CSV/XML y un servicio web SDMX para consulta automatizada ([documentación SDMX](https://data.ecb.europa.eu/help/getting-data-web-services-sdmx-0)).

- Son tipos informativos, no cotizaciones de transacción.
- La cobertura es una selección de monedas; no debe suponerse que incluya divisas históricas, exóticas, suspendidas o monedas sin mercado representativo.
- El BCE suspendió la publicación del tipo de referencia EUR/RUB desde marzo de 2022 por falta de representatividad.
- Recomendación: usarlo como fuente gratuita primaria para las divisas que cubre, guardar fecha y fuente de cada tasa y dejar sin valoración automática las monedas sin tipo fiable. Para monedas extinguidas, utilizar factores históricos de conversión documentados, no tipos FX actuales.

La API SDMX ofrece acceso programático a datos y metadatos; no se ha identificado una cuota numérica pública ni un precio por consulta en la documentación consultada. Deben respetarse las condiciones del portal y evitar asumir SLA o disponibilidad ilimitada.

## Bancos centrales y autoridades emisoras nacionales

No se ha localizado una API mundial común de bancos centrales. La estrategia realista es una lista de autoridades por emisor: banco central, tesoro, casa de moneda o imprenta oficial según quién publique la información. Sus webs y catálogos son fuentes primarias para emisiones y diseños, pero **no debe inferirse una licencia abierta por el mero hecho de que el contenido sea oficial**. Registrar condiciones de reutilización por país y por recurso; si no hay licencia clara, usar la fuente para verificar metadatos y conservar solo el enlace.
