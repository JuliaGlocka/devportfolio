# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a static portfolio website for Julia Głocka showcasing programming, testing, and game development work. It's a single-page application using vanilla HTML/CSS/JavaScript with no build system or dependencies.

**Deployment:** GitHub Pages (indicated by `.nojekyll` file) - files are served directly without any build step.

## Development

No build commands - edit files directly and refresh browser to test. To serve locally, use any static file server:
```bash
python -m http.server 8000
# or
npx serve .
```

## Architecture

### Core Components

**Circular Menu System** (`js/script.js:91-270`)
- Three category items (Coding, Testing, Game Dev) positioned on a circular path
- Drag/rotation support for both mouse and touch with threshold detection to distinguish taps from drags
- Radius calculated dynamically based on viewport size via `getRadius()`

**Data-Driven Content** (`js/script.js:1-71`)
- Portfolio data defined as JavaScript object with `programming`, `testing`, and `gamedev` arrays
- Each item has `type` (project/experience), `title`, `description`, optional `link`, `linkIndex`, and `role`
- Cards generated dynamically in `showCategory()` function

**Matrix Rain Effect** (`js/script.js:388-455`)
- Canvas-based background animation using Unicode characters from multiple ranges
- Toggle button controls `isMatrixActive` flag; animation skips rendering when off

### File Structure

```
index.html      # Entry point - menu structure and content view containers
css/style.css   # All styling - CSS variables, responsive breakpoints, animations
js/script.js    # Application logic - menu interactions, data, matrix effect
media/          # Images (avatar.png, category icons as SVG)
```

### Key Patterns

**Security:** URL validation via `isValidUrl()` before creating links, text sanitization via `sanitizeText()`, external links use `rel="noopener noreferrer"`

**Responsive Design:** CSS variables define sizes (`--menu-size`, `--item-size`, etc.), media queries at 768px and 480px breakpoints, landscape-specific rules

**Touch Handling:** Passive event listeners disabled for touch events that need `preventDefault()`, drag threshold (15px) distinguishes taps from drags
