# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Language

- Speak in Czech language
- Comments, Docs and commit messages write in English

## Package Manager

This project uses **Bun** as the package manager (specified in package.json).

## Common Commands

- `bun dev` - Start development servers for all apps
- `bun build` - Build all apps and packages
- `bun lint` - Run Biome linting across all packages
- `bun run lint:fix` - Run Biome linting with auto-fix
- `bun run format` - Format code with Biome
- `bun run check-types` - Run TypeScript type checking

## Architecture

This is a **Turborepo monorepo** configured for **Astro** development:

### Workspace Organization
- `apps/` - Application packages:
  - `web` - Astro web application
- `packages/` - Shared packages:
  - `@21-000-000/ui` - Astro component library with exports pattern `"./*": "./src/*.astro"`
  - `@21-000-000/biome-config` - Shared Biome configurations (base and Astro-specific)
  - `@21-000-000/typescript-config` - Shared TypeScript configurations

### Build Pipeline
- Turborepo handles build orchestration with dependency management
- Tasks are configured in `turbo.json` with proper dependency chains (`dependsOn: ["^build"]`)
- Development servers run persistently without caching
- Build outputs cached for both `.next/**` and `dist/**` directories

### Component Generation
The UI package includes Turbo generators:
- `bun run generate:component` - Generate new Astro components using templates
- Templates located in `packages/ui/turbo/generators/templates/`

### Code Quality
- **Biome** for linting, formatting, and import organization
- Astro-specific Biome configuration in `@21-000-000/biome-config/astro`
- TypeScript strict mode with Astro integration

### Key Technologies
- **Astro 5** as the primary framework
- TypeScript throughout (100% TypeScript codebase)
- Biome for code quality and formatting
- Node.js >=18 required