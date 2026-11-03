# Rueda Libre · Semana 2 · Layout y responsive

Esta semana el sitio pasó de verse bien solo en el computador a funcionar en celular, tablet y escritorio. Trabajé con Flexbox, Grid y media queries, y al final probé Bootstrap para comparar (versión v1.5).

## MiniReto 1 · Flexbox en encabezado y pie

- Agrupé el logo y el nombre en `.marca` para que el `header` tuviera solo dos hijos.
- `header` con `display: flex`, `justify-content: space-between` (marca a un lado y menú al otro) y `align-items: center`.
- El menú es flexible, con `gap` y `flex-wrap: wrap`, así baja en vez de desbordarse.
- El pie tiene tres bloques en fila, alineados arriba con `align-items: flex-start`.
- Usé `gap` en vez de márgenes porque separa solo entre elementos y no deja espacio de más en los extremos.

## MiniReto 2 · La flota con Grid

Hice la sección "Nuestra flota" con 7 modelos. Cada uno es un `article` con foto, nombre, descripción, precio y botón "Reservar".

```css
.flota-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(18rem, 1fr));
  gap: var(--esp-l);
}
```

`auto-fit` mete tantas columnas como quepan, y cada una mide mínimo 18rem. No usé media queries. Cuando agregué el séptimo modelo (Tándem), la cuadrícula lo acomodó sola.

Cada tarjeta es un Flexbox en columna con `justify-content: space-between`, así el botón queda siempre al final aunque la descripción sea corta.

| Ancho | Columnas |
|---|---|
| 1280 px | 3 |
| 900 px | 2 |
| 500 px | 1 |

## MiniReto 3 · Layout de escritorio

| Caso | Qué usé | Por qué |
|---|---|---|
| Portada | Grid `1fr 1fr` | Texto y foto con la mitad exacta cada uno; `align-items: center` centra el texto |
| Galería de rutas | Grid `repeat(3, 1fr)` | Es una cuadrícula de tres tarjetas iguales |
| Reservas | Grid `2fr 1fr` | El boceto pide el formulario en 2/3 y el contacto en 1/3 |
| Fila documento y celular | Flexbox | Son solo dos campos en una dirección |
| Encabezado | Flexbox | Una fila y cada parte del tamaño de su contenido |
| Pie | Flexbox | Bloques de distinto tamaño que se apilan con `wrap` |

Mi criterio: si es una sola dirección, Flexbox; si tengo que definir las columnas o alinear filas y columnas a la vez, Grid.

## MiniReto 4 · Mobile-first

Reorganicé `styles.css` para que los estilos sin media query sean la versión del celular, todo en una columna. Después agregué solo lo que cambia:

- **Desde 768 px:** encabezado y pie en fila, portada en dos columnas, rutas en tres y documento y celular juntos.
- **Desde 1200 px:** reservas en 2:1.

También agregué `img { max-width: 100%; height: auto; }` para que ninguna imagen se salga.

Problemas que encontré a 360 px:

1. El menú se partía en dos líneas. Le bajé el padding a los enlaces en móvil.
2. La tabla de recorridos obligaba a desplazarse de lado. Bajé la letra y el relleno en móvil.
3. La flota se podía salir en pantallas muy pequeñas. Usé `minmax(min(18rem, 100%), 1fr)`.
4. El 2:1 de reservas quedaba apretado en tablet, así que lo dejé desde 1200 px.
5. El correo del pie podía desbordarse. Le puse `overflow-wrap: anywhere`.

## MiniReto 5 · La flota en Bootstrap

En `pruebas/catalogo-bootstrap.html` rehice la flota con Bootstrap 5.3 por CDN, sin CSS propio:

```html
<div class="row g-4">
  <div class="col-12 col-sm-6 col-lg-4 col-xl-3"> ... </div>
</div>
```

Así sale 1 columna en celular, 2 desde `sm`, 3 desde `lg` y 4 desde `xl`.

| | CSS propio | Bootstrap |
|---|---|---|
| Tiempo aproximado | 45 min | 20 min |
| CSS de distribución | 7 declaraciones | 0 |
| Columnas | Las decide el espacio | Las decido yo por breakpoint |

Bootstrap fue más rápido, pero perdí control sobre las columnas, el HTML quedó más cargado y no tiene el estilo de la marca. Para Rueda Libre me quedo con la versión propia.

## Publicación

- Sitio v1.5: https://mariangeles05.github.io/CSS_HTML_trayectoria1/
- Probado en DevTools a 360, 768 y 1280 px, y en un celular real.
