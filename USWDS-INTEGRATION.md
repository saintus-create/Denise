# USWDS Integration Guide

## Overview

This project has been successfully migrated from Tailwind CSS to the **United States Web Design System (USWDS)**. USWDS is the official design system for the U.S. federal government, providing accessible, mobile-first components and design tokens.

## What Changed

### 1. Design Tokens
USWDS provides a comprehensive set of design tokens that ensure consistency across all components:

- **Color System**: Theme-based color palette with semantic naming (primary, secondary, accent, etc.)
- **Typography**: Type scale with font families (Public Sans, Merriweather, Roboto Mono)
- **Spacing**: 8px-based spacing units with named tokens
- **Border Radius**: Consistent border radius tokens

### 2. Components Updated

All components have been updated to use USWDS classes and patterns:

- **Layout**: Uses USWDS grid system (`grid-container`, `grid-row`, `grid-col-*`)
- **Buttons**: USWDS button styles (`usa-button`, `usa-button--outline`)
- **Forms**: USWDS form controls (`usa-input`, `usa-label`, `usa-form-group`)
- **Cards**: USWDS card components (`usa-card`)
- **Navigation**: USWDS header and navigation patterns
- **Footer**: USWDS footer with proper spacing

### 3. Removed Dependencies

The following Tailwind CSS dependencies have been removed:
- `tailwindcss`
- `@tailwindcss/vite`
- `@tailwindcss/typography`
- `@fontsource-variable/bricolage-grotesque`
- `@fontsource-variable/inter`

### 4. Added Dependencies

New dependencies for USWDS:
- `@uswds/uswds` (v3.13.0) - The USWDS package
- `@fontsource/public-sans` - Sans-serif font for UI
- `@fontsource/merriweather` - Serif font for headings
- `@fontsource/roboto-mono` - Monospace font for code

## File Structure

```
src/
├── styles/
│   ├── global.css          # Main stylesheet with USWDS imports
│   └── uswds-settings.scss  # USWDS theme configuration
├── layouts/
│   └── Layout.astro        # Main layout with USWDS fonts
├── components/
│   ├── ui/
│   │   └── button.astro    # Button component (USWDS classes)
│   ├── container.astro     # Container with USWDS grid
│   ├── navbar/navbar.astro # Navigation (USWDS header)
│   ├── footer.astro        # Footer (USWDS footer)
│   └── ...                 # Other components
└── pages/                  # Page components
```

## USWDS Settings Configuration

The `uswds-settings.scss` file configures the USWDS theme:

### Color Tokens

```scss
// Primary color (blue family)
$theme-color-primary: "blue-60v";
$theme-color-primary-vivid: "blue-warm-60v";

// Secondary color (red family)
$theme-color-secondary: "red-50";

// Base colors (gray family)
$theme-color-base: "gray-cool-50";
$theme-color-base-dark: "gray-cool-60";
```

### Typography Settings

```scss
$theme-font-type-sans: "public-sans";
$theme-font-type-serif: "merriweather";
$theme-font-type-mono: "roboto-mono";

$theme-body-font-size: "sm";
$theme-body-line-height: 5;
```

### Spacing Settings

```scss
$theme-border-radius-sm: 2px;
$theme-border-radius-md: 0.5;  // 4px
$theme-border-radius-lg: 1;    // 8px
```

## Using USWDS Classes

### Buttons

```astro
<!-- Primary button -->
<button class="usa-button">Primary</button>

<!-- Outline button -->
<button class="usa-button usa-button--outline">Outline</button>
```

### Forms

```astro
<div class="usa-form-group">
  <label for="email" class="usa-label">Email</label>
  <input 
    type="email" 
    id="email" 
    class="usa-input"
    placeholder="Enter email"
  />
</div>
```

### Grid System

```astro
<div class="grid-container">
  <div class="grid-row grid-gap">
    <div class="tablet:grid-col-8">
      <!-- Content -->
    </div>
    <div class="tablet:grid-col-4">
      <!-- Sidebar -->
    </div>
  </div>
</div>
```

### Cards

```astro
<div class="usa-card">
  <div class="usa-card__media">
    <!-- Image -->
  </div>
  <div class="usa-card__body">
    <h2 class="usa-card__heading">Card Title</h2>
    <p class="usa-card__text">Card content</p>
  </div>
</div>
```

### Typography

```astro
<h1 class="usa-display">Display Heading</h1>
<h2 class="usa-section__heading">Section Heading</h2>
<p class="usa-intro">Intro text with larger font size</p>
```

## Custom Styles

Custom styles are added in `global.css` using USWDS mixins and functions:

```scss
@use "uswds-settings" as *;
@use "@uswds/uswds/packages/uswds-core/src/styles/uswds-core";

.custom-button {
  @include u-bg('primary');
  @include u-text('white');
  @include u-padding-x(2.5);
  @include u-padding-y(2);
  @include u-radius('md');
}
```

## Accessibility Features

USWDS includes built-in accessibility features:

- **Focus styles**: Visible focus indicators
- **Color contrast**: WCAG AA compliant color combinations
- **Semantic HTML**: Proper heading hierarchy
- **Skip link**: Keyboard navigation support
- **Form labels**: Associated with inputs
- **ARIA attributes**: Where appropriate

## Responsive Design

USWDS uses a mobile-first approach with responsive breakpoints:

- `mobile`: < 640px
- `mobile-lg`: ≥ 640px
- `tablet`: ≥ 1024px
- `tablet-lg`: ≥ 1280px
- `desktop`: ≥ 1440px

Use responsive prefixes:
```astro
<div class="tablet:grid-col-6">
  <!-- 6 columns on tablet and up -->
</div>
```

## Building the Project

```bash
# Install dependencies
npm install

# Development server
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview
```

## Benefits of USWDS

1. **Accessibility**: Built with WCAG 2.1 AA compliance
2. **Consistency**: Design tokens ensure visual harmony
3. **Maintainability**: Standardized patterns and components
4. **Performance**: Optimized CSS with tree-shaking
5. **Flexibility**: Customizable through Sass variables
6. **Documentation**: Comprehensive guides and examples
7. **Government Standard**: Trusted by federal agencies

## Resources

- [USWDS Documentation](https://designsystem.digital.gov/)
- [USWDS GitHub](https://github.com/uswds/uswds)
- [Design Tokens](https://designsystem.digital.gov/design-tokens/)
- [Components](https://designsystem.digital.gov/components/)
- [Utilities](https://designsystem.digital.gov/utilities/)

## Migration Notes

### From Tailwind to USWDS

| Tailwind | USWDS |
|---------|-------|
| `bg-black` | `u-bg('black')` or `.usa-button` |
| `text-white` | `u-text('white')` |
| `p-4` | `u-padding(2)` |
| `m-4` | `u-margin(2)` |
| `rounded` | `u-radius('md')` |
| `font-bold` | `u-font-weight('bold')` |
| `grid-cols-2` | `grid-row` + `tablet:grid-col-6` |

## Browser Support

USWDS supports:
- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

Note: Internet Explorer 11 is not supported.

## Future Enhancements

Consider adding:
- USWDS navigation component
- USWDS accordion for FAQ sections
- USWDS modal for dialogs
- USWDS search component
- USWDS footer with extended navigation

## Troubleshooting

### Styles not applying
- Ensure `uswds-settings.scss` is imported before USWDS core
- Check that Sass is compiling correctly
- Verify load paths include `node_modules/@uswds/uswds/packages`

### Fonts not loading
- Confirm font packages are installed
- Check import statements in `Layout.astro`
- Verify font files exist in `node_modules`

### Build errors
- Run `npm install` to ensure all dependencies
- Clear `.astro` cache if needed
- Check for Sass compilation errors

## Conclusion

The migration to USWDS provides a solid foundation for building accessible, consistent, and maintainable government and public-facing websites. The design system's comprehensive token system and component library ensure that your project follows best practices while remaining flexible enough to meet your specific needs.
