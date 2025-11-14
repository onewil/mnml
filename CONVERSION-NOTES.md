# Hugo to Blot/Mustache Conversion Notes

## Conversion Summary

This document outlines the conversion process from Hugo template syntax to Mustache for Blot.

## Template Mapping

### Hugo → Blot Template Files

| Hugo Template | Blot Template | Purpose |
|--------------|---------------|---------|
| `post/single.html` | `entry.html` | Individual post display |
| `index.html` | `entries.html` | Homepage/post listing |
| `_default/list.archivehtml.html` | `archives.html` | Archive page with categories |
| N/A (Hugo taxonomy) | `tagged.html` | Tag-filtered posts |
| N/A | `error.html` | 404 error page |

### Partials

All Hugo partials in `layouts/partials/` were converted to Mustache partials in the **root directory** (Blot doesn't support subdirectories for templates):

- `head.html` ✓
- `header.html` ✓
- `footer.html` ✓
- `post-content.html` ✓
- `scroll-to-top.html` ✓

**Not Converted** (Micro.blog specific):
- `microblog_head.html`
- `conversation-link.html`
- `reply-by-email.html`
- `reply-on-mastodon.html`
- `tinylytics.html`

## Syntax Conversion Reference

### Variables

| Hugo Syntax | Mustache/Blot Syntax |
|------------|---------------------|
| `{{ .Title }}` | `{{{title}}}` or `{{entry.title}}` |
| `{{ .Content }}` | `{{{entry.html}}}` |
| `{{ .Summary }}` | `{{{entry.teaser}}}` |
| `{{ .Date }}` | `{{entry.date}}` |
| `{{ .Permalink }}` | `{{entry.url}}` or `{{url}}` |
| `{{ .Site.Title }}` | `{{blog.title}}` |
| `{{ .Site.Author.avatar }}` | `{{blog.avatar}}` |

### Conditionals

| Hugo Syntax | Mustache Syntax |
|------------|-----------------|
| `{{- if .Title }}...{{- end }}` | `{{#title}}...{{/title}}` |
| `{{- if not .Title }}...{{- end }}` | `{{^title}}...{{/title}}` |
| `{{- with .Params.audio }}...{{- end }}` | `{{#audio}}...{{/audio}}` |

### Loops

| Hugo Syntax | Mustache Syntax |
|------------|-----------------|
| `{{- range .Pages }}...{{- end }}` | `{{#entries}}...{{/entries}}` |
| `{{- range .Site.Menus.main }}...{{- end }}` | `{{#blog.menu}}...{{/blog.menu}}` |
| `{{- range .GetTerms "categories" }}...{{- end }}` | `{{#entry.tags}}...{{/entry.tags}}` |

### Partials

| Hugo Syntax | Mustache Syntax |
|------------|-----------------|
| `{{ partial "head.html" . }}` | `{{> head}}` |
| `{{ partial "header.html" . }}` | `{{> header}}` |
| `{{ partial "footer.html" . }}` | `{{> footer}}` |

### Functions

| Hugo Function | Blot Alternative |
|--------------|------------------|
| `{{ .Date.Format "2006-01-02" }}` | `{{entry.date}}` (ISO format) |
| `{{ .Date \| time.Format ":date_short" }}` | `{{entry.dateStamp}}` |
| `{{ .ReadingTime }}` | Not available (removed) |
| `{{ T "Continue reading" }}` | Hardcoded English text |
| `{{ .Paginate }}` | `{{#entries}}` with Blot pagination |
| `{{ truncate 300 }}` | Not available (removed) |
| `{{ safeHTML }}` | `{{{triple braces}}}` for unescaped HTML |

## Key Changes

### 1. Removed Features

These features from the Hugo version are not implemented in the Blot version:

- **Reading time display** - Hugo's `.ReadingTime` not available in Blot
- **Internationalization (i18n)** - Hugo's `T` function not available; hardcoded English
- **Pinned posts** - Complex filtering logic not easily ported
- **Micro.blog integration** - conversation.js, reply buttons, etc.
- **Custom avatar option** - Now uses Blot's avatar setting
- **Conditional photo layouts** - Masonry vs grid (defaulted to grid)
- **Category filtering on homepage** - Uses all posts
- **Post count display** - Available in Blot but may need configuration

### 2. Adapted Features

These features work differently in Blot:

- **Categories → Tags** - Blot uses "tags" instead of "categories"
- **Pagination** - Uses Blot's built-in pagination system
- **Menu system** - Configured via Blot dashboard, not config file
- **Date formatting** - Uses Blot's date format system
- **Avatar** - Pulled from Blot settings, not theme config

### 3. Static Assets

All static assets copied from `static/` to root:
- `static/css/` → `css/`
- `static/js/` → `js/`
- `static/fonts/` → `fonts/`
- `static/humans.txt` → `humans.txt`

### 4. Configuration

Hugo's `plugin.json` configuration system replaced with Blot's `package.json`:

**Not Ported**:
- Most theme customization options (27 config parameters)
- Language selection
- Feature toggles (show_full_post, show_read_time, etc.)
- Photo layout options
- Search configuration
- Footer customization options

**Alternative**: Users must edit template files directly for customization.

## Testing Recommendations

After installation, test these pages:

1. **Homepage** (`/`) - Should show list of posts
2. **Individual post** (`/entry`) - Test with titled and untitled posts
3. **Archives** (`/archives`) - Should show posts grouped by month
4. **Tagged posts** (`/tagged/[tag-name]`) - Test tag filtering
5. **404 page** (`/nonexistent-page`) - Should show error page
6. **Mobile responsive** - Test hamburger menu
7. **Dark mode** - Test with system dark mode enabled

## Known Limitations

1. **No reading time** - Would require custom JavaScript implementation
2. **No search functionality** - `search.js` included but may need Blot-specific adaptation
3. **Limited customization** - Many Hugo config options not available
4. **English only** - No built-in internationalization
5. **Single photo layout** - Masonry layout CSS included but not fully wired up
6. **No pinned posts** - Feature removed in conversion

## Future Enhancements

Potential improvements for future versions:

1. Add search functionality adapted for Blot
2. Implement reading time calculation with JavaScript
3. Add photo masonry layout support
4. Create configuration system via package.json locals
5. Add RSS feed template
6. Add sitemap.xml template
7. Implement multi-language support
8. Add page templates (about, contact, etc.)

## Files Created/Modified

### New Blot Template Files
- `entry.html`
- `entries.html`
- `archives.html`
- `tagged.html`
- `error.html`
- `package.json`
- `head.html` (partial)
- `header.html` (partial)
- `footer.html` (partial)
- `post-content.html` (partial)
- `scroll-to-top.html` (partial)

### Copied Assets
- `css/` directory (4 CSS files)
- `js/` directory (4 JavaScript files)
- `fonts/` directory (8 font files)
- `humans.txt`

### Documentation
- `BLOT-README.md` - User-facing documentation
- `CONVERSION-NOTES.md` - This file

## Resources

- [Blot Template Documentation](https://blot.im/templates/developers)
- [Mustache Documentation](https://mustache.github.io/)
- [Blot Template Reference](https://blot.im/templates/developers/reference)
- [Original Hugo Theme](https://github.com/jimmitchell/mnml)
