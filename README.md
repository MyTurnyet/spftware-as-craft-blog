# Software As Craft Blog

The "Software As Craft" blog (https://www.softwareascraft.com) is a Hugo-powered static site focused on software development practices, Extreme Programming, collaborative programming, and ADHD-friendly development practices.

## Tech Stack

- **Static Site Generator**: Hugo (Extended version, min 0.141.0)
- **Theme**: Hinode v1.19.3 (via Hugo modules)
- **Package Manager**: npm for frontend tooling
- **Module System**: Hugo modules (managed via Go modules)
- **Deployment**: Netlify

## Prerequisites

Before setting up the development environment, ensure you have the following installed:

### 1. Node.js and npm
```bash
# Check if installed
node --version
npm --version

# Install via Homebrew (macOS)
brew install node
```

### 2. Go
Required for Hugo module management.

```bash
# Check if installed
go version

# Install via Homebrew (macOS)
brew install go
```

### 3. Hugo Extended
Installed automatically via npm when you run `npm install`.

## Development Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/MyTurnyet/spftware-as-craft-blog.git
   cd spftware-as-craft-blog
   ```

2. **Install npm dependencies**
   ```bash
   npm install
   ```

3. **Vendor Hugo modules**

   Hugo modules must be vendored before running the development server:
   ```bash
   npm run mod:vendor
   ```

   This downloads theme and component modules to the `_vendor/` directory.

4. **Start the development server**
   ```bash
   npm start              # Standard development mode
   npm run start:drafts   # Include draft posts
   ```

   The site will be available at http://localhost:1313

## Available Commands

### Development
- `npm start` - Start Hugo dev server (bind to 0.0.0.0, disable fast render)
- `npm run start:drafts` - Start dev server including draft posts
- `npm run start:prod` - Start dev server in production mode with i18n warnings

### Building
- `npm run build` - Production build (runs clean:public and mod:vendor first)
- `npm run build:cache` - CI build with mod:vendor
- `npm run build:debug` - Debug build with verbose output
- `npm run build:preview` - Build including drafts and future posts

### Hugo Module Management
- `npm run mod:vendor` - Vendor Hugo modules to `_vendor/` (required before builds)
- `npm run mod:update` - Update all Hugo modules and re-vendor
- `npm run mod:clean` - Clean module cache
- `npm run mod:tidy` - Tidy go.mod and go.sum

**IMPORTANT**: Always run `npm run mod:vendor` after:
- Cloning the repository
- Updating Hugo modules
- Before running builds

### Linting
- `npm run lint` - Run markdown linting
- `npm run lint:markdown` - Lint markdown files
- `npm run lint:markdown-fix` - Auto-fix markdown issues
- `npm run lint:styles` - Lint SCSS files
- `npm run lint:scripts` - Lint JavaScript files
- `npm test` - Run all linters

### Cleaning
- `npm run clean:public` - Remove public/ directory
- `npm run clean:install` - Clean node_modules and package-lock.json

### Utilities
- `npm run env` - Show Hugo environment info
- `npm run check` - Show Hugo version

## Project Structure

```
.
├── assets/              # Source assets (SCSS, JS, images for Hugo processing)
│   └── img/            # Images used in templates (processed by Hugo)
├── config/
│   └── _default/       # Hugo configuration files
│       ├── hugo.toml   # Main Hugo config
│       ├── params.toml # Theme parameters and site settings
│       └── menus/      # Navigation menus
├── content/            # Markdown content
│   ├── posts/         # Main blog posts
│   ├── adhd/          # ADHD-friendly development content
│   ├── talks/         # Conference talks
│   └── workshops/     # Workshop offerings
├── layouts/            # Hugo template overrides (minimal)
├── static/             # Static files (copied directly to output)
├── _vendor/           # Vendored Hugo modules (generated, do not edit)
├── public/            # Generated site output (excluded from git)
└── go.mod             # Hugo module dependencies
```

## Content Sections

The site has four main content sections:

1. **posts** - Main blog content about software craft practices
2. **adhd** - ADHD-specific development content
3. **talks** - Conference presentations
4. **workshops** - Workshop descriptions

## Hugo Modules

This project uses Hugo modules (not npm) for theme and component dependencies. Key modules:

- `github.com/gethinode/hinode` - Main Hinode theme
- `github.com/gethinode/mod-bootstrap` - Bootstrap integration
- `github.com/gethinode/mod-fontawesome` - FontAwesome icons
- `github.com/gethinode/mod-flexsearch` - Search functionality
- `github.com/gethinode/mod-katex` - Math rendering
- `github.com/gethinode/mod-leaflet` - Map integration

The `_vendor/` directory contains vendored modules and should NOT be edited directly.

## Deployment

- Automatically deployed to Netlify on push to main branch
- Production URL: https://www.softwareascraft.com

## Troubleshooting

### "binary with name 'go' not found"
Install Go using Homebrew: `brew install go`

### "Cannot find image resource"
Images for Hugo processing must be in `assets/img/` and referenced without a leading slash (e.g., `img/logo.png` not `/img/logo.png`)

### npm authentication errors
If you see Nexus/Sonatype authentication errors, delete `package-lock.json` and run `npm install` again to regenerate with public registry URLs.

### Module errors
Run `npm run mod:vendor` to ensure Hugo modules are properly vendored.

## Contributing

1. Create a feature branch
2. Make your changes
3. Run linters: `npm test`
4. Commit your changes
5. Push and create a pull request

## License

MIT

## Author

Paige Watson - https://www.softwareascraft.com
