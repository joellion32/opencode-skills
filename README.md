# Opencode Skills

Skills especializadas para el desarrollo de aplicaciones React, diseñadas para
used con [opencode](https://opencode.ai). Cada skill codifica la arquitectura,
convenciones y flujos de trabajo de patrones probados de proyectos.

## Skills Disponibles

### 📱 React Native + Expo

Para aplicaciones móviles con React Native y Expo.

- Arquitectura en 3 capas: config, core/models, presentation
- Navegación con React Navigation (bottom tabs + stacks)
- Sistema de temas light/dark
- Componentes agrupados por feature
- TypeScript estricto

**Uso:** `skill("react-native-expo")`

### 🌐 React + Vite

Para aplicaciones web con React y Vite.

- Arquitectura en 3 capas: config, core/models, presentation
- Enrutamiento con React Router
- UI con Material UI
- Sistema de temas light/dark con CSS custom properties
- TypeScript estricto

**Uso:** `skill("react-vite")`

## Instalación

```bash
# Clonar o copiar las skills deseadas
cp -r skills/react-native-expo ~/.agents/skills/
cp -r skills/react-vite ~/.agents/skills/
Estructura Compartida
Ambas skills siguen el mismo patrón de arquitectura:
src/
├── config/          # Configuración global, temas, helpers
├── core/            # Modelos de dominio, tipos, interfaces
└── presentation/    # UI: componentes, hooks, context, pages/screens
Licencia
MIT
