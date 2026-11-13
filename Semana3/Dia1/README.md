# Rueda Nocturna · Week 3 · Day 1 · Introduction to Tailwind CSS

The client is launching **Rueda Nocturna** (guided night rides, Thursday to Saturday at 7:30 p. m.) and wants a landing that does not look like "just another Bootstrap site". Today I started it with Tailwind CSS in `nocturna/`.

### Mini-Challenge 1 · Prototype with the Play CDN
`nocturna/prototipo.html`: the hero (tag, title, subtitle, two highlights and "Inscríbete") only with utilities, using the Tailwind v4 Play CDN. The Bootstrap button was 3 classes with a look already decided; the Tailwind one is 7 utilities and the design is mine.

### Mini-Challenge 2 · CLI and buttons
`npm install tailwindcss @tailwindcss/cli`, `src/input.css` with `@import "tailwindcss";` and `npx @tailwindcss/cli -i ./src/input.css -o ./src/output.css --watch` to generate `src/output.css`. `node_modules/` is in `.gitignore`. Three button variants (main, secondary, outline) with `hover:` and a visible `focus:ring`. The CLI only writes the classes it finds in my files: `bg-emerald-600` is in `output.css`, `bg-pink-500` is not.

### Mini-Challenge 3 · Route cards
Luces del Centro, Miradores de la Ciudad and Luna en Las Palmas, with image, level tag (fácil, medio, difícil), distance, duration, meeting point, price and button. The hover changes the border and the shadow without moving the content.

### Mini-Challenge 4 · Component kit v0.1
`nocturna/componentes.html`: buttons, card, three alerts (information, success with `role="status"`, warning) and two fields with label, help text and visible focus. Kit rules: `rounded-lg` everywhere, spacing scale 2/3/4/6 and the same focus ring.

### Publication
Github: `https://github.com/mariangeles05/CSS_HTML-Trayectoria-1-week3.git`
GitHub Pages: `https://mariangeles05.github.io/CSS_HTML-Trayectoria-1-week3/`
- Log: `bitacora.md`
