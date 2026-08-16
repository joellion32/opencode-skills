---
name: react-native-expo
description: >
  REQUIRED when creating, extending, or reviewing a React Native + Expo mobile
  application. Use when scaffolding a new RN/Expo project, adding screens,
  components, models, navigation, or theming to an existing one, generating a
  project README, or verifying architecture conformance. Triggers: React Native,
  Expo, mobile app, create-expo-app, expo init, screens, navigation,
  bottom tabs, theme, light/dark mode. Use ONLY for React Native/Expo projects,
  not generic web, backend, or other mobile frameworks (Flutter, native iOS/Android).
---

# React Native + Expo Skill

Build and maintain React Native + Expo applications using a layered
architecture with a clear separation of concerns. This skill encodes the
structure, conventions, and workflows of a proven mobile app project pattern.

## When This Skill MUST Be Used

**ALWAYS invoke this skill for ANY of these:**

- Scaffolding a NEW React Native/Expo project from scratch
- Adding screens, components, hooks, contexts, models, or navigation to an existing RN/Expo project
- Implementing or modifying theming (light/dark) and styling
- Generating a project README for an RN/Expo app
- Reviewing an RN/Expo project for conformance with this pattern

**Do NOT use this skill** for web apps, backends, or other mobile stacks
(Flutter, React Native Web only, native iOS/Android).

## Canonical Tech Stack

| Area | Package | Version |
|------|---------|---------|
| Core | react-native | `^0.79.2` |
| Core | expo | `^53.0.9` |
| Core | typescript | `~5.8.3` |
| Core | react | `~19.0.0` |
| Navigation | @react-navigation/native | `^7.1.10` |
| Navigation | @react-navigation/bottom-tabs | `^7.3.14` |
| Navigation | @react-navigation/stack | `^6.4.1` |
| UI/UX | react-native-paper | `^5.14.5` |
| UI/UX | @expo/vector-icons | `^14.0.2` |
| UI/UX | expo-linear-gradient | `~14.1.5` |
| UI/UX | expo-font | `^13.3.1` |
| Utils | react-native-gesture-handler | `^2.25.0` |
| Utils | react-native-safe-area-context | `5.4.0` |
| Utils | react-native-screens | `~4.11.1` |
| Utils | react-native-prompt-android | `^1.1.0` |

## Layered Architecture

Three layers, each with clear responsibilities:

- **Presentation Layer**: UI components, screens, navigation, hooks, contexts
- **Core Layer**: Domain models, types, interfaces (no UI concerns)
- **Config Layer**: Global configuration, themes, helpers

State management:
- **Context API**: only for global state (e.g. theme)
- **Local state**: `useState`/`useEffect` for component state
- **Navigation state**: handled by React Navigation

## Directory Structure (Scaffold)

Generate this exact layout for a new project:

```
<project-name>/
├── assets/                     # Static resources
│   ├── icon.png
│   ├── splash.png
│   ├── adaptive-icon.png
│   └── favicon.png
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
│       ├── navigation/        # Navigation configuration
│       │   ├── Navigation.tsx
│       │   └── <Type>Navigation.tsx
│       └── screens/           # Main screens
│           └── <feature>/
│               └── <Name>Screen.tsx
├── App.tsx                    # Root component
├── app.json                   # Expo configuration
├── package.json               # Dependencies
├── tsconfig.json              # TypeScript configuration
└── babel.config.js            # Babel configuration
```

## Code Conventions

- **TypeScript** for static typing on every file.
- **Naming**:
  - Models: `<name>.model.ts` (e.g. `product.model.ts`)
  - Helpers: `<name>.helper.ts`
  - Components: `PascalCase.tsx` (e.g. `ProductCard.tsx`)
  - Hooks: `use<Name>.tsx` (e.g. `useSearchBar.tsx`)
  - Contexts: `<Name>Context.tsx` (e.g. `ThemeContext.tsx`)
  - Screens: `<Name>Screen.tsx` (e.g. `HomeScreen.tsx`)
- Keep components **small and reusable**; place base UI in `components/ui/`.
- Use **custom hooks** for shared logic.
- Group components and screens **by feature** in subfolders.
- Define domain models as TypeScript interfaces in `src/core/models/`.

## State Management & Navigation

Context API for global state. Navigation structure:

```
App
└── ThemeProvider
    └── NavigationContainer
        └── BottomTabNavigator
            ├── HomeScreen
            ├── FeatureScreen
            │   └── FeatureDetailScreen (stack)
            ├── AIScreen (optional)
            └── SettingsScreen (optional)
```

## Theming System

Implement a dynamic light/dark theme system:
- Auto-detect system preference
- Manual toggle in the UI (via `ThemeContext`)

Reference palette:

```typescript
// Light theme
const lightColors = {
  primary: "#3BAA4A",
  secondary: "#004D1A",
  tertiary: "#808080",
  text: "black",
  background: "#FFFF",
  cardBackground: "#F7F3F9",
};

// Dark theme
const darkColors = {
  primary: "#3BAA4A",
  secondary: "#004D1A",
  tertiary: "#FFFF",
  text: "white",
  background: "#090909",
  cardBackground: "#2d2d2d",
};
```

## Scaffold Workflow

1. **Create project**: `npx create-expo-app <project-name> --template blank-typescript`
2. **Install dependencies** (navigation, paper, icons, utils listed above): `npm install`
3. **Create folders**: `assets/`, `src/config/helpers/`, `src/core/models/`, `src/presentation/{components,context,hooks,navigation,screens}/`
4. **Create base files**: `src/config/theme.tsx`, `src/presentation/context/ThemeContext.tsx`, navigation files, sample models and a base `ui/` component.
5. **Verify**: run `npm start` (or `npx tsc --noEmit`) and confirm no errors.

## README Template

When generating a README, follow this structure (Spanish for consistency with
the reference project, or match the user's requested language):

1. Title with emoji + one-line description
2. Table of Contents (linked anchors)
3. Características (implemented + planned)
4. Tecnologías (tables: Core, Navegación, UI/UX, Utilidades)
5. Estructura del Proyecto (tree code block)
6. Instalación (prerequisites + steps)
7. Scripts Disponibles
8. Arquitectura (pattern description + state management)
9. Componentes Principales (screens, UI components, navigation)
10. Modelos de Datos (TypeScript interfaces)
11. Temas y Estilos (palette)
12. Navegación (tree)
13. Screenshots (placeholder)
14. Roadmap (current version + next versions)
15. Contribución (how to contribute + code standards)
16. Licencia, Desarrollador, Nota final

## Conformance Checklist

Before finishing, verify the project follows:

- [ ] Three-layer structure: `config/`, `core/models/`, `presentation/`
- [ ] Components grouped by feature + base `ui/` folder
- [ ] Screens grouped by feature, named `<Name>Screen.tsx`
- [ ] Models as `.model.ts` interfaces in `core/models/`
- [ ] Helpers in `config/helpers/` as `.helper.ts`
- [ ] Custom hooks as `use<Name>.tsx` in `presentation/hooks/`
- [ ] Global state via Context API; local state via `useState`/`useEffect`
- [ ] React Navigation with bottom tabs (and stack for detail screens)
- [ ] Theme system with light/dark palettes and ThemeContext
- [ ] README follows the template structure
