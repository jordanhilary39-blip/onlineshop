# Hills Shop project notes

These notes describe the existing website code. No HTML, CSS, or JavaScript code was changed to create them.

## Project overview

Hills Shop is a static storefront made from HTML pages, one shared stylesheet, and JavaScript written inside the relevant HTML pages. There is no separate JavaScript file or visible server-side code. The pages link to one another with ordinary relative links, and the product data is written directly into the HTML.

The pages load Font Awesome 6.7.2 from a CDN for icons. The site also uses the local product and logo image files in the project folder.

## Code files

### `index.html` — home page

- Defines the page title and description, links the shared stylesheet and Font Awesome, and sets the document language and mobile viewport.
- Builds the shared header with the store logo, product search, account/contact link, cart count, and navigation.
- Presents the main promotional hero, shopping benefits, four featured products, a deals banner, and category links.
- Includes the shared footer with shop, category, and customer-care links.
- Its small inline JavaScript reads `hills-shop-cart-count` from browser `localStorage` and displays the saved number in the cart badge. Invalid or missing values display as zero.

### `shop.html` — product listing and shopping interactions

- Contains nine product cards. Their `data-name`, `data-category`, `data-price`, and `data-featured` attributes provide the values used by the page's JavaScript.
- Provides controls for text search, category selection, maximum price, favorites-only filtering, sorting, and clearing filters.
- Defines the cart and quick-view dialogs; JavaScript fills their contents when opened.
- The inline JavaScript:
  - Reads and validates saved cart and favorite data from `localStorage`.
  - Filters products by name/category search, selected categories, maximum price, and favorite status; sorts the remaining cards and updates the visible count and empty-results message.
  - Formats prices using the `en-UG` number format.
  - Adds quick-view and favorite buttons to each product card. Favorite changes are saved in `hills-shop-favorites`.
  - Adds products to the cart, increments/decrements quantities, removes individual items, clears the cart, and saves cart data in `hills-shop-cart`. It also updates the shared `hills-shop-cart-count` value used by the other pages.
  - Shows the subtotal and prepares an order summary link to `contact.html`.
  - Reads the `q` URL parameter to prefill the search field and opens the cart when the page URL ends in `#cart`.
- Cart data is stored in this browser only. This page does not send orders to a server or process payments.

### `catergories.html` — category page

- Presents six category cards: Electronics, Fashion, Accessories, Home & Living, Sports, and Beauty.
- Each card links to `shop.html` with its category in the `q` URL parameter. The shop page treats that value as a search query against product names and categories.
- Uses the shared header/footer and reads the saved cart-count value for its cart badge.

### `about.html` — about page

- Presents the Hills Shop introduction, store story, three values/benefits, and links to browse products.
- Uses the shared header/footer, stylesheet, icons, and cart-count display script.

### `contact.html` — contact page

- Provides a form with required name, email, topic, and message fields. Browser validation checks the required fields, email format, and a minimum message length of 10 characters.
- Includes links to the shop, categories, and about page.
- Its inline JavaScript:
  - Reads the shared cart-count value.
  - If an `order` URL parameter exists, selects the order/delivery topic and inserts the order summary into the message field.
  - Prevents normal form submission and displays a status message. The form is not connected to an email or message service, so it does not actually deliver submissions.

### `admin.html` — sample dashboard

- Displays a dashboard layout with summary metrics, example recent orders, and sample inventory counts.
- The page explicitly labels these values as sample/demo data and says that store records and admin access are not configured.
- Its `noindex, nofollow` metadata asks search engines not to index or follow links from the page. It is not an authentication or access-control mechanism.
- Contains page-specific CSS in an inline `<style>` block, including responsive dashboard layouts. It also loads the shared stylesheet and Font Awesome.
- It has no JavaScript and does not read or update live store data.

### `style.css` — shared storefront styling

- Defines shared color variables, typography, box sizing, page widths, and accessibility helpers such as `.visually-hidden`.
- Styles the shared header, search box, navigation, cart badge, buttons, product cards, category cards, footer, and common links.
- Adds page-specific layouts for the home hero and benefits, shop filters/results, category showcase, about sections, and contact form.
- Uses CSS Grid and Flexbox for page layouts, hover/focus states for interactive elements, and image sizing/cropping for product and promotional images.
- Includes responsive breakpoints at 760px and 480px to adapt navigation, grids, filters, forms, and page layouts for smaller screens.
- The stylesheet controls presentation only; product/cart behavior is in the inline JavaScript on `shop.html`.

## Image and asset files

The `.jpg` files and `Hills Shop Green Cart Logo.png` are visual assets, not executable code. HTML references them for product, category, hero, and logo imagery. Some images use lazy loading so the browser can defer loading them until needed. Font Awesome icons are loaded externally from its CDN.

## Important behavior and limitations

- The project is a front-end demo: products and admin figures are hard-coded in the pages; there is no database, server API, account authentication, or order-processing backend.
- Cart and favorites data persist only in the current browser's `localStorage`.
- Contact form submissions are not delivered; the page only displays an explanatory message.
- The shared header on pages other than `shop.html` displays the stored cart count but does not itself manage cart items.
