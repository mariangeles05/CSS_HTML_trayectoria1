# Rueda Libre · Week 1 · Day 3

Last day of the week. I converted styles into variables, grasped inheritance and specificity, compared the two box models, and applied positioning for the v1.0 launch.

## Variables

I defined colors, fonts, and spacing once within `:root`. If the client decides to change a color, I only need to update it in one place.

```css
:root {
--verde-ruta: #1E7A4F; 
--azul-noche: #14213D; 
--esp-m: 1rem;
}
```

## Inheritance

I selected a `<p>` element and checked the "Computed" tab.

- **`font-family` is inherited:** the paragraph displays "Open Sans," even though I only declared it on the `body`.
- **`background-color` is not inherited:** the paragraph shows `rgba(0,0,0,0)`—it’s transparent. It appears cream-colored only because the `body` background shows through.

## Specificity

The link for the current page had the `.activo` class, but its color wasn't changing; in DevTools, the style appeared crossed out.

- `#menu a` → (1,0,1): one ID and one element
- `.activo` → (0,1,0): one class

`#menu a` takes precedence because it includes an ID. I resolved this using `#menu a.activo` → (1,1,1)—no `!important` required.

I also updated the header to have a white background, as the previous gray menu color against the "Midnight Blue" (`Azul Noche`) background only yielded a 2.66:1 contrast ratio.

## Box Model

I measured a card within a 1280px viewport: `width: 100%` (the `main` container is 960px wide), with 1.5rem of padding and a 1px border. - **content-box:** measures 1010px (960 + 48 padding + 2 border) and extends outside the `main` element.
- **border-box:** measures 960px, because the padding and border are contained within it. The content itself measures 910px.

That is why I set `box-sizing: border-box` for the entire site.

## Positioning (v1.0 release)

- **"New" label:** the `.tarjeta` (card) has `position: relative`, and the `.etiqueta` (label) has `position: absolute` with `top` and `right` properties, placing it in the corner of its respective card.
- **WhatsApp button:** uses `position: fixed` at the bottom right, so it remains in place while scrolling. I added `padding-bottom` to the `body` to ensure it doesn't cover the footer.
- **styles.css** is now organized into logical blocks (variables, base, navigation, components, form) with no duplicate rules.
- **Final review:** 0 404 errors, no inline styles, and the focus indicator is visible when navigating via the Tab key across all three pages.

## Weekly Summary

- **v0.1:** repository setup, homepage, pricing tables, booking section, and menu.
- **v0.2:** semantic HTML, forms, native validation, accessibility, and color palette.
- **v1.0:** variables, menu states, box model, and positioning.

Responsive design using Flexbox and Grid remains to be addressed in week 2.
