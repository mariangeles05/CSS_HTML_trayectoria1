# Rueda Libre · Semana 1 · Día 3

Último día de la semana. Pasé los estilos a variables, entendí la herencia y la especificidad, comparé los dos box model y usé posicionamiento para el lanzamiento de la v1.0.

## Variables

Definí los colores, las fuentes y los espacios una sola vez en `:root`. Si el cliente cambia un color, lo cambio en un solo lugar.

```css
:root {
  --verde-ruta: #1E7A4F;
  --azul-noche: #14213D;
  --esp-m: 1rem;
}
```

## Herencia

Seleccioné un `<p>` y miré la pestaña Computed.

- **Se hereda `font-family`:** el párrafo muestra "Open Sans" aunque solo la declaré en el `body`.
- **No se hereda `background-color`:** el párrafo muestra `rgba(0,0,0,0)`, o sea transparente. Se ve crema porque deja ver el fondo del `body`.

## Especificidad

El enlace de la página actual tenía la clase `.activo`, pero el color no cambiaba. En DevTools aparecía tachado.

- `#menu a` → (1,0,1): un id y un elemento
- `.activo` → (0,1,0): una clase

Gana `#menu a` porque tiene un id. Lo resolví con `#menu a.activo` → (1,1,1), sin `!important`.

También ajusté el header a fondo blanco, porque el gris del menú sobre Azul Noche solo daba 2.66:1.

## Box model

Medí una tarjeta en una ventana de 1280 px: `width: 100%` (el main mide 960 px), padding de 1.5rem y borde de 1 px.

- **content-box:** mide 1010 px (960 + 48 de padding + 2 de borde) y se sale del main.
- **border-box:** mide 960 px, porque el padding y el borde quedan por dentro. El contenido queda en 910 px.

Por eso dejé `box-sizing: border-box` para todo el sitio.

## Posicionamiento (lanzamiento v1.0)

- **Etiqueta "Nuevo":** la `.tarjeta` tiene `position: relative` y la `.etiqueta` tiene `position: absolute` con `top` y `right`. Así queda en la esquina de su tarjeta.
- **Botón de WhatsApp:** `position: fixed` abajo a la derecha, para que se quede en su lugar con el scroll. Le puse `padding-bottom` al `body` para que no tape el pie.
- **styles.css** quedó ordenado por bloques (variables, base, navegación, componentes, formulario) y sin reglas duplicadas.
- **Revisión final:** 0 errores 404, sin estilos en línea y el foco se ve con Tab en las tres páginas.

## Resumen de la semana

- **v0.1:** repositorio, inicio, tarifas con tablas, reservas y menú.
- **v0.2:** semántica, formulario, validación nativa, accesibilidad y paleta.
- **v1.0:** variables, estados del menú, box model y posicionamiento.

Lo que quedó pendiente para la semana 2 es el diseño responsive con Flexbox y Grid.