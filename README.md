# 📄 Offer Letter Generator

A lightweight, client‑side web application that turns a Google Forms CSV export into personalized PDF offer letters. Upload your CSV, select a recipient, edit the template with `{{placeholders}}`, and download a polished PDF—all in your browser. No server, no data upload.

---

## ✨ Features

- **Drag‑and‑drop CSV upload** – works with any CSV that has a header row.
- **Smart column detection** – automatically identifies the name column; you can override it.
- **Live recipient preview** – select a person from the list; see their data and the rendered letter.
- **Fully editable template** – use `{{ColumnName}}` placeholders; click any chip to insert it.
- **Real‑time preview** – the letter updates as you type or change the selection.
- **One‑click PDF download** – generates a beautifully styled A4 PDF using `html2pdf.js`.
- **Copy to clipboard** – copy the rendered letter text with one button.
- **Keyboard shortcut** – `Ctrl+Enter` (or `Cmd+Enter` on Mac) to quickly download the PDF.
- **Zero server dependencies** – runs entirely in the browser; no data is sent anywhere.

---

## 🧑‍💻 For End Users

### Quick Start

1. **Open the app** – just load the `index.html` file in any modern browser (Chrome, Firefox, Edge, Safari).
2. **Upload your CSV** – drag a `.csv` file into the upload zone or click to browse.
3. **Select a recipient** – choose a person from the dropdown. The preview updates automatically.
4. **Edit the template (optional)** – modify the letter text in the editor. Use `{{ColumnName}}` to insert data from the CSV. Click any placeholder chip to add it at the cursor position.
5. **Preview & download** – check the rendered letter in the preview box, then click **Download PDF**.
6. **Copy** – use the **Copy Text** button to copy the letter to your clipboard.

### CSV Format Requirements

- The CSV must have a **header row** with column names.
- The app will auto‑detect a column containing "name", "full name", "candidate", etc. You can manually choose the correct name column from the dropdown.
- All columns are available as placeholders, e.g., `{{Email}}`, `{{Position}}`, `{{Company}}`, etc.
- Empty rows are automatically skipped.

### Example CSV

| Date              | Name              | Email                    | Position                 | Company   | Start_Date    | Duration          | GitHub_Username   |
|-------------------|-------------------|--------------------------|--------------------------|-----------|---------------|-------------------|-------------------|
| July 14th, 2026   | Lokesh Ragishetty | 24211a05ft@bvrit.ac.in   | Software Development Intern | Pragament | July 1, 2026  | three (3) months  | LokeshRagishetty  |
| July 14th, 2026   | Ananya Sharma     | ananya.s@example.com     | Frontend Intern          | Pragament | July 15, 2026 | two (2) months    | ananya-dev        |

> 👉 **Note:** The column names in your CSV can be different. Just update the template placeholders accordingly (e.g., `{{FullName}}` instead of `{{Name}}`).

---

## 👨‍💻 For Developers

### Setup & Dependencies

The entire application is a single HTML file. No build tools, package managers, or servers are required. Just open it in a browser.

#### External Libraries (CDN)

- **[PapaParse](https://www.papaparse.com/)** – robust CSV parsing.
- **[html2pdf.js](https://github.com/eKoopmans/html2pdf.js)** – PDF generation from HTML.
- **Font (Inter)** – loaded from Google Fonts via CSS.

All libraries are loaded from CDN in the `<head>` section. If you prefer offline use, download the libraries and update the `src` attributes.

### Code Structure

The entire logic resides in `index.html`:

- **HTML** – semantic sections for upload, selection, template editing, and download.
- **CSS** – fully responsive, modern UI with custom properties.
- **JavaScript** – state management, CSV parsing, template rendering, PDF generation, and event handling.

#### Key State Variables

```javascript
const state = {
  csvData: [],        // array of objects (rows)
  headers: [],        // column names
  selectedIndex: -1,  // currently selected row index
  template: '',       // current template string
  nameColumn: '',     // column used for recipient names
};
```

#### Core Functions

| Function | Purpose |
|----------|---------|
| `handleFile(file)` | Parses CSV using PapaParse and updates state. |
| `renderTable(data)` | Displays first few rows of CSV in a table. |
| `populateRecipients()` | Fills the recipient dropdown based on the name column. |
| `updatePreview()` | Renders the template with the selected row's data and updates the preview box. |
| `renderTemplate(data)` | Replaces `{{ColumnName}}` placeholders with actual values. |
| `generatePDF()` | Builds an HTML document from the rendered letter and converts it to PDF. |
| `copyPreviewText()` | Copies the rendered letter to clipboard. |

### Customization

#### Changing the Default Template

The default template is stored in the constant `DEFAULT_TEMPLATE` (around line 180). Modify it to match your company's letter style. Use `{{ColumnName}}` placeholders that correspond to your CSV headers.

#### Adjusting PDF Styling

The PDF output is generated from an inline HTML document inside `generatePDF()`. You can customize the CSS within the `<style>` block of that HTML string to change fonts, margins, colors, etc.

#### Adding New Features

- **Additional columns**: Just add them to your CSV and use `{{NewColumn}}` in the template.
- **Different export formats**: You can extend the `generatePDF()` function to also generate DOCX or TXT using other libraries.

### Browser Compatibility

The app uses modern JavaScript (ES6+) and CSS features. It works on the latest versions of Chrome, Firefox, Edge, and Safari. For older browsers, consider transpiling with Babel.

---

## 📁 File Structure

```
.
├── index.html          # Single‑file application (HTML, CSS, JS)
└── README.md           # This file
```

> There are no additional files or assets. The app is self‑contained.

---

## 🤝 Contributing

Contributions are welcome! If you find a bug or have a feature request, please open an issue or submit a pull request.

### Development Workflow

1. Clone the repository.
2. Open `index.html` in your browser.
3. Make changes to the HTML, CSS, or JavaScript.
4. Test with your own CSV files.
5. Submit your changes.

---

## 🙏 Acknowledgements

- [PapaParse](https://www.papaparse.com/) – for effortless CSV parsing.
- [html2pdf.js](https://github.com/eKoopmans/html2pdf.js) – for reliable PDF generation.
- Google Fonts – for the Inter typeface.
