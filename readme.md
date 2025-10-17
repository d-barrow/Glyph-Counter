# Letter & Glyph Counter for Handwritten Transcripts

A tool to analyze transcripts of handwritten manuscripts and identify which letters and glyphs are present in transcripts.

## Purpose

When creating typefaces from (transcribed)  handwriting samples, this tool helps you:
- Count occurrences of each letter, number, and special character
- Identify missing glyphs (highlighted in red)
- Locate positional letter variants (initial, medial, and final forms)
- Find isolated letter forms (single-letter words)
- Discover uncategorized glyphs in your text
- Generate printable reports for reference during design work

**Target Audience:** Type designers and font creators working with handwritten source material.

## Features

- **Uppercase Letters:** Counts A-Z individually
- **Lowercase Letters with Positional Variants:** 
  - Initial form (a.init - z.init): lowercase at word beginning
  - Medial form (a.mid - z.mid): lowercase in word middle
  - Final form (a.fina - z.fina): lowercase at word end
- **Isolated Letters:** Single-letter words (e.g., "I", "a") displayed separately
- **Digits:** Counts 0-9 separately
- **Punctuation:** . , ; : ! ? ' " ` - – — … 
- **Brackets:** ( ) [ ] { } 
- **Math & Symbols:** + - × ÷ = ± % ‰ ° # @ & * / \
- **Currency:** $ € £ ¥ ¢
- **Quotes:** " " ' ' « » ‹ ›
- **Other Glyphs:** Automatically detects and displays any characters not in predefined categories (sorted by frequency)

### Visual Color Coding
- **Red:** Missing glyphs (0 occurrences)
- **Blue:** Abundant (6-10 occurrences)
- **Green:** Very abundant (10+ occurrences)
- **Default:** Standard frequency (1-5 occurrences, no color)

### Output
- Results displayed in color-coded divisions
- Print to PDF via browser (Cmd+P / Ctrl+P) with preserved colors
- Page break optimization for clean printing
- Single self-contained HTML file
- WordPress Custom HTML block compatible

## Technical Specifications

- **Technology:** Pure HTML, CSS, JavaScript (ES5 compatible)
- **Execution:** Client-side only (no server required)
- **Character Support:** Full Unicode
- **Browser:** Optimized for Safari, compatible with all modern browsers
- **Code Size:** Under 500 lines total
- **Architecture:** Well-structured with namespaced CSS and IIFE-wrapped JavaScript for maintainability

## Files

- **`index.html`** - Standalone version for direct browser use
- **`wordpress-version.html`** - WordPress Custom HTML block optimized version (no document structure tags)

## Installation

### Standalone Usage
1. Open `index.html` directly in any web browser
2. No installation or server required

### WordPress Custom HTML Block
1. Copy the entire content of `wordpress-version.html`
2. In WordPress editor, add a "Custom HTML" block
3. Paste the code into the block
4. Save/publish the page

**Important:** Use `wordpress-version.html` for WordPress, not `index.html`. The WordPress version is specifically formatted to avoid HTML nesting issues and uses ES5 syntax for maximum compatibility.

## Usage

1. **Input Transcript:** Paste your handwritten text into the input textarea
2. **Analyze:** Click the "Count Glyphs" button to process the text
3. **Review Results:** 
   - Each glyph displayed with its count
   - Lowercase letters show three positional variants (init, mid, fina)
   - Color coding shows frequency at a glance
   - Red items indicate glyphs you still need to find in manuscripts
   - "Other Glyphs" section shows unexpected characters (accents, special Unicode, etc.)
4. **Clear:** Click "Clear" button to reset input and output
5. **Print/Save:** Use browser print (Cmd+P) to save as PDF with colors preserved

## Display Format

Results organized by category:
- **Uppercase:** Single card per letter with definition (top) and count (bottom)
- **Lowercase:** Grouped cards showing letter name as header, then three rows:
  - `init` (count) - word-initial position
  - `mid` (count) - word-medial position
  - `fina` (count) - word-final position
- **Isolated Letters:** Only displayed if found - single-letter words
- **Numbers & Symbols:** Single card per glyph
- **Other Glyphs:** Dynamically shows any Unicode characters not in standard categories

Each element uses background color for visual frequency indication based on configurable thresholds.

## Customization Guide

### Modifying Color Thresholds

In the configuration block at the top of the JavaScript section:

```javascript
// COLOR THRESHOLD CONFIGURATION
// Modify these values to change when colors appear
var THRESHOLDS = {
  missing: 0,      // Red: Change to highlight different "missing" definition
  abundant: 6,     // Blue: Change minimum for "abundant" classification
  veryAbundant: 10 // Green: Change minimum for "very abundant" classification
};
```

### Adding New Character Categories

To track additional glyphs:

1. Locate the `CHARACTERS` configuration object
2. Add new category with array of characters:
```javascript
CHARACTERS.diacritics = ['ä', 'ö', 'ü', 'ß', 'é', 'è', 'à'];
```
3. Add display section in `displayResults()` function following existing pattern
4. The tool will automatically count them

### Color Customization

Modify CSS variables in the style section:

```css
/* COLOR SCHEME CONFIGURATION */
#glyph-counter-app {
  --color-missing: #ffcccc;      /* Red background for 0 occurrences */
  --color-abundant: #cce5ff;     /* Blue background for 6-10 */
  --color-very-abundant: #ccffcc; /* Green background for 10+ */
}
```

## Technical Notes

### WordPress Compatibility
The `wordpress-version.html` file includes several WordPress-specific optimizations:
- All CSS scoped with `#glyph-counter-app` prefix to avoid theme conflicts
- JavaScript wrapped in IIFE to prevent variable collisions
- ES5 syntax (var, function) instead of ES6 (const, let, arrows) for older WordPress themes
- Nested `if` statements instead of `&&` operators (WordPress HTML-encodes `&&` to `&#038;&#038;`)
- Defensive DOM element detection with retry logic
- No `<!DOCTYPE>`, `<html>`, `<head>`, or `<body>` tags (prevents nested HTML issues)

### Counting Logic
- Uppercase letters are counted separately and NOT included in lowercase positional variants
- Single-letter words are tracked as "isolated" forms only (not counted as init OR fina)
- Words are split on whitespace, then cleaned to remove punctuation for positional analysis
- "Other Glyphs" section catches any Unicode character not in predefined categories (useful for finding accented letters, special punctuation, etc.)

## Version History

**1.0.0 - October 2025**
- Initial release with uppercase, lowercase, digits, punctuation, and symbols
- Color-coded frequency visualization
- Print-to-PDF support

**1.1.0 - October 2025**
- Added positional variants for lowercase (init, mid, fina)
- Added isolated letter detection
- Added "Other Glyphs" auto-detection
- WordPress Custom HTML block compatibility
- Print color preservation
- Page break optimization

## License

This work is licensed under a **Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License** (CC BY-NC-SA 4.0).

Copyright © 2025 Harald Geisler

### You are free to:
- **Share** — copy and redistribute the material in any medium or format
- **Adapt** — remix, transform, and build upon the material

### Under the following terms:
- **Attribution** — You must give appropriate credit to Harald Geisler, provide a link to the license, and indicate if changes were made.
- **NonCommercial** — You may not use the material for commercial purposes.
- **ShareAlike** — If you remix, transform, or build upon the material, you must distribute your contributions under the same license as the original.

### Commercial Use
For commercial licensing or inquiries, please contact Harald Geisler.

**Full License:** https://creativecommons.org/licenses/by-nc-sa/4.0/

[![CC BY-NC-SA 4.0](https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png)](https://creativecommons.org/licenses/by-nc-sa/4.0/)
