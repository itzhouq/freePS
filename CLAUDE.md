# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

FreePS is a browser-based image editor forked from [miniPaint](https://github.com/viliusle/miniPaint). It provides a free online Photoshop alternative using HTML5 Canvas and JavaScript.

**Key characteristic**: This is a **production-only repository** - the source code is already compiled and bundled into `dist/bundle.js`. There is no build process, no package.json, and no source code in this repository.

## Architecture

- **Single HTML entry point**: `index.html` - contains the application skeleton
- **Bled JavaScript**: `dist/bundle.js` (~1.3MB) - contains all application logic, minified
- **Static assets**: `images/` directory contains icons, logos, and manifest files

The application uses:
- HTML5 Canvas for image rendering and manipulation
- Pure JavaScript (no framework dependencies detectable in bundle)
- AlertifyJS for dialogs (bundled)
- In-memory layer system for image editing

## UI Structure

The application has a classic image editor layout:

- **Main menu** (`#main_menu`): Top navigation bar
- **Tools container** (`#tools_container`): Left sidebar with editing tools
- **Canvas area** (`#canvas_minipaint`): Central editing workspace with rulers
- **Right sidebar**:
  - Preview
  - Colors picker
  - Information panel
  - Layer details
  - Layers panel (`#layers_base`)

## Development Notes

**No source code available**: This repository contains only the production build. The original source code is not included. To modify functionality, you would need to:

1. Work with the original miniPaint repository: https://github.com/viliusle/miniPaint
2. Or work directly with the minified bundle (not recommended for significant changes)

## Deployment

This is a static site with no build step:

1. Simply upload all files to any web server
2. The entry point is `index.html`
3. No server-side processing required
4. All processing happens client-side in the browser

## Browser Support

- Chrome
- Firefox
- Opera
- Edge
- Safari

## Related Projects

- Original: https://github.com/viliusle/miniPaint
- Live demo: https://itzhouq.github.io/freePS/
- Chinese version: https://zaixianps.net/
