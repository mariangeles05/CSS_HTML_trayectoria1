# Rueda Libre · Week 1 · Day 1

Day one of the "Rueda Libre" (Free Wheel) project—a bicycle rental business in Medellín. Today, I set up the foundation for the site: the repository, three pages, and a navigation menu to move between them (version v0.1).

## What I did

- Created the repository and folder structure: `index.html` in the root directory, a `paginas/` folder for rates and reservations, a `css/` folder for styles, and an `img/` folder for images.
- Built the homepage, featuring an introduction to the business and its services.
- Created the rates page, which includes two tables: one for bike rentals by type and another for guided tours. I used `caption`, `thead`, `tbody`, and the `scope` attribute in the headers to ensure proper readability.
- Built the reservations page, including contact email and operating hours.
- Added a consistent navigation menu across all three pages.

## Reviewing the Network tab

I opened the site using Live Server and examined the initial request in DevTools:

- URL: `http://127.0.0.1:5500/index.html`
- Protocol: `http`; host: `127.0.0.1` (my computer); port: `5500` (used by Live Server); path: `/index.html`
- Method: `GET`; status code: `200 OK`—this means the server successfully located and delivered the page.

I then requested a page that does not exist (`/promociones.html`), which returned a `404 Not Found` response. This clarified that a 404 error does not mean the server is down; rather, it indicates that the requested file is missing.

## HTML, CSS, and JavaScript

- **HTML** defines the structure and content, such as the rates table.
- **CSS** determines the visual appearance, including brand colors and the horizontal navigation menu. - **JavaScript** represents the behavior—for example, validating a booking form.

## Relative paths

The most helpful approach for me has been to always think from the perspective of the file where I am writing the link. If I am inside `paginas/` and want to return to the home page, I need to move up one folder using `../`.

| From | To | Path |
|---|---|---|
| index.html | paginas/tarifas.html | `paginas/tarifas.html` |
| paginas/tarifas.html | index.html | `../index.html` |
| paginas/tarifas.html | paginas/reservas.html | `reservas.html` |
| paginas/tarifas.html | img/logo.png | `../img/logo.png` |

If I forget the `../`, the image will not load, and a 404 error will appear in the Network tab.
