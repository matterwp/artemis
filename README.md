# Artemis WordPress Starter Theme

[![GitHub release](https://img.shields.io/github/v/release/pressxco/flex?color=ed64a6)](https://github.com/pressxco/flex/releases) [![license](https://img.shields.io/badge/license-GPL--2.0%2B-orange)](https://github.com/pressxco/flex/blob/master/LICENSE) [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/pressxco/flex/pulls)

Artemis is a modern WordPress starter theme that includes a complete development environment with Sass, PostCSS, Autoprefixer, stylelint, Webpack, ESLint, imagemin, Browsersync, and more.

## Requirements

- PHP 7.4.30 or higher
- WordPress 5.7.2 or higher
- Node.js & NPM
- Composer

## Getting Started

### 1. Install Dependencies

```bash
composer install
yarn install
```

### 2. Start Development Environment

```bash
yarn dev
```

## Project Structure

```
artemis/
├── .dev/                  # Development configuration files
├── build/                 # Compiled assets (generated)
├── src/
│   ├── Core/             # Core framework classes
│   ├── Setup/            # Theme setup and configuration
│   ├── Theme/
│   │   ├── Blocks/       # Gutenberg blocks
│   │   ├── Layouts/      # Layout templates
│   │   ├── Main/         # Main theme assets
│   │   ├── Page/         # Page templates
│   │   └── Post/         # Post templates
│   └── Utils/            # Utility classes
└── vendor/               # Composer dependencies
```

## Configuration

### Theme Configuration

The theme configuration is handled through the Bootstrap class. Reference:

```php
public static $config = [
    'name' => 'Artemis Starter Theme',
    'version' => 'v1.0.0',
    'text_domain' => 'artemis',
    'jquery' => false,
    'custom_fields' => false,
    'icon_dir' => '/build/icons/',
    'image_dir' => '/build/images/'
];
```

### Development Configuration

Webpack configuration can be modified in `.dev/webpack.mix.js`:

```javascript
mix
    .browserSync({
        proxy: 'http://artemis.local',
        open: 'external',
        port: 3000,
        files: ['*.php', 'src/**/**/*'],
        reloadDelay: 500
    });
```

## Core Features

### 1. Registrable Interface

All service classes implement the Registrable interface, ensuring consistent registration of components:

```php
interface Registrable {
    public function register();
}
```

### 2. Performance Optimizations

The Performance class handles various WordPress optimizations:

```php
// ----------------------------------------------------
// Cleanup Header.
// ----------------------------------------------------
\remove_action( 'wp_head', 'rsd_link' );
\remove_action( 'wp_head', 'wlwmanifest_link' );
\remove_action( 'wp_head', 'wp_generator' );
\remove_action( 'wp_head', 'rest_output_link_wp_head', 10 );
\remove_action( 'wp_head', 'wp_oembed_add_discovery_links', 10 );
\remove_action( 'wp_head', 'feed_links_extra', 3 );
\remove_action( 'wp_head', 'feed_links', 2 );
```

### 3. Security Enhancements

Security features are managed through the Security class:

```php
/**
 * Disable WLWManifest Link
 *
 * @since 1.0.5
 * @return void
 * -----------------------------------------------------------------------------
 * -----------------------------------------------------------------------------
 */
public function disable_wlw_manifest_link() {
    \remove_action( 'wp_head', 'wlwmanifest_link' );
}

/**
 * Disable Shortlink
 *
 * @since 1.0.5
 * @return void
 * -----------------------------------------------------------------------------
 * -----------------------------------------------------------------------------
 */
public function disable_shortlink() {
    \remove_action( 'wp_head', 'wp_shortlink_wp_head' );
    \remove_action( 'template_redirect', 'wp_shortlink_header', 11, 0 );
}
```

## Theme Components

### 1. Layouts

Layouts are managed through the `Kit::layout()` helper function. Example usage:

```php
Kit::layout('default', function() {
    // Your content here
});
```

### 2. Components

Components can be included using the `Kit::component()` helper:

```php
Kit::component('header/head');
// With parameters
Kit::component('footer/footer', ['variable' => 'value']);
```

### 3. Assets

Assets (icons and images) can be included using helper functions:

```php
// SVG icons
Kit::icon('logo', 'inline');  // Inline SVG
Kit::icon('logo', 'tag');     // <img> tag

// Images
Kit::image('header.jpg');
```

## Development

### Asset Compilation

The theme uses Laravel Mix for asset compilation. Main configuration:

```javascript
.sass(
    'src/Theme/Main/Static/styles/main.scss',
    'styles.bundle.css',
    { sassOptions: { outputStyle: 'compressed' } }
)
.options({
    postCss: [
        require('css-declaration-sorter')({
            order: 'smacss'
        })
    ],
    autoprefixer: {
        options: {
            browsers: [
                'last 6 versions',
            ]
        }
    },
});
```

### Tailwind CSS

Tailwind CSS is configured in `.dev/tailwind.config.js`:

```javascript
module.exports = {
    content: [
        './src/**/*.{svg,css,png,jpg,js}',
        './src/**/*.php',
        './src/**/**/*.php',
    ],
    plugins: [
        require('@tailwindcss/typography')
    ]
}
```

## Available Scripts

- `yarn dev`: Start development environment with hot reloading
- `yarn build`: Build assets for development
- `yarn build:production`: Build assets for production
- `composer test`: Run PHP CodeSniffer tests
- `composer fix`: Auto-fix PHP coding standards

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the GPL-2.0+ License.

---

Brought to you by [MatterWP](https://matterwp.com).
