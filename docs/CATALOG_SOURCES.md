# Fuentes del catálogo y licencias

**Estado:** investigación pendiente. No importar ni redistribuir datos o imágenes hasta verificar las condiciones aplicables.

## Fuentes que deben evaluarse

| Fuente | Qué investigar | Riesgo/condición |
|---|---|---|
| Numista | API, cobertura, campos, cuota, caché, atribución, licencia de datos e imágenes por recurso | No asumir que la API gratuita autoriza copiar imágenes o redistribuir datos |
| Wikidata | Emisores, monedas, periodos, identificadores y calidad de statements | Verificar licencia, referencias y cobertura numismática |
| Wikimedia Commons | Imágenes de monedas y billetes, licencia individual y atribución | Licencia distinta por archivo; revisar restricciones y derechos de diseño |
| BCE y bancos centrales | Diseños euro, billetes vigentes, conmemorativas y datos oficiales | Comprobar reutilización de imágenes y marcas |
| ISO 4217 / ISO 3166 | Códigos actuales e históricos de monedas y emisores | Revisar acceso, formato y derechos de publicación |
| Catálogos/datasets abiertos | Cobertura, mantenimiento, estructura y licencia | No usar datasets sin licencia explícita compatible |

## Matriz de evaluación

Para cada fuente registrar: URL oficial, fecha de consulta, cobertura (monedas/billetes/periodos), campos disponibles, precisión y referencias, licencia de datos, licencia por imagen, atribución, caché, redistribución, uso comercial, API/cuotas, automatización y riesgos.

## Estrategia provisional

Construir un catálogo propio curado y versionado, con procedencia por registro y estados `seed`, `pending_review` y `verified`. Usar importadores reproducibles solo cuando las condiciones lo permitan. Cuando no se pueda copiar un recurso, guardar identificador y enlace externo o usar imágenes propias/autorizadas.

## Estado de verificación

Aún no hay fuente aprobada como origen de datos o imágenes del catálogo. Las notas de cuotas que aparecen en el PRD son hallazgos previos que deben revalidarse antes de depender de ellos.
