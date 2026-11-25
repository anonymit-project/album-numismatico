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
