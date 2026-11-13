# Bitácora Rueda Nocturna · Week 3 · Day 1

The client is launching "Rueda Nocturna" (guided night rides, Thursday to Saturday at 7:30 p. m.) and wants a landing that does not look like "just another Bootstrap site". I am building it with Tailwind CSS in the `nocturna/` folder.

# Day 1 · Introduction to Tailwind CSS

## MiniChallenge 1: Night Prototype with the Play CDN

### What I Did
- I created `nocturna/prototipo.html` with the base structure and the Tailwind v4 Play CDN (`<script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4">`). The script reads the classes in the HTML and creates the CSS in the browser.
- The hero has everything design asked for: the tag "Nuevo · Jueves a sábado", one `h1` ("Rueda Nocturna"), the subtitle, the two highlights ("3 rutas" and "Desde $55.000") and the "Inscríbete" link.
- No `<style>`, no `style=""` and no Bootstrap: only utilities.

| Family | Utilities I used |
|---|---|
| Spacing | `px-6 py-24`, `mb-4`, `mb-6`, `mb-10`, `p-4`, `gap-4`, `mx-auto` |
| Sizes | `max-w-3xl`, `max-w-xl`, `max-w-md`, `w-1/2` |
| Colors | `bg-slate-950`, `bg-slate-800`, `bg-amber-300`, `bg-emerald-600`, `text-slate-100`, `text-slate-300`, `text-amber-300` |
| Typography | `text-5xl`, `text-xl`, `font-extrabold`, `font-semibold`, `leading-tight`, `tracking-widest`, `uppercase` |

### The "Inscríbete" Button: Bootstrap vs Tailwind
- **Week 2 (Bootstrap):** `<a class="btn btn-primary btn-lg">`. Three classes, and Bootstrap already decides the padding, the radius, the colors, the hover and the focus. To give it the Verde Ruta I had to override `--bs-primary` and the `--bs-btn-*` variables in `styles.css`.
- **Today (Tailwind):** `<a class="inline-block rounded-lg bg-emerald-600 px-8 py-3 text-lg font-semibold text-white">`. Seven classes, and each one is a single property. Nothing comes "for free": there is no hover or focus until I write it.
- **Key difference:** a component framework gives me finished pieces with a look already decided, and I adapt them. A utility-first framework gives me small building blocks (one property each), and the design is mine from the start. That is why the client's request ("it should not look like another Bootstrap site") fits Tailwind better.

## MiniChallenge 2: From Prototype to Real Project (CLI and Buttons)

### Setup
Inside `nocturna/` (it needs Node.js):

```bash
npm install tailwindcss @tailwindcss/cli
npx @tailwindcss/cli -i ./src/input.css -o ./src/output.css --watch
```

- `src/input.css` has only one line: `@import "tailwindcss";`.
- `.gitignore` has `node_modules/`, so the packages (about 27 MB here) do not go to GitHub.
- `nocturna/index.html` links `src/output.css` and no longer has the Play CDN script. I moved the hero from the prototype there.
- I do commit `src/output.css`: GitHub Pages only serves files, it does not run the CLI. If I forget it, the page loads without styles.

### How the Classes Are Generated
I searched `src/output.css` (13 KB):
- `.bg-emerald-600` **is there**, with its variable `--color-emerald-600: oklch(59.6% 0.145 163.225)`.
- `.bg-pink-500` **is not there**, and neither is `--color-pink-500`.

Why: the CLI reads my files (`.html` inside `nocturna/`), looks for text that looks like a class and only writes the CSS for the classes it finds. That is why the classes must be written complete in the HTML: if I built `bg-${color}-500` by joining text, Tailwind would never see it. It also explains why the file is small: it does not carry the whole framework like Bootstrap.

### The Three Buttons
All of them share the same base: `inline-block rounded-lg border-2 px-6 py-3 font-semibold` plus the focus ring.

| Variant | Colors | Hover |
|---|---|---|
| Main ("Inscríbete") | `bg-emerald-600 text-white border-transparent` | `hover:bg-emerald-700 hover:shadow-lg` |
| Secondary ("Ver rutas") | `bg-amber-300 text-slate-950 border-transparent` | `hover:bg-amber-200 hover:shadow-lg` |
| Outline ("¿Cómo funciona?") | `border-slate-100 text-slate-100` | `hover:bg-slate-100 hover:text-slate-950` |

- The filled buttons also have `border-2`, but transparent. That way the three measure exactly the same (52 px high); otherwise the outline one would be 4 px taller.
- **Focus:** I removed the browser outline with `focus:outline-none`, so I replaced it with a visible ring: `focus:ring-4 focus:ring-amber-300 focus:ring-offset-2 focus:ring-offset-slate-950` (a 2 px dark gap and then a 4 px yellow ring).

### Keyboard Test
With Tab I went through the three buttons: each one shows the yellow ring and the computed `box-shadow` contains the ring. With hover the background changes in all three.

## MiniChallenge 3: Night Route Cards

### What I Did
- In `nocturna/index.html` I created the "Rutas" section (`id="rutas"`) with one card per route, one below the other (`space-y-8`). The grid comes tomorrow.
- Each card has: an image with `h-48 w-full object-cover` (same height and full width in the three), the level tag, the name (`h3`), a `dl` with distance, duration and meeting point, the price and the main button from MiniChallenge 2.
- The photos are the route photos of the site with a night color grade (darker and bluer), saved in `nocturna/img/`.

### Card Classes
| Part | Utilities |
|---|---|
| Box | `overflow-hidden rounded-lg border border-slate-700 bg-slate-900 shadow-md` |
| Hover | `hover:border-amber-300 hover:shadow-xl` |
| Body | `p-6` |
| Data name | `text-xs uppercase tracking-wide text-slate-400` (small and secondary) |
| Data value | `text-lg font-semibold` (highlighted) |
| Price | `text-3xl font-extrabold text-amber-300` + "por persona" in `text-sm text-slate-400` |

### Level Tag
| Level | Classes |
|---|---|
| Nivel fácil | `bg-emerald-200 text-emerald-950` |
| Nivel medio | `bg-amber-200 text-amber-950` |
| Nivel difícil | `bg-rose-200 text-rose-950` |

The color helps, but the text says the level too, so a person who does not see colors well still knows it.

### Checks
- The three `article` have exactly the same classes; only the data and the tag color change.
- On hover the border changes from slate to amber and the shadow gets bigger. I measured the position of the title, the data and the button inside the card before and after the hover: nothing moved, because the border is still 1 px and I did not use `translate` or `scale`.
- The button text has `<span class="sr-only">a Luces del Centro</span>`, so a screen reader hears "Inscríbete a Luces del Centro" and not three identical "Inscríbete".
- No CSS of my own: everything comes from utilities.

## MiniChallenge 4: Rueda Nocturna Component Kit v0.1

### What I Did
- I created `nocturna/componentes.html` with the four component types: the three buttons, one route card (copied from MiniChallenge 3), three alerts and two form fields.
- **Alerts:** information (sky), success (emerald) and warning (amber). Each one has a soft background (`bg-*-950`), a colored left border (`border-l-4`), a bold title and the text. The success alert has `role="status"`, so screen readers announce it as a notice without interrupting.
- **Fields:** email and phone, each with a visible `<label for="...">`, border, padding, placeholder, a help text below linked with `aria-describedby` and a visible focus (yellow border + the same ring as the buttons).

### Kit Rules
| Rule | Value | Where |
|---|---|---|
| Border radius | always `rounded-lg` (8 px) | buttons, cards, alerts and fields (pills only for tags) |
| Spacing scale | only 2, 3, 4 and 6 (`px-6 py-3` buttons, `p-6` card, `p-4` alerts, `px-4 py-3` fields, `mb-2`/`mt-2` label and help) | all components |
| Main color | `emerald-600` (hover `emerald-700`) | main button |
| Accent color | `amber-300` | secondary button, prices, focus ring, card hover |
| Neutrals | `slate-950` page, `slate-900` card and field, `slate-700`/`slate-600` borders, `slate-400` secondary text | all |
| Focus | `focus:outline-none focus:ring-4 focus:ring-amber-300 focus:ring-offset-2 focus:ring-offset-slate-950` | everything you can focus |

I checked the rules in the browser: every button, card, alert and field has `border-radius: 8px`.

### Keyboard Test
With Tab: "Ver la landing" → the three buttons → the card button → email → phone. All of them show the yellow ring. The two fields have their associated label.

### Publication
After pushing, the kit is at `https://github.com/mariangeles05/CSS_HTML-Trayectoria-1-week3.git`. GitHub Pages: `https://mariangeles05.github.io/CSS_HTML-Trayectoria-1-week3/` loads with 200 and there are no 404 errors.
