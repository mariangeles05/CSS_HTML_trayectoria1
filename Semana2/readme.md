# Rueda Libre · Semana 2 · Layout y responsive

This week, the site evolved from looking good only on a computer to working across mobile, tablet, and desktop. I worked with Flexbox, Grid, and media queries, and also experimented with Bootstrap (version v1.5) for comparison.

### Mini-Challenge 1· Flexbox in the header and footer
I grouped the logo and the name into a `.marca` container so that the header would have only two direct children.
The header uses `display: flex`, `justify-content: space-between` (placing the brand on one side and the menu on the other), and `align-items: center`.

The menu is flexible, utilizing `gap` and `flex-wrap: wrap`, which allows it to wrap to the next line instead of overflowing.
The footer contains three blocks arranged in a row, aligned to the top using `align-items: flex-start`.
I used `gap` instead of margins because it only adds spacing between elements, avoiding unnecessary extra space at the edges.


### Mini-Challenge 2 · The fleet using Grid
I built the "Our Fleet" section, featuring 7 models. Each model is an `article` containing a photo, name, description, price, and a "Book" button.

.flota-grid {
display: grid; 
grid-template-columns: repeat(auto-fit, minmax(18rem, 1fr)); 
gap: var(--esp-l);
}
`auto-fit` automatically fits as many columns as possible, with each column having a minimum width of 18rem. I didn't need any media queries; when I added the seventh model (Tandem), the grid adjusted itself automatically.

Each card is a Flexbox container with a column layout and `justify-content: space-between`, ensuring the button always stays at the bottom, even if the description is short.

Width	Columns
1280 px	3
900 px	2
500 px	1

### Mini-Challenge 3 · Desktop layout
Section	What I used	Why
Hero/Cover	Grid 1fr 1fr	Text and photo each occupy exactly half the space; `align-items: center` centers the text.
Route Gallery: `Grid repeat(3, 1fr)` — A grid of three identical cards.
Reservations: `Grid 2fr 1fr` — The design calls for the form to occupy 2/3 of the space and the contact section 1/3.
Document and mobile phone row: `Flexbox` — Just two fields arranged in a single direction.
Header: `Flexbox` — A single row where each element is sized according to its content.
Footer: `Flexbox` — Blocks of varying sizes that stack using `wrap`.
My rule of thumb: use `Flexbox` for a single-direction layout; use `Grid` when you need to define columns or align both rows and columns simultaneously.

### Mini-Challenge 4 · Mobile-first
I reorganized `styles.css` so that the styles outside of any media queries represent the mobile version—everything in a single column. Then, I added only the necessary changes:

From 768px: Header and footer in a row, the hero section in two columns, routes in three, and the document and mobile phone fields grouped together.
From 1200px: Reservations section set to a 2:1 ratio.
I also added `img { max-width: 100%; height: auto; }` to ensure no images overflow their containers.

Issues encountered at 360px:

The menu was breaking into two lines; I reduced the padding on the links for mobile.
The route table forced horizontal scrolling; I reduced the font size and padding for mobile.
The fleet section could overflow on very small screens; I used `minmax(min(18rem, 100%), 1fr)`.
The 2:1 layout for reservations felt too cramped on tablets, so I applied it only from 1200px onwards.
The email address in the footer could overflow; I added `overflow-wrap: anywhere`. Mini-Challenge 5 · The Fleet in Bootstrap
In `pruebas/catalogo-bootstrap.html`, I rebuilt the fleet section using Bootstrap 5.3 via CDN, without any custom CSS:

<div class="row g-4">
<div class="col-12 col-sm-6 col-lg-4 col-xl-3"> ... </div>
</div>
This results in 1 column on mobile, 2 from the `sm` breakpoint, 3 from `lg`, and 4 from `xl`.

Custom CSS	Bootstrap
Approximate time	45 min	20 min
Layout CSS	7 declarations	0
Columns	Determined by available space	Defined by me via breakpoints
Bootstrap was faster, but I lost control over the columns, the HTML became more cluttered, and it lacks the brand's specific style. For "Rueda Libre," I’ll stick with my custom version.

Publication
Site v1.5: https://mariangeles05.github.io/CSS_HTML_trayectoria1/
