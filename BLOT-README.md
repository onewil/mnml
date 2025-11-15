# mnml for Blot

A minimal, responsive theme for Blot, converted from the Hugo/Micro.blog mnml theme.

## About This Conversion

This theme has been converted from Hugo template syntax to Mustache templating for use with [Blot](https://blot.im). The original mnml theme was designed for Hugo/Micro.blog by [Jim Mitchell](https://jimmitchell.org).

## Features

- Clean, minimal design
- Responsive layout
- Dark mode support (automatic based on system preference)
- Custom GT Web font family
- Photo grid/masonry layouts
- Code block copy button
- Mobile hamburger menu
- Archive with category filtering
- Tagged post views
- Scroll to top button

## Installation

1. **Upload to Blot**: Copy all files from this directory to your Blot folder
2. **Required files** (Blot uses a flat structure - all template/CSS/JS files in root):
   - **Templates:**
     - `entry.html` - Individual post template
     - `entries.html` - Homepage/post list template
     - `archives.html` - Archive page template
     - `tagged.html` - Tag archive template
     - `error.html` - 404 error page
   - **Partials:**
     - `head.html` - Partial for HTML head
     - `header.html` - Partial for site header
     - `footer.html` - Partial for site footer
     - `post-content.html` - Partial for post content
     - `scroll-to-top.html` - Partial for scroll button
   - **Stylesheets:**
     - `fonts.css` - Font declarations
     - `main.css` - Primary styles
     - `photos-grid.css` - Photo grid layout
     - `photos-masonry.css` - Photo masonry layout
   - **JavaScript:**
     - `menu.js` - Mobile menu toggle
     - `copybutton.js` - Code copy button
     - `scroll-to-top.js` - Scroll button functionality
     - `search.js` - Search functionality
   - **Other:**
     - `package.json` - Blot configuration
     - `fonts/` directory with GT Web font files (WOFF/WOFF2)

## Template Structure

### Main Templates

- **entry.html** - Displays individual blog posts with title, date, content, and tags
- **entries.html** - Shows a list of posts on the homepage with pagination
- **archives.html** - Displays all posts grouped by month/year with category filters
- **tagged.html** - Shows posts filtered by a specific tag
- **error.html** - 404 error page

### Partials

Located in the root directory (Blot doesn't support subdirectories for templates):

- **head.html** - HTML head with meta tags, fonts, and stylesheets
- **header.html** - Site header with logo/avatar and navigation menu
- **footer.html** - Site footer with copyright and credits
- **post-content.html** - Reusable post content rendering logic
- **scroll-to-top.html** - Scroll to top button

These partials are included in main templates using `{{> partial-name}}` syntax.

## Blot Variables Used

This theme uses the following Blot template variables:

### Blog Variables
- `{{blog.title}}` - Your blog title
- `{{blog.url}}` - Your blog URL
- `{{blog.avatar}}` - Your avatar/profile picture
- `{{blog.menu}}` - Navigation menu items
- `{{blog.year}}` - Current year
- `{{blog.yearStarted}}` - Year your blog started
- `{{blog.description}}` - Blog description

### Entry Variables
- `{{entry.title}}` - Post title
- `{{entry.html}}` - Full post HTML content
- `{{entry.body}}` - Post content without title
- `{{entry.teaser}}` - Post excerpt/summary
- `{{entry.url}}` - Post permalink
- `{{entry.date}}` - Post date (ISO format)
- `{{entry.dateStamp}}` - Formatted date string
- `{{entry.tags}}` - Post tags/categories
- `{{entry.thumbnail.large}}` - Featured image
- `{{entry.nextEntry}}` - Next post (for navigation)
- `{{entry.previousEntry}}` - Previous post (for navigation)

### Archive Variables
- `{{archives}}` - All posts grouped by date
- `{{archives.months}}` - Posts grouped by month
- `{{all_tags}}` - All tags with post counts
- `{{tagged}}` - Posts filtered by tag
- `{{tag.name}}` - Current tag name

### Pagination
- `{{pagination.next}}` - Next page
- `{{pagination.previous}}` - Previous page

## Customization

### Changing Colors

Edit `main.css` (in the root directory) and modify the CSS variables in the `:root` selector:

```css
:root {
  --text-color: #20232a;
  --background-color: #ffffff;
  --link-color: #0e79e7;
  /* ... more variables */
}
```

### Menu Items

Menu items are managed through Blot's dashboard. Go to Settings → Menu to add or modify navigation items.

### Avatar

Your avatar is pulled from Blot's settings. Update it in Settings → Profile.

### Date Format

The date format can be configured in `package.json`:

```json
{
  "blot": {
    "locals": {
      "dateFormat": "MMMM D, YYYY"
    }
  }
}
```

## Differences from Hugo Version

Due to the differences between Hugo and Blot, some features have been adapted:

1. **Configuration**: The extensive `plugin.json` configuration from the Micro.blog version isn't directly supported. Many features are now hardcoded or use Blot's built-in settings.

2. **Internationalization**: The i18n strings from Hugo have been replaced with English text. You can customize these by editing the template files directly.

3. **Pagination**: Uses Blot's built-in pagination system instead of Hugo's `.Paginate` function.

4. **Taxonomies**: Categories are now called "tags" in Blot and work slightly differently.

5. **Pinned Posts**: The pinned category feature from the Hugo version is not implemented in this conversion.

6. **Micro.blog Integration**: Features specific to Micro.blog (conversation.js, reply buttons, etc.) have been removed.

7. **Custom Partials**: Some Hugo partials (like `microblog_head.html`, `conversation-link.html`) that were Micro.blog-specific are not included.

## Static Assets

### CSS Files
- `fonts.css` - GT Web font declarations
- `main.css` - Primary styles (1,279 lines)
- `photos-grid.css` - Photo grid layout
- `photos-masonry.css` - Photo masonry layout (currently not fully implemented)

### JavaScript Files
- `menu.js` - Mobile hamburger menu toggle
- `copybutton.js` - Code block copy button
- `scroll-to-top.js` - Scroll to top functionality
- `search.js` - Search functionality (may need adaptation for Blot)

### Fonts
- GT Web Regular, Oblique, Bold, and Bold Oblique in WOFF and WOFF2 formats

## Viewing Template Data

To see all available variables for any page, append `?debug=true` to the URL:
```
https://yourblog.blot.im/?debug=true
https://yourblog.blot.im/entry?debug=true
```

## Support

For issues with this theme conversion, please open an issue on the [GitHub repository](https://github.com/jimmitchell/mnml).

For Blot-specific questions, consult the [Blot documentation](https://blot.im/templates/developers).

## Credits

- **Original Theme Design**: [Jim Mitchell](https://jimmitchell.org)
- **Original Hugo Theme**: [mnml on GitHub](https://github.com/jimmitchell/mnml)
- **Blot Conversion**: Automated conversion to Mustache templates
- **Blot Platform**: [David Merfield](https://blot.im)

## License

MIT License - see LICENSE file for details
