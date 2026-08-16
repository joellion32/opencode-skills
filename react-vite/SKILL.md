---
name: react-vite
description: >
  REQUIRED when creating, extending, or reviewing a React + Vite web
  application. Use when scaffolding a new React/Vite project, adding pages,
  components, hooks, contexts, models, or routing to an existing one, generating
  a project README, or verifying architecture conformance. Triggers: React,
  Vite, web app, create-vite, pages, routing, theme, light/dark mode. Use ONLY
  for React + Vite projects, not React Native, backends, or other frameworks.
---

# React + Vite Skill

Build and maintain React + Vite web applications using a layered
architecture with a clear separation of concerns. This skill encodes the
structure, conventions, and workflows of a proven web app project pattern.

## When This Skill MUST Be Used

**ALWAYS invoke this skill for ANY of these:**

- Scaffolding a NEW React + Vite project from scratch
- Adding pages, components, hooks, contexts, models, or routing to an existing React/Vite project
- Implementing or modifying theming (light/dark) and styling
- Generating a project README for a React/Vite app
- Reviewing a React/Vite project for conformance with this pattern

**Do NOT use this skill** for React Native, backends, mobile apps (Flutter, native iOS/Android), or other frameworks.

## Canonical Tech Stack

| Area | Package | Version |
|------|---------|---------|
| Core | react | `^19.1.0` |
| Core | react-dom | `^19.1.0` |
| Core | vite | `^6.3.5` |
| Core | typescript | `~5.8.3` |
| Routing | react-router-dom | `^7.6.1` |
| UI/UX | @mui/material | `^7.1.1` |
| UI/UX | @mui/icons-material | `^7.1.1` |
| UI/UX | @emotion/react | `^11.14.0` |
| UI/UX | @emotion/styled | `^11.14.0` |
| Utils | axios | `^1.9.0` |
| Utils | date-fns | `^4.1.0` |

## Layered Architecture

Three layers, each with clear responsibilities:

- **Presentation Layer**: UI components, pages, routing, hooks, contexts
- **Core Layer**: Domain models, types, interfaces (no UI concerns)
- **Config Layer**: Global configuration, themes, helpers

State management:
- **Context API**: only for global state (e.g. theme, auth)
- **Local state**: `useState`/`useEffect` for component state
- **Routing state**: handled by React Router

## Directory Structure (Scaffold)

Generate this exact layout for a new project:

```
<project-name>/
├── public/                     # Static assets
│   ├── favicon.ico
│   └── logo.svg
├── src/
│   ├── config/                 # Global configurations
│   │   ├── theme.tsx          # Theme definition and styles
│   │   └── helpers/           # Helper functions
│   │       └── <name>.helper.ts
│   ├── core/                  # Business logic
│   │   └── models/            # Types and interfaces
│   │       └── <name>.model.ts
│   └── presentation/          # Presentation layer
│       ├── components/        # Reusable components
│       │   ├── <feature>/     # Feature-scoped components
│       │   └── ui/            # Base UI components
│       ├── context/           # React contexts
│       │   └── <Name>Context.tsx
│       ├── hooks/             # Custom hooks
│       │   └── use<Name>.tsx
│       ├── pages/             # Main pages/routes
│       │   └── <feature>/
│       │       └── <Name>Page.tsx
│       └── layouts/           # Layout components
│           └── MainLayout.tsx
├── App.tsx                    # Root component with routing
├── main.tsx                   # Entry point
├── index.html                 # HTML entry
├── vite.config.ts             # Vite configuration
├── package.json               # Dependencies
├── tsconfig.json              # TypeScript configuration
└── tsconfig.node.json         # Node TypeScript config
```

## Code Conventions

- **TypeScript** for static typing on every file.
- **Naming**:
  - Models: `<name>.model.ts` (e.g. `product.model.ts`)
  - Helpers: `<name>.helper.ts`
  - Components: `PascalCase.tsx` (e.g. `ProductCard.tsx`)
  - Hooks: `use<Name>.tsx` (e.g. `useSearchBar.tsx`)
  - Contexts: `<Name>Context.tsx` (e.g. `ThemeContext.tsx`)
  - Pages: `<Name>Page.tsx` (e.g. `HomePage.tsx`)
- Keep components **small and reusable**; place base UI in `components/ui/`.
- Use **custom hooks** for shared logic.
- Group components and pages **by feature** in subfolders.
- Define domain models as TypeScript interfaces in `src/core/models/`.

## State Management & Routing

Context API for global state. Routing structure:

```
App
└── ThemeProvider
    └── BrowserRouter
        └── Routes
            ├── "/" → MainLayout
            │   ├── index → HomePage
            │   ├── "feature" → FeaturePage
            │   │   └── "feature/:id" → FeatureDetailPage
            │   ├── "about" → AboutPage (optional)
            │   └── "settings" → SettingsPage (optional)
            └── "*" → NotFoundPage
```

## Theming System

Implement a dynamic light/dark theme system:
- Auto-detect system preference via `prefers-color-scheme`
- Manual toggle in the UI (via `ThemeContext`)
- CSS custom properties for theme values

Reference palette:

```typescript
// Light theme
const lightColors = {
  primary: "#1976d2",
  secondary: "#9c27b0",
  tertiary: "#ff9800",
  text: "#212121",
  textSecondary: "#757575",
  background: "#ffffff",
  surface: "#f5f5f5",
  cardBackground: "#ffffff",
  border: "#e0e0e0",
};

// Dark theme
const darkColors = {
  primary: "#90caf9",
  secondary: "#ce93d8",
  tertiary: "#ffb74d",
  text: "#ffffff",
  textSecondary: "#b0b0b0",
  background: "#121212",
  surface: "#1e1e1e",
  cardBackground: "#2d2d2d",
  border: "#424242",
};
```

## Scaffold Workflow

1. **Create project**: `npm create vite@latest <project-name> -- --template react-ts`
2. **Install dependencies** (router, MUI, utils listed above): `npm install`
3. **Create folders**: `public/`, `src/config/helpers/`, `src/core/models/`, `src/presentation/{components,context,hooks,pages,layouts}/`
4. **Create base files**: `src/config/theme.tsx`, `src/presentation/context/ThemeContext.tsx`, routing setup in `App.tsx`, sample models and a base `ui/` component.
5. **Configure Vite**: Update `vite.config.ts` with path aliases and plugins.
6. **Verify**: run `npm run dev` (or `npx tsc --noEmit`) and confirm no errors.

## README Template

When generating a README, follow this structure (Spanish for consistency with
the reference project, or match the user's requested language):

1. Title with emoji + one-line description
2. Table of Contents (linked anchors)
3. Características (implemented + planned)
4. Tecnologías (tables: Core, Routing, UI/UX, Utilidades)
5. Estructura del Proyecto (tree code block)
6. Instalación (prerequisites + steps)
7. Scripts Disponibles
8. Arquitectura (pattern description + state management)
9. Componentes Principales (pages, UI components, routing)
10. Modelos de Datos (TypeScript interfaces)
11. Temas y Estilos (palette)
12. Enrutamiento (tree)
13. Screenshots (placeholder)
14. Roadmap (current version + next versions)
15. Contribución (how to contribute + code standards)
16. Licencia, Desarrollador, Nota final

## Conformance Checklist

Before finishing, verify the project follows:

- [ ] Three-layer structure: `config/`, `core/models/`, `presentation/`
- [ ] Components grouped by feature + base `ui/` folder
- [ ] Pages grouped by feature, named `<Name>Page.tsx`
- [ ] Models as `.model.ts` interfaces in `core/models/`
- [ ] Helpers in `config/helpers/` as `.helper.ts`
- [ ] Custom hooks as `use<Name>.tsx` in `presentation/hooks/`
- [ ] Global state via Context API; local state via `useState`/`useEffect`
- [ ] React Router with nested routes and layouts
- [ ] Theme system with light/dark palettes and ThemeContext
- [ ] README follows the template structure
