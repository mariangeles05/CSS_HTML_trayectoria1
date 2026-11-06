# Rueda Libre · Week 1 · Day 2

Today’s goal was to ensure the site was well-constructed under the hood: semantic tags, a functional booking form, validation without JavaScript, accessibility, and a color palette with good readability (version v0.2).

## Semantic HTML

I replaced all structural containers with tags that explicitly define their purpose. No `div` or `span` elements remain for structural layout.

- **index.html:** `header` (h1 + nav), `main` containing four `section` elements (the one for services includes three `article` elements), and a `footer`.
- **tarifas.html:** `header` (with logo, site name, and menu), `main` (containing tables), an `aside` ("What to bring"), and a `footer`.
- **reservas.html:** `header`, `main` (containing the booking form), an `aside` (with operating hours), and a `footer`.

I used `article` for the services, as each one is self-contained, and `aside` for supplementary information.

## Booking Form

I selected each input control based on the nature of the user's choice:

- **Bicycle type → radio buttons:** Three options, only one of which can be selected; this allows all choices to be visible at once.
- **Plan and route → `select` (dropdown):** A fixed list of options; a dropdown menu saves space.
- **Policies → checkbox:** A simple yes/no decision.

I grouped the fields using `fieldset` and `legend` (Your Details, Your Rental, Confirmation), and each input is paired with a corresponding `label` (via the `for` attribute).

## Native Validation

| Field | Test Data | Result | Reason |
|---|---|---|---|
| Name | "Jo" | Rejected | `minlength="3"` |
| ID/Document | "12ab45" | Rejected | `pattern="[0-9]{6,10}"` |
| ID/Document | "12345" | Reject | Less than 6 digits |
| Email | "hola@" | Reject | `type="email"` |
| Mobile | 3001234567 | Accept | Meets the pattern |
| Mobile | 1234567890 | Reject | Does not start with 3 (`pattern="3[0-9]{9}"`) |
| Date | 2026-10-31 | Reject | Earlier than `min` |
| Quantity | 7 | Reject | `max="6"` |
| Policies | Unchecked | Reject | `required` |

I also navigated through the form using only the keyboard. The tab order is logical; I can move through radio buttons using the arrow keys, check the checkbox using the spacebar, and submit the form by pressing Enter.

## Accessibility

The basics were already in place: `lang="es"`, a single `h1` per page, `alt` text for images, and keyboard navigation. I identified six areas for improvement:

1. "See how to get there" was unclear on its own, so I changed it to "How to get to our location."
2. The link to the map opened in a new tab without warning. I added "(opens in a new tab)."
3. The logo repeated the name displayed next to it. I set it to `alt=""` since it is purely decorative in this context.
4. "Book now" appeared twice. I updated them to "Book your bike now" and "Book a guided tour," respectively.
5. Field formatting information was only provided in the `title` attribute, which is not visible. I made it visible using `<small>`.
6. The menu did not indicate the current page. I added `aria-current="page"`.

## Color Palette and Contrast

For standard text, a minimum ratio of 4.5:1 is required.

| Combination | Ratio | Suitable? |
|---|---|---| | White / Route Green | 5.31:1 | Yes |
| White / Pedal Orange | 2.22:1 | No |
| Midnight Blue / Orange | 7.20:1 | Yes |
| Midnight Blue / Cream | 14.83:1 | Yes |
| Asphalt Gray / Cream | 5.57:1 | Yes |
| Route Green / Cream | 4.93:1 | Yes |
| Pedal Orange / Cream | 2.06:1 | No |
| White / Midnight Blue | 15.97:1 | Yes |

Orange is the brand's most striking color, but it is not legible when paired with white. For this reason, I only use it as a background, with Midnight Blue text on top.

## Publication

- Repository: https://github.com/mariangeles05/CSS_HTML_trayectoria1
- GitHub Pages: https://mariangeles05.github.io/CSS_HTML_trayectoria1/
