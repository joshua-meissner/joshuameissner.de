# Joshua Meissner - Portfolio Website Documentation

This document provides an overview of the components and architecture of this Jekyll-based static website. This documentation covers how the different parts of the site interact to create a clean, responsive portfolio website.

## 1. Site Architecture Overview

This website is built with [Jekyll](https://jekyllrb.com/), a static site generator that converts Markdown and HTML files into a complete, static website. The site follows a modular structure with the following key components:

- **Configuration**: Managed through `_config.yml`
- **Layouts**: Templates in the `_layouts` directory 
- **Includes**: Reusable HTML snippets in the `_includes` directory
- **Collections**: Custom content types, primarily `_projects`
- **Styling**: SASS/SCSS in the `_sass` directory and `css` folder
- **Assets**: Images in `img` and `uploads` directories, fonts in `fonts` directory

## 2. Configuration (`_config.yml`)

The `_config.yml` file contains the site's global configuration settings including:

- Site title, description, and contact information
- Base URL and URL settings
- Collection definitions (e.g., projects)
- Build settings (markdown processor, SASS configuration)
- Plugin information

Key plugins used:
- `jekyll-seo-tag`: Handles SEO metadata
- `jekyll-sitemap`: Generates a sitemap.xml file
- `jekyll-target-blank`: Adds `target="_blank"` to external links automatically

## 3. Layouts

Layouts are HTML templates that define the structure of different page types. They use Liquid templating to include dynamic content:

- **`default.html`**: The base layout that defines the overall HTML structure
  - Includes the `head.html`, `header.html`, and `footer.html` components
  - Wraps content in standard page structure

- **`compress.html`**: A special layout that compresses HTML output
  - Used as the parent for `default.html`
  - Reduces file size by removing whitespace

- **`page.html`**: Extends default layout for basic pages
  - Used for general content pages like homepage and about page

- **`project.html`**: Extends page layout for project display
  - Specialized template for displaying project content
  - Adds appropriate heading and content structure

- **`post.html`**: Extends default layout for blog posts (if used)
  - Includes metadata like date and author

## 4. Includes

The `_includes` directory contains HTML snippets that are reused across the site:

- **`head.html`**: Contains metadata, CSS links, and other `<head>` elements
- **`header.html`**: Navigation and site header with responsive menu
- **`footer.html`**: Site footer with contact information and copyright
- **`googleanalytics.html`**: Google Analytics tracking code (currently commented out)
- **`vcard.html`**: Contact information in vCard format

## 5. Collections

Custom content types are defined as collections, with `_projects` being the main collection:

### Projects Collection (`_projects`)

Each project is defined in its own Markdown file with:

- **Front matter**: YAML metadata at the top of each file defining:
  - `layout`: Usually set to "project"
  - `title`: Project title
  - `class`: CSS class for styling
  - `headline`: Short project descriptor
  - `picture`: Path to featured image
  - `order`: Numeric value for sorting on index page

- **Body content**: Markdown content with project description and images
  - Special CSS classes like `copy` and `image-content` are applied using Kramdown's IAL syntax: `{: class="className"}`

## 6. Styling System

The site uses a combination of SCSS for custom styling and utility classes:

### SCSS Architecture

- **`style.scss`** in the `css` directory imports all SCSS partials
- **`_helpers.scss`**: Contains SCSS mixins and helper functions
  - Includes the `fluid-aspect` mixin for responsive image containers
  - Defines media queries for responsive design
- **`_webfont.scss`**: Font definitions and typography settings
- **`_mailchimp.scss`**: Styling for newsletter subscription forms (if used)
- **`_backup.scss`**: Legacy styles kept for reference

### External CSS

- **`normalize.css`**: Normalizes browser default styles
- **`basscss.min.css`**: Utility-first CSS framework for layout helpers

## 7. Assets

The site includes various static assets:

- **Images**:
  - `img/`: Core site images like profile photos
  - `uploads/`: Project-specific images
- **Fonts**: Custom web fonts in the `fonts` directory
  - Includes Font Awesome icons and custom typefaces

## 8. Site Generation Process

When Jekyll builds the site:

1. Configuration is loaded from `_config.yml`
2. Collections (like `_projects`) are processed
3. Pages are rendered through their assigned layouts
4. Assets are copied to the output directory
5. The complete static site is generated in the `_site` directory (not tracked in git)

## 9. How Pages Are Structured

### Homepage (`index.html`)

The homepage lists all projects in the site's `_projects` collection:
- Projects are sorted by their `order` property
- Each project is displayed in a grid with hover effects
- Project images are displayed with title overlay on hover

### Project Pages

Individual project pages use the `project.html` layout:
- Display a large title
- Show project content with styled typography
- Support image galleries formatted with the `image-content` class

### About Page

The `about.html` page uses the standard `page.html` layout and contains:
- A profile image with responsive styling
- Biographical information
- Contact details

## 10. Deployment

The site is designed to be deployed to GitHub Pages or any static hosting service. The presence of a `CNAME` file suggests it's configured for a custom domain (joshuameissner.de).

## 11. Responsive Design

The site implements responsive design through:
- Media queries managed through the `for-phone-only` mixin
- Fluid aspect ratios for images
- Typography that scales according to viewport size
- Responsive navigation that adapts to mobile devices
