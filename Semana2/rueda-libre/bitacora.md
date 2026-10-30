# Bitácora Rueda Libre v1.5

## MiniReto 1: Flexbox

### Qué hice
- Agrupé logo y nombre en `.marca` para que el `header` tuviera solo dos hijos: la marca y el menú.
- Encabezado: `display: flex` con `justify-content: space-between` (nombre y menú en extremos opuestos) y `align-items: center` (centrados verticalmente).
- Menú: `#menu` flexible con `gap` y `flex-wrap: wrap`. Eliminé los márgenes de los `li` y el `inline-block` de la semana 1.
- Pie: tres bloques (marca, contacto y horario) en fila, alineados por arriba con `align-items: flex-start` y separados con `gap`.
- Usé el mismo HTML de encabezado y pie en las tres páginas; los estilos están en `css/styles.css`.

### Al estrechar la ventana
- **Encabezado:** a unos ___ px el menú baja debajo del nombre en lugar de desbordarse. A unos ___ px los enlaces se parten en dos líneas.
- **Pie:** a unos ___ px el bloque del horario baja a otra línea. A unos ___ px los tres bloques quedan apilados.

### Por qué gap en vez de márgenes e inline-block
`gap` separa solo entre elementos y se define una vez en el contenedor, sin corregir extremos. Con Flexbox el `inline-block` ya no hace falta.

### Problemas
- El `header` tenía tres hijos y `space-between` dejaba el nombre en el centro. Lo resolví agrupando logo y nombre en `.marca`.
- Los títulos del pie no se veían (azul sobre azul). Lo resolví con `footer h2` en blanco.