# Fuentes del catálogo y licencias

**Estado:** prueba documental de cobertura completada; selección de fuentes aún provisional.  
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
| [Banco de España — Gabinete Numismático](https://www.bde.es/wbe/es/punto-informacion/contenidos/servicios/archivo-historico/colecciones-numismaticas/) | Colección institucional de moneda y billete español; fondos de billetes desde Banco de San Carlos (1783) y colecciones históricas. Recurso de consulta y bibliografía, no catálogo exhaustivo descargable. | No se ha localizado una licencia abierta general de imágenes/datos. La reproducción de billetes euro y de billetes o monedas en pesetas se rige por las condiciones y criterios específicos publicados por el Banco de España; comprobar el uso concreto antes de reutilizar. | No se ha verificado API pública ni cuota de automatización. | **Fuente de contraste histórico**, no asumir reutilización de sus imágenes. |
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
- En España, la reproducción de billetes euro y de billetes o monedas en pesetas está sujeta a los criterios específicos publicados por el Banco de España; no tratar la licencia de una fotografía como autorización automática para reproducir el diseño monetario.
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

- Ampliar la prueba de cobertura a más denominaciones, años y emisiones históricas; la muestra documental actual no equivale a un censo exhaustivo ni a una importación.
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
- [Banknotes.com — catálogo secundario de billetes de Cuba (solo referencia, no reutilización)](https://www.banknotes.com/cu.htm)\n- [ISO 4217 currency codes](https://www.iso.org/iso-4217-currency-codes.html)
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


## Prueba de cobertura con piezas y emisiones concretas (25/11/2026)

### Método y criterio de lectura

Se ha realizado una prueba documental de cobertura: localizar una fuente primaria o institucional que permita identificar ejemplos concretos, comprobar qué campos publica y separar el acceso a la información del permiso para reutilizar imágenes. No es un censo exhaustivo ni una importación de datos. No se han descargado ni incorporado imágenes al repositorio.

**Leyenda:** «metadatos» significa que la fuente permite contrastar al menos denominación, periodo/diseño o emisor; no implica que exista un fichero estructurado reutilizable. «Imagen de referencia» significa que se ve o descarga en la web de origen, no que se haya acreditado permiso de redistribución.

### Matriz de muestra

| Ámbito | Ejemplo comprobado | Fuente y cobertura observada | Resultado de reutilización |
|---|---|---|---|
| España — pesetas, moneda | 100 pesetas, 1992 | Commons contiene un archivo identificado como 100 pesetas, fechado en 1992, con autoría fotográfica y declaración de dominio público. | No importar por ahora: la licencia declarada de la fotografía no resuelve por sí sola las condiciones españolas aplicables a la reproducción de la moneda. |
| España — pesetas, billete | 1.000 pesetas, serie 1992; también hay categoría Commons con múltiples denominaciones y años | Commons permite localizar ejemplos y algunos ficheros muestran una licencia o declaración de dominio público. Banco de España publica reglas específicas para reproducir imágenes de billetes y monedas en pesetas. | Fuente de localización, no autorización suficiente. Placeholder hasta que la reproducción concreta encaje inequívocamente en las condiciones oficiales. |
| España — euro regular | Ocho denominaciones y tres diseños nacionales españoles en distintas series | BCE describe las ocho denominaciones y los diseños nacionales españoles, incluidas las series y el cambio de 2010/2015. | Metadatos utilizables como referencia. No reutilizar automáticamente las imágenes del BCE ni las fotos de Commons: los derechos del diseño y de la fotografía son capas distintas. |
| España — euro conmemorativo | Monedas de 2 € conmemorativas | El BCE mantiene un índice por países/años; identifica al Diario Oficial de la UE como publicación autoritativa de los nuevos diseños. | Buena fuente de metadatos y detección de novedades. Las imágenes de las caras nacionales no quedan abiertas por estar publicadas en el BCE/DOUE. |
| España — billete euro | Series 1 y Europa; ocho denominaciones en la familia euro | BCE ofrece imágenes oficiales digitales marcadas «SPECIMEN» y explica las condiciones de reproducción. | Candidato condicionado: solo usar la reproducción oficial que cumpla íntegramente las reglas (marca diagonal, proporciones, contraste, resolución máxima de 72 dpi al 100 % y fondo no confundible). No quitar la marca ni reconstruir una imagen limpia. |
| Andorra — euro | Ocho denominaciones; diseños nacionales descritos por el BCE y la AFA | AFA confirma el acuerdo monetario y la capacidad de Andorra para acuñar euros; BCE describe los motivos de las ocho denominaciones. | Cobertura de metadatos razonable para moneda euro. No se ha encontrado una licencia abierta general para las imágenes institucionales. |
| Cuba — CUP | Billetes del peso cubano de distintas emisiones; ejemplo histórico de 1 peso y emisiones recientes | El catálogo comercial Banknotes.com enumera referencias y diseños; la legislación identifica al Banco Central como emisor. La búsqueda no localizó un dataset oficial descargable con licencia abierta. | Referencias secundarias solo para orientar la investigación. No reutilizar imágenes ni datos extraídos de catálogos cerrados o sin licencia explícita. |
| Cuba — CUC | Billetes convertibles de 1, 3, 5, 10, 20, 50 y 100 CUC, con distintas fechas | Catálogos secundarios documentan la familia. La retirada oficial del CUC comenzó el 1/1/2021 y terminó el 30/6/2021; ISO 4217 registra CUC como código histórico retirado en junio de 2021. | El periodo histórico se puede modelar con fuentes oficiales/normalizadas; no hay base para importar imágenes o un catálogo completo con licencia abierta. |
| Ecuador — sucre | Sucre de 1884 a 2000; el BCE describe la historia y emisiones. Ejemplo: moneda de 1 sucre de 2000, conmemorativa y no puesta en circulación. | Museo Numismático y BCE publican artículos con descripciones y datos técnicos de piezas concretas; no se localizó una licencia abierta general para sus imágenes. | Buena fuente primaria de contraste histórico, no de redistribución de imágenes. El 1 sucre de 2000 debe etiquetarse como pieza no circulante/conmemorativa, no como moneda corriente. |
| Ecuador — dólar estadounidense | Monedas fraccionarias nacionales de 1, 5, 10, 25 y 50 centavos emitidas desde 2000; programa de acuñación 2023–2025 | BCE explica que Ecuador adoptó el dólar el 9/1/2000 y que el banco central continuó acuñando moneda fraccionaria nacional. | Metadatos oficiales verificables. No confundir moneda de curso legal USD con una emisión estadounidense: el emisor/diseño nacional debe quedar diferenciado. |
| XAF — BEAC | Billetes 2020 de 500, 1.000, 2.000, 5.000 y 10.000 CFA; series 2002 y 1992; monedas 2006 y nueva gama tipo 2024 | BEAC publica páginas separadas para billetes vigentes, antiguos y desmonetizados, y para monedas. La página histórica enumera los seis estados de la zona de emisión. | Buena cobertura institucional de familias y denominaciones. No se ha localizado licencia abierta de reutilización de las imágenes institucionales. |
| XOF — BCEAO | Billetes vigentes, billetes retirados y monedas en circulación; billetes anteriores a BCEAO por territorio | BCEAO separa las secciones de billetes vigentes, retirados, anteriores a BCEAO y monedas. La unión monetaria comprende ocho estados miembros. | Buena fuente primaria de familias y contexto histórico. No se ha localizado licencia abierta general para las imágenes. |

### Lectura de cobertura

- **Mejor cobertura institucional:** euro y CFA, porque BCE/Comisión, BEAC y BCEAO publican familias, denominaciones y diseños. La automatización debe ser específica por fuente; no se ha probado una API común.
- **Cobertura histórica razonable pero dispersa:** peseta y sucre ecuatoriano. Los bancos centrales y museos permiten contrastar piezas, pero no ofrecen un catálogo integral abierto listo para importar.
- **Principal laguna:** Cuba. Se pueden localizar referencias y ejemplos, pero no se ha identificado un catálogo público oficial con estructura y licencia reutilizable que cubra CUP y CUC.
- **Billetes:** la documentación institucional ayuda a reconocer series y denominaciones, pero los derechos de imagen son una barrera más fuerte que la disponibilidad visual.
- **No confundir país usuario con emisor:** XOF y XAF son dos monedas distintas y cada una corresponde a una autoridad monetaria supranacional; los países miembros usan la moneda común. El catálogo debe distinguir zona monetaria, autoridad emisora y países usuarios. Andorra y Ecuador también demuestran que el emisor de una moneda no siempre coincide con el país que la utiliza.

### Comprobación individual de imágenes y derechos

Se han localizado ejemplos concretos en Commons, entre ellos una fotografía de 100 pesetas de 1992 declarada de dominio público, un billete ecuatoriano de 100 sucres de 1992 bajo CC BY-SA 3.0 y una fotografía de una moneda española de 2 € bajo CC0. Estos ejemplos demuestran que Commons tiene material con licencias abiertas explícitas, pero **no bastan para aprobar su incorporación**: la licencia de la fotografía no necesariamente despeja los derechos o reglas de reproducción del diseño monetario representado, ni las condiciones de la jurisdicción correspondiente.

- **Pesetas (España):** el trámite del Banco de España contempla la reproducción de billetes euro y de billetes o monedas en pesetas. Para pesetas describe condiciones específicas: tamaño superior al doble o inferior a la mitad del original, un solo lado por soporte y restricciones adicionales para reproducciones de monedas. No dar por válida una imagen Commons sin comprobar también estas reglas y el uso concreto en pantalla.
- **Monedas euro:** la Comisión distingue cara común (derechos de la UE/Comisión, con reglas de reproducción específicas) y cara nacional (legislación del emisor). Para la cara nacional de monedas conmemorativas remite a la autoridad competente. La publicación en el BCE o en el Diario Oficial no equivale a una licencia abierta.
- **Billetes euro:** el BCE permite reproducciones digitales que cumplan sus criterios; sus imágenes oficiales de baja resolución ya incluyen «SPECIMEN». La reproducción completa en línea debe conservar la marca diagonal y no superar 72 dpi al tamaño original, además de cumplir los demás criterios publicados.
- **Cuba:** el Decreto-Ley 361/2018 establece autorización previa del Banco Central para usos publicitarios de imágenes o reproducciones de billetes y monedas que tengan o hayan tenido curso legal. No se ha encontrado una licencia abierta de las imágenes oficiales; quedan fuera de la ingesta.
- **Ecuador, Andorra, BEAC y BCEAO:** que una autoridad publique fotografías no acredita licencia de redistribución. Al no localizarse una licencia abierta explícita para los archivos examinados, se conservan como referencia y no se copian.
- **Commons:** validar siempre la página de archivo y su licencia, autor, procedencia y condiciones; registrar la fecha de revisión. Una etiqueta CC0/PD del fotógrafo no sustituye el análisis de derechos del objeto representado.

**Decisión operativa conforme a D-008:** para esta prueba no se aprueba ninguna imagen monetaria de terceros para incorporar al catálogo. Las imágenes institucionales se usarán como referencia visual y documental, no como assets. Se mantienen los placeholders y las fotos propias de los usuarios como vía segura de visualización, con tratamiento de privacidad ya previsto en el modelo.

### Datasets especializados: evaluación de encaje

| Proyecto | Licencia / tamaño publicado | Encaje con el catálogo del álbum |
|---|---|---|
| [Nomisma.org](https://www.nomisma.org/datasets) | Nomisma declara CC BY para los conceptos publicados en su dominio; los datasets contribuidos mantienen licencias propias (por ejemplo ODbL, CC0, CC BY o condiciones sin licencia indicada). | Infraestructura valiosa de linked open data, pero predominan moneda antigua, hallazgos y colecciones arqueológicas. No cubre de forma suficiente pesetas, euro moderno, billetes, CUP/CUC ni CFA. Evaluar dataset por dataset, no asumir licencia global. |
| [Syllogeum](https://syllogeum.org/data) | Release rights-clean v1.1: 118.883 sightings, 21.512 fichas de tipo, 237.699 imágenes y 9,7 GB. Los metadatos e imágenes conservan las licencias de sus colecciones de origen; el release incluye LICENSE-DATA.md. | Ejemplo positivo de auditoría de procedencia y exclusión de imágenes NC/ND/ambiguas. Es un archivo de moneda antigua, demasiado grande y fuera del alcance moderno prioritario. No incorporar. |
| [CANOA](https://canoanumis.org/en/data/) | Agregador de corpus de moneda antigua; base agregada ODbL 1.0, textos CC BY 4.0, código Apache 2.0; las imágenes siguen siendo © de los museos y las fuentes NC/ND mantienen sus licencias. | No cubre el catálogo moderno. La ODbL requiere revisar obligaciones de atribución y share-alike antes de mezclar bases; las imágenes no son reutilizables por defecto. No incorporar al MVP. |
| [NumisLib](https://numislib.com/) | El sitio anuncia una base abierta de 249 países y 170 monedas, pero en esta revisión no se pudo verificar un texto de licencia de la base descargable ni una versión/dataset con trazabilidad de piezas. | Posible apoyo para relaciones país-moneda, no catálogo numismático demostrado. Estado **VERIFICAR**; no importar hasta localizar licencia exacta, fuente de cada dato y cobertura de emisiones/piezas. |

**Conclusión de datasets:** Nomisma, Syllogeum y CANOA son proyectos reales y útiles en sus ámbitos, pero no resuelven el catálogo moderno mundial. NumisLib no pasa todavía el umbral de verificación de licencia. No se ha confirmado un dataset especializado apto para incorporar ahora.

### Fuentes consultadas en esta prueba

- [BCE — monedas euro](https://www.ecb.europa.eu/euro/coins/html/index.en.html)
- [BCE — monedas conmemorativas de 2 €](https://www.ecb.europa.eu/euro/coins/comm/html/index.es.html)
- [BCE — caras nacionales de 2 €](https://www.ecb.europa.eu/euro/coins/2euro/html/index.es.html)
- [Comisión Europea — derechos de autor y reproducción de monedas y billetes euro](https://economy-finance.ec.europa.eu/euro/euro-coins-and-notes/copyright-and-reproduction-rules-euro-coins-and-notes_en)
- [BCE — imágenes y reglas de reproducción de billetes euro](https://www.ecb.europa.eu/euro/banknotes/images/html/index.en.html)
- [Banco de España — autorización de reproducción](https://sedeelectronica.bde.es/sede/es/tramites/autorizacion-reproduccion-billetes-p55.html)
- [BOE — Ley 10/1975, art. 9](https://www.boe.es/buscar/act.php?id=BOE-A-1975-5294)
- [Commons — moneda española de 100 pesetas, 1992](https://commons.wikimedia.org/wiki/File:ESP-100ptas8.jpg)
- [Commons — billete ecuatoriano de 100 sucres, 1992](https://commons.wikimedia.org/wiki/File:Ecu_100S_AnRvCb_1K240px.jpg)
- [Commons — moneda española de 2 €, 1999](https://commons.wikimedia.org/wiki/File:Espagne_-_Pi%C3%A8ce_de_2_euros_1999.jpg)
- [AFA — monedas euro de Andorra](https://www.afa.ad/en/eu/monedes-en-euros)
- [BCE — Andorra](https://www.ecb.europa.eu/euro/coins/html/ad.en.html)
- [Museo Numismático del BCE Ecuador — monedas y billetes](https://museodelamoneda.bce.fin.ec/index.php/colecciones/monedas-y-billetes.html)
- [BCE Ecuador — seguridad en billetes y monedas](https://www.bce.fin.ec/seguridades-en-billetes-y-monedas/)
- [BCE Ecuador — el último sucre](https://museodelamoneda.bce.fin.ec/index.php/museo/item/132-el-%C3%BAltimo-sucre.html)
- [BEAC — historia de la emisión monetaria en África Central](https://www.beac.int/billets-pieces/histoire-franc-cfa/histoire-de-lemission-monetaire-afrique-centrale/)
- [BEAC — billetes de la gama 2020](https://www.beac.int/billets-pieces/signes-monetaires/billets-de-gamme-2020/)
- [BEAC — billetes demonetizados tipo 92](https://www.beac.int/billets-pieces/signes-monetaires/billets-demonetises/billets-de-gamme-1992/)
- [BCEAO — historia del franco CFA](https://www.bceao.int/fr/content/histoire-du-franc-cfa)
- [BCEAO — billetes retirados](https://www.bceao.int/album-photo/anciens-billets-de-la-bceao-retires-de-la-circulation)
- [BCEAO — billetes anteriores a BCEAO](https://www.bceao.int/album-photo/billets-anterieurs-la-bceao)
- [BCEAO — monedas en circulación](https://www.bceao.int/fr/content/pieces-en-circulation)
- [ISO 4217 Amendment 178 — retirada del CUC](https://www.six-group.com/dam/download/financial-information/data-center/iso-currrency/amendments/dl-currency-iso-amendment-178.pdf)
- [Bundesbank — metadatos de Cuba y fin del sistema CUP/CUC](https://www.bundesbank.de/resource/blob/710190/bdb65d76a0d2f93425fdb54224dc87ef/472B63F073F071307366337C94F8C870/metadaten-en-data.pdf)
- [Decreto-Ley 361/2018 — Banco Central de Cuba](https://233773342789-lic.s3.eu-central-1.amazonaws.com/attachments/legislation/cuba/Decreto%20No.361%20-%20Banco%20central%20de%20Cuba_14.09.2018.pdf)
- [Nomisma — datasets y licencias](https://www.nomisma.org/datasets)
- [Syllogeum — datos y procedencia](https://syllogeum.org/data)
- [CANOA — datos y licencias](https://canoanumis.org/en/data/)
- [NumisLib](https://numislib.com/)

**Alcance jurídico:** evaluación conservadora de fuentes públicas, no dictamen legal. No se han solicitado permisos ni aclaraciones a titulares, de acuerdo con D-008.


## Investigación operativa de fuentes y automatización (25/11/2026)

### 1. Euro: Diario Oficial, EUR-Lex y CELLAR

**Hallazgo:** existe una vía oficial estructurada y reutilizable para detectar y recuperar publicaciones sobre nuevas caras nacionales y emisiones conmemorativas. No hace falta depender de scraping visual del sitio del BCE.

- EUR-Lex ofrece un servicio web SOAP para usuarios registrados, con resultados XML. Es gratuito tras registro y tiene límites diarios de llamadas; sirve para buscar, pero no descarga directamente los documentos.
- El repositorio CELLAR de la Oficina de Publicaciones expone metadatos mediante SPARQL y REST, además de documentos en varios formatos. Para actos del Diario Oficial hay contenido en XML Formex; también se ofrecen HTML/XHTML y PDF cuando están disponibles.
- CELLAR ofrece feeds RSS y Atom de ingesta que notifican nuevas publicaciones y modificaciones de documentos/metadatos, incluso por idioma. El feed general puede ser voluminoso y no es, por sí solo, un feed filtrado de monedas.
- EUR-Lex dispone de RSS predefinidos para categorías del Diario Oficial L y C, y permite crear alertas RSS personalizadas para búsquedas/documentos cuando se inicia sesión. La serie C es relevante porque los avisos «New national side of euro coins intended for circulation» se publican ahí.
- La Comisión declara que publica descripciones de los nuevos diseños de monedas. Los avisos encontrados incluyen país emisor, tema de conmemoración, descripción del diseño, tirada estimada y fecha prevista de emisión. También se publican cambios de caras nacionales de monedas regulares (ejemplo: Mónaco, C/2026/419), por lo que el flujo no debe limitarse a 2 € conmemorativas.

**Ejemplos verificables de 2026:**
- [C/2026/406 — Lituania, moneda conmemorativa de 2 €](https://eur-lex.europa.eu/eli/C/2026/406/oj/eng)
- [C/2026/412 — Andorra, moneda conmemorativa de 2 €](https://eur-lex.europa.eu/eli/C/2026/412/oj)
- [C/2026/419 — nuevas caras nacionales regulares de Mónaco](https://eur-lex.europa.eu/eli/C/2026/419/oj/eng)

**Diseño de ingesta recomendado (propuesta, no implementada):**
1. Consultar publicaciones de la serie C mediante CELLAR SPARQL/REST o una alerta RSS de búsqueda EUR-Lex; no consumir sin filtrar el feed global de CELLAR.
2. Filtrar por el título estable «New national side of euro coins intended for circulation» y por el identificador/serie del Diario Oficial. Mantener también una búsqueda secundaria por términos multilingües para detectar cambios de redacción.
3. Obtener el registro/notice y el documento Formex/XML; conservar ELI, CELEX/PUB si existe, número del DOUE, fecha, idioma y URL estable.
4. Extraer campos en una tabla de staging: emisor, tipo (regular/conmemorativa), denominación si se indica, tema, descripción, diseñador, tirada estimada, fecha de emisión y fuente.
5. Generar propuesta de cambio para revisión humana. No crear una pieza definitiva ni sustituir una cara nacional de forma automática.
6. Reconciliar avisos repetidos o correcciones por ELI/identificador de publicación, no por título.

**Limitación pendiente:** se ha verificado la existencia de interfaces y formatos oficiales, y se han identificado ejemplos reales, pero no se ha ejecutado una consulta SPARQL ni configurado una alerta personalizada. La sintaxis final de consulta, los campos CDM más robustos y el comportamiento de paginación deben probarse antes de escribir el importador.

**Reutilización:** la Decisión 2011/833/UE establece reutilización general gratuita de documentos de la Comisión, sujeta a condiciones como citar la fuente y no alterar el sentido, pero excluye materiales que la Comisión no pueda reutilizar por derechos de terceros. Esto permite tratar los metadatos y textos oficiales como candidatos reutilizables con atribución; **no convierte automáticamente las imágenes de diseños monetarios en assets libres**. Las caras nacionales y los derechos de diseños/imágenes deben seguir verificándose por emisor y recurso. No copiar imágenes del DOUE en esta fase.

Fuentes:
- [EUR-Lex — servicio web SOAP/XML y registro](https://eur-lex.europa.eu/content/help/data-reuse/webservice.html?locale=es)
- [EUR-Lex — reutilización de contenido, CELLAR, REST, SPARQL y Formex](https://eur-lex.europa.eu/content/help/data-reuse/reuse-contents-eurlex-details.html?locale=es)
- [CELLAR — datos y servicios](https://op.europa.eu/en/web/cellar/cellar-data)
- [CELLAR — RSS y Atom](https://op.europa.eu/en/web/cellar/cellar-data/rss-and-atom-feeds)
- [EUR-Lex — alertas RSS predefinidas](https://eur-lex.europa.eu/content/help/search/predefined-rss.html)
- [Decisión 2011/833/UE sobre reutilización de documentos de la Comisión](https://eur-lex.europa.eu/eli/dec/2011/833/oj/spa)

### 2. BEAC (XAF): estructura y extracción controlada

**Hallazgo:** la BEAC mantiene una sección oficial organizada por familias y estados, con páginas HTML y documentos PDF descargables. No se ha identificado API pública, feed específico de emisiones ni dataset estructurado descargable.

- La página [Signes monétaires](https://www.beac.int/billets-pieces/signes-monetaires/) enlaza páginas diferenciadas para billetes 2020, billetes 2002, tipos antiguos, billetes demonetizados 1992/1982/1972, monedas 2006, nueva gama de monedas «Type 2024» y monedas demonetizadas.
- La ficha HTML de la gama 2020 describe cinco denominaciones (500, 1.000, 2.000, 5.000 y 10.000 XAF) y sus temas/iconografía. La información está en texto HTML, acompañada de imágenes.
- La sección de billetes demonetizados declara que las gamas 1972, 1982 y los tipos antiguos dejaron de tener curso legal el 1/4/2004; el canje en BEAC terminó el 30/9/2006. La ficha enlaza documentos de las familias.
- La sección de monedas demonetizadas publica una tabla con título, tamaño, ámbito y año; en la consulta aparece una nota de 2026 relativa a la demonetización de la antigua gama.
- Hay PDFs institucionales asociados a las familias y a la historia. Una brochure oficial de la BEAC contiene una prohibición expresa de reproducción o representación, total o parcial, del texto y/o billetes contenidos en esa publicación. Sus imágenes quedan descartadas; no se debe interpretar que la presencia de archivos descargables concede derechos.

**Extracción controlada recomendada:**
- Mantener un manifiesto pequeño de URLs oficiales por familia, con idioma, fecha de revisión, hash/contenido observado y enlace de origen.
- Extraer solo texto HTML visible: denominación, tipo/gama, fechas, estado legal, descripciones y enlaces documentales.
- Tratar los PDF como documentos de referencia; extraer metadatos textuales solo cuando el contenido y sus condiciones lo permitan. No guardar ni redistribuir imágenes.
- Registrar por separado la fecha de emisión, entrada en circulación, retirada de curso legal y fin del canje: no son el mismo evento.
- Toda modificación detectada genera una propuesta revisable. No inferir el estado actual solo por la existencia de una página bajo «signes monétaires».
- Revalidar con las decisiones y notas oficiales de demonetización, especialmente la nota de 2026 de monedas antiguas.

Fuentes:
- [BEAC — Signes monétaires](https://www.beac.int/billets-pieces/signes-monetaires/)
- [BEAC — Billets de la gamme 2020](https://www.beac.int/billets-pieces/signes-monetaires/billets-de-gamme-2020/)
- [BEAC — Billets démonétisés](https://www.beac.int/billets-pieces/signes-monetaires/billets-demonetises/)
- [BEAC — Pièces démonétisées](https://www.beac.int/billets-pieces/signes-monetaires/pieces-demonetisees/)
- [BEAC — brochure du 30ème anniversaire (incluye prohibición expresa de reproducción)](https://www.beac.int/wp-content/uploads/2016/11/billets-et-pieces-brochure-du-30eme-anniversaire.pdf)
- [Estatutos BEAC revisados en 2021, art. 74](https://www.beac.int/wp-content/uploads/2021/11/Statuts-de-la-BEAC-modifi%C3%A9s-2021.pdf)

### 3. BCEAO (XOF): estructura y extracción controlada

**Hallazgo:** la BCEAO también mantiene páginas HTML oficiales separadas por estado y tipo de pieza. No se ha identificado API pública, feed específico de emisiones ni dataset estructurado descargable.

- El índice [Billets et pièces](https://www.bceao.int/fr/content/billets-et-pieces) enlaza billetes con curso legal, billetes demonetizados, billetes anteriores a la BCEAO y monedas en circulación.
- La sección de billetes retirados organiza el material por cada uno de los ocho estados miembros; la sección de billetes anteriores a BCEAO es una categoría histórica separada.
- La página de monedas en circulación publica para las piezas de 500 y 200 FCFA fecha de puesta en circulación (24/12/2003), diámetro, grosor, peso, composición bicolor y temas de anverso/reverso. No es un inventario exhaustivo de todas las denominaciones.
- La página de historia del franco CFA distingue la zona UMOA/BCEAO (ocho miembros) de la zona CEMAC/BEAC (seis miembros); no se deben fusionar XOF y XAF en una moneda o autoridad única.

**Extracción controlada recomendada:**
- Mantener URLs de índice y páginas hijas por estado/serie; detectar altas o cambios en el HTML y en sus enlaces.
- Extraer texto técnico y cronológico, enlazando cada dato con su página concreta.
- Para galerías históricas, tratar cada imagen como referencia no reutilizable salvo licencia expresa del archivo; no descargar en lote.
- No asumir que la página «en circulation» enumera toda la familia: usarla como muestra parcial y mantener los huecos explícitos.
- Revisar la sección de billetes anteriores a BCEAO por país/territorio y periodo antes de modelar esos ejemplares.

Fuentes:
- [BCEAO — Billets et pièces](https://www.bceao.int/fr/content/billets-et-pieces)
- [BCEAO — Billets ayant cours légal](https://www.bceao.int/fr/content/billets-et-pieces)
- [BCEAO — Anciens billets retirés](https://www.bceao.int/album-photo/anciens-billets-de-la-bceao-retires-de-la-circulation)
- [BCEAO — Billets antérieurs à la BCEAO](https://www.bceao.int/album-photo/billets-anterieurs-la-bceao)
- [BCEAO — Pièces en circulation](https://www.bceao.int/fr/content/pieces-en-circulation)
- [BCEAO — Histoire du franc CFA et estados miembros](https://www.bceao.int/fr/content/histoire-du-franc-cfa)

### 4. Cuba (CUP/CUC): fuentes primarias y límite de cobertura

**Hallazgo:** se han encontrado instrumentos normativos primarios que permiten verificar hechos de emisión y algunos atributos, pero no un catálogo oficial abierto, estructurado y con licencia reutilizable para cubrir las series CUP/CUC.

- El [Decreto-Ley 361/2018 del Banco Central de Cuba](https://233773342789-lic.s3.eu-central-1.amazonaws.com/attachments/legislation/cuba/Decreto%20No.361%20-%20Banco%20central%20de%20Cuba_14.09.2018.pdf), publicado en la Gaceta Oficial, establece que el Banco Central tiene el derecho exclusivo de emitir moneda nacional y responsabilidad sobre billetes y monedas (art. 61). El art. 65 exige autorización previa del Banco Central para publicidad que utilice total o parcialmente billetes o monedas que tengan o hayan tenido curso legal o sus reproducciones. La tercera disposición especial también confirma que el Banco Central aprueba y supervisa emisiones numismáticas conmemorativas.
- Se localizó el texto de la [Resolución 357/1994 del Banco Nacional de Cuba sobre la emisión del peso convertible](https://www.oncubanews.com/wmag/wp-content/uploads/2013/12/5.01-Resoluci%C3%B3n-No.-357-de-de-20-de-diciembre-de-1994.-Sobre-la-emisi%C3%B3n-del-peso-convertible.pdf). Es una norma primaria reproducida en un servidor no institucional, no un repositorio oficial. El texto describe la emisión inicial de billetes CUC y enumera denominaciones de 1, 3, 5, 10, 20, 50 y 100 pesos convertibles, con rasgos de diseño y dimensiones. Sirve como pista documental para contrastar, no como dataset ni como permiso de reutilización.
- La [Resolución 50/2003](https://www.cibercuba.com/s/gacetaoficial/resolucion-50-de-2003-de-banco-central-de-cuba) documenta la desmonetización de billetes CUP impresos por el Banco Nacional hasta 1990. El texto se ha localizado en una reproducción secundaria de la Gaceta; conviene localizar el ejemplar oficial antes de utilizarlo como base de datos.
- Se encontró una referencia bibliográfica a un catálogo impreso del Museo Numismático del Banco Nacional de Cuba, «Cuba: Emisiones de Monedas y Billetes 1915–1980», con descripción de campos (fechas, impresor, colores, medidas, aleación, peso y diámetro). No se ha localizado un ejemplar digital oficial abierto ni licencia de reutilización; la referencia comercial no valida el contenido del libro.
- Las búsquedas en los dominios institucionales consultados no localizaron API, CSV, catálogo descargable ni política abierta de reutilización para diseños/imagenes CUP/CUC.

**Conclusión:** para Cuba se puede mantener un esqueleto cronológico apoyado en legislación y fuentes secundarias claramente etiquetadas, pero no generar una carga automática ni declarar completa ninguna serie. Las denominaciones de la Resolución 357/1994 corresponden a la emisión inicial descrita por ese texto, no prueban por sí solas todas las variantes, fechas o emisiones CUC posteriores.

**Restricción de imágenes:** no reutilizar billetes/monedas cubanos ni reproducciones de ellos. El art. 65 del Decreto-Ley 361/2018 exige autorización previa para usos publicitarios; D-008 prohíbe contactar para pedir excepciones. Mantener placeholders y enlaces de referencia. No se ha localizado licencia abierta que permita salvar esta restricción.

Fuentes:
- [Gaceta Oficial — Decreto-Ley 361/2018 (copia digital del texto oficial)](https://233773342789-lic.s3.eu-central-1.amazonaws.com/attachments/legislation/cuba/Decreto%20No.361%20-%20Banco%20central%20de%20Cuba_14.09.2018.pdf)
- [Resolución 357/1994 — texto reproducido, alojamiento no institucional](https://www.oncubanews.com/wmag/wp-content/uploads/2013/12/5.01-Resoluci%C3%B3n-No.-357-de-de-20-de-diciembre-de-1994.-Sobre-la-emisi%C3%B3n-del-peso-convertible.pdf)
- [Resolución 50/2003 — reproducción secundaria de la Gaceta Oficial](https://www.cibercuba.com/s/gacetaoficial/resolucion-50-de-2003-de-banco-central-de-cuba)
- [Referencia bibliográfica del catálogo del Museo Numismático 1915–1980](https://www.cubacollectibles.com/cuba-book-numismatic-museum-cat.html)
- [Bundesbank — metadatos sobre Cuba y unificación monetaria](https://www.bundesbank.de/resource/blob/710190/bdb65d76a0d2f93425fdb54224dc87ef/472B63F073F071307366337C94F8C870/metadaten-en-data.pdf)

### 5. Resultado operativo

| Fuente | Estructura encontrada | Automatización realista | Reutilización |
|---|---|---|---|
| EUR-Lex/CELLAR | SPARQL, REST, RSS/Atom, XML Formex, HTML/PDF | **Alta para detección y descarga de metadatos/textos**; falta probar consulta filtrada de monedas | Metadatos/textos sujetos a política de reutilización y derechos de terceros; imágenes monetarias excluidas por defecto |
| BEAC | HTML por familias/estado + PDFs | **Media**: extracción controlada por URLs conocidas y revisión de cambios; sin API localizada | No usar imágenes; brochure oficial prohíbe expresamente reproducción |
| BCEAO | HTML por categorías y país + galerías | **Media**: extracción controlada de textos y metadatos; sin API localizada | No se localizó licencia abierta de imágenes |
| Cuba CUP/CUC | Legislación y normas dispersas; catálogo impreso referenciado | **Baja**: investigación y curación manual; sin dataset ni API identificados | No usar imágenes; restricción legal y D-008 |

**Decisión de ingeniería recomendada, aún no implementada:** usar un pipeline de ingesta por lotes con manifiestos de fuentes, extracción de metadatos y staging de propuestas; no hacer scraping general ni cargar imágenes. EUR-Lex/CELLAR sería el primer adaptador automatizable. BEAC/BCEAO tendrían adaptadores de páginas específicas con revisión humana. Cuba seguiría como carga manual/documental hasta encontrar un catálogo primario reutilizable.

**Alcance jurídico:** revisión conservadora de documentación pública, no dictamen legal. No se ha contactado con proveedores, autoridades ni titulares; se mantiene D-008.


**Detalle técnico adicional verificado en la documentación de desarrollo CELLAR:** la Oficina de Publicaciones publica una guía para desarrolladores con ejemplo de consulta SPARQL y recuperación de ficheros. El grafo organiza cada publicación en jerarquía WEMI (Work, Expression, Manifestation, Item); el identificador/URL del fichero está en Item. La guía muestra el endpoint `https://publications.europa.eu/webapi/rdf/sparql` y descarga mediante URL de recurso CELLAR con negociación HTTP (por ejemplo, `Accept: application/zip;mtype=fmx4` y `Accept-Language`). Esto concreta el camino técnico y confirma que el adaptador no dependería de automatizar el HTML de EUR-Lex. La guía es un ejemplo de integración, no una consulta específica de monedas ya ejecutada. [Guía oficial de desarrolladores CELLAR](https://op.europa.eu/documents/d/cellar/cellar_ml_dataset_guide) · [Colección Postman oficial CELLAR](https://op.europa.eu/documents/d/cellar/cellartraining-postman_collection_january2025).
