# FilamentPHP ToggleButtons Component Issue Reproduction

## 🎥 Issue Demonstration

<video controls src="issue_screen_recording.mov" title="ToggleButtons Component Issue Demo"></video>

## 📋 Issue Summary

This repository reproduces a bug in FilamentPHP where the `ToggleButtons` component becomes unusable when using a custom theme during development mode. Additionally, the production build process generates CSS syntax errors related to modern CSS features.

**GitHub Issue:** [#16844](https://github.com/filamentphp/filament/issues/16844)

## 🐛 Problem Description

### Development Mode Issues
- The `ToggleButtons` component appears unusable in the browser
- Users are unable to select/click the toggle buttons
- Component becomes non-interactive when custom theme is applied

### Production Build Issues
- CSS syntax errors during Vite build process
- Warnings about unexpected ")" characters
- Issues with `:where()` pseudo-selectors and `color-mix()` functions

## 🛠️ Technical Environment

- **Package:** `filament/filament`
- **Package Version:** `4.x-dev`
- **Laravel Version:** `v12.0`
- **Livewire Version:** `v3.6`
- **PHP Version:** `PHP 8.3.22`

## 🔧 Reproduction Steps

### 1. Setup Custom Theme
Follow the FilamentPHP documentation to set up a custom theme CSS file.

### 2. Implement ToggleButtons Component
```php
ToggleButtons::make('is_active')
    ->label('Active')
    ->boolean()
    ->inline()
    ->required()
```

### 3. Development Mode Testing
1. Run development server: `npm run dev`
2. Open the admin panel and visit vendor edit page
3. Observe the ToggleButtons component behavior

### 4. Production Build Testing
1. Run production build: `npm run build`
2. Check for CSS syntax errors in the build output

## 📊 Expected vs Actual Behavior

### Expected Behavior
- ToggleButtons component should work correctly in both development and production modes
- Component should be interactive and functional regardless of custom theme usage

### Actual Behavior
- Component is unusable in development mode with custom theme
- Production build generates CSS syntax warnings
- Component appears non-interactive in browser

## 🚨 Build Warnings

When running `npm run build`, the following warnings appear:

```
▲ [WARNING] Unexpected ")" [css-syntax-error]
    <stdin>:2:279171:
      2 │ ...table .selectedCell:after:where(){background-color:var(--gray-80...
        ╵                                    ^

▲ [WARNING] Unexpected ")" [css-syntax-error]
    <stdin>:2:279311:
      2 │ ...table .selectedCell:after:where(){background-color:color-mix(in ...
        ╵                                    ^
```

## 📁 Repository Structure

This repository contains:
- Laravel application with FilamentPHP admin panel
- Custom theme configuration
- Vendor resource with ToggleButtons component
- Screen recording demonstrating the issue

## 🔍 Files of Interest

- `app/Filament/Resources/Vendors/Schemas/VendorForm.php` - Contains the problematic ToggleButtons component
- `resources/css/filament/admin/theme.css` - Custom theme configuration
- `issue_screen_recording.mov` - Visual demonstration of the issue

## 🎯 Impact

This issue affects:
- Development workflow when using custom themes
- Production deployments due to CSS build warnings
- Development experience with ToggleButtons component functionality

## 📝 Notes

- Issue occurs specifically with custom themes
- Default FilamentPHP theme works correctly
- Problem manifests in both development