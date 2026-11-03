# Rueda Libre · Semana 1 · Día 2

Hoy el objetivo fue que el sitio estuviera bien construido por dentro: etiquetas semánticas, un formulario de reservas real, validación sin JavaScript, accesibilidad y una paleta de colores que se lea bien (versión v0.2).

## HTML semántico

Pasé todas las regiones a etiquetas que dicen lo que son. No quedó ningún `div` ni `span` para las regiones.

- **index.html:** `header` (h1 + nav), `main` con cuatro `section` (la de servicios tiene tres `article`) y `footer`.
- **tarifas.html:** `header` con logo, nombre y menú; `main` con las tablas y un `aside` "Qué llevar"; `footer`.
- **reservas.html:** `header`, `main` con el formulario y un `aside` con el horario, y `footer`.

Usé `article` en los servicios porque cada uno se entiende solo, y `aside` en lo que es información de apoyo.

## Formulario de reservas

Escogí cada control según cómo responde la persona:

- **Tipo de bicicleta → radio:** son tres opciones y solo se escoge una. Así se ven todas a la vez.
- **Plan y recorrido → select:** es una lista cerrada, y en un desplegable ocupa menos espacio.
- **Políticas → checkbox:** es una sola decisión de sí o no.

Agrupé los campos con `fieldset` y `legend` (Tus datos, Tu alquiler, Confirmación), y cada campo tiene su `label for`.

## Validación nativa

| Campo | Dato de prueba | Resultado | Por qué |
|---|---|---|---|
| Nombre | "Jo" | Rechaza | `minlength="3"` |
| Documento | "12ab45" | Rechaza | `pattern="[0-9]{6,10}"` |
| Documento | "12345" | Rechaza | Tiene menos de 6 dígitos |
| Correo | "hola@" | Rechaza | `type="email"` |
| Celular | 3001234567 | Acepta | Cumple el pattern |
| Celular | 1234567890 | Rechaza | No empieza por 3 (`pattern="3[0-9]{9}"`) |
| Fecha | 2026-10-31 | Rechaza | Es anterior a `min` |
| Cantidad | 7 | Rechaza | `max="6"` |
| Políticas | sin marcar | Rechaza | `required` |

También recorrí el formulario solo con el teclado. El orden del Tab es lógico, en los radios me muevo con las flechas, el checkbox se marca con espacio y con Enter se envía.

## Accesibilidad

Lo básico ya estaba bien: `lang="es"`, un solo `h1` por página, `alt` en las fotos y navegación con teclado. Encontré seis cosas por mejorar:

1. "mira cómo llegar" no se entendía solo, así que lo cambié por "cómo llegar a nuestra sede".
2. El enlace al mapa abría otra pestaña sin avisar. Le agregué "(se abre en otra pestaña)".
3. El logo repetía el nombre que está al lado. Le dejé `alt=""` porque ahí es decorativo.
4. "Reservar ahora" estaba repetido. Ahora uno dice "Reservar ahora tu bicicleta" y el otro "Reservar un recorrido guiado".
5. El formato de los campos solo estaba en el `title`, que no se ve. Lo puse visible con `<small>`.
6. El menú no indicaba la página actual. Le agregué `aria-current="page"`.

## Paleta y contraste

Para texto normal se necesita mínimo 4.5:1.

| Combinación | Ratio | ¿Sirve? |
|---|---|---|
| Blanco / Verde Ruta | 5.31:1 | Sí |
| Blanco / Naranja Pedal | 2.22:1 | No |
| Azul Noche / Naranja | 7.20:1 | Sí |
| Azul Noche / Crema | 14.83:1 | Sí |
| Gris Asfalto / Crema | 5.57:1 | Sí |
| Verde Ruta / Crema | 4.93:1 | Sí |
| Naranja Pedal / Crema | 2.06:1 | No |
| Blanco / Azul Noche | 15.97:1 | Sí |

El naranja es el color más llamativo de la marca, pero con blanco no se lee. Por eso solo lo uso como fondo, con texto Azul Noche encima.

## Publicación

- Repositorio: https://github.com/mariangeles05/CSS_HTML_trayectoria1