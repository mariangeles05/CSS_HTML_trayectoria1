# Bitácora Rueda Nocturna · Week 3 · Day 2

Starting point: the Day 1 landing (hero, buttons, route cards) and the component kit.

# Day 2 · Layouts and Responsive with Tailwind; Bootstrap vs Tailwind

## MiniChallenge 5: Building the Landing Layout

### What I Did
- `nocturna/index.html` is now the full landing, with semantic tags: `header`, `main` with one `section` per block (each one with an `id` for the anchors: `#inicio`, `#rutas`, `#como-funciona`, `#inscripcion`) and `footer`.
- **Same container everywhere:** the content of the header, every section and the footer is inside `mx-auto max-w-6xl px-6`. At 1280 px all of them measure 1152 px with 24 px of side padding.
- **Header:** `flex items-center justify-between`. Logo and name on one side; the section links and the "Inscríbete" button on the other, vertically centered.
- **Routes:** the three cards from the kit in `grid grid-cols-3 gap-8`.
- **¿Cómo funciona?:** four steps (Elige tu ruta, Inscríbete, Recoge tu equipo, Rueda) in an `ol` with `grid grid-cols-4 gap-6`.
- **Registration strip:** a section with an emerald background, the text on one side and the outline button on the other (`flex justify-between items-center`).
- **Footer:** three blocks (Rueda Libre, Contacto, Salidas) with `flex justify-between gap-8`.
- I copied the buttons and the cards from `componentes.html` without creating new variants.

### Grid or Flex for the Steps?
I used **Grid**. The four steps must have exactly the same width, whatever the length of their text, and tomorrow they have to become a 2×2 square on tablet. With flex I would have to force the widths by hand (`basis-1/4`) and the second row would not line up with the first one. With `grid-cols-4` → `grid-cols-2` the columns stay aligned. The header and the footer are flex because they are just one row of pieces that take the size of their content.

### Checks at 1280 px
- Header in one row (logo and nav at the same height).
- Routes: 3 columns of 347 px. Steps: 4 columns of 258 px.
- The 3 header anchors exist as sections and take me to each one.

## MiniChallenge 6: The Night Fits in Your Phone (Responsive)

### What Broke at 360 px (Before)
1. The page measured 561 px wide: horizontal scroll.
2. The header tried to fit logo, three links and the button in one row; "¿Cómo funciona?" broke into two lines and the button went outside the screen.
3. The routes were 3 columns of 83 px: the names were cut ("Luce", "Mira") and the tags broke.
4. The steps were 4 columns of 60 px.
5. The registration strip and the footer squeezed their blocks side by side.
6. The `h1` at `text-5xl` used two lines and almost the whole screen.

### What I Changed (Mobile-First)
The classes without a prefix are now the phone version; `sm:` (640 px), `md:` (768 px) and `lg:` (1024 px) only add what changes on bigger screens. I never use `sm:` for the phone.

| Element | Phone (no prefix) | Bigger screens |
|---|---|---|
| Header | `flex-col` (logo above, button below) | `md:flex-row md:justify-between` |
| Section links | `hidden` | `md:flex` |
| "Inscríbete" button in the header | always visible | — |
| Routes | `grid-cols-1` | `sm:grid-cols-2`, `lg:grid-cols-3` |
| Steps | `grid-cols-1` | `sm:grid-cols-2`, `lg:grid-cols-4` |
| Strip and footer | `flex-col` | `md:flex-row` |
| `h1` | `text-4xl` | `sm:text-5xl`, `lg:text-7xl` |
| Section titles | `text-2xl` | `lg:text-4xl` |
| Section padding | `py-12` (hero `py-16`) | `lg:py-20` (hero `lg:py-28`) |

### Tests in Device Mode
| Width | Header | Links | Routes | Steps | `h1` | Horizontal scroll |
|---|---|---|---|---|---|---|
| 360 px | stacked | hidden | 1 column | 1 column | 36 px | no |
| 768 px | one row | visible | 2 columns | 2 columns | 48 px | no |
| 1024 px | one row | visible | 3 columns | 4 columns | 72 px | no |
| 1280 px | one row | visible | 3 columns | 4 columns | 72 px | no |

I also checked 640 px: the routes change to 2 columns exactly there (`sm`), and at 1024 px to 3 (`lg`).

## MiniChallenge 7: Night Brand (Own Theme and Dark Mode)

### What I Did
- In `src/input.css`, after `@import "tailwindcss";`, I added an `@theme` block with the six brand colors and the two fonts:

```css
@theme {
  --color-verde-ruta: #1E7A4F;
  --color-naranja-pedal: #F39A2B;
  --color-azul-noche: #14213D;
  --color-crema: #FAF6EF;
  --color-gris-asfalto: #5B6470;
  --color-amarillo-farol: #FFD166;
  --font-titulos: "Montserrat", Arial, sans-serif;
  --font-texto: "Open Sans", Helvetica, sans-serif;
}
```

- Tailwind creates the utilities from those names: `bg-verde-ruta`, `text-azul-noche`, `border-naranja-pedal`, `font-titulos`, `font-texto`... The fonts load from Google Fonts in the `head`; the `body` has `font-texto` and the headings have `font-titulos`.
- I replaced every generic color in the landing and in `componentes.html`. I searched both files for `slate-`, `emerald-`, `amber-`, `rose-` and `sky-`: 0 results. Only brand colors remain (and white/black with opacity, like `bg-white/5` for the dark cards).
- **Dark mode:** I added `dark:` to backgrounds, texts, cards, borders and fields. I used the default strategy (the system preference, `prefers-color-scheme`), so I did not need any JavaScript.

| Part | Light | Dark |
|---|---|---|
| Page | `bg-crema text-azul-noche` | `dark:bg-azul-noche dark:text-crema` |
| Hero | `bg-white` | `dark:bg-black/30` |
| Cards and steps | `bg-white border-gris-asfalto/30` | `dark:bg-white/5 dark:border-white/15` |
| Secondary text | `text-gris-asfalto` | `dark:text-crema/80` |
| Prices and links | `text-verde-ruta` | `dark:text-amarillo-farol` |
| Fields | `bg-white border-gris-asfalto` | `dark:bg-white/5 dark:border-crema/40` |
| Focus ring | `ring-azul-noche` | `dark:ring-amarillo-farol` |

- Level tags: fácil `bg-verde-ruta text-white`, medio `bg-amarillo-farol text-azul-noche`, difícil `bg-naranja-pedal text-azul-noche`.
- The registration strip is Amarillo Farol with Azul Noche text in both modes; the footer is Azul Noche like the main site.

### Contrast in Dark Mode
| Combination | Ratio | Result |
|---|---|---|
| **Verde Ruta on Azul Noche** | **3.01:1** | **Fails.** I do not use green as text in dark mode: prices and links change to Amarillo Farol |
| Amarillo Farol on Azul Noche | 11.08:1 | Passes |
| Crema on Azul Noche | 14.83:1 | Passes |
| Crema 80 % on Azul Noche (secondary text) | 9.90:1 | Passes |
| Crema 70 % on a dark field (placeholder) | 7.11:1 | Passes |
| White on Verde Ruta (main button) | 5.31:1 | Passes in both modes |
| Azul Noche on Amarillo Farol (strip, tags) | 11.08:1 | Passes |
| Azul Noche on Naranja Pedal ("difícil" tag) | 7.20:1 | Passes |

I also checked every text of the two pages automatically (text color against its real background): in dark mode the minimum is 5.31:1. In light mode one alert failed: the green title of the success alert on its light green background gave 4.30:1. I changed the title to Azul Noche and kept the green in the border and background.

The focus ring also changes: Amarillo Farol is almost invisible on Crema (1.3:1), so in light mode the ring is Azul Noche.

### How I Tested It
DevTools → Rendering → "Emulate CSS media feature prefers-color-scheme: dark". All sections change together; with "light" the landing looks the same as before.

## MiniChallenge 8: Readable Code and Verdict (Bootstrap vs Tailwind)

### Most Repeated Class Lists (Before)
| Class list | Times in the landing | Classes per element |
|---|---|---|
| Main button | 6 | 21 |
| Data name in the cards (`text-xs uppercase tracking-wide text-gris-asfalto dark:text-crema/75`) | 9 | 5 |
| Data value (`text-lg font-semibold`) | 9 | 2 |
| Step box / card box | 4 / 3 | 7 / 11 |
| Level tag | 3 | 8 |
| Secondary and outline buttons | 1 each (also in the kit) | 19 and 21 |

### What I Changed
- **Buttons with `@apply`:** a button is one small element that repeats a lot and always looks the same, so in `src/input.css` I created three classes inside `@layer components`: `.btn-principal`, `.btn-secundario` and `.btn-contorno`. Each one has the same utilities it had in the HTML (including `hover:`, `focus:` and `dark:`). Now a button is `<a class="btn-principal">`. Those are the only three classes of my own.
- **Bigger pieces stay as markup:** the cards, the steps and the tags keep the kit utilities. I reuse the same markup in the three cards instead of creating `.card` with `@apply`, because then I would be rebuilding Bootstrap and I would lose the advantage of seeing the design in the HTML.
- **Order of the classes:** in every element they now go by category: layout → spacing → typography → color, borders and shadows → states. Responsive (`sm:`, `md:`, `lg:`) and `dark:` go right after the base class of their category, and `hover:`/`focus:` go at the end. For example, the level tag: `inline-block mb-3 px-3 py-1 text-xs font-bold uppercase tracking-wide rounded-full bg-verde-ruta text-white`.

### Did Anything Change on Screen?
I saved the computed styles (position, size, colors, borders, shadows, padding) of every visible element before and after the refactor, at 360 and 1280 px, in light and dark mode, plus the focus ring of a button: **0 differences** in the 16 comparisons. The page looks exactly the same.

### Measurements
`npx @tailwindcss/cli -i ./src/input.css -o ./src/output.css --minify`. Sizes of the files; the gzip column is what travels over the network when the server compresses them (DevTools → Network shows this "transferred" size).

| File | Size | gzip |
|---|---|---|
| Tailwind `output.css` without minify | 31.8 KB | 5.0 KB |
| **Tailwind `output.css` --minify (whole landing)** | **24.8 KB** | **4.6 KB** |
| Tailwind JavaScript | 0 KB | 0 KB |
| `bootstrap.min.css` (site v2.0) | 227.3 KB | 30.1 KB |
| `bootstrap.bundle.min.js` (site v2.0) | 78.8 KB | 23.3 KB |
| `bootstrap-icons.min.css` + `bootstrap-icons.woff2` | 83.9 KB + 127.3 KB | 13.3 KB + 127.3 KB |
| `styles.css` (my identity over Bootstrap) | 8.2 KB | 2.5 KB |

In Network, the v2.0 home page loads `bootstrap.min.css`, `bootstrap-icons.min.css`, the icon font, `bootstrap.bundle.min.js` and `styles.css`. The landing loads only `output.css` (and Google Fonts in both). Only Bootstrap CSS + JS is **306.1 KB** against **24.8 KB** of Tailwind: about 12 times more.

### Bootstrap vs Tailwind
| Criterion | Bootstrap (site v2.0) | Tailwind (Rueda Nocturna) |
|---|---|---|
| **Learning curve** | Faster to start. With `container`, `row`, `col-*` and copying components from the docs I had a page working in one session. | Slower at the beginning: I had to learn many utility names, Node and the CLI, and nothing comes ready (I wrote every hover and every focus ring). After building the kit, the landing was put together very quickly. |
| **Customization** | Possible, but on top of the framework: I had to override `--bs-primary`, `--bs-body-*` and the `--bs-btn-*` variables in `styles.css`, and some things (the focus and the checked state of the form fields, the focus of the carousel controls, the red of the validation) had no variable and needed extra rules. | Natural: `@theme` creates `bg-verde-ruta`, `font-titulos`... and the dark mode is just `dark:`. The landing does not look like any template. |
| **Final size** | 306.1 KB of CSS + JS (plus 211 KB of icons), even if I only use a part. | 24.8 KB of CSS and 0 KB of JS, because the CLI only generates the classes I use. |
| **Use cases** | Admin panels, internal tools, prototypes, teams that need interactive components (navbar collapse, modal, carousel, validation) without writing JavaScript. | Sites with their own identity, landings and products where the design matters and performance on mobile counts. Interactive pieces need some JavaScript of my own. |

### Recommendation for Rueda Libre
I recommend **Tailwind CSS** for the next version of the whole site. Rueda Libre is a small, content site with a strong brand, and most of its traffic comes from phones (the campaign is promoted on social networks): Tailwind gives the brand without fighting the framework and loads 12 times less CSS and JS. The kit I built this week (buttons, card, alert, field) already covers most of the pages. The cost: the navbar, the carousel and the reservation modal now come from the Bootstrap bundle, so in Tailwind I would have to write that small JavaScript or simplify those pieces (for example, a mobile menu with a `<details>` and no carousel). If the client did not have anyone to maintain that JavaScript, Bootstrap would still be a reasonable option.
