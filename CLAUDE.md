# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Sollei Canine Academy is a static marketing website for a dog training business. The site is built as a single-page application with inline styles and minimal JavaScript.

## Tech Stack

- **HTML5**: Single-page structure with semantic markup
- **Tailwind CSS**: Embedded directly in the `<style>` tag within index.html (compiled/minified)
- **Vanilla JavaScript**: Minimal interactivity for expandable cards and form handling
- **No build system**: This is a pure static site with no compilation step

## File Structure

```
.
├── index.html       # Main HTML file (~507KB due to embedded Tailwind CSS)
├── styles.css       # Additional custom styles (~65KB)
├── assets/          # Image assets (4 PNG files)
└── CLAUDE.md        # This file
```

## Development Workflow

### Viewing the Site

Open `index.html` directly in a browser:
```bash
open index.html
```

Or use a simple HTTP server:
```bash
python3 -m http.server 8000
# Then visit http://localhost:8000
```

### Making Changes

Since there's no build process, edit files directly:
- Modify HTML content and structure in `index.html`
- Add custom CSS to `styles.css`
- JavaScript is embedded in a `<script>` tag at the bottom of `index.html`

**Important**: The Tailwind CSS in the `<style>` tag is pre-compiled and minified. To modify Tailwind styles, you'll need to:
1. Set up a Tailwind build process (currently not configured)
2. Or add utility classes using the existing embedded Tailwind classes
3. Or use custom CSS in `styles.css`

## Site Architecture

### Single-Page Structure

The site uses a vertical scroll layout with these sections (in order):
1. **Hero Section**: Large header with value proposition
2. **Training Programs**: Expandable cards showing different program offerings
3. **Methodology Section**: Overview of training approach
4. **Contact Form**: Lead generation form at the bottom
5. **Footer**: Copyright and basic information

### JavaScript Functionality

Two main interactive features (see bottom of index.html):

1. **Expandable Program Cards**: `toggleDetailsCard(card)`
   - Clicking a program card expands/collapses additional details
   - Rotates chevron icon and toggles "Learn More"/"Show Less" text

2. **Form Submission**: `contactForm` event listener
   - Prevents default form submission
   - Shows visual feedback ("Request Submitted!")
   - Resets button state after 3 seconds
   - **Note**: No actual backend integration - form doesn't send data anywhere

### Design System

Custom CSS variables defined in `:root`:
- Font families: Playfair Display (headings), Inter (body)
- Color scheme: Green/earth tones with cream backgrounds
  - Primary: Forest green (#2d5745 area)
  - Accent: Warm orange/amber
  - Background: Cream/off-white
- Dark mode variables available but not actively used

### Images

Assets are stored in `assets/` with generated filenames:
- All images are PNG format
- Used for hero section and program illustrations
- No optimization pipeline currently in place

## Common Modifications

### Adding a New Section

Add HTML markup between existing sections in index.html. Use existing Tailwind classes for consistency with the design system.

### Updating Content

All content is in index.html. Search for the relevant heading text to find the section to edit.

### Styling Changes

- For layout/spacing: Use existing Tailwind utility classes in the embedded CSS
- For custom styles: Add to styles.css
- For completely new utility classes: Would require setting up Tailwind build process

### Form Integration

The contact form currently has no backend. To make it functional:
1. Add a form handler service (e.g., Formspree, Basin, or custom backend)
2. Update the form submission JavaScript to POST to the service
3. Add proper error handling and validation
