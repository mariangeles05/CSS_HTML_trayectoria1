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