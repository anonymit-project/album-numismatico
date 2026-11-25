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
- [ ] Localizar una fuente primaria estructurada y reutilizable para el catálogo histórico de Cuba CUP/CUC.
- [ ] Verificar automatización concreta del Diario Oficial/Comisión UE para altas de monedas euro y conmemorativas.
- [ ] Verificar opciones de extracción/versionado por lotes de fuentes BEAC y BCEAO sin depender de imágenes sin licencia.
- [ ] Aprobar imágenes concretas solo tras verificar licencia de archivo y derechos/reglas de reproducción del objeto monetario; en caso contrario mantener placeholder.
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
