# Rueda Libre · Semana 1 · Día 1

Primer día del proyecto Rueda Libre, un negocio de alquiler de bicicletas en Medellín. Hoy armé la base del sitio: el repositorio, las tres páginas y el menú para moverse entre ellas (versión v0.1).

## Qué hice

- Creé el repositorio y la estructura de carpetas: `index.html` en la raíz, `paginas/` con tarifas y reservas, `css/` para los estilos y `img/` para las imágenes.
- Hice la página de inicio con la presentación del negocio y los servicios.
- Hice la página de tarifas con dos tablas: alquiler por tipo de bicicleta y recorridos guiados. Usé `caption`, `thead`, `tbody` y `scope` en los encabezados para que se lean bien.
- Hice la página de reservas con el correo de contacto y el horario.
- Agregué el mismo menú en las tres páginas.

## Lo que revisé en Network

Abrí el sitio con Live Server y miré la primera petición en DevTools:

- URL: `http://127.0.0.1:5500/index.html`
- Protocolo `http`, host `127.0.0.1` (mi computador), puerto `5500` (el de Live Server), ruta `/index.html`
- Método `GET` y código `200 OK`, es decir, el servidor encontró la página y la envió.

Después pedí una página que no existe (`/promociones.html`) y respondió `404 Not Found`. Con eso entendí que el 404 no quiere decir que el servidor esté caído, sino que ese archivo no está.

## HTML, CSS y JavaScript

- **HTML** es la estructura y el contenido, como la tabla de tarifas.
- **CSS** es cómo se ve: los colores de la marca y el menú horizontal.
- **JavaScript** es el comportamiento, por ejemplo validar el formulario de reservas.

## Rutas relativas

Lo que más me sirvió fue pensar siempre desde el archivo donde escribo el enlace. Si estoy dentro de `paginas/` y quiero volver a inicio, tengo que salir una carpeta con `../`.

| Desde | Hacia | Ruta |
|---|---|---|
| index.html | paginas/tarifas.html | `paginas/tarifas.html` |
| paginas/tarifas.html | index.html | `../index.html` |
| paginas/tarifas.html | paginas/reservas.html | `reservas.html` |
| paginas/tarifas.html | img/logo.png | `../img/logo.png` |

Si se me olvida el `../`, la imagen no carga y en Network aparece un 404.
