# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an Angular 20 e-commerce application built with standalone components using modern Angular patterns. The project uses Tailwind CSS for styling and integrates with external APIs for product data.

## Development Commands

- **Start development server**: `npm start` or `ng serve` (runs on http://localhost:4200)
- **Build for production**: `npm run build` or `ng build`
- **Build for development with watch**: `npm run watch` or `ng build --watch --configuration development`
- **Run tests**: `npm test` or `ng test` (uses Karma and Jasmine)
- **Generate components**: `ng generate component component-name` (creates standalone components by default)
- **Generate other Angular schematics**: `ng generate directive|pipe|service|class|guard|interface|enum`

## Architecture

### Domain-Driven Structure
The application follows a domain-driven architecture organized under `src/app/domains/`:

- **`shared/`** - Common components, services, models, pipes, and directives used across domains
- **`products/`** - Product-related functionality (list, detail pages, product component)
- **`info/`** - Information pages (about, not-found, audio wave component)

### Key Architectural Patterns

- **Standalone Components**: All components are configured as standalone (no NgModules)
- **Lazy Loading**: Routes use `loadComponent()` for code splitting
- **Path Aliases**: TypeScript paths configured for clean imports:
  - `@shared/*` → `./src/app/domains/shared/*`
  - `@products/*` → `./src/app/domains/products/*`
  - `@info/*` → `./src/app/domains/info/*`
- **Dependency Injection**: Uses modern `inject()` function instead of constructor injection
- **Router Configuration**: Uses `withComponentInputBinding()` and `withPreloading(PreloadAllModules)`

### External Dependencies
- **API Integration**: Uses `https://api.escuelajs.co/api/v1/products` for product data
- **Audio Processing**: Integrates `wavesurfer.js` for audio visualization
- **Date Utilities**: Uses `date-fns` for date manipulation
- **Styling**: Tailwind CSS with PostCSS and Autoprefixer

## Configuration Details

### Angular Configuration
- **Project Name**: `store`
- **Tests Disabled**: All Angular schematics configured with `skipTests: true`
- **Strict TypeScript**: Enabled with strict templates and injection parameters
- **Bundle Budgets**: 500kb warning, 1mb error for initial bundle; 2kb warning, 4kb error for component styles

### File Structure Conventions
- Components follow the pattern: `component-name/component-name.component.{ts,html,css}`
- Services are in `domains/shared/services/`
- Models are in `domains/shared/models/`
- Pipes and directives are in `domains/shared/pipes/` and `domains/shared/directives/`

## API Integration
The application consumes external APIs through services:
- **ProductService**: Handles product listing and individual product retrieval
- **CategoryService**: Manages product categories
- **CartService**: Shopping cart functionality

When working with API-dependent features, consider that the application relies on external services that may have rate limits or availability issues.