# Mini Telco-Ready Close Out Package Builder

A single-page web tool that fills in the Verizon Mini Telco-Ready Close Out Package template and exports it as a PDF.

## Use it

Open `index.html` in a browser (Chrome, Edge, Safari or Firefox). Everything runs locally in the browser; photos are never uploaded anywhere.

1. **Site details** – type them in, or copy the cells in Excel and paste them into the "Paste from Excel" box.
2. **Photos** – click **Choose folder** and pick the site's photo folder (subfolders are searched too), or drop a folder onto the page. Each photo is matched to its slot by file name (case, punctuation, extension and copy suffixes like "(1)" are ignored). When several photos match the same slot (e.g. "POWER PLANT ... -48V.jpg", "... -48V (2).jpg", "... -48V_3.jpg"), all of them are included, each in its own box with the same title. Number suffixes like (2), _3, -4 or " 5" are left out of the title, and the photos are ordered by that number (you can reorder them with the arrows). Photos that don't match are listed under "Unused photos" and stay out of the PDF unless you move one into a slot or add it as an extra photo. Empty slots print "Pending Photo".
3. **Export PDF** – downloads `[Site Name] - Mini Telco-Ready COP.pdf`.

## Host it on GitHub Pages

1. Create a new repository and upload `index.html` (and this README).
2. Go to **Settings → Pages**, set **Source** to "Deploy from a branch", choose `main` and `/ (root)`, then **Save**.
3. After a minute the tool is live at `https://<your-username>.github.io/<repo-name>/`.

## Editable site details in the PDF

The site details on the cover (and the Site Name at the top of every photo page) are exported as fillable PDF form fields, so they can still be corrected after export in Adobe Acrobat/Reader, Edge, Chrome, Foxit and most other PDF viewers. Site Name is a single field shown on every page, so changing it once updates all pages.

## Editing the photo list

The photo titles are in the `PHOTO_TITLES` array near the top of the `<script>` block in `index.html`. Add, remove or reorder entries there; the pages follow that order, two photos per page.

## Notes

- Uses [jsPDF 2.5.1](https://github.com/parallax/jsPDF) and [pdf-lib 1.17.1](https://pdf-lib.js.org/) (for the form fields) from cdnjs; an internet connection is needed when the page loads.
- HEIC photos (iPhone default) must be converted to JPG or PNG first.
- Photos are embedded in their original quality: JPEG and PNG files go into the PDF byte-for-byte at full resolution, scaled only to fit inside the box (never cropped). Phone photos are rotated using their EXIF orientation. WEBP, GIF and BMP are converted to lossless PNG at full resolution, since PDFs can't hold those formats.
- Because photos aren't compressed, the PDF size is roughly the total size of the photos.
