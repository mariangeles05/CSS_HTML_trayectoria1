# Rueda Nocturna · Week 3 · Day 2 · Layouts, responsive and Bootstrap vs Tailwind

Today the kit became the full Rueda Nocturna landing: layout, mobile-first, the brand theme with dark mode, a cleaner code and a verdict between the two frameworks with my own measurements.

### Mini-Challenge 5 · Landing layout
Header, hero, routes, "¿Cómo funciona?" (four steps), registration strip and footer, all in the same container (`mx-auto max-w-6xl px-6`). Grid for the routes and the steps (equal columns), Flexbox for the header and the footer (one row).

### Mini-Challenge 6 · Mobile-first
The classes without a prefix are the phone; `sm:`, `md:` and `lg:` add the rest. Routes 1 → 2 → 3 columns, steps 1 → 2 → 4, header stacked on mobile and in a row from `md`. No horizontal scroll at 360, 768, 1024 or 1280 px.

### Mini-Challenge 7 · Brand theme and dark mode
`@theme` with the six brand colors (the five of the site + Amarillo Farol) and the two fonts. Dark mode with `dark:`. Verde Ruta on Azul Noche gives only 3.01:1, so in dark mode prices and links use Amarillo Farol (11.08:1).

### Mini-Challenge 8 · @apply and verdict
Three classes with `@apply` (`.btn-principal`, `.btn-secundario`, `.btn-contorno`), classes ordered by category, and the CSS minified with `--minify`. Measured: Tailwind 24.8 KB of CSS and 0 KB of JS against 306.1 KB of Bootstrap CSS + JS in the site v2.0. Recommendation: Tailwind for the next version of the site.

### Publication
- Landing: https://mariangeles05.github.io/CSS_HTML_trayectoria1/Semana3/Dia2/nocturna/
- Component kit: https://mariangeles05.github.io/CSS_HTML_trayectoria1/Semana3/Dia2/nocturna/componentes.html
- Log: `bitacora.md`
