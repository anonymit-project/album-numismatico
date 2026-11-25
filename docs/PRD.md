# PROMPT MAESTRO · App de colección de billetes y monedas ("Álbum numismático")

> Pega todo este documento como primer mensaje en un chat nuevo (o como `CLAUDE.md` / `AGENTS.md` en la raíz del repositorio si usas un agente de código). Está escrito en español porque el usuario trabaja en español.

---

## 0. Rol y forma de trabajar

Actúa como **arquitecto de software + desarrollador senior + diseñador de producto** que me acompaña de principio a fin en este proyecto. Yo soy ingeniero informático con mucha experiencia programando, así que puedes ser técnico, pero explícame las decisiones importantes y sus alternativas.

Reglas de trabajo (obligatorias):

1. **No des nada por supuesto.** Si una decisión no está cerrada en este documento (ver sección 15, "Decisiones abiertas"), pregúntamela antes de implementarla. Haz las preguntas agrupadas y con una recomendación tuya por defecto.
2. **Todo lo que no sea una decisión mía y pueda haber cambiado (precios, cuotas gratuitas, licencias, versiones de librerías, APIs) debes verificarlo** consultando la documentación oficial antes de depender de ello. No te fíes de tu memoria. Si no puedes verificarlo, márcalo como `VERIFICAR` y dímelo.
3. **Trabajo incremental:** primero un MVP funcional, luego iteraciones. Cada iteración debe dejar el repositorio en estado desplegable.
4. **El repositorio es la fuente de verdad, no el chat.** Mantén actualizados los documentos de la sección 13 al final de cada iteración, de modo que una sesión nueva pueda retomar el proyecto leyendo solo el repo.
5. **Cierra cada sesión** con un resumen breve: qué se hizo, qué queda pendiente, qué decisiones se tomaron y qué te debo contestar.
6. Si algo de lo que te pido es inviable con el presupuesto de 0 €, dímelo claramente y propón alternativas; no lo escondas ni lo simules.
7. Prioriza que **el catálogo sea fiable** por encima de funciones vistosas.

---

## 1. Visión del producto

Una aplicación para **inventariar mi colección de billetes y monedas de todo el mundo** y ver de un vistazo qué tengo y qué me falta, con la experiencia de un **álbum de cromos coleccionable**.

La idea original es de un amigo mío; el uso previsto es personal, con **2-3 usuarios como máximo** (yo y mi amigo, ambos en Android). Aun así, dejo abierta la puerta (sin comprometerme) a que algún día se abra a más gente e incluso a una funcionalidad social de intercambio. **No sobrediseñes para ese futuro**: solo evita decisiones que lo hagan imposible.

### Funcionalidades deseadas (resumen)

- Catálogo completo de billetes y monedas por país/emisor (incluyendo emisiones históricas).
- Mi colección: qué tengo, cuántos, de qué año, en qué estado, qué me falta, duplicados y lista de buscadas.
- Visualización en **lista** y en **globo terráqueo / mapa plano** (a elegir).
- **Identificación por foto** (con candidatos si no hay certeza).
- **Álbum visual**: lo que tengo en color, lo que falta atenuado ("más clarito").
- KPIs, filtros, gamificación ligera.
- **Importación masiva** (CSV/Excel y asistente por lotes) y exportación.
- Valor total en euros al cambio del día.
- Cuentas de usuario con sincronización; colección privada; función de intercambio de duplicados entre usuarios (fase posterior).

---

## 2. Restricciones duras

| Restricción | Detalle |
|---|---|
| **Presupuesto** | **0 €** de infraestructura y servicios. Solo cuotas gratuitas. Si algo requiere pago, avísame antes. |
| **Plataforma** | **PWA** (web instalable) pensada primero para móvil Android, usable también en PC (sobre todo para importar datos). Sin tiendas de apps en el MVP. |
| **Conectividad** | Se acepta depender de internet. Deseable: consultar la colección sin conexión (caché local de solo lectura). La escritura sin conexión es opcional/fase posterior. |
| **Equipo** | Yo solo desarrollando. Mi amigo valida mockups y funcionalidades. |
| **Plazo** | Sin plazo. Enfoque MVP + iteración. |
| **Idiomas** | Español obligatorio. Catalán e inglés opcionales **si cuesta poco** (preparar i18n desde el inicio). |
| **Tema** | Modo claro y oscuro. |
| **Calidad** | Quiero tests automáticos, CI/CD y documentación desde el principio. |

---

## 3. Descubrimientos ya verificados (no los des por buenos sin reverificar)

Verificados el 25/11/2026; **reverifica antes de depender de ellos**:

- **API de Numista** (catálogo mundial de monedas y billetes): plan gratuito con cuota de **2000 peticiones/mes**. El endpoint de **búsqueda por imagen** solo está en un plan de pago (cuota de activación + mínimo mensual de 100 € + coste por consulta) → **incompatible con el presupuesto de 0 €. Descartado para la identificación por foto.**
- Las **imágenes de Numista** tienen licencia **por imagen** (el API devuelve el nombre y la URL de la licencia) y su uso general está limitado a fines no comerciales; la licencia por defecto puede ser "solo Numista". Además hay restricciones de caché/redistribución (sobre todo con precios). **Hay que leer sus condiciones de uso y respetar la licencia de cada imagen antes de copiar o mostrar nada.**
- **Supabase (plan gratuito):** Postgres con ~500 MB de base de datos por proyecto, 1 GB de almacenamiento de ficheros, 50 000 usuarios activos/mes, 2 proyectos activos y **pausa automática tras 1 semana de inactividad** (mitigable con un ping programado, p. ej. GitHub Actions). Sin copias de seguridad automáticas en el plan gratuito → hay que **exportar copias propias**.
- **API de Gemini (plan gratuito):** existe cuota gratuita con límites bajos, y en el nivel gratuito los datos pueden usarse para mejorar los productos de Google (**implicación de privacidad**: avisar al usuario). Los límites y modelos cambian a menudo → `VERIFICAR` antes de elegir modelo.

Ver también sección 6 (fuentes del catálogo) y 9 (foto).

---

## 4. Decisiones ya tomadas por mí (el usuario)

### Catálogo
- Alcance: piezas **vigentes e históricas retiradas** (billetes ya no vigentes, pesetas, etc.), incluyendo **conmemorativas de 2 €** y **euros por país emisor y año** (con caras nacionales).
- **No** quiero llegar a cecas ni variantes raras. Si dudas si algo entra, **pregúntame caso por caso con un ejemplo**. Sí me interesan algunas variantes (p. ej. series de pesetas de las que solo me faltan variantes concretas).
- Incluir **países con moneda ajena** (Andorra, Mónaco, San Marino, Vaticano...), **territorios dependientes**, **estados no reconocidos** y **estados desaparecidos** (URSS, Yugoslavia, RDA...).
- Países que han tenido varias monedas (Cuba: CUC y CUP; Ecuador: sucre y luego USD) y monedas compartidas por varios países (Euro, CFA XOF/XAF, dólar del Caribe Oriental...) deben modelarse correctamente (ver sección 5).
- Fuentes de terceros aceptadas (la más oficial/completa). A largo plazo puede convenir un **catálogo propio alimentado desde fuentes externas**. Quiero actualización **automatizada**, y que cualquier usuario pueda **proponer piezas que falten** sin romper el catálogo (moderación/validación).
- Imágenes: me encantaría ver las piezas con imagen (las que tengo a color; las que faltan atenuadas). Si hay problemas de licencia, como mínimo las **fotos subidas por los propios usuarios**.

### Mi colección (datos por ejemplar)
Cantidad, año, estado de conservación (**escala simple**), valor facial, valor estimado, fecha y lugar de adquisición, notas, foto propia, ubicación física (carpeta/álbum/caja), marca de **duplicado** y **lista de buscadas (wishlist)**.

### Valor en euros
- **Valor facial convertido al cambio del día.** Sin valor de coleccionista de momento.
- Los tipos de cambio se actualizan **al abrir la app**; fuente gratuita cualquiera. Divisa base: **solo euro** (dejar preparado cambiarla en el futuro).
- Para piezas de monedas extintas o no convertibles: ver propuesta en sección 8 (pendiente de mi confirmación).

### Foto
- Reconocer **billetes y monedas**. Subir las fotos que quiera; **no obligar** a anverso y reverso (una sola foto debería valer).
- Si no hay certeza, mostrar **candidatos** (estilo Vivino) para que yo confirme.
- Para monedas con escritura ilegible: ofrecer **búsqueda guiada** (la que consideres mejor).
- Se permite enviar fotos a un servicio externo **mientras sea gratis**. Inferencia propia solo si hiciera falta por coste/escala.
- El sistema debe **mejorar con el tiempo** con las confirmaciones de los usuarios.
- En el peor caso, puedo introducir la pieza a mano: **la fiabilidad del catálogo importa más que la foto**.

### Importación / exportación
- No tengo inventario digital previo (partiré de Excel/Google Sheets si hace falta). Quiero **dos vías**: (a) importación CSV/Excel con plantilla, y (b) **asistente por lotes** (por ejemplo, "tengo todas las pesetas de España de la serie X salvo estas variantes"). Tengo colecciones completas sin inventariar.
- **Exportación** de mis datos (CSV/JSON): sí.
- Importar desde Numista: **no** de momento.

### Diseño y funciones
- Estilo **álbum de cromos coleccionable** como propuesta de partida (mi amigo puede cambiarlo; deja el diseño preparado para variar la estética).
- **Globo 3D y mapa plano**, a elegir; países coloreados por criterio **elegible** (p. ej. % completado, nº de piezas). Los países pequeños deben verse (círculo/marcador visible).
- **Gamificación** si no cuesta en exceso (logros, insignias por continente/serie, progreso).
- **KPIs**: todos los que se te ocurran (ver sección 11). **Filtros**: país, moneda, tipo, año/década, estado, tengo/me falta, valor, continente y los que veas necesarios.
- Idioma: español; catalán e inglés opcionales. **Modo oscuro**: sí.

### Cuentas y social
- **Registro de usuario** (para no perder la colección si pierdo el móvil) y **sincronización entre dispositivos**.
- **Colección privada por usuario**, con **función social de intercambio de duplicados** (por ejemplo, ver qué duplicados tengo yo y qué le falta a mi amigo). Idea a largo plazo: red social de coleccionistas (no es objetivo del MVP).

---

## 5. Modelo de dominio (propuesta inicial a validar conmigo)

Principio clave: **separar "país/entidad emisora" de "moneda"**, con relación muchos-a-muchos y **con vigencia temporal**.

### Entidades

- **`issuer` (emisor/entidad)**: país, territorio dependiente, estado no reconocido, estado desaparecido o unión monetaria. Campos: id, nombre (multilenguaje), tipo (`country`, `dependency`, `unrecognized`, `historical_state`, `monetary_union`), código ISO 3166 si existe, fechas de existencia, continente, coordenadas de referencia (para marcador), nota.
- **`currency` (moneda)**: id, nombre, código ISO 4217 si existe (histórico si procede), símbolo, fecha de introducción y de retirada, estado (`active`, `withdrawn`, `redenominated`), relación de sustitución (p. ej. peseta → euro) con **factor de conversión fijo si existe** (p. ej. 166,386 pesetas = 1 €; `VERIFICAR` cada caso).
- **`issuer_currency` (vigencia)**: qué emisor usó/usa qué moneda y **entre qué fechas**, y si la emite él mismo o la usa como moneda ajena (`issues_own` booleano).
  - Andorra: sin moneda propia → usó peseta y franco, hoy euro (con acuerdo para acuñar euros propios).
  - Cuba: CUP y CUC (CUC con vigencia 1994-2021, `VERIFICAR`).
  - Ecuador: sucre hasta ~2000, luego USD.
  - Euro y CFA (XOF, XAF): una moneda ↔ muchos emisores.
- **`catalog_item` (pieza de catálogo)**: id, tipo (`coin` / `banknote`), moneda, emisor (quién la emite, p. ej. Francia en un euro francés), denominación, año o rango de años, serie/emisión, flag `commemorative`, descripción, material/medidas (monedas), tamaño (billetes), referencias externas (id Numista N#, KM, Pick...), **estado de verificación** (`seed`, `verified`, `pending_review`, `rejected`), fuente y fecha de importación, imágenes (con su licencia y autoría).
- **`catalog_image`**: url/almacenamiento, lado (`obverse`/`reverse`), origen (`official`, `wikimedia`, `user`, `numista`), **licencia y atribución** (obligatorios), `allowed_use`.
- **`user_collection_entry`**: usuario, `catalog_item`, cantidad, año concreto (si el ítem es una serie), estado de conservación (escala simple), fecha/lugar de adquisición, notas, ubicación física, foto propia, valor estimado (manual), `is_duplicate_for_trade` (derivado de cantidad > 1 y/o marca manual).
- **`wishlist_entry`**: usuario, `catalog_item`, prioridad, nota.
- **`contribution`**: propuesta de usuario de nueva pieza o corrección, estado (`pending`, `approved`, `rejected`), revisor, motivo.
- **`photo_identification`**: usuario, foto, candidatos devueltos, elección confirmada (alimenta la mejora del sistema).
- **`fx_rate`** (caché): moneda, tasa respecto al EUR, fecha, fuente.
- **`user_profile`**: preferencias (idioma, tema, vista por defecto del mapa).

### Reglas de integridad que quiero ver con tests
- Una pieza siempre pertenece a una moneda y a un emisor válidos para la fecha de la pieza (aviso, no bloqueo, si hay dudas históricas).
- Una moneda puede tener varios emisores; un emisor puede tener varias monedas a lo largo del tiempo o a la vez.
- Los contribuyentes **no pueden crear duplicados evidentes**: antes de aceptar una propuesta, buscar piezas similares y sugerirlas.
- Los cambios en el catálogo oficial no deben borrar ni invalidar `user_collection_entry`; usar **versionado/alias** (si una pieza se fusiona con otra, redirigir).

---

## 6. Fuentes del catálogo y estrategia de carga (Fase 0: investigación obligatoria)

**Antes de construir nada, haz un "spike" de investigación** y entrégame un informe comparativo (con enlaces oficiales y fecha de verificación) sobre al menos:

1. **Numista** (API gratuita: ¿qué endpoints, qué campos, qué licencia de datos e imágenes, qué se puede cachear y por cuánto tiempo, cómo atribuir?).
2. **Wikidata / Wikimedia Commons** (¿cobertura de monedas/billetes? ¿licencias de imágenes? ¿datos de emisores, monedas históricas y vigencias?).
3. **Bancos centrales y fuentes oficiales** (BCE y bancos centrales de la zona euro para diseños y conmemorativas de 2 €; otras fuentes oficiales para billetes vigentes).
4. **Listados ISO 4217** (incluida la lista histórica "withdrawn") y **ISO 3166** para emisores/monedas.
5. Cualquier **dataset abierto** de catálogos numismáticos con licencia compatible (indícamelos si los encuentras).

Para cada fuente: cobertura, calidad, licencia, límites de uso, coste (debe ser 0 €), facilidad de automatización y riesgos legales. **Recomiéndame una estrategia**, por ejemplo:

- **Catálogo propio** en Postgres alimentado por scripts de importación reproducibles (en el repo), con campo `source` + `verification_status` en cada fila.
- **Semillas curadas versionadas** (CSV/JSON en el repo) para emisores y monedas (el esqueleto lo conviene controlar yo).
- Importadores incrementales respetando cuotas (p. ej. Numista 2000 peticiones/mes → importar por lotes y cachear lo permitido).
- Cola de **revisión humana** de lo importado/contribuido antes de marcarlo `verified`.

Si las condiciones de una fuente no permiten copiar datos/imágenes, la alternativa es **guardar solo identificadores y enlazar** a la fuente, o usar imágenes subidas por usuarios. Dímelo y decidimos.

---

## 7. Funcionalidad detallada y criterios de aceptación

### 7.1 Navegación principal
Inicio (resumen/KPIs) · Álbum (por país/moneda) · Mapa (globo/plano) · Escáner (foto) · Buscar · Importar/Exportar · Perfil/Ajustes.

### 7.2 Álbum
- Vista por **emisor → moneda → serie → piezas** como páginas de álbum con "cromos".
- Pieza que tengo: imagen a color, insignia con cantidad. Pieza que falta: misma imagen atenuada/en escala de grises.
- Navegación y filtros rápidos (tengo/me falta/duplicados/buscadas).
- Modo lista compacta y modo cuadrícula.
- **Criterio de aceptación:** con 5 000 piezas en pantalla/lista el scroll es fluido (virtualización) en un Android medio.

### 7.3 Mapa
- **Globo 3D rotatorio** y **mapa plano**, conmutables.
- Coloreado de países por criterio elegible (completado %, nº de piezas, valor).
- Emisores sin polígono propio o muy pequeños (Mónaco, Vaticano, San Marino, Andorra...) → **círculo marcador** visible.
- Estados desaparecidos (URSS, RDA...) → sin polígono actual; mostrarlos en una sección/leyenda propia y/o con marcador en su capital histórica. **Dime tu propuesta.**
- Uniones monetarias (Euro, CFA) → resaltar el conjunto de países miembros al seleccionar la moneda.
- Debe funcionar **sin coste** (nada de teselas de mapas de pago). Propuesta a validar: **D3-geo + datos Natural Earth/world-atlas** (proyección ortográfica para el globo, equirectangular/Natural Earth para el plano) servidos como estáticos.

### 7.4 Escáner por foto
Ver sección 9.

### 7.5 Wishlist y duplicados
- Marcar piezas como buscadas con prioridad.
- Listado de duplicados disponibles para intercambio.
- **Fase 2:** comparar mi lista de duplicados con la wishlist de otro usuario (mi amigo) y proponer posibles intercambios.

### 7.6 Importación (ver sección 10)

### 7.7 Gamificación ligera
- Logros (p. ej. "primer país completo", "10 países", "serie completada", "pieza más antigua").
- Progreso por continente, por moneda y por serie.
- Rachas/insignias **sin** mecánicas manipuladoras; coste de implementación bajo.

### 7.8 Ajustes
Idioma, tema (claro/oscuro/sistema), vista de mapa por defecto, exportar datos, eliminar cuenta y datos.

---

## 8. Valoración en euros (propuesta a validar conmigo)

El total en euros = suma de **valor facial × cantidad × tipo de cambio**, con estas reglas por moneda:

1. **Moneda vigente con cotización** → conversión al tipo de cambio de la última actualización (fecha visible).
2. **Moneda sustituida por otra con factor fijo oficial** (p. ej. peseta → euro) → "**equivalencia nominal**" con el factor fijo, marcada como *valor facial histórico, no implica que sea canjeable* (`VERIFICAR` la situación de canje cuando lo muestres).
3. **Moneda extinta o sin cotización** (URSS, monedas retiradas sin equivalencia, etc.) → **valor manual** introducido por el usuario; **por defecto 0** (mi idea). Mi propuesta: mostrarlas con insignia "sin valoración" y **no mezclar** con el total principal.

**KPI propuesto:** dos totales, "Valor facial vigente (€)" y "Valor facial histórico/manual (€)", más el total combinado.

**FX:** buscar una fuente **gratuita, sin clave si es posible, con cobertura amplia de divisas** (las de los bancos centrales suelen cubrir pocas). Cachear la tasa (p. ej. con fecha) y refrescar **al abrir la app** con tolerancia a fallos (usar la última tasa conocida si falla). `VERIFICAR` cobertura de divisas poco comunes y licencias de uso.

---

## 9. Identificación por foto

### Principios
- **0 € obligatorio.** El endpoint de búsqueda por imagen de Numista **queda descartado** por coste.
- **Salida con candidatos + confirmación del usuario**, nunca una afirmación ciega.
- Aceptar **una sola foto** (anverso o reverso) y **varias** si el usuario quiere.
- Fallback siempre disponible: **búsqueda guiada** (continente/país probable, forma, color, metal, diámetro aproximado, símbolos o alfabeto visible, denominación) y **entrada manual**.

### Arquitectura propuesta (a validar y verificar)
1. El usuario hace/elige una foto en la PWA (captura vía cámara del navegador).
2. La PWA redimensiona y comprime la imagen en el cliente y la envía a una **función serverless propia** (para no exponer claves).
3. La función llama a un **modelo multimodal con cuota gratuita** (p. ej. la API de Gemini; `VERIFICAR` modelo, cuotas y condiciones de privacidad de la capa gratuita) pidiendo **salida estructurada (JSON)**: tipo (moneda/billete), países/emisores probables, denominación, año visible, alfabeto/idioma de la leyenda, texto legible, colores y rasgos distintivos, y nivel de confianza.
4. Con esos atributos se hace **búsqueda en el catálogo propio** (filtros + búsqueda de texto/trigramas y, si compensa, embeddings) y se devuelve un **ranking de candidatos** con imagen del catálogo si hay.
5. El usuario confirma o corrige; **la confirmación se guarda** (`photo_identification`) para mejorar: afinado de prompts, ejemplos, alias, y más adelante posibles embeddings de imagen propios con las fotos aportadas por usuarios (con su consentimiento).

### Cosas que quiero que me adviertas
- Precisión realista esperada en **monedas** (desgaste, reflejos, caras múltiples) frente a **billetes**.
- **Privacidad:** si se usa una capa gratuita en la que el proveedor puede usar los datos para mejorar sus productos, debe constar en la política de privacidad y en una aviso previo al usuario.
- Límites de cuota: cómo degradar con elegancia (mensaje claro + búsqueda guiada) cuando se agote.
- Alternativas de inferencia **en el dispositivo** (p. ej. modelos ligeros en navegador) como vía de ahorro futuro, **sin implementarla aún**.

---

## 10. Importación y exportación

### 10.1 Importación por plantilla (CSV/XLSX)
- Ofrecer **plantilla descargable** con columnas claras (emisor, moneda, tipo, denominación, año, cantidad, estado, notas, ...) y ejemplos.
- Importar **CSV y XLSX** (también pegar desde Google Sheets).
- **Emparejamiento inteligente** con el catálogo (nombre de país en varios idiomas, ISO, denominaciones "1 peseta" ↔ "1 PTS", etc.).
- **Vista previa** antes de confirmar, con tres grupos: coincidencias seguras, coincidencias dudosas (elegir candidato) y filas no reconocidas (proponer crear contribución).
- Informe final: importadas, ignoradas, errores; **deshacer** la última importación.

### 10.2 Asistente por lotes (la funcionalidad estrella para colecciones sin inventariar)
Flujo ejemplo: **País/moneda → serie/emisión → rejilla de denominaciones y años** donde marco "tengo todas", "tengo todas menos…" o "marcar manualmente". Ejemplo real: *"España, peseta, serie de acuñaciones de 1 a 500 pesetas: las tengo todas excepto estas variantes."* Debe permitir marcar cantidades por lote y aplicar un estado de conservación por defecto.

### 10.3 Exportación
CSV y JSON de toda mi colección y wishlist (también como **copia de seguridad** dado que el plan gratuito de BD no incluye backups).

---

## 11. KPIs y filtros

### KPIs (todos los viables)
- Total de piezas y de piezas **distintas** (monedas / billetes por separado).
- Países/emisores con al menos una pieza; monedas distintas; continentes cubiertos.
- % de completitud por emisor, moneda, serie, continente y global.
- Valor total en € (ver sección 8) y por emisor/moneda.
- Pieza más antigua, más reciente, más valiosa (facial), con más duplicados.
- Últimas incorporaciones y evolución temporal (altas por mes, valor acumulado).
- Top países por piezas y por completitud; "lo que más te falta para completar".
- Estado de conservación (distribución).

### Filtros
Emisor/país, continente, moneda, tipo (moneda/billete), año/década, conmemorativa, estado de conservación, tengo/me falta/duplicado/buscada, rango de valor, ubicación física, fuente (oficial/usuario), verificado/pendiente. Guardar **filtros favoritos**. Propón los que falten.

---

## 12. Cuentas, privacidad y RGPD

- Registro con **correo (enlace mágico) y/o Google** (propón la opción más simple con la herramienta elegida). Aunque la autenticación esté activa, mi colección es **privada por defecto**.
- **Seguridad:** reglas de acceso por fila (RLS) para que cada usuario solo vea/edite lo suyo; el catálogo es de lectura general; contribuciones moderadas.
- **RGPD (en español, explicado para no expertos):** guardar solo lo mínimo (correo, colección, ajustes, fotos aportadas), política de privacidad clara, **exportación y borrado de cuenta**, consentimiento explícito para el uso de fotos con servicios externos y para usarlas en mejorar el sistema.
- Aviso legal mínimo y atribución de fuentes/imágenes con sus licencias.
- Cada imagen de usuario: no almacenar metadatos personales innecesarios (limpiar EXIF/GPS al subir).

---

## 13. Arquitectura, repositorio y documentación

### Stack propuesto (a validar; justifica y verifica límites gratuitos)
- **Frontend:** TypeScript + React + Vite, **PWA** (service worker, manifest, caché de lectura en IndexedDB), UI móvil primero, i18n (es obligatorio; ca/en opcionales), tema claro/oscuro.
- **Backend como servicio:** Supabase (Postgres, Auth, Storage, funciones) o alternativa gratuita que recomiendes con razones. **Tener en cuenta:** pausa por inactividad, 500 MB de BD, ausencia de backups → plan de mitigación (ping programado + export periódico a repo/almacén gratuito).
- **Hosting estático:** el que recomiendes con plan gratuito sin tarjeta (verifica).
- **Mapas:** D3-geo + datos Natural Earth (ver 7.3) u otra alternativa gratuita.
- **Tests:** unitarios (Vitest), de integración y e2e (Playwright). **CI/CD:** GitHub Actions (lint, tipos, tests, despliegue, tareas programadas como el ping y los backups).
- **Migraciones de BD versionadas en el repo** y scripts de importación reproducibles.

### Estructura del repositorio (propuesta)
```
/ (raíz)
├─ README.md                 # qué es, cómo arrancar, cómo desplegar
├─ CLAUDE.md / AGENTS.md     # reglas de trabajo para agentes (copiadas de la sección 0)
├─ docs/
│  ├─ PRD.md                 # requisitos y alcance (basado en este documento)
│  ├─ STATE.md               # ESTADO ACTUAL: qué está hecho, qué falta, siguiente paso
│  ├─ DECISIONS.md           # registro de decisiones (ADR) con fecha y motivo
│  ├─ DATA_MODEL.md          # modelo de datos y reglas de integridad
│  ├─ CATALOG_SOURCES.md     # fuentes, licencias, límites, fecha de verificación
│  ├─ BACKLOG.md             # tareas priorizadas por fase
│  ├─ PRIVACY.md             # RGPD, fotos, servicios externos
│  └─ CHANGELOG.md
├─ data/seeds/               # emisores, monedas, vigencias (CSV/JSON versionado)
├─ scripts/                  # importadores de catálogo, copias de seguridad
├─ supabase/ (o equivalente) # migraciones y funciones
├─ src/                      # app
└─ tests/
```

### Documentación viva (obligatoria)
Al terminar cada iteración, actualiza `docs/STATE.md`, `docs/DECISIONS.md` y `docs/BACKLOG.md`. **`STATE.md` debe permitir que una sesión nueva (humana o IA) retome el trabajo sin leer el chat.** Incluye siempre: objetivo de la iteración, qué se hizo, qué falló, qué decisiones quedan abiertas y el siguiente paso exacto.

---

## 14. Hoja de ruta por fases (con criterio de "hecho")

**Fase 0 · Descubrimiento (sin código de producto)**
Informe de fuentes de catálogo (sección 6), verificación de límites gratuitos (BD, hosting, foto, FX), validación del modelo de datos con ejemplos reales (Andorra, Cuba, Ecuador, Euro, CFA, peseta, URSS) y propuesta de diseño (mockups). *Hecho cuando yo apruebo las decisiones clave.*

**Fase 1 · MVP**
Repo + CI + despliegue gratuito de una PWA instalable; auth; catálogo semilla (emisores, monedas y piezas de un conjunto acotado: zona euro + pesetas + algunos países como prueba); álbum con tengo/falta; alta manual de piezas; importación CSV básica; KPIs básicos; modo oscuro. *Hecho cuando mi amigo y yo podemos registrarnos, cargar piezas y verlas en el móvil.*

**Fase 2 · Mapa, import avanzado y valor**
Globo + mapa plano; asistente por lotes; FX y total en €; wishlist y duplicados; exportación y copias de seguridad.

**Fase 3 · Foto**
Escáner con candidatos y búsqueda guiada, registro de confirmaciones y mejora continua.

**Fase 4 · Catálogo ampliado y contribuciones**
Importadores automáticos por lotes, cola de revisión, contribuciones de usuarios, imágenes con licencia correcta.

**Fase 5 · Social y extras**
Comparación de duplicados/buscadas entre usuarios, intercambios, gamificación completa, catalán/inglés, pulido visual.

---

## 15. Decisiones abiertas (pregúntamelas cuando toque)

1. Confirmar el **stack** y servicios gratuitos concretos (backend, hosting, función serverless para la foto, FX) tras la verificación de la Fase 0.
2. **Estados desaparecidos en el mapa** (URSS, RDA...): ¿sección propia, marcador, o ambas?
3. Reglas de **valoración** de monedas extintas o sin cotización (propuesta de la sección 8).
4. **Escala de estados de conservación simple** (propón 4-5 niveles).
5. **Imágenes del catálogo:** qué se puede usar legalmente y qué se queda en solo-enlaces o solo-usuarios.
6. **Moderación** de contribuciones: ¿quién aprueba? (¿solo yo?).
7. **Nivel de detalle numismático** por país (casos concretos con ejemplo, empezando por España/pesetas y euros conmemorativos).
8. Identidad visual (nombre de la app, paleta, estilo de álbum) tras ver mockups; el amigo valida.
9. **Offline:** ¿solo lectura en el MVP o también escritura con sincronización posterior?
10. **Idiomas opcionales** (ca/en): ¿cuándo?

---

## 16. Primera tarea (empieza aquí)

1. Lee este documento entero y devuélveme **un resumen de 10 líneas** de lo que has entendido, más **cualquier contradicción o hueco** que detectes.
2. Hazme **solo las preguntas imprescindibles** de la sección 15 que bloqueen la Fase 0 (agrupadas, con tu recomendación por defecto).
3. Lanza la **Fase 0**: informe de fuentes del catálogo, verificación de cuotas gratuitas y borrador de `DATA_MODEL.md` validado con los casos Andorra, Cuba/CUC-CUP, Ecuador, Euro, CFA y peseta.
4. Propón **mockups** (pantallas de álbum, mapa, escáner e importación) para enseñárselos a mi amigo.
5. Crea la estructura inicial del repositorio y los documentos de la sección 13 (`README`, `STATE`, `DECISIONS`, `BACKLOG`, ...), con el contenido ya conocido.

No empieces a programar el MVP hasta que yo apruebe el cierre de la Fase 0.
