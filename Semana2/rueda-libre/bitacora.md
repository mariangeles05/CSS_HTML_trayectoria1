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

## MiniReto 2: Grid para la flota

### Qué hice
- En `index.html` creé la sección `#flota` con el título "Nuestra flota" y un `div.flota-grid` con un `article` por modelo. Cada uno tiene imagen, nombre (`h3`), descripción, precio por hora y el enlace "Reservar".
- La cuadrícula es `display: grid` con `grid-template-columns: repeat(auto-fit, minmax(18rem, 1fr))`. Así el navegador mete tantas columnas como quepan con mínimo 18rem cada una, y el espacio que sobra se reparte con `1fr`. No usé ninguna media query.
- La separación entre filas y columnas es la misma: `gap: var(--esp-l)`.
- Cada tarjeta es un Flexbox en columna (`flex-direction: column`). Adentro tiene dos hijos: `.modelo-info` (imagen, nombre, descripción y precio) y el enlace. Con `justify-content: space-between` el enlace queda siempre abajo, aunque la descripción sea más corta, como pasa con la Infantil.
- Las tarjetas usan la clase `.tarjeta` de la semana 1, así que conservan el padding, el borde de 1 px y las esquinas redondeadas. Solo les quité el `margin-bottom`, porque ahora la separación la hace el `gap`.

### Por qué 18rem
Probé con valores más pequeños y a 900 px me seguían saliendo 3 columnas muy apretadas, porque el `main` tiene un máximo de 60rem. Con 18rem (288 px) a 900 px ya caben solo 2, y las tarjetas no se ven estrechas.

### Séptimo modelo
Agregué el Tándem ($20.000) como un `article` más, sin tocar el CSS. La cuadrícula lo acomodó sola: a 1280 px quedó en una tercera fila, en la primera columna.

### Columnas observadas (modo dispositivo de DevTools)
| Ancho | Columnas | Filas con 7 modelos |
|---|---|---|
| 1280 px | 3 | 3 |
| 900 px | 2 | 4 |
| 500 px | 1 | 7 |

En los tres anchos las tarjetas de una misma fila tienen la misma altura y los botones "Reservar" quedan alineados abajo. Tampoco aparece scroll horizontal.

### Por qué la altura es igual
Grid estira por defecto los elementos de una fila a la altura del más alto (`align-items: stretch`). Como la tarjeta también es Flexbox en columna, ese espacio extra queda entre la información y el botón, y el botón se va al final.

### Problemas
- La regla `.tarjeta img` de la semana 1 ponía las imágenes de 16rem de alto, y en la cuadrícula las tarjetas quedaban muy largas. Agregué `.modelo img` con 10rem; como tiene la misma especificidad y va después en el CSS, gana sin `!important`.
- Todos los enlaces decían solo "Reservar" y con lector de pantalla no se sabía cuál era cuál. Les agregué el nombre del modelo en un `span.visually-hidden`, que no se ve pero sí se lee.
- En `tarifas.html` el menú marcaba "Reservas" como página actual. Lo corregí para que `activo` y `aria-current` queden en "Tarifas y rutas".

## MiniReto 3: Layout de escritorio con Grid y Flexbox

### Criterio que usé
Si solo necesito acomodar cosas en una dirección (una fila o una columna) y que cada una ocupe según su contenido, uso **Flexbox**. Si quiero definir desde el contenedor cuánto mide cada columna, o que los elementos queden alineados en filas y columnas a la vez, uso **Grid**.

### Decisiones
| Caso | Qué usé | Por qué |
|---|---|---|
| Portada | Grid (`1fr 1fr`) | Es la estructura de la página: quiero que el texto y la foto tengan exactamente la mitad cada uno sin importar cuánto texto haya. Con `align-items: center` el texto queda centrado verticalmente frente a la foto. |
| Galería de rutas | Grid (`repeat(3, 1fr)`) | Es una cuadrícula: las tres tarjetas miden lo mismo y, si mañana agregan más rutas, bajan a otra fila alineadas con las de arriba. Eso es trabajar en dos dimensiones. |
| Reservas | Grid (`2fr 1fr`) | El boceto pide una proporción exacta: el formulario ocupa dos partes y el contacto una. Con `fr` lo defino en el contenedor y no tengo que calcular porcentajes. Usé `align-items: start` para que el contacto no se estire hasta el largo del formulario. |
| Fila del formulario | Flexbox | Son solo dos campos uno al lado del otro, en una sola dirección. Con `flex: 1` cada uno toma la mitad, y con `gap` quedan separados. No necesitaba filas y columnas. |
| Encabezado | Flexbox | Es una sola fila: marca a un lado y menú al otro con `justify-content: space-between`. Cada parte mide lo que mide su contenido, y con `flex-wrap` el menú baja si no cabe. |
| Pie | Flexbox | Son tres bloques en una fila con tamaños distintos según el texto. Con `flex-wrap` se apilan cuando no caben, sin que yo defina columnas. |

### Comprobaciones
- A 1280 px: la portada queda en dos columnas iguales, las rutas en una fila de tres y reservas en proporción 2:1.
- Todas las columnas están definidas con `fr`, sin porcentajes ni `px`.
- El menú, la flota (sigue en 3 columnas a 1280 px) y la validación del formulario siguen funcionando. Probé otra vez el celular 1234567890 y lo sigue rechazando.

### Problemas
- Al principio envolví documento y celular en la misma fila, pero el correo estaba entre los dos y quedaron tres campos juntos. Moví el correo arriba para que la fila tenga solo los dos campos cortos relacionados.
- Los títulos del formulario y del contacto no quedaban alineados por arriba porque el `h2` tenía margen superior. Lo quité dentro del layout de reservas.

## MiniReto 4: Mobile-first (v1.5)

### Cómo reorganicé styles.css
Dejé el archivo por bloques: variables, base, encabezado, pie, componentes, tablas y formulario. Todo lo que está fuera de una media query es la versión del celular, en una sola columna. Después hay dos media queries con `min-width`, que solo agregan lo que cambia:
- **768 px (tablet):** encabezado y pie en fila, portada en dos columnas, rutas en tres columnas, documento y celular en la misma fila, tablas con letra normal.
- **1200 px (escritorio):** reservas en proporción 2:1.

No puse media query para la flota porque con `auto-fit` ya se acomoda sola.

### Encabezado y pie
- **Celular:** el nombre va arriba y el menú debajo, centrado (`flex-direction: column` y `justify-content: center` en el menú). En el pie los tres bloques quedan uno debajo del otro.
- **Desde 768 px:** vuelve la distribución del MiniReto 1, con el nombre a la izquierda y el menú a la derecha (`flex-direction: row` y `space-between`). El pie queda con los tres bloques en fila.

### Columnas por ancho (modo dispositivo)
| Ancho | Flota | Rutas | Portada | Reservas |
|---|---|---|---|---|
| 360 px | 1 | 1 | 1 (texto arriba, foto abajo) | 1 (contacto debajo del formulario) |
| 768 px | 2 | 3 | 2 | 1 |
| 1280 px | 3 | 3 | 2 | 2:1 |

A 360 px no hay scroll horizontal en ninguna de las tres páginas.

### Imágenes fluidas
Agregué `img { max-width: 100%; height: auto; }` en la base, así ninguna imagen puede ser más ancha que su contenedor.

### Problemas que encontré y cómo los resolví
1. **El menú se partía en dos líneas a 360 px.** "Reservas" bajaba solo a otra fila porque cada enlace tenía 1rem de padding a los lados. En móvil lo bajé a 0.6rem y desde 768 px vuelve a 1rem. Ahora los tres enlaces caben en una sola línea.
2. **La tabla de recorridos obligaba a desplazarse de lado.** Tiene cinco columnas y con la letra normal no cabía en 360 px. En móvil le puse `font-size: 0.8rem` y menos relleno en `th` y `td`. Ahora se lee completa sin scroll. Desde 768 px vuelve al tamaño normal.
3. **La flota se podía salir en pantallas muy pequeñas.** Con `minmax(18rem, 1fr)` cada tarjeta mide mínimo 288 px, y en un celular de 320 px eso es más ancho que el contenido. Lo cambié por `minmax(min(18rem, 100%), 1fr)`, así la tarjeta nunca es más ancha que su contenedor.
4. **El 2:1 de reservas quedaba muy estrecho en tablet.** A 768 px el formulario quedaba en menos de 500 px y los campos se veían apretados. Por eso el 2:1 empieza en 1200 px, y en tablet el contacto va debajo del formulario.
5. **El correo del pie se podía desbordar.** En pantallas angostas la dirección de correo es una palabra larga sin espacios. Le puse `overflow-wrap: anywhere` para que pueda partirse.

### Publicación
URL v1.5: https://mariangeles05.github.io/CSS_HTML_trayectoria1/

## MiniReto 5: La flota en Bootstrap (primera comparación)

### Qué hice
- Creé `pruebas/catalogo-bootstrap.html` con la plantilla inicial de Bootstrap 5.3 de la documentación oficial: el CSS por CDN en el `head` y el bundle de JavaScript antes de cerrar el `body`.
- Copié los siete modelos de la flota y cambié las rutas de las imágenes a `../img/flota/...`, porque ahora el archivo está dentro de la carpeta `pruebas`.
- La distribución sale solo de la grilla: `container` > `row g-4` > cada modelo en un `col-12 col-sm-6 col-lg-4 col-xl-3`.
- En esta página no escribí CSS ni enlacé `styles.css`.

### Columnas observadas (modo dispositivo)
| Ancho | Breakpoint activo | Columnas |
|---|---|---|
| 360 px | ninguno (`col-12`) | 1 |
| 600 px | `sm` (desde 576 px) | 2 |
| 800 px | `sm` (`md` no lo usé) | 2 |
| 1000 px | `lg` (desde 992 px) | 3 |
| 1280 px | `xl` (desde 1200 px) | 4 |

En Network, `bootstrap.min.css` y `bootstrap.bundle.min.js` cargan con código 200 y no aparece ningún error.

### Comparación
| | CSS propio (MiniReto 2) | Bootstrap |
|---|---|---|
| Tiempo aproximado | 45 min | 20 min |
| CSS de distribución de la flota | 7 declaraciones en 2 reglas (`.flota-grid`: display, grid-template-columns, gap; `.modelo`: display, flex-direction, justify-content, gap) | 0 líneas de CSS |
| Clases en el HTML para la distribución | 2 (`flota-grid` y `modelo`) | 6 distintas (`row`, `g-4`, `col-12`, `col-sm-6`, `col-lg-4`, `col-xl-3`); las de columna se repiten en los 7 modelos (28 veces) |
| Para alinear "Reservar" abajo | `justify-content: space-between` | `h-100`, `d-flex flex-column` y `mt-auto` |
| Media queries | 0 (`auto-fit` se adapta sola) | 0 escritas por mí; Bootstrap ya las trae en sus clases |

En la versión propia el tiempo se fue en entender `auto-fit` y `minmax()`, probar cuál ancho mínimo dejaba 3 columnas a 1280 px y 2 a 900 px, y lograr que el botón quedara abajo en todas las tarjetas. Con Bootstrap casi todo el tiempo fue copiar el marcado, cambiar las rutas de las imágenes y buscar en la documentación los nombres de las clases.

### Qué me dio Bootstrap sin esfuerzo
- Los breakpoints ya están hechos: solo escribo `col-sm-6` y desde 576 px ya son dos columnas.
- Los gutters con una sola clase (`g-4`), iguales entre filas y columnas.
- La tarjeta (`card`) ya trae borde, esquinas y relleno, y el botón trae estilos de hover y foco.

### Qué control perdí
- Ahora soy yo quien decide cuántas columnas hay en cada breakpoint; antes salían del espacio disponible. Con `auto-fit`, si cambio el ancho mínimo de la tarjeta, la cuadrícula se reacomoda sola. Aquí tendría que cambiar las clases de los 7 modelos.
- Los breakpoints son los de Bootstrap (576, 768, 992, 1200 px), no los que necesita mi contenido. Por ejemplo, a 800 px se siguen viendo 2 columnas aunque cabrían 3.
- El HTML queda más cargado: cada modelo necesita un `div` extra para la columna, y la distribución queda mezclada con el contenido en lugar de estar en el CSS.
- El estilo no es el de Rueda Libre (fuente y colores de la marca). Para eso tendría que sobrescribir Bootstrap.
- La página descarga todo Bootstrap aunque solo use la grilla y la tarjeta.

### Conclusión
Bootstrap fue más rápido de armar, pero la versión propia se adapta mejor al contenido, deja el HTML más limpio y mantiene la identidad de la marca. Para una prueba rápida Bootstrap sirve; para la flota de Rueda Libre me quedaría con la versión en CSS propio.
