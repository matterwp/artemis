# Artemis WordPress Starter Theme

[![GitHub release](https://img.shields.io/github/v/release/matterwp/artemis?color=ed64a6)](https://github.com/matterwp/artemis/releases) [![license](https://img.shields.io/badge/license-GPL--2.0%2B-orange)](https://github.com/matterwp/artemis/blob/master/LICENSE) [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/matterwp/artemis/pulls)

Artemis is a modern WordPress starter theme built with a focus on performance, security, and developer experience. It includes a complete development environment with Sass, PostCSS, Autoprefixer, stylelint, Webpack, ESLint, imagemin, Browsersync, and more.

## Features

- 🚀 Modern PHP architecture with PSR-4 autoloading
- 🎨 TailwindCSS integration for utility-first styling
- 📦 Laravel Mix for asset compilation and bundling
- 🔒 Built-in security enhancements
- ⚡ Performance optimizations out of the box
- 🧩 Gutenberg blocks support
- 🎯 Carbon Fields integration for custom fields
- 🔄 BrowserSync for live reload during development
- 📱 Mobile-first, responsive approach
- 🛠️ Modern development tools and standards

## Requirements

- PHP 7.4.30 or higher
- WordPress 5.7.2 or higher
- Node.js 14+ & NPM
- Composer 2+

## Getting Started

### 1. Installation

```bash
# Clone the repository
git clone https://github.com/wparray/artemis.git

# Install PHP dependencies
composer install

# Install Node dependencies
yarn install
```

### 2. Configuration

1. Update your local development URL in `.dev/webpack.mix.js`
2. Configure theme settings in `src/Core/Bootstrap.php`
3. Set up environment-specific settings if needed

### 3. Development

```bash
# Start development server with hot reload
yarn dev

# Build for production
yarn build:production

# Run WordPress coding standards check
composer test

# Fix coding standards automatically
composer fix
```

## Project Structure

```
artemis/
├── .dev/                  # Development configuration files
│   └── webpack.mix.js     # Laravel Mix configuration
├── src/
│   ├── Core/             # Core framework classes
│   │   ├── Bootstrap.php # Main theme initialization
│   │   ├── Config.php    # Configuration utilities
│   │   ├── Support.php   # Theme support features
│   │   └── Templates.php # Template handling
│   ├── Setup/            # Theme setup and configuration
│   │   ├── Assets.php    # Asset management
│   │   ├── Fields.php    # Carbon Fields setup
│   │   ├── Menus.php     # Navigation menus
│   │   └── Widgets.php   # Widget areas
│   ├── Theme/
│   │   ├── Blocks/       # Gutenberg blocks
│   │   ├── Layouts/      # Layout templates
│   │   ├── Main/         # Main theme assets
│   │   ├── Page/         # Page templates
│   │   └── Post/         # Post templates
│   └── Utils/            # Utility classes
│       ├── Helpers.php   # Helper functions
│       ├── Performance.php # Performance optimizations
│       └── Security.php  # Security enhancements
├── functions.php         # Theme functions
└── style.css            # Theme metadata
```

## Core Components

### Bootstrap System

The Bootstrap class (`src/Core/Bootstrap.php`) is the heart of the theme, handling:

- Theme configuration
- Service container management
- Feature registration
- Asset loading

```php
// Example configuration
public static $config = [
    'name' => 'Artemis Starter Theme',
    'version' => 'v1.0.0',
    'text_domain' => 'artemis',
    'jquery' => false,
    'custom_fields' => false,
];
```

### Helper Functions

The Utils class provides various helper functions for common tasks:

```php
// Template components
Kit::component('header/header');
Kit::component('footer/footer', ['data' => $value]);

// Layouts
Kit::layout('default', function() {
    // Content here
});

// Assets
Kit::icon('logo', 'inline');
Kit::image('header.jpg');
```

### Security Features

Built-in security enhancements include:

- XML-RPC disabled by default
- WordPress version number hidden
- Unnecessary header links removed
- REST API endpoints protection
- Feed links disabled
- Heartbeat API optimization

### Performance Optimizations

Automatic performance improvements:

- Emoji script removal
- Optimized heartbeat API
- Cleaned up WordPress header
- Efficient asset loading
- Minified and combined assets

## Development Tools

### Laravel Mix Configuration

The theme uses Laravel Mix for asset compilation. Main features:

- SASS/SCSS compilation
- PostCSS processing
- JavaScript bundling
- Image optimization
- BrowserSync integration

### Coding Standards

The theme follows WordPress Coding Standards, enforced through:

- PHP_CodeSniffer
- ESLint
- Stylelint
- Prettier

Run checks using:
```bash
composer test    # Check coding standards
composer fix     # Auto-fix coding standards
```

### Asset Management

Assets are managed through the Assets class (`src/Setup/Assets.php`):

- Automatic versioning
- Conditional loading
- Dependencies management
- Footer/Header placement control

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the GPL-2.0+ License - see the [LICENSE](LICENSE) file for details.

## Credits

Brought to you by [MatterWP](https://matterwp.com).
