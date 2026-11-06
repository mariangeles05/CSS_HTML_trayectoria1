# Bitácora Rueda Libre v1.5

## MiniChallenge 1: Flexbox

### What I Did
- I grouped the logo and name inside `.marca` so that the `header` had only two children: the brand and the menu.
- Header: `display: flex` with `justify-content: space-between` (name and menu on opposite sides) and `align-items: center` (vertically centered).
- Menu: flexible `#menu` with `gap` and `flex-wrap: wrap`. I removed the margins from the `li` elements and the `inline-block` from week 1.
- Footer: three blocks (brand, contact, and schedule) in a row, aligned at the top with `align-items: flex-start` and separated with `gap`.
- I used the same header and footer HTML on all three pages; the styles are in `css/styles.css`.

### When Narrowing the Window
- **Header:** At around ___ px, the menu moves below the name instead of overflowing. At around ___ px, the links break into two lines.
- **Footer:** At around ___ px, the schedule block moves to another line. At around ___ px, the three blocks are stacked vertically.

### Why Use gap Instead of Margins and inline-block
`gap` only adds space between elements and is defined once in the container, without needing to adjust the edges. With Flexbox, `inline-block` is no longer necessary.

### Problems
- The `header` had three children, and `space-between` placed the name in the center. I solved this by grouping the logo and name inside `.marca`.
- The footer headings were not visible (blue text on a blue background). I fixed this with `footer h2` in white.

## MiniChallenge 2: Grid for the Fleet

### What I Did
- In `index.html`, I created the `#flota` section with the title "Our Fleet" and a `div.flota-grid` containing one `article` for each model. Each one has an image, name (`h3`), description, hourly price, and the "Book Now" link.
- The grid uses `display: grid` with `grid-template-columns: repeat(auto-fit, minmax(18rem, 1fr))`. This allows the browser to fit as many columns as possible, with a minimum width of 18rem each, and the remaining space is distributed using `1fr`. I did not use any media queries.
- The spacing between rows and columns is the same: `gap: var(--esp-l)`.
- Each card is a Flexbox column (`flex-direction: column`). Inside, it has two children: `.modelo-info` (image, name, description, and price) and the link. With `justify-content: space-between`, the link always stays at the bottom, even when the description is shorter, as happens with the Children's model.
- The cards use the `.tarjeta` class from week 1, so they keep their padding, 1 px border, and rounded corners. I only removed `margin-bottom` because the spacing is now handled by `gap`.

### Why 18rem
I tested smaller values, but at 900 px I still got three very narrow columns because `main` has a maximum width of 60rem. With 18rem (288 px), only two columns fit at 900 px, and the cards do not look narrow.

### Seventh Model
I added the Tandem ($20,000) as another `article`, without changing the CSS. The grid arranged it automatically: at 1280 px, it appeared in a third row, in the first column.

### Observed Columns (DevTools Device Mode)

| Width | Columns | Rows with 7 Models |
|---|---|---|
| 1280 px | 3 | 3 |
| 900 px | 2 | 4 |
| 500 px | 1 | 7 |

At all three widths, cards in the same row have the same height, and the "Book Now" buttons stay aligned at the bottom. There is also no horizontal scrolling.

### Why the Height Is the Same
Grid stretches the elements in a row by default to match the height of the tallest element (`align-items: stretch`). Since the card is also a Flexbox column, the extra space stays between the information and the button, moving the button to the bottom.

### Problems
- The `.tarjeta img` rule from week 1 set the images to 16rem high, making the cards too long in the grid. I added `.modelo img` with 10rem; since it has the same specificity and appears later in the CSS, it takes priority without using `!important`.
- All the links only said "Book Now", so screen reader users could not tell which model each link referred to. I added the model name inside a `span.visually-hidden`, which is invisible but can still be read.
- In `tarifas.html`, the menu marked "Reservations" as the current page. I fixed it so that `activo` and `aria-current` are set to "Rates and Routes".

## MiniChallenge 3: Desktop Layout with Grid and Flexbox

### Criteria I Used
If I only need to arrange elements in one direction (a row or a column), and each element should take up space according to its content, I use **Flexbox**. If I want to define the width of each column from the container, or align elements in rows and columns at the same time, I use **Grid**.

### Decisions

| Case | What I Used | Why |
|---|---|---|
| Homepage | Grid (`1fr 1fr`) | It is the page structure: I want the text and the photo to take up exactly half each, regardless of how much text there is. With `align-items: center`, the text is vertically centered next to the photo. |
| Routes Gallery | Grid (`repeat(3, 1fr)`) | It is a grid: all three cards have the same size, and if more routes are added tomorrow, they move to another row aligned with the ones above. This means working in two dimensions. |
| Reservations | Grid (`2fr 1fr`) | The design requires an exact proportion: the form takes up two parts and the contact section takes up one. With `fr`, I define this in the container without calculating percentages. I used `align-items: start` so the contact section does not stretch to the full height of the form. |
| Form Row | Flexbox | There are only two fields next to each other, in one direction. With `flex: 1`, each one takes up half the space, and with `gap`, they stay separated. I did not need rows and columns. |
| Header | Flexbox | It is a single row: the brand on one side and the menu on the other using `justify-content: space-between`. Each part takes up the space required by its content, and with `flex-wrap`, the menu moves down if there is not enough space. |
| Footer | Flexbox | There are three blocks in one row, with different sizes depending on the text. With `flex-wrap`, they stack when there is not enough space, without needing to define columns. |

### Checks
- At 1280 px: the homepage has two equal columns, the routes are in one row with three columns, and reservations have a 2:1 proportion.
- All columns are defined with `fr`, without percentages or `px`.
- The menu, the fleet (which still has 3 columns at 1280 px), and the form validation continue working. I tested the phone number 1234567890 again, and it is still rejected.

### Problems
- At first, I placed the document and phone fields in the same row, but the email field was between them, so three fields ended up together. I moved the email field above so the row only contains the two related short fields.
- The form and contact headings were not aligned at the top because the `h2` had a top margin. I removed it inside the reservations layout.

## MiniChallenge 4: Mobile-First (v1.5)

### How I Reorganized styles.css
I organized the file into sections: variables, base, header, footer, components, tables, and form. Everything outside a media query is the mobile version, in a single column. Then there are two media queries with `min-width` that only add the necessary changes:
- **768 px (tablet):** header and footer in a row, homepage in two columns, routes in three columns, document and phone fields in the same row, and tables with normal font size.
- **1200 px (desktop):** reservations with a 2:1 proportion.

I did not add a media query for the fleet because `auto-fit` already adjusts it automatically.

### Header and Footer
- **Mobile:** the name goes at the top and the menu below it, centered (`flex-direction: column` and `justify-content: center` in the menu). In the footer, the three blocks are stacked vertically.
- **From 768 px:** the layout from MiniChallenge 1 returns, with the name on the left and the menu on the right (`flex-direction: row` and `space-between`). The footer has the three blocks in a row.

### Columns by Width (Device Mode)

| Width | Fleet | Routes | Homepage | Reservations |
|---|---|---|---|---|
| 360 px | 1 | 1 | 1 (text above, photo below) | 1 (contact below the form) |
| 768 px | 2 | 3 | 2 | 1 |
| 1280 px | 3 | 3 | 2 | 2:1 |

At 360 px, there is no horizontal scrolling on any of the three pages.

### Responsive Images
I added `img { max-width: 100%; height: auto; }` to the base styles, so no image can be wider than its container.

### Problems I Found and How I Solved Them
1. **The menu broke into two lines at 360 px.** "Reservations" moved to another row by itself because each link had 1rem of padding on the sides. On mobile, I reduced it to 0.6rem, and from 768 px it returns to 1rem. Now all three links fit on a single line.
2. **The routes table required horizontal scrolling.** It has five columns, and with the normal font size, it did not fit at 360 px. On mobile, I set `font-size: 0.8rem` and reduced the padding in `th` and `td`. Now the entire table is readable without scrolling. From 768 px, it returns to the normal size.
3. **The fleet could overflow on very small screens.** With `minmax(18rem, 1fr)`, each card has a minimum width of 288 px, which is wider than the content on a 320 px phone. I changed it to `minmax(min(18rem, 100%), 1fr)`, so the card is never wider than its container.
4. **The 2:1 reservations layout was too narrow on tablets.** At 768 px, the form was less than 500 px wide, and the fields looked cramped. That is why the 2:1 layout starts at 1200 px, while on tablets the contact section goes below the form.
5. **The footer email could overflow.** On narrow screens, the email address is a long word without spaces. I added `overflow-wrap: anywhere` so it can break into multiple lines.

### Publication
URL v1.5: https://mariangeles05.github.io/CSS_HTML_trayectoria1/

## MiniChallenge 5: The Fleet in Bootstrap (First Comparison)

### What I Did
- I created `pruebas/catalogo-bootstrap.html` using the initial Bootstrap 5.3 template from the official documentation: the CSS through CDN in the `head` and the JavaScript bundle before closing the `body`.
- I copied the seven fleet models and changed the image paths to `../img/flota/...` because the file is now inside the `pruebas` folder.
- The layout comes entirely from the grid: `container` > `row g-4` > each model inside a `col-12 col-sm-6 col-lg-4 col-xl-3`.
- I did not write any CSS or link `styles.css` on this page.

### Observed Columns (Device Mode)

| Width | Active Breakpoint | Columns |
|---|---|---|
| 360 px | None (`col-12`) | 1 |
| 600 px | `sm` (from 576 px) | 2 |
| 800 px | `sm` (`md` was not used) | 2 |
| 1000 px | `lg` (from 992 px) | 3 |
| 1280 px | `xl` (from 1200 px) | 4 |

In Network, `bootstrap.min.css` and `bootstrap.bundle.min.js` load with status code 200, and no errors appear.

### Comparison

| | Custom CSS (MiniChallenge 2) | Bootstrap |
|---|---|---|
| Approximate Time | 45 min | 20 min |
| Fleet Layout CSS | 7 declarations in 2 rules (`.flota-grid`: display, grid-template-columns, gap; `.modelo`: display, flex-direction, justify-content, gap) | 0 lines of CSS |
| HTML Classes for Layout | 2 (`flota-grid` and `modelo`) | 6 different ones (`row`, `g-4`, `col-12`, `col-sm-6`, `col-lg-4`, `col-xl-3`); the column classes are repeated in all 7 models (28 times) |
| Aligning "Book Now" at the Bottom | `justify-content: space-between` | `h-100`, `d-flex flex-column`, and `mt-auto` |
| Media Queries | 0 (`auto-fit` adjusts automatically) | 0 written by me; Bootstrap already includes them in its classes |

In the custom version, most of the time was spent understanding `auto-fit` and `minmax()`, testing which minimum width allowed 3 columns at 1280 px and 2 columns at 900 px, and making sure the button stayed at the bottom of every card. With Bootstrap, almost all the time was spent copying the markup, changing the image paths, and looking up the class names in the documentation.

### What Bootstrap Gave Me Without Extra Work
- The breakpoints are already defined: I only need to write `col-sm-6`, and from 576 px onward, there are two columns.
- Gutters with a single class (`g-4`), with equal spacing between rows and columns.
- The card (`card`) already includes a border, rounded corners, and padding, and the button already has hover and focus styles.

### What Control I Lost
- Now I have to decide how many columns there are at each breakpoint; before, they were determined by the available space. With `auto-fit`, if I change the minimum card width, the grid rearranges itself automatically. Here, I would have to change the classes of all 7 models.
- The breakpoints are Bootstrap's standard values (576, 768, 992, 1200 px), not the ones my content actually needs. For example, at 800 px, there are still 2 columns even though 3 would fit.
- The HTML becomes more crowded: each model needs an extra `div` for the column, and the layout is mixed with the content instead of being defined in the CSS.
- The style does not match Rueda Libre's brand identity (font and colors). I would have to override Bootstrap to achieve that.
- The page downloads all of Bootstrap even though I only use the grid and the card.

### Conclusion
Bootstrap was faster to build, but the custom version adapts better to the content, keeps the HTML cleaner, and maintains the brand identity. Bootstrap is useful for a quick test; however, for the Rueda Libre fleet, I would choose the custom CSS version.
