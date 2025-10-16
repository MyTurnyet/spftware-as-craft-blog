# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is the "Software As Craft" blog (https://www.softwareascraft.com) - a Hugo static site using the Hinode theme. The blog focuses on software development practices, Extreme Programming, collaborative programming, and ADHD-friendly development practices.

## Tech Stack

- **Static Site Generator**: Hugo (Extended version, min 0.141.0)
- **Theme**: Hinode v1.19.3 (via Hugo modules)
- **Package Manager**: npm for frontend tooling
- **Deployment**: Netlify
- **Module System**: Hugo modules (managed via go.mod)

## Key Commands

### Development

```bash
npm start                 # Start Hugo dev server (bind to 0.0.0.0, disable fast render)
npm run start:drafts      # Start dev server including draft posts
npm run start:prod        # Start dev server in production mode with i18n warnings
```

### Building

```bash
npm run build            # Production build (runs clean:public and mod:vendor first)
npm run build:cache      # CI build with mod:vendor
npm run build:debug      # Debug build with verbose output
npm run build:preview    # Build including drafts and future posts
```

### Hugo Module Management

Hugo modules are the PRIMARY dependency system for themes and components. These commands are critical:

```bash
npm run mod:vendor       # Vendor Hugo modules to _vendor/ (required before builds)
npm run mod:update       # Update all Hugo modules and re-vendor
npm run mod:clean        # Clean module cache
npm run mod:tidy         # Tidy go.mod and go.sum
```

**IMPORTANT**: Always run `npm run mod:vendor` after:
- Cloning the repository
- Updating Hugo modules
- Before running builds

The `_vendor/` directory contains vendored Hugo modules and should NOT be edited directly.

### Linting

```bash
npm run lint                  # Run markdown linting
npm run lint:markdown         # Lint markdown files
npm run lint:markdown-fix     # Auto-fix markdown issues
npm run lint:styles           # Lint SCSS files
npm run lint:scripts          # Lint JavaScript files
npm test                      # Run all linters
```

### Cleaning

```bash
npm run clean:public         # Remove public/ directory
npm run clean:install        # Clean node_modules and package-lock.json
```

### Environment Info

```bash
npm run env              # Show Hugo environment info
npm run check            # Show Hugo version
```

## Architecture

### Hugo Module System

This project uses Hugo modules (not npm) for theme and component dependencies. Key modules (from go.mod):

- `github.com/gethinode/hinode` - Main theme
- `github.com/gethinode/mod-bootstrap` - Bootstrap integration
- `github.com/gethinode/mod-fontawesome` - FontAwesome icons
- `github.com/gethinode/mod-flexsearch` - Search functionality
- `github.com/gethinode/mod-katex` - Math rendering
- `github.com/gethinode/mod-leaflet` - Map integration

### Directory Structure

- `content/` - Markdown content organized by section:
  - `posts/` - Main blog posts about software practices
  - `adhd/` - Posts about ADHD-friendly development
  - `talks/` - Conference talks and presentations
  - `workshops/` - Workshop offerings
- `config/_default/` - Hugo configuration files:
  - `hugo.toml` - Main Hugo config
  - `params.toml` - Theme parameters and site settings
  - `menus/` - Navigation menus
  - `languages.toml` - Language settings
  - `markup.toml` - Markdown rendering config
- `layouts/` - Hugo template overrides (minimal - most come from Hinode theme)
- `assets/` - Source assets (SCSS, JS, images)
  - `img/` - Blog images and graphics
- `static/` - Static files copied directly to output
- `_vendor/` - Vendored Hugo modules (generated, do not edit)
- `public/` - Generated site output (excluded from git)

### Content Sections

The site has four main content sections defined in `config/_default/params.toml`:

1. **posts** - Main blog content about software craft practices
2. **adhd** - ADHD-specific development content
3. **talks** - Conference presentations
4. **workshops** - Workshop descriptions

Each section has custom display settings (card style, columns, sort order) in params.toml.

### Theme Customization

- Theme is Hinode, pulled via Hugo modules
- Customizations are made through:
  - `config/_default/params.toml` - Theme parameters
  - `layouts/` - Template overrides (sparingly used)
  - `assets/` - Custom assets
- DO NOT modify files in `_vendor/` - these are generated

### Hugo Module Workflow

When working with Hugo modules:
1. Dependencies are declared in `go.mod`
2. Run `hugo mod vendor` (or `npm run mod:vendor`) to copy modules to `_vendor/`
3. Hugo uses vendored modules during builds
4. To update modules: `npm run mod:update`

### Content Front Matter

Blog posts use YAML front matter with:
- `title` - Post title
- `date` - Publication date
- `draft` - Draft status (true/false)
- `description` - Post description for SEO
- `thumbnail` - Image with attribution (url, author, authorURL, origin, originURL)
- `author` - Author name
- `tags` - Post tags

### Deployment

- Deployed to Netlify
- Deploy status badge in README.md
- Production builds use `npm run build`
- Site URL: https://www.softwareascraft.com

## Managed Links

The site uses managed links defined in `config/_default/params.toml` under `[links]`. Use these shortcodes in content rather than hardcoding URLs:
- `{{% fast-io %}}` - FAST Agile website
- `{{% mob-sh %}}` - mob.sh tool
- `{{% calendly %}}` - Calendly booking link
- Many more - see params.toml

## Analytics

GoatCounter analytics enabled for site metrics (config in params.toml).

## Social Sharing

Custom social sharing configuration with Bluesky, LinkedIn, Facebook, and email/clipboard sharing.