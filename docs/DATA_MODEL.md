# Modelo de datos conceptual

**Estado:** propuesta para validar durante Fase 0. No es todavía un esquema SQL aprobado.

## Principios

1. Separar entidad emisora, moneda, diseño visual, emisión y posesión.
2. No duplicar fichas visuales por año o por diferencias técnicas invisibles.
3. Conservar procedencia, licencia y estado de verificación de cada dato.
4. Los cambios de catálogo no deben borrar ni romper referencias usadas por colecciones.
5. La colección y sus preferencias pertenecen a un usuario.

## Entidades propuestas

### Emisor (`issuer`)

País, territorio, estado histórico, entidad no reconocida o unión monetaria. Atributos: nombre y alias, tipo, códigos cuando existan, vigencia histórica, continente y geometría/coordenada de referencia. No asumir que todos los emisores equivalen a países soberanos actuales.

### Moneda (`currency`)

Nombre, código ISO 4217 si existe, símbolo, estado, fechas de vigencia y relación de redenominación/sustitución cuando esté documentada.

### Uso de moneda por emisor (`issuer_currency`)

Relación temporal muchos-a-muchos entre emisor y moneda; indica fechas y si el emisor la acuña/emite o simplemente la utiliza. Necesaria para euro, CFA, USD en Ecuador, peseta/franco en Andorra, etc.

### Diseño de catálogo (`catalog_design`)

Unidad visual del álbum: tipo (moneda/billete), denominación, moneda, emisor principal y referencias a imágenes de anverso/reverso. Su identidad se basa en el diseño visible de ambas caras. Puede existir inicialmente sin imagen, con placeholder.

### Emisión (`catalog_issue`)

Concreta un diseño para un emisor, periodo/año, serie, tirada u otros datos necesarios. El año se registra aquí o en el ejemplar según la granularidad real de la fuente; no crea automáticamente un diseño distinto. Diferencias técnicas como metal o diámetro se almacenan como atributos de emisión cuando sean útiles. Solo se separan diseños cuando la diferencia visual lo justifique o el usuario necesite distinguirla.

### Imágenes (`catalog_image`)

Diseño/issue asociado, cara, URL o almacenamiento, autor, fuente, licencia, atribución, restricciones de uso y fecha de verificación. No reutilizar imágenes sin permiso compatible. EXIF/GPS de fotos de usuario se eliminará al subirlas.

### Posesión (`user_collection_entry`)

Usuario, diseño/emisión, cantidad, año concreto si aplica, conservación, adquisición, notas, ubicación física, foto propia y valor estimado opcional. Duplicados pueden derivarse de cantidad > 1, con posibilidad de marcar unidades disponibles para intercambio más adelante.

### Wishlist (`wishlist_entry`)

Usuario, pieza, prioridad y nota.

### Perfil y preferencias (`user_profile` / `user_preferences`)

Idioma, tema y preferencias de interfaz. Incluir filtros del álbum: emisor/país seleccionado, tipo (monedas/billetes/todos), orden y otros filtros activos. Persistir en backend por usuario para sincronizar entre dispositivos; se puede usar caché local como optimización, no como única fuente.

### Contribuciones e identificación (fases posteriores)

Propuestas de alta/corrección con estado y moderador; sesiones de identificación con candidatos y confirmación del usuario. No forman parte del MVP inicial.

## Reglas de integridad

- Cada emisión apunta a un diseño, moneda y emisor válidos.
- Las relaciones emisor-moneda tienen vigencia temporal; advertir si las fechas no encajan.
- La identidad visual no se deriva solo de denominación y año.
- La fusión/reemplazo de registros debe conservar alias o redirecciones para no invalidar posesiones.
- RLS/controles de autorización: cada usuario solo lee y modifica su inventario y preferencias privadas; el catálogo es de lectura general.
- Compartición futura será explícita y de solo lectura.

## Preguntas pendientes

- Granularidad de emisión/año en series con múltiples años y diseños idénticos.
- Cómo representar variantes que el usuario quiera separar aunque sean visualmente casi iguales.
- Escala de conservación y tratamiento de monedas sin cotización.
- Modelo de almacenamiento y licencia de imágenes.
- Revisión de constraints tras contrastar fuentes reales.
