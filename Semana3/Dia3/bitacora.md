# Bitácora Rueda Nocturna · Week 3 · Day 3

Starting point: the Day 2 landing (responsive, brand theme, dark mode, `@apply` buttons) and the Rueda Libre v2.0 site made with Bootstrap in week 2, which is in the root of this folder.

# Day 3 · Delivery, Presentation and Review (Time Trials)

## MiniChallenge 9: Time Trial 1 · Registration for Rueda Nocturna

**Time limit:** 40 min · **Real time:** approx. 38 min · **Pending:** nothing.

### What I Did
- I split the yellow strip and the form: the strip keeps the "Quiero inscribirme" button, and the new section `#inscripcion` has its heading, a short text and the form.
- The form has three `fieldset` with their `legend`: "Tus datos", "Tu recorrido" and "Confirmación".

| Data | Control | Rule |
|---|---|---|
| Full name | `input type="text"` | `required minlength="3"` |
| Email | `input type="email"` | `required` (the type checks the format) |
| Phone | `input type="tel"` | `required pattern="3[0-9]{9}"` with `title` (10 digits, starts with 3) |
| Route | `select` with the three routes | `required` and an empty first option |
| Departure day | 3 `radio` (jueves, viernes, sábado) inside a `fieldset` | `required` in the group |
| Companions | `input type="number"` | `required min="0" max="3"` |
| Experience level | `select` (principiante, intermedio, avanzado) | `required` |
| Own bike | 2 `radio` (sí / no) | `required` |
| Conditions | `checkbox` | `required` |

- Every field has its label: the text fields and selects with `label for`, and the radios and the checkbox wrapped inside their `label`.
- **Style:** the same fields from the kit (`INPUT` classes, `rounded-lg`, focus ring). The short fields go in `grid grid-cols-1 md:grid-cols-2`; the name uses `md:col-span-2`. Radios and checkbox use `accent-verde-ruta` (`dark:accent-amarillo-farol`), and the `body` has `dark:scheme-dark` so the native lists of the `select` are also dark.
- **Without JavaScript:** only native validation. The form sends to `#inscripcion` (`method="get"`), so on a static site like GitHub Pages it does not give an error.

### Tests
| Test | Result |
|---|---|
| Empty | It is not sent; the browser marks the 8 required groups (name, email, phone, route, day, level, own bike, conditions) |
| Invalid data (`Al`, `ana@`, `2001234567`, 5 companions) | It is not sent: minimum 3 characters, incomplete email, format of the phone and "must be less than or equal to 3" |
| Complete | It is sent: the page reloads at `#inscripcion` with the data in the URL |
| Keyboard only | Tab between fields, arrows in the `select`, Space for radios and checkbox, Enter on "Enviar inscripción": sent |
| 360 px / 768 px | 1 column / 2 columns, no horizontal scroll |
| Light and dark | No text under 4.5:1 (minimum 4.93:1 light and 5.31:1 dark) |

## MiniChallenge 10: Time Trial 2 · One Ecosystem

**Time limit:** 40 min · **Real time:** approx. 35 min · **Pending:** nothing.

### What I Did
**In the site v2.0 (Bootstrap):**
- "Rueda Nocturna" (with the `bi-moon-stars` icon) is now in the navbar of the three pages: `nocturna/index.html` from the home page and `../nocturna/index.html` from `paginas/`.
- The carousel has a fourth slide after the three promotions, "Nuevo: Rueda Nocturna", with its indicator and a "Conoce Rueda Nocturna" button to the landing. The button uses my own variant from week 2, `btn btn-pedal`.
- I added Amarillo Farol to the brand variables of `styles.css` (`--amarillo-farol: #FFD166`), so the site and the landing have the same six colors.
- I added the WhatsApp line to the footer of the three pages, so the contact data is the same as in the landing.

**In the landing (Tailwind):**
- The logo now goes to the site home page (`../index.html`), with an `aria-label` that says so.
- In the hero there is a "Reserva tu bici" button (outline variant) to `../paginas/reservas.html`.
- In the footer: the same contact data as the site (email and WhatsApp 300 000 0000) and the opening hours of the office.

### Relative Paths
| From | To | Path |
|---|---|---|
| `index.html` (root of the site) | landing | `nocturna/index.html` |
| `paginas/tarifas.html`, `paginas/reservas.html` | landing | `../nocturna/index.html` |
| `nocturna/index.html` | site home | `../index.html` |
| `nocturna/index.html` | reservations | `../paginas/reservas.html` |
| `nocturna/index.html` | logo | `../img/logo.svg` (the same file as the site) |

### Same Brand in Both Products
I compared the values in `css/styles.css` (Bootstrap site) and `nocturna/src/input.css` (`@theme`):

| Color | Bootstrap | Tailwind |
|---|---|---|
| Verde Ruta | `#1E7A4F` | `#1E7A4F` |
| Naranja Pedal | `#F39A2B` | `#F39A2B` |
| Azul Noche | `#14213D` | `#14213D` |
| Crema | `#FAF6EF` | `#FAF6EF` |
| Gris Asfalto | `#5B6470` | `#5B6470` |
| Amarillo Farol | `#FFD166` | `#FFD166` |

Fonts: `"Montserrat", Arial, sans-serif` for headings and `"Open Sans", Helvetica, sans-serif` for text in both. I also made the Google Fonts link the same in the four pages (Montserrat 700 and 800, Open Sans 400, 600 and 700).

### Link Check
I served the repository like GitHub Pages and went through every link of the four pages (home, tarifas, reservas and landing), including the anchors: no 404 and no missing anchor. From any page of the site the landing is one click away, and from the landing I get back to the site and to reservations.

## MiniChallenge 11: Time Trial 3 · Last-Minute Request

**Time limit:** 45 min · **Real time:** approx. 42 min · **Pending:** nothing.

### What I Did
- New section `#planes` ("Planes Rueda Nocturna"), before the registration, and a "Planes" link in the header.
- **Grid:** `grid grid-cols-1 gap-8 lg:grid-cols-3`. Grid stretches the items of a row by default, so the three cards have the same height.
- **Each card in a column:** `flex flex-col justify-between gap-8`. The card has two children (the content and the button), so `justify-between` sends the button to the end even when the list is shorter.
- **Benefits list:** `flex flex-col gap-3`, and each item `flex items-start gap-3` with a ✓ (`aria-hidden="true"`, the text already says the benefit).
- **Pareja plan:** the tag "Más elegido" at the beginning of the card, a different background (`bg-verde-ruta/5`, dark `bg-white/10`) and a thicker colored border.

### The Box Model Problem with the Thicker Border
My first version used `border-4` in Pareja and `border-2` in the others. In DevTools the three cards measured 347 px wide, but the Pareja button ended 2 px higher (393 px vs 395 px from the top of the card): the extra 2 px of border on each side push the content inside the box. So the buttons were not on the same line.

Solution: all the cards have `border-2` and `p-8`, and Pareja adds `ring-2`. The ring is a `box-shadow`, so it is drawn outside the box and does not take space: visually the border is 4 px, but the box model is the same as the others.

### Checks in DevTools (Computed)
| Card | Width | Height | Padding | Border | Bottom of the button |
|---|---|---|---|---|---|
| Individual | 347 px | 425 px | 32 px | 2 px | 391 px |
| Pareja | 347 px | 425 px | 32 px | 2 px (+ 2 px ring) | 391 px |
| Grupo | 347 px | 425 px | 32 px | 2 px | 391 px |

- 360 px: one column, no horizontal scroll.
- Pareja stands out by color and by text ("Más elegido").
- Dark mode: border and ring in Amarillo Farol. Lowest contrast of the section: 4.61:1 (the green price on the light green background of Pareja, light mode), so it passes.

## MiniChallenge 12: Rueda Nocturna Launch (Delivery and Demo)

### Final Checklist (Both Products)
I checked the five pages (home, tarifas, reservas, landing and kit) at 360, 768 and 1280 px, and the landing and the kit also in dark mode:

| Item | Result |
|---|---|
| Semantic structure | One `h1` per page and headings without jumps |
| Images | All of them have `alt` (decorative logo with `alt=""`) |
| Contrast | No text under 4.5:1 (the lowest is 4.61:1, the Pareja price) |
| Keyboard | Everything can be reached with Tab and shows a visible focus |
| Forms | Every field has its label; reservations and registration do not send with errors |
| Responsive | No horizontal scroll at 360, 768 or 1280 px |
| Dark mode (landing and kit) | All sections change, light mode still works |
| 404 errors | 0 (I went through every link and anchor) |
| Inline styles | 0 `style=""` and 0 `<style>` |
| `output.css` | Minified (26.6 KB with the form and the plans; 24.8 KB when I measured it in MiniChallenge 8), one single line and committed |

### W3C Validator
I validated the landing, the kit, the prototype and the site pages (home, tarifas and reservas) with the W3C Nu HTML Checker: **0 errors and 0 warnings** in every page. The policies modal of reservas already had `role="dialog"` next to its `aria-labelledby` since week 2, so there was nothing to fix this time.

### README
I turned this log into `README.md`: description, live links, pages, structure, technologies, how to run it, screenshots (desktop, mobile and dark mode, in `capturas/`), the framework recommendation, the checklist, what I learned and the author.

### Publication
Launch commit and tag `v3.0`, published in GitHub Pages.

### Demo Script (3 minutes)
| Time | What I show | What I say |
|---|---|---|
| 0:00 – 0:30 | Site home page | "Rueda Libre rents bikes in Medellín. They are launching Rueda Nocturna, night rides Thursday to Saturday, and they wanted a landing that does not look like a Bootstrap template." |
| 0:30 – 1:15 | Navbar → "Rueda Nocturna" → hero, routes, how it works, plans | "From any page of the site you get here with one click. Same brand, but built with Tailwind." |
| 1:15 – 1:45 | Registration: send it empty, then complete it | "Native validation: name of 3 characters, phone of 10 digits that starts with 3, 0 to 3 companions." |
| 1:45 – 2:15 | Device mode at 360 px and DevTools → dark mode | "Mobile-first: one column on the phone. Dark mode follows the system preference." |
| 2:15 – 3:00 | Two technical decisions | 1) "I measured both frameworks: 26.6 KB of Tailwind for the whole landing against 306 KB of Bootstrap CSS + JS, so I recommend Tailwind for the next version." 2) "In the plans, a thicker border moved the Pareja button 2 px; I used a `ring`, which does not take space in the box model, and the three buttons are on the same line." |

### Rehearsal Feedback
- Classmate: ______
- Real duration: ___ min ___ s
- Feedback: ______
- What I will change: ______

### Week Summary
- **Day 1 (MiniChallenges 1–4):** Play CDN prototype, Tailwind CLI project, buttons, route cards and the component kit.
- **Day 2 (MiniChallenges 5–8):** full landing, mobile-first, `@theme` + dark mode, `@apply` and the Bootstrap vs Tailwind verdict.
- **Day 3 (MiniChallenges 9–12):** registration form, integration with the site, plans section and the launch.
