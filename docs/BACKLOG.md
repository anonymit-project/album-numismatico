# Backlog

Prioridad orientativa. No implica autorización para saltarse el cierre de Fase 0.

## Fase 0 — Descubrimiento (actual)

**Criterio obligatorio:** solo incorporar datos e imágenes con derechos de reutilización claros y compatibles. No contactar con proveedores para pedir permisos o aclaraciones. Ante ambigüedad, excluir el material o conservar únicamente un enlace de referencia.

- [x] Comparar Numista, Wikidata/Wikimedia Commons, fuentes oficiales y datasets abiertos a nivel documental.
- [x] Verificar licencias generales de Wikidata, Commons, Natural Earth e ISO; documentar restricciones de imágenes oficiales euro/peseta.
- [x] Verificar cuota/precio y condiciones de Numista; documentar riesgo contractual para una PWA privada multiusuario.
- [x] Documentar límites operativos actuales de Wikimedia API y Wikidata SPARQL.
- [x] Excluir Numista de la ingesta y de la aplicación: sus condiciones no garantizan el uso previsto y no se solicitarán excepciones.
- [x] Realizar prueba documental de cobertura con ejemplos concretos de pesetas, euros regulares y conmemorativos, billetes españoles, Andorra, Cuba CUP/CUC, Ecuador sucre/USD y monedas XOF/XAF.
- [x] Revisar ejemplos individuales de imágenes Commons y separar licencia de la fotografía de derechos/reglas del diseño monetario; no aprobar assets en esta iteración.
- [x] Evaluar Nomisma, Syllogeum y CANOA; confirmar que su cobertura es principalmente de moneda antigua y no satisface el catálogo moderno.
- [x] Identificar NumisLib como candidato auxiliar, pendiente de verificar licencia exacta y trazabilidad de la base.
- [ ] Identificar dataset especializado de monedas y billetes modernos con licencia explícita compatible y mantenimiento suficiente.
- [x] Buscar fuentes primarias y estructuradas para Cuba CUP/CUC: se localizaron normas de emisión y retirada, pero no catálogo abierto ni API. Se mantiene el bloqueo de ingesta automatizada.
- [x] Verificar las interfaces oficiales de EUR-Lex/CELLAR (SOAP/XML, REST, SPARQL, RSS/Atom y Formex) y localizar avisos reales de monedas euro.
- [x] Ejecutar manualmente consulta SPARQL para C/2026/406 y recuperar los recursos WEMI en español y lituano; se obtuvieron seis bindings.
- [x] Recuperar y examinar XHTML español y Formex/XML en español y lituano para C/2026/406; validar manualmente la presencia de campos numismáticos.
- [ ] Implementar y probar un parser/mapeo Formex/XML → staging con tests; no es código de producto.
- [x] Documentar estructura HTML, enlaces y categorías históricas de BEAC/BCEAO, con propuesta de extracción controlada de metadatos. No se ha localizado API/feed específico.
- [x] Confirmar que las páginas institucionales de BEAC/BCEAO/Cuba no aportan licencia abierta general para sus imágenes; mantener placeholders. La brochure oficial BEAC incluye prohibición expresa de reproducción.
- [ ] Validar el modelo con Andorra, Cuba CUP/CUC, Ecuador, euro, CFA, peseta y estados históricos.
- [ ] Definir tratamiento cartográfico de microestados, territorios y estados desaparecidos.
- [ ] Resolver valoración de monedas sin cotización y equivalencias históricas.
- [ ] Proponer escala sencilla de conservación.
- [ ] Definir moderación de contribuciones e imágenes aportadas por usuarios.
- [ ] Validar mockups con el usuario y su amigo.
- [ ] Verificar cuotas gratuitas y condiciones actuales de backend, hosting, almacenamiento y servicios de identificación.
- [ ] Validar proveedor FX. El BCE ofrece SDMX y tipos de referencia diarios para una selección de divisas; no cubre necesariamente todas las monedas históricas o exóticas y sus tipos son informativos.
- [ ] Obtener aprobación expresa para cerrar Fase 0.

## Fase 1 — MVP (bloqueada hasta aprobar Fase 0)

- [ ] Crear PWA móvil primero y despliegue gratuito.
- [ ] Autenticación y colecciones privadas con control de acceso.
- [ ] Catálogo semilla acotado y trazable, basado solo en datos con derechos compatibles.
- [ ] Álbum por emisor/país, moneda, serie y pieza.
- [ ] Selector visible de país/emisor.
- [ ] Orden por denominación y filtros de monedas/billetes.
- [ ] Persistencia de filtros y preferencias por usuario, sincronizada entre dispositivos.
- [ ] Marcar posesión/cantidad; faltantes atenuados.
- [ ] Importación CSV/XLSX básica.
- [ ] KPIs básicos, modo oscuro, tests y CI.

## Fases posteriores

- Mapa plano/globo, estadísticas avanzadas y asistente por lotes.
- Wishlist, duplicados, exportación y backups automatizados.
- Identificación asistida por foto, solo si se mantiene gratuita y privacidad aceptable.
- Catálogo ampliado, importadores y contribuciones moderadas.
- Compartición voluntaria de solo lectura e intercambio asistido.


## Investigación operativa — siguiente bloque técnico (sin código de producto)

- [x] Ejecutar en el editor oficial la consulta SPARQL preparada para C/2026/406; confirmar URIs de Expression, Manifestation e Item y formatos PDF/A, Formex y XHTML en español y lituano.
- [x] Recuperar el XML Formex por navegador/descarga y validar manualmente el mapeo de campos en dos expresiones lingüísticas del mismo aviso. Evidencia en [`docs/CELLAR_POC.md`](CELLAR_POC.md).
- [x] Validar un segundo aviso: C/2026/419 (Mónaco). SPARQL localizó Work/Expressions/Manifestations/Items; la Expression ENG ofrece `pdfa2a`, `fmx4` y `xhtml`; Formex descargado como ZIP con 3 XML y 8 TIFF. El XML principal `C_202600419EN.000101.fmx.xml` contiene ocho denominaciones y datos de emisor, fecha, diseños, ceca y canto de la moneda de 2 €. Prueba manual, sin demostrar automatización general ni derechos de imágenes; detalle en `docs/CELLAR_POC.md`.
- [ ] Implementar y probar un parser/mapeo pequeño Formex/XML → staging con tests; conservar procedencia por campo y revisión humana.
- [x] Investigar y documentar CELLAR RSS/Atom frente a alertas RSS de EUR-Lex; recomendación híbrida y limitaciones en docs/CELLAR_POC.md.
- [ ] **Pendiente por bloqueo del entorno:** ejecutar la prueba operativa del feed CELLAR (estructura real de eventos, identificadores, filtros, paginación y recuperación de metadatos). El intento del 25/11/2026 no obtuvo respuesta HTTP por fallo DNS general del entorno; no es un fallo demostrado de CELLAR. Repetir desde un entorno con DNS/HTTPS funcional. Detalle en `docs/CELLAR_POC.md`.
- [ ] Configurar y validar, con autorización y acceso del usuario a EUR-Lex, una búsqueda guardada RSS para las variantes de títulos numismáticos; no se ha creado ninguna alerta.
- [ ] Crear manifiesto versionado de URLs BEAC/BCEAO por familia, estado legal, país y fecha de consulta; validar cambios de HTML antes de automatizar extracción.
- [ ] Comprobar individualmente las condiciones de reutilización de cada PDF o texto de BEAC/BCEAO antes de almacenar copias; no extraer imágenes.
- [ ] Continuar Cuba solo con ejemplares oficiales de la Gaceta y catálogos institucionales accesibles; mantener las copias secundarias como pistas, no como autoridad de importación.

**Límite actual de la validación CELLAR:** pruebas manuales positivas para C/2026/406 (Lituania) y C/2026/419 (Mónaco). La investigación de RSS/Atom y alertas EUR-Lex es documental; no acredita ejecución del feed, alerta configurada, automatización desatendida, parser probado, cobertura general ni derechos de reutilización de imágenes.
